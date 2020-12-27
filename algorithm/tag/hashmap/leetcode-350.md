---
title: 350. 两个数组的交集 II
date: '2020-07-13T16:12:57.000Z'
tags:
  - leetcode
  - java
  - 哈希表
  - 排序
  - 双指针
categories: 算法笔记
notshow: true
---

# 350. 两个数组的交集 II

## 1. [问题](https://leetcode-cn.com/problems/intersection-of-two-arrays-ii/)

给定两个数组，编写一个函数来计算它们的交集。

示例 1：

```text
输入：nums1 = [1,2,2,1], nums2 = [2,2]
输出：[2,2]
```

示例 2:

```text
输入：nums1 = [4,9,5], nums2 = [9,4,9,8,4]
输出：[4,9]
```

说明：

* 输出结果中每个元素出现的次数，应与元素在两个数组中出现次数的最小值一致。
* 我们可以不考虑输出结果的顺序。

进阶：

* 如果给定的数组已经排好序呢？你将如何优化你的算法？
* 如果 nums1 的大小比 nums2 小很多，哪种方法更优？
* 如果 nums2 的元素存储在磁盘上，磁盘内存是有限的，并且你不能一次加载所有的元素到内存中，你该怎么办？

## 2. 解法1 - 哈希表

### Java

```java
class Solution {
    public int[] intersect(int[] nums1, int[] nums2) {
        // 保证第一个数组比第二个数组短
        if(nums1.length > nums2.length) {
            return intersect(nums2, nums1);
        }

        // 遍历nums1，计算nums1数组中的元素个数 
        Map<Integer, Integer> map = new HashMap<>();
        for (int num: nums1) {
            if(map.containsKey(num)) {
                int cnt = map.get(num);
                map.put(num, cnt + 1);
            } else {
                map.put(num, 1);
            }
        }

        // 结果数组
        int[] res = new int[nums1.length];
        int index = 0;

        // 遍历nums2，计算交集
        for (int num: nums2) {
            int count = map.getOrDefault(num, 0);
            // count非0，说明map中存在num
            if (count > 0) {
                // 添加到结果数组中
                res[index++] = num;
                // num的次数--
                count--;
                // 若count不为0就更新
                if (count > 0) {
                    map.put(num, count);
                } else {
                    // count为0直接移除该数字
                    map.remove(num);
                }
            }
        }

        return Arrays.copyOfRange(res, 0, index);
    }
}
```

## 3. 解法2 - 排序

### Java

```java
class Solution {
    public int[] intersect(int[] nums1, int[] nums2) {
        // 双指针
        int i=0, j=0;

        // 将数组排好序
        Arrays.sort(nums1);
        Arrays.sort(nums2);

        int[] res = new int[nums1.length < nums2.length ? nums1.length : nums2.length];
        int index = 0;

        // 指针未越界就一直遍历
        while (i<nums1.length && j<nums2.length) {
            if(nums1[i] == nums2[j]) {
                res[index++] = nums1[i];
                i++;
                j++;
            } else if (nums1[i] < nums2[j]){
                i++;
            } else {
                j++;
            }
        }

        return Arrays.copyOfRange(res, 0, index);
    }
}
```

## 4. 参考

* [https://leetcode-cn.com/problems/intersection-of-two-arrays-ii/](https://leetcode-cn.com/problems/intersection-of-two-arrays-ii/)
* [https://leetcode-cn.com/problems/intersection-of-two-arrays-ii/solution/liang-ge-shu-zu-de-jiao-ji-ii-by-leetcode-solution/](https://leetcode-cn.com/problems/intersection-of-two-arrays-ii/solution/liang-ge-shu-zu-de-jiao-ji-ii-by-leetcode-solution/)

## 5. 笔记

![](https://777blog.oss-cn-shanghai.aliyuncs.com/leetcode/leetcode-350-1.jpg) ![](https://777blog.oss-cn-shanghai.aliyuncs.com/leetcode/leetcode-350-2.jpg)

