# 57. 和为s的两个数字

## 1. [问题](https://leetcode-cn.com/problems/he-wei-sde-liang-ge-shu-zi-lcof/)

输入一个递增排序的数组和一个数字 s，在数组中查找两个数，使得它们的和正好是 s。如果有多对数字的和等于 s，则输出任意一对即可。

**示例 1：**

```text
输入：nums = [2,7,11,15], target = 9
输出：[2,7] 或者 [7,2]
```

**示例 2：**

```text
输入：nums = [10,26,30,31,47,60], target = 40
输出：[10,30] 或者 [30,10]
```

**限制：**

* `1 <= nums.length <= 10^5`
* `1 <= nums[i] <= 10^6`

## 2. 标签

* 数组
* 双指针
* 哈希表

## 3. 解法 - 双指针

> 还有个方法是哈希表，解法与力扣第一题两数之和相同。

### 3.1 Java

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        // 双指针
        int left = 0;
        int right = nums.length - 1;

        // 两个指针相遇时结束循环
        while (left < right) {
            // 求出当前两个指针指向的两数之和
            int sum = nums[left] + nums[right];

            // 判断该两数之和与目标 target 的大小关系
            if (sum < target) {
                // 由于数组递增有序，所以此时可以将 left 指针右移，以获得更大的值
                left++;
            } else if (sum > target) {
                // 此时可以将 right 指针左移，以获得更小的值
                right--;
            } else {
                // 如果相等，返回结果即可
                return new int[] {nums[left], nums[right]};
            }
        }

        // 没找到符合条件的数字组合，返回 0
        return new int[] {0};
    }
}
```

### 3.2 Kotlin

```kotlin
class Solution {
    fun twoSum(nums: IntArray, target: Int): IntArray {
        // 双指针
        var left = 0
        var right = nums.size - 1

        // 两个指针相遇时结束循环
        while (left < right) {
            // 求出当前两个指针指向的两数之和
            val sum = nums[left] + nums[right]

            // 判断该两数之和与目标 target 的大小关系
            if (sum < target) {
                // 由于数组递增有序，所以此时可以将 left 指针右移，以获得更大的值
                left++
            } else if (sum > target) {
                // 此时可以将 right 指针左移，以获得更小的值
                right--
            } else {
                // 如果相等，返回结果即可
                return intArrayOf(nums[left], nums[right])
            }
        }

        // 没找到符合条件的数字组合，返回 0
        return intArrayOf(0)
    }
}
```

### 3.3 复杂度分析

* 时间复杂度 `O(N)` ：N 是数组的长度，双指针一起遍历了整个数组。
* 空间复杂度 `O(1)` ：双指针两个变量只占用了常数大小的额外空间。

## 4. 参考

* [https://leetcode-cn.com/problems/he-wei-sde-liang-ge-shu-zi-lcof/](https://leetcode-cn.com/problems/he-wei-sde-liang-ge-shu-zi-lcof/)
* [https://leetcode-cn.com/problems/he-wei-sde-liang-ge-shu-zi-lcof/solution/mian-shi-ti-57-he-wei-s-de-liang-ge-shu-zi-shuang-/](https://leetcode-cn.com/problems/he-wei-sde-liang-ge-shu-zi-lcof/solution/mian-shi-ti-57-he-wei-s-de-liang-ge-shu-zi-shuang-/)

