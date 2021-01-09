# LEETCODE 17. 电话号码的字母组合

## 1. [问题](https://leetcode-cn.com/problems/letter-combinations-of-a-phone-number/)

给定一个仅包含数字 `2-9` 的字符串，返回所有它能表示的字母组合。

给出数字到字母的映射如下（与电话按键相同）。注意 1 不对应任何字母。

![](../../../.gitbook/assets/image%20%2821%29.png)

**示例:**

```text
输入："23"
输出：["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"].
```

**说明:**  
尽管上面的答案是按字典序排列的，但是你可以任意选择答案输出的顺序。

## 2. 标签

* 回溯

## 3. 解法 - 回溯

### 3.1 Java

```java
class Solution {
    public List<String> letterCombinations(String digits) {
        // 所有可能的字母组合
        List<String> combinations = new ArrayList<String>();
        // 判空
        if (digits.length() == 0) {
            return combinations;
        }
        // 使用哈希表存储每个数字对应的所有可能字母
        Map<Character, String> phoneMap = new HashMap<Character, String>() {{
            put('2', "abc");
            put('3', "def");
            put('4', "ghi");
            put('5', "jkl");
            put('6', "mno");
            put('7', "pqrs");
            put('8', "tuv");
            put('9', "wxyz");
        }};
        // 进行回溯操作
        backtrack(combinations, phoneMap, digits, 0, new StringBuffer());
        // 返回所有组合即可
        return combinations;
    }

    /**
     * 回溯
     * @param combinations 所有可能的字母组合
     * @param phoneMap 哈希表
     * @param digits 需要判断的字符串
     * @param index 从字符串的下标为 index 的字符开始回溯
     * @param combination 已有的字母排列
     */
    public void backtrack(List<String> combinations, Map<Character, String> phoneMap, String digits, int index, StringBuffer combination) {
        // 如果遍历到了最后，也就找到了一个完整的字母排列，加入结果里即可
        if (index == digits.length()) {
            combinations.add(combination.toString());
        } else {
            // 字符串 dights 中下标为 index 的字符
            char digit = digits.charAt(index);
            // 从哈希表里找出，该字符对应的字母有哪些
            String letters = phoneMap.get(digit);
            int lettersCount = letters.length();
            // 遍历这些对应的字母
            for (int i = 0; i < lettersCount; i++) {
                // 添加到当前已有的字母排列中
                combination.append(letters.charAt(i));
                // 继续往下一个字符遍历
                backtrack(combinations, phoneMap, digits, index + 1, combination);
                // 回溯，在已有的字母排列中删去当前字符
                combination.deleteCharAt(index);
            }
        }
    }
}
```

### 3.2 复杂度分析

* 时间复杂度 `O(3^m x 4^n)` ：其中 m 是输入中对应 3 个字母的数字个数（包括数字 2、3、4、5、6、8），n 是输入中对应 4 个字母的数字个数（包括数字 7、9），m+n 是输入数字的总个数。当输入包含 m 个对应 3 个字母的数字和 n 个对应 4 个字母的数字时，不同的字母组合一共有 3^m x 4^n 种，需要遍历每一种字母组合。
* 空间复杂度 `O(m+n)` ：除了返回值以外，空间复杂度主要取决于哈希表以及回溯过程中的递归调用层数，哈希表的大小与输入无关，可以看成常数，递归调用层数最大为 m+n。

## 4. 参考

* [https://leetcode-cn.com/problems/letter-combinations-of-a-phone-number/](https://leetcode-cn.com/problems/letter-combinations-of-a-phone-number/)
* [https://leetcode-cn.com/problems/letter-combinations-of-a-phone-number/solution/dian-hua-hao-ma-de-zi-mu-zu-he-by-leetcode-solutio/](https://leetcode-cn.com/problems/letter-combinations-of-a-phone-number/solution/dian-hua-hao-ma-de-zi-mu-zu-he-by-leetcode-solutio/)

