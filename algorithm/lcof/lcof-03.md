---
title: 03. 数组中重复的数字
date: '2020-08-10T23:21:04.000Z'
tags:
  - 数组
  - 哈希表
  - leetcode
  - lcof
  - java
  - kotlin
categories: 算法笔记
notshow: true
---

# 03. 数组中重复的数字

## 1. [问题](https://leetcode-cn.com/problems/shu-zu-zhong-zhong-fu-de-shu-zi-lcof/)

找出数组中重复的数字。

在一个长度为 n 的数组 nums 里的所有数字都在 0～n-1 的范围内。数组中某些数字是重复的，但不知道有几个数字重复了，也不知道每个数字重复了几次。请找出数组中任意一个重复的数字。

示例 1：

```text
输入：
[2, 3, 1, 0, 2, 5, 3]
输出：2 或 3
```

限制：

* 2 &lt;= n &lt;= 100000

## 2. 解法1 - 排序

### 2.1 Java

```java
class Solution {
    public int findRepeatNumber(int[] nums) {
        Arrays.sort(nums);
        for (int i=0;i<nums.length;i++) {
            if (nums[i] == nums[i+1])
                return nums[i];
        }
        return -1;
    }
}
```

### 2.2 Kotlin

```kotlin
class Solution {
    fun findRepeatNumber(nums: IntArray): Int {
        Arrays.sort(nums)
        for (i in nums.indices) {
            if (nums[i] == nums[i + 1])
                return nums[i]
        }
        return -1
    }
}
```

## 3. 解法2 - 哈希表

### 3.1 Java

```java
class Solution {
    public int findRepeatNumber(int[] nums) {
        Map<Integer, Integer> map = new HashMap<>();
        for(int num: nums){
            if(map.containsKey(num)){
                return num;
            }else{
                map.put(num, 1);
            }
        }
        return -1;
    }
}
```

### 3.2 Kotlin

```kotlin
class Solution {
    fun findRepeatNumber(nums: IntArray): Int {
        val map = HashMap<Int, Int>()
        for (num in nums) {
            if (map.containsKey(num)) {
                return num
            } else {
                map[num] = 1
            }
        }
        return -1
    }
}
```

## 4. 解法3 - 比较交换

### 4.1 Java

```java
class Solution {
    public int findRepeatNumber(int[] nums) {
        // 从头到尾扫描数字
        for(int i=0;i<nums.length;i++) {
            // 当前扫描的数字为cur
            int cur = nums[i];

            // 判断cur和i是否相等
            // 若相等，继续扫描下一个数
            // 若不相等，比较cur和第cur个数
            while (cur != i) {
                if (cur == nums[cur]) {
                    // cur和第cur个数相等，说明找到了重复数，返回即可
                    return cur;
                } else {
                    // 不相等，交换两个数
                    int tmp = nums[cur];
                    nums[cur] = nums[i];
                    nums[i] = tmp;
                    cur = nums[i];
                }
            }
        }

        return -1;
    }
}
```

### 4.2 Kotlin

```kotlin
class Solution {
    fun findRepeatNumber(nums: IntArray): Int {
        // 从头到尾扫描数字
        for (i in nums.indices) {
            // 当前扫描的数字为cur
            var cur = nums[i]

            // 判断cur和i是否相等
            // 若相等，继续扫描下一个数
            // 若不相等，比较cur和第cur个数
            while (cur != i) {
                if (cur == nums[cur]) {
                    // cur和第cur个数相等，说明找到了重复数，返回即可
                    return cur
                } else {
                    // 不相等，交换两个数
                    val tmp = nums[cur]
                    nums[cur] = nums[i]
                    nums[i] = tmp
                    cur = nums[i]
                }
            }
        }

        return -1
    }
}
```

## 5. 参考

* [https://leetcode-cn.com/problems/shu-zu-zhong-zhong-fu-de-shu-zi-lcof/](https://leetcode-cn.com/problems/shu-zu-zhong-zhong-fu-de-shu-zi-lcof/)
* [《剑指Offer（第2版）》](https://book.douban.com/subject/27008702/)

## 6. 笔记

![](https://777blog.oss-cn-shanghai.aliyuncs.com/leetcode/lcof-03-1.jpg) ![](https://777blog.oss-cn-shanghai.aliyuncs.com/leetcode/lcof-03-2.jpg)

## 7. 关键词

* 数组
* 哈希表

