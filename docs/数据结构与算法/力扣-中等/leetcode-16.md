---
title: 16. 最接近的三数之和
date: 2020-06-30 10:45:22
tags:
- leetcode
- java
- 排序
- 双指针
categories: 算法笔记
notshow: true
---
# 16. 最接近的三数之和
## [1. 问题](https://leetcode-cn.com/problems/3sum-closest/)
给定一个包括 n 个整数的数组 nums 和 一个目标值 target。找出 nums 中的三个整数，使得它们的和与 target 最接近。返回这三个数的和。假定每组输入只存在唯一答案。

示例：
>输入：nums = [-1,2,1,-4], target = 1
输出：2
解释：与 target 最接近的和是 2 (-1 + 2 + 1 = 2) 。
 
提示：
- 3 <= nums.length <= 10^3
- -10^3 <= nums[i] <= 10^3
- -10^4 <= target <= 10^4
<!--more-->

## 2. 解法
```java
class Solution {
    public int threeSumClosest(int[] nums, int target) {
        Arrays.sort(nums);
        int ans = nums[0] + nums[1] + nums[2];
        // int left = 0;
        int sum = 0;
        // int right = 0;
        for (int i=0;i<nums.length;i++) {
            int left = i + 1;
            int right = nums.length - 1;

            while(left < right) {
                if(left == right){
                    return sum;
                }

                 sum = nums[i] + nums[left] + nums[right];
                 if (Math.abs(sum-target) < Math.abs(ans-target))
                    ans = sum;
                 if (sum < target) {
                     left++;
                 } else if (sum > target) {
                     right--;
                 } else {
                     return sum;
                 }
            }
            

        }
        return ans;
    }
}
```

## 3. 参考
- https://leetcode-cn.com/problems/3sum-closest
- https://leetcode-cn.com/problems/3sum-closest/solution/zui-jie-jin-de-san-shu-zhi-he-by-leetcode-solution/

## 4. 笔记
![](https://777blog.oss-cn-shanghai.aliyuncs.com/blog%20pic/leetcode16.jpg)