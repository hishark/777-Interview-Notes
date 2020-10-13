---
title: 154. 寻找旋转排序数组中的最小值 II
date: 2020-07-22 16:57:12
tags:
- leetcode
- java
- kotlin
- 二分查找
categories: 算法笔记
notshow: true
---
# 154. 寻找旋转排序数组中的最小值 II
## 1. [问题](https://leetcode-cn.com/problems/find-minimum-in-rotated-sorted-array-ii/)
假设按照升序排序的数组在预先未知的某个点上进行了旋转。

( 例如，数组 [0,1,2,4,5,6,7] 可能变为 [4,5,6,7,0,1,2] )。

请找出其中最小的元素。

注意数组中可能存在重复的元素。

示例 1：
```
输入: [1,3,5]
输出: 1
```

示例 2：
```
输入: [2,2,2,0,1]
输出: 0
```

说明：
- 这道题是 寻找旋转排序数组中的最小值 的延伸题目。
- 允许重复会影响算法的时间复杂度吗？会如何影响，为什么？
<!--more-->

## 2. 解法 - 二分查找

### 2.1 Java
```java
class Solution {
    public int findMin(int[] nums) {
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
    fun findMin(nums: IntArray): Int {
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
- [https://leetcode-cn.com/problems/find-minimum-in-rotated-sorted-array-ii/](https://leetcode-cn.com/problems/find-minimum-in-rotated-sorted-array-ii/)
- [https://leetcode-cn.com/problems/find-minimum-in-rotated-sorted-array-ii/solution/xun-zhao-xuan-zhuan-pai-xu-shu-zu-zhong-de-zui--16/](https://leetcode-cn.com/problems/find-minimum-in-rotated-sorted-array-ii/solution/xun-zhao-xuan-zhuan-pai-xu-shu-zu-zhong-de-zui--16/)
- [https://leetcode-cn.com/problems/find-minimum-in-rotated-sorted-array-ii/solution/154-find-minimum-in-rotated-sorted-array-ii-by-jyd/](https://leetcode-cn.com/problems/find-minimum-in-rotated-sorted-array-ii/solution/154-find-minimum-in-rotated-sorted-array-ii-by-jyd/)

## 4. 笔记
![](https://777blog.oss-cn-shanghai.aliyuncs.com/leetcode/leetcode-154-1.jpg)
![](https://777blog.oss-cn-shanghai.aliyuncs.com/leetcode/leetcode-154-2.jpg)