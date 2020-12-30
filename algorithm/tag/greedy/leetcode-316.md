# \*LEETCODE 316. 去除重复字母

## 1. [问题](https://leetcode-cn.com/problems/remove-duplicate-letters/)

给你一个字符串 `s` ，请你去除字符串中重复的字母，使得每个字母只出现一次。需保证 **返回结果的字典序最小**（要求不能打乱其他字符的相对位置）。

**示例 1：**

```text
输入：s = "bcabc"
输出："abc"
```

**示例 2：**

```text
输入：s = "cbacdcbc"
输出："acdb"
```

**提示：**

* `1 <= s.length <= 104`
* `s` 由小写英文字母组成

## 2. 标签

* 贪心
* 栈
* 字符串

## 3. 解法 - 贪心 栈

### 3.1 Java

```java
class Solution {
    public String removeDuplicateLetters(String s) {
        // 记录每个字符是否出现在栈中
        boolean[] inStack = new boolean[26];

        // 使用数组计算字符串中每个字符出现的次数
        int[] num = new int[26];
        for (int i = 0; i < s.length(); i++) {
            num[s.charAt(i) - 'a']++;
        }

        // 栈
        StringBuffer stack = new StringBuffer();
        // 遍历字符串
        for (int i = 0; i < s.length(); i++) {
            // 当前遍历字符
            char ch = s.charAt(i);
            // 如果当前字符不在栈中 
            if (!inStack[ch - 'a']) {
                // 给定一个字符串 s，如何去掉其中的一个字符 ch，使得得到的字符串字典序最小呢？
                // 答案是：找出最小的满足 s[i]>s[i+1] 的下标 i，并去除字符 s[i]。该字符即为「关键字符」
                // 如果栈不为空，且栈顶的字符大于当前字符，说明栈顶字符就是「关键字符」
                while (stack.length() > 0 && stack.charAt(stack.length() - 1) > ch) {
                    // 如果后面还有关键字符，就可以放心让此时栈顶的关键字符出栈
                    if (num[stack.charAt(stack.length() - 1) - 'a'] > 0) {
                        inStack[stack.charAt(stack.length() - 1) - 'a'] = false;
                        stack.deleteCharAt(stack.length() - 1);
                    } else {
                        // 如果后面没有关键字符了，就留下它
                        break;
                    }
                }
                // 处理好了关键字符后，就来处理当前字符
                // 把当前字符放入栈中
                stack.append(ch);
                inStack[ch - 'a'] = true;
            }
            // 如果当前字符已经在栈中了，就不要再放进去了，我们的目标就是去除重复字符
            num[ch - 'a'] -= 1;
        }
        // 此时栈中剩下的就是去除了重复字符的字符串
        return stack.toString();
    }
}
```

### 3.2 复杂度分析

* 时间复杂度 `O(n)` ：其中 n 是字符串长度，每个字符最多只会入栈、出栈各一次。
* 空间复杂度 `O(m)` ：其中 m 为字符集合的总数。本题中字符均为小写字母，所以 m=26。由于栈中的字符不能重复，因此栈中最多只能有 m 个字符，另外需要维护两个数组，分别记录每个字符是否出现在栈中以及每个字符的剩余数量。

## 4. 参考

* [https://leetcode-cn.com/problems/remove-duplicate-letters/](https://leetcode-cn.com/problems/remove-duplicate-letters/)
* [https://leetcode-cn.com/problems/remove-duplicate-letters/solution/qu-chu-zhong-fu-zi-mu-by-leetcode-soluti-vuso/](https://leetcode-cn.com/problems/remove-duplicate-letters/solution/qu-chu-zhong-fu-zi-mu-by-leetcode-soluti-vuso/)

