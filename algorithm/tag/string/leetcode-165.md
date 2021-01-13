# \*LEETCODE 165. 比较版本号

## 1. [问题](https://leetcode-cn.com/problems/compare-version-numbers/)

给你两个版本号 version1 和 version2 ，请你比较它们。

版本号由一个或多个修订号组成，各修订号由一个 '.' 连接。每个修订号由 多位数字 组成，可能包含 前导零 。每个版本号至少包含一个字符。修订号从左到右编号，下标从 0 开始，最左边的修订号下标为 0 ，下一个修订号下标为 1 ，以此类推。例如，2.5.33 和 0.1 都是有效的版本号。

比较版本号时，请按从左到右的顺序依次比较它们的修订号。比较修订号时，只需比较 忽略任何前导零后的整数值 。也就是说，修订号 1 和修订号 001 相等 。如果版本号没有指定某个下标处的修订号，则该修订号视为 0 。例如，版本 1.0 小于版本 1.1 ，因为它们下标为 0 的修订号相同，而下标为 1 的修订号分别为 0 和 1 ，0 &lt; 1 。

返回规则如下：

如果 version1 &gt; version2 返回 1， 如果 version1 &lt; version2 返回 -1， 除此之外返回 0。

示例 1：

```text
输入：version1 = "1.01", version2 = "1.001"
输出：0
解释：忽略前导零，"01" 和 "001" 都表示相同的整数 "1"
```

示例 2：

```text
输入：version1 = "1.0", version2 = "1.0.0"
输出：0
解释：version1 没有指定下标为 2 的修订号，即视为 "0"
```

示例 3：

```text
输入：version1 = "0.1", version2 = "1.1"
输出：-1
解释：version1 中下标为 0 的修订号是 "0"，version2 中下标为 0 的修订号是 "1" 。0 < 1，所以 version1 < version2
```

示例 4：

```text
输入：version1 = "1.0.1", version2 = "1"
输出：1
```

示例 5：

```text
输入：version1 = "7.5.2.4", version2 = "7.5.3"
输出：-1
```

提示：

* 1 &lt;= version1.length, version2.length &lt;= 500 
* version1 和 version2 仅包含数字和 '.' 
* version1 和 version2 都是 有效版本号 
* version1 和 version2 的所有修订号都可以存储在 32 位整数 中

## 2. 标签

* 字符串
* 双指针

## 3. 解法 - 分割字符串

### 3.1 Java

```java
class Solution {
    public int compareVersion(String version1, String version2) {
        // 分割版本号
        String[] nums1 = version1.split("\\.");
        String[] nums2 = version2.split("\\.");

        // 两个版本号的长度
        int len1 = nums1.length, len2 = nums2.length;

        // 当前遍历的数字
        int str1, str2;
        // 遍历较长的数组
        for (int i = 0; i < Math.max(len1, len2); i++) {
            // 逐个比较
            // 如果其中一个数组结束了，需要尾部补0，以进行比较
            // version1 的某块
            str1 = i < len1 ? Integer.parseInt(nums1[i]) : 0;
            // version2 的某块
            str2 = i < len2 ? Integer.parseInt(nums2[i]) : 0;
            // 如果对应的两块数字不相同，那么直接返回即可
            if (str1 != str2) {
                return str1 > str2 ? 1 : -1;
            }
        }
        // 如果遍历完数组，每一块数字都相同，那么就返回 0
        return 0;
    }
}
```

### 3.2 复杂度分析

* 时间复杂度 `O(N + M + max(N, M))` ：其中 N 和 M 指的是输入字符串的长度。
* 空间复杂度 `O(N + M)` ：使用了两个数组 `nums1` 和 `nums2` 存储两个字符串的块。

## 4. 解法 - 双指针

### 4.1 Java

```java
//
```

### 4.2 复杂度分析

* 时间复杂度 `O(max(N, M))` ：其中 N 和 M 指的是输入字符串的长度。
* 空间复杂度 `O(1)` ：未占用额外存储空间。

## 5. 参考

* [https://leetcode-cn.com/problems/compare-version-numbers/](https://leetcode-cn.com/problems/compare-version-numbers/)
* [https://leetcode-cn.com/problems/compare-version-numbers/solution/bi-jiao-ban-ben-hao-by-leetcode/](https://leetcode-cn.com/problems/compare-version-numbers/solution/bi-jiao-ban-ben-hao-by-leetcode/)

