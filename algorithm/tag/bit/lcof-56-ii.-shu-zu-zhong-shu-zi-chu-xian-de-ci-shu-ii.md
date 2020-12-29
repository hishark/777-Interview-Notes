# LCOF 56 - II. 数组中数字出现的次数 II

## 1. [问题](https://leetcode-cn.com/problems/shu-zu-zhong-shu-zi-chu-xian-de-ci-shu-ii-lcof/)

在一个数组 `nums` 中除一个数字只出现一次之外，其他数字都出现了三次。请找出那个只出现一次的数字。

**示例 1：**

```text
输入：nums = [3,4,3,3]
输出：4
```

**示例 2：**

```text
输入：nums = [9,1,7,9,7,9,7]
输出：1
```

**限制：**

* `1 <= nums.length <= 10000`
* `1 <= nums[i] < 2^31`

## 2. 标签

* 位运算

## 3. 解法

### 3.1 Java

```java
class Solution {
    public int singleNumber(int[] nums) {
        // 建立一个长度为 32 的数组
        // 记录所有数字的各个二进制位中 1 出现的次数
        int[] counts = new int[32];
        for (int i = 0; i < nums.length; i++) {
            for (int j = 0; j < 32; j++) {
                // 使用与运算，可以获取 nums[i] 的二进制最低位 n0
                counts[j] += nums[i] & 1;
                // 无符号右移 nums[i]，在之后的循环中不断的获取 nums[i] 的二进制每一位 n1,n2,...,n31
                nums[i] >>>= 1;
            }
        }
        // 将 counts 各元素对 3 求余，结果就是「只出现一次的数字」的各二进制位
        for (int i = 0; i < 32; i++)
            counts[i] %= 3;

        // 只出现一次的数字
        int onlyOne = 0;
        for (int i = counts.length - 1; i >= 0; i--) {
            // 把结果左移一位，空出最低位
            onlyOne <<= 1;
            // 把第 i 位的二进制值恢复到 onlyOne 上
            onlyOne |= counts[i];
        }
        return onlyOne;
    }
}
```

### 3.2 Kotlin

```kotlin
class Solution {
    fun singleNumber(nums: IntArray): Int {
        // 建立一个长度为 32 的数组
        // 记录所有数字的各个二进制位中 1 出现的次数
        val counts = IntArray(32)
        for (i in nums.indices) {
            for (j in 0..31) {
                // 使用与运算，可以获取 nums[i] 的二进制最低位 n0
                counts[j] += nums[i] and 1
                // 无符号右移 nums[i]，在之后的循环中不断的获取 nums[i] 的二进制每一位 n1,n2,...,n31
                nums[i] = nums[i] ushr 1
            }
        }
        // 将 counts 各元素对 3 求余，结果就是「只出现一次的数字」的各二进制位
        for (i in 0..31)
            counts[i] %= 3

        // 只出现一次的数字
        var onlyOne = 0
        for (i in counts.indices.reversed()) {
            // 把结果左移一位，空出最低位
            onlyOne = onlyOne shl 1
            // 把第 i 位的二进制值恢复到 onlyOne 上
            onlyOne = onlyOne or counts[i]
        }
        return onlyOne
    }
}
```

### 3.3 复杂度分析

* 时间复杂度 `O(N)` ：其中 N 是 nums 数组的长度，遍历数组占用 `O(N)` 时间，每次遍历时的位运算仅占用 `O(1)` 时间。
* 空间复杂度 `O(1)` ：数组 counts 仅占用了常数大小的额外存储空间。

## 4. 参考

* [https://leetcode-cn.com/problems/shu-zu-zhong-shu-zi-chu-xian-de-ci-shu-ii-lcof/](https://leetcode-cn.com/problems/shu-zu-zhong-shu-zi-chu-xian-de-ci-shu-ii-lcof/)
* [https://leetcode-cn.com/problems/shu-zu-zhong-shu-zi-chu-xian-de-ci-shu-ii-lcof/solution/mian-shi-ti-56-ii-shu-zu-zhong-shu-zi-chu-xian-d-4/](https://leetcode-cn.com/problems/shu-zu-zhong-shu-zi-chu-xian-de-ci-shu-ii-lcof/solution/mian-shi-ti-56-ii-shu-zu-zhong-shu-zi-chu-xian-d-4/)

