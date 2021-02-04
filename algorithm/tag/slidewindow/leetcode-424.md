# LEETCODE 424. 替换后的最长重复字符

## 1. [问题](https://leetcode-cn.com/problems/longest-repeating-character-replacement/)

给你一个仅由大写英文字母组成的字符串，你可以将任意位置上的字符替换成另外的字符，总共可最多替换 k 次。在执行上述操作后，找到包含重复字母的最长子串的长度。

注意：字符串长度 和 k 不会超过 104。

示例 1：

```text
输入：s = "ABAB", k = 2
输出：4
解释：用两个'A'替换为两个'B',反之亦然。
```

示例 2：

```text
输入：s = "AABABBA", k = 1
输出：4
解释：
将中间的一个'A'替换为'B',字符串变为 "AABBBBA"。
子串 "BBBB" 有最长重复字母, 答案为 4。
```

## 2. 标签

* 双指针
* 滑动窗口

## 3. 解法 - 双指针

### 3.1 Java

```java
class Solution {
    public int characterReplacement(String s, int k) {
        // 字符串中仅包含大写字母，可以使用一个长度为26的数组维护每一个字符的出现次数
        int[] num = new int[26];
        // 字符串长度
        int n = s.length();
        // 【重复字符出现次数】的最大值
        int max = 0;
        // 双指针，区间边界
        int left = 0, right = 0;
        while (right < n) {
            // 每次区间右移，更新右移位置的字符出现的次数
            num[s.charAt(right) - 'A']++;
            // 并尝试用它更新【重复字符出现次数】的历史最大值
            max = Math.max(max, num[s.charAt(right) - 'A']);
            // 计算区间内【非最长重复字符】的数量，以此判断左指针是否需要右移
            // 如果【非最长重复字符】的数量大于 k，说明区间不满足条件，右移左指针
            if (right - left + 1 - max > k) {
                num[s.charAt(left) - 'A']--; // 记得减1，num记录的是区间中字符出现的次数
                left++;// 右移左指针
            }
            // 如果【非最长重复字符】的数量不大于 k，说明区间满足条件，继续右移右指针
            right++;
        }
        // 最后找到的区间就是包含重复字母的最长子串的长度
        return right - left;
    }
}

```

### 3.2 复杂度分析

* 时间复杂度 `O(n)` ：其中 n 是字符串的长度，最多只需要遍历该字符串一次。
* 空间复杂度 `O(m)` ：其中 m 是字符集的大小，这里需要存储每个大写英文字母的出现次数。

## 4. 参考

* [https://leetcode-cn.com/problems/longest-repeating-character-replacement/](https://leetcode-cn.com/problems/longest-repeating-character-replacement/)
* [https://leetcode-cn.com/problems/longest-repeating-character-replacement/solution/ti-huan-hou-de-zui-chang-zhong-fu-zi-fu-n6aza/](https://leetcode-cn.com/problems/longest-repeating-character-replacement/solution/ti-huan-hou-de-zui-chang-zhong-fu-zi-fu-n6aza/)

