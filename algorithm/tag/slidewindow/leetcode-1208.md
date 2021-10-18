# LEETCODE 1208. 尽可能使字符串相等

## 1. [问题](https://leetcode-cn.com/problems/get-equal-substrings-within-budget/)

给你两个长度相同的字符串，s 和 t。

将 s 中的第 i 个字符变到 t 中的第 i 个字符需要 |s\[i] - t\[i]| 的开销（开销可能为 0），也就是两个字符的 ASCII 码值的差的绝对值。

用于变更字符串的最大预算是 maxCost。在转化字符串时，总开销应当小于等于该预算，这也意味着字符串的转化可能是不完全的。

如果你可以将 s 的子字符串转化为它在 t 中对应的子字符串，则返回可以转化的最大长度。

如果 s 中没有子字符串可以转化成 t 中对应的子字符串，则返回 0。

示例 1：

```
输入：s = "abcd", t = "bcdf", cost = 3
输出：3
解释：s 中的 "abc" 可以变为 "bcd"。开销为 3，所以最大长度为 3。
```

示例 2：

```
输入：s = "abcd", t = "cdef", cost = 3
输出：1
解释：s 中的任一字符要想变成 t 中对应的字符，其开销都是 2。因此，最大长度为 1。
```

示例 3：

```
输入：s = "abcd", t = "acde", cost = 0
输出：1
解释：你无法作出任何改动，所以最大长度为 1。
```

**提示：**

* `1 <= s.length, t.length <= 10^5`
* `0 <= maxCost <= 10^6`
* `s` 和 `t` 都只含小写英文字母。

## 2. 标签

* 数组
* 滑动窗口

## 3. 解法 - 滑动窗口

### 3.1 Java

```java
class Solution {
    public int equalSubstring(String s, String t, int maxCost) {
        // 数组长度
        int n = s.length();
        // 数组 diff 中的每一项为 s 和 t 数组对应位置数字的差值
        // 于是题目转换为：计算数组 diff 的元素和不超过 maxCost 的最长子数组长度
        int[] diff = new int[n];
        for (int i = 0; i < n; i++) {
            diff[i] = Math.abs(s.charAt(i) - t.charAt(i));
        }

        // diff 数组元素和不超过 maxCost 的最长子数组长度
        int maxLength = 0;

        // 双指针，滑动窗口的左右边界
        int left = 0, right = 0;

        // 当前滑动窗口的元素和
        int sum = 0;
        while (right < n) {
            // 更新滑动窗口的元素和
            sum += diff[right];
            // 如果元素和超过了最大预算，就不断地将滑动窗口的左边界右移
            while (sum > maxCost) {
                // 删去滑动窗口最左边的元素
                sum -= diff[left];
                // 收缩左边界
                left++;
            }
            // 如果元素和未超过最大预算，或者在超过之后收缩了左边界
            // 更新最长子数组长度
            maxLength = Math.max(maxLength, right - left + 1);
            // 向右扩张滑动窗口
            right++;
        }
        // 返回最长子数组长度即可
        return maxLength;
    }
}
```

### 3.2 复杂度分析

* 时间复杂度 `O(n)` ：其中 n 是字符串的长度，遍历数组需要时间。
* 空间复杂度 `O(n)` ：需要创建长度为 n                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    的数组 diff。

## 4. 参考

* [https://leetcode-cn.com/problems/get-equal-substrings-within-budget/](https://leetcode-cn.com/problems/get-equal-substrings-within-budget/)
* [https://leetcode-cn.com/problems/get-equal-substrings-within-budget/solution/jin-ke-neng-shi-zi-fu-chuan-xiang-deng-b-higz/](https://leetcode-cn.com/problems/get-equal-substrings-within-budget/solution/jin-ke-neng-shi-zi-fu-chuan-xiang-deng-b-higz/)
