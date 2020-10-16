---
title: 21. 调整数组顺序使奇数位于偶数前面
date: '2020-09-14T21:03:14.000Z'
tags:
  - 双指针
  - leetcode
  - java
  - kotlin
  - lcof
categories: 算法笔记
---

# 21. 调整数组顺序使奇数位于偶数前面

## 1. [问题](https://leetcode-cn.com/problems/diao-zheng-shu-zu-shun-xu-shi-qi-shu-wei-yu-ou-shu-qian-mian-lcof/)

输入一个整数数组，实现一个函数来调整该数组中数字的顺序，使得所有奇数位于数组的前半部分，所有偶数位于数组的后半部分。

示例：

```text
输入：nums = [1,2,3,4]
输出：[1,3,2,4] 
注：[3,1,2,4] 也是正确的答案之一。
```

提示：

* 1 &lt;= nums.length &lt;= 50000
* 1 &lt;= nums\[i\] &lt;= 10000

## 2. 解法

### 2.1 Java

```java
class Solution {
    public int[] exchange(int[] nums) {
        // 使用双指针i和j，i从左向右移动，j从右向左移动
        int i = 0;
        int j = nums.length - 1;
        // 工具人tmp
        int tmp;

        // i和j没有相遇就一直循环下去
        while (i < j) {
            /**
             * 除了使用 n%2 是否等于 0 来判断n的奇偶，还可以使用 n&1 是否等于 0 来判断 n 的奇偶
             * 如果 n&1 == 0 说明 n 是偶数，如果 n&1 == 1 说明 n 是奇数。
             * 
             * i 从左往右寻找偶数，j 从右往左寻找奇数，找到了就将二者指向的数字交换一下
             */

            // 如果 i 指向的数字是奇数就不停的往右移动
            while (i < j && (nums[i] & 1) == 1)
                i++;

            // 如果 j 指向的数字是偶数就不停的往左移动
            while (i < j && (nums[j] & 1) == 0)
                j--;

            // 当 i 指向了偶数，j 指向了奇数，就交换二者指向的数字，派出工具人 tmp
            tmp = nums[i];
            nums[i] = nums[j];
            nums[j] = tmp;
        }

        return nums;
    }
}
```

### 2.2 Kotlin

```kotlin
class Solution {
    fun exchange(nums: IntArray): IntArray {
        // 使用双指针i和j，i从左向右移动，j从右向左移动
        var i = 0
        var j = nums.size - 1
        // 工具人tmp
        var tmp: Int

        // i和j没有相遇就一直循环下去
        while (i < j) {
            /**
             * 除了使用 n%2 是否等于 0 来判断n的奇偶，还可以使用 n&1 是否等于 0 来判断 n 的奇偶
             * 如果 n&1 == 0 说明 n 是偶数，如果 n&1 == 1 说明 n 是奇数。
             *
             * i 从左往右寻找偶数，j 从右往左寻找奇数，找到了就将二者指向的数字交换一下
             */

            // 如果 i 指向的数字是奇数就不停的往右移动
            while (i < j && nums[i] and 1 == 1)
                i++

            // 如果 j 指向的数字是偶数就不停的往左移动
            while (i < j && nums[j] and 1 == 0)
                j--

            // 当 i 指向了偶数，j 指向了奇数，就交换二者指向的数字，派出工具人 tmp
            tmp = nums[i]
            nums[i] = nums[j]
            nums[j] = tmp
        }

        return nums
    }
}
```

### 2.3 复杂度分析

* 时间复杂度 O\(N\)：N是数组的长度，两个指针会遍历完整个数组。
* 空间复杂度 O\(1\)：两个双指针使用的是常数大小的额外空间。

## 3. 参考

* [https://leetcode-cn.com/problems/diao-zheng-shu-zu-shun-xu-shi-qi-shu-wei-yu-ou-shu-qian-mian-lcof/](https://leetcode-cn.com/problems/diao-zheng-shu-zu-shun-xu-shi-qi-shu-wei-yu-ou-shu-qian-mian-lcof/)
* [https://leetcode-cn.com/problems/diao-zheng-shu-zu-shun-xu-shi-qi-shu-wei-yu-ou-shu-qian-mian-lcof/solution/mian-shi-ti-21-diao-zheng-shu-zu-shun-xu-shi-qi-4/](https://leetcode-cn.com/problems/diao-zheng-shu-zu-shun-xu-shi-qi-shu-wei-yu-ou-shu-qian-mian-lcof/solution/mian-shi-ti-21-diao-zheng-shu-zu-shun-xu-shi-qi-4/)

