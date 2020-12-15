---
title: 11. 旋转数组的最小数字
date: '2020-08-27T20:54:20.000Z'
tags:
  - 二分查找
  - leetcode
  - lcof
  - java
  - kotlin
categories: 算法笔记
---

# 11. 旋转数组的最小数字

## 1. [问题](https://leetcode-cn.com/problems/xuan-zhuan-shu-zu-de-zui-xiao-shu-zi-lcof/)

把一个数组最开始的若干个元素搬到数组的末尾，我们称之为数组的旋转。输入一个递增排序的数组的一个旋转，输出旋转数组的最小元素。例如，数组 \[3,4,5,1,2\] 为 \[1,2,3,4,5\] 的一个旋转，该数组的最小值为1。  


示例 1：

```text
输入：[3,4,5,1,2]
输出：1
```

示例 2：

```text
输入：[2,2,2,0,1]
输出：0
```

## 2. 解法 - 二分查找

### 2.1 Java

```java
class Solution {
    public int minArray(int[] nums) {
        // 如果只有一个元素，直接返回
        if (nums.length == 1)
            return nums[0];

        // 左右边界
        int left = 0;
        int right = nums.length - 1;

        // 二分查找
        // 经过旋转之后的数组被分为了两个数组，nums1和nums2
        // nums1中的元素的任一个都会【大于等于】nums2中的元素的任一个
        // 使用二分查找在nums数组中找到nums2中的第一个元素nums[i]（也就是最小值）
        while (left < right) {
            // 中点
            int mid = left + (right - left) / 2;

            // 比较nums[mid]和nums[right]的大小
            if (nums[mid] < nums[right]) {
                // nums[mid]更小，说明此时nums[mid]处于第二个数组中，left<i<=mid<right
                right = mid;
            } else if (nums[mid] > nums[right]) {
                // nums[mid]更大，说明此时nums[mid]处于第一个数组中，left<mid<i<right
                left = mid + 1;
            } else {
                // 由于存在重复元素，所以无法判断mid目前的位置，但是由于nums[mid]=nums[right]，所以可以忽略右端点
                right -= 1;
            }
        }

        // 返回nums[left]或nums[right]
        return nums[left];

    }
}
```

### 2.2 Kotlin

```kotlin
class Solution {
    fun minArray(nums: IntArray): Int {
        // 如果只有一个元素，直接返回
        if (nums.size == 1)
            return nums[0]

        // 左右边界
        var left = 0
        var right = nums.size - 1

        // 二分查找
        // 经过旋转之后的数组被分为了两个数组，nums1和nums2
        // nums1中的元素的任一个都会【大于等于】nums2中的元素的任一个
        // 使用二分查找在nums数组中找到nums2中的第一个元素nums[i]（也就是最小值）
        while (left < right) {
            // 中点
            val mid = left + (right - left) / 2

            // 比较nums[mid]和nums[right]的大小
            if (nums[mid] < nums[right]) {
                // nums[mid]更小，说明此时nums[mid]处于第二个数组中，left<i<=mid<right
                right = mid
            } else if (nums[mid] > nums[right]) {
                // nums[mid]更大，说明此时nums[mid]处于第一个数组中，left<mid<i<right
                left = mid + 1
            } else {
                // 由于存在重复元素，所以无法判断mid目前的位置，但是由于nums[mid]=nums[right]，所以可以忽略右端点
                right -= 1
            }
        }

        // 返回nums[left]或nums[right]
        return nums[left]

    }
}
```

## 3. 参考

* [https://leetcode-cn.com/problems/xuan-zhuan-shu-zu-de-zui-xiao-shu-zi-lcof/](https://leetcode-cn.com/problems/xuan-zhuan-shu-zu-de-zui-xiao-shu-zi-lcof/)
* [https://leetcode-cn.com/problems/xuan-zhuan-shu-zu-de-zui-xiao-shu-zi-lcof/solution/xuan-zhuan-shu-zu-de-zui-xiao-shu-zi-by-leetcode-s/](https://leetcode-cn.com/problems/xuan-zhuan-shu-zu-de-zui-xiao-shu-zi-lcof/solution/xuan-zhuan-shu-zu-de-zui-xiao-shu-zi-by-leetcode-s/)
* [https://leetcode-cn.com/problems/xuan-zhuan-shu-zu-de-zui-xiao-shu-zi-lcof/solution/mian-shi-ti-11-xuan-zhuan-shu-zu-de-zui-xiao-shu-3/](https://leetcode-cn.com/problems/xuan-zhuan-shu-zu-de-zui-xiao-shu-zi-lcof/solution/mian-shi-ti-11-xuan-zhuan-shu-zu-de-zui-xiao-shu-3/)

