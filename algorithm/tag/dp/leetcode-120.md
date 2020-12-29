---
title: 120. 三角形最小路径和
date: '2020-07-14T16:20:55.000Z'
tags:
  - leetcode
  - java
  - kotlin
  - 动态规划
categories: 算法笔记
notshow: true
---

# LEETCODE 120. 三角形最小路径和

## 1. [问题](https://leetcode-cn.com/problems/triangle)

给定一个三角形，找出自顶向下的最小路径和。每一步只能移动到下一行中相邻的结点上。

相邻的结点 在这里指的是 下标 与 上一层结点下标 相同或者等于 上一层结点下标 + 1 的两个结点。

例如，给定三角形：

```text
[
     [2],
    [3,4],
   [6,5,7],
  [4,1,8,3]
]
```

自顶向下的最小路径和为 11（即，2 + 3 + 5 + 1 = 11）。

说明： 如果你可以只使用 O\(n\) 的额外空间（n 为三角形的总行数）来解决这个问题，那么你的算法会很加分。

## 2. 解法 - 动态规划

### 2.1 Java

```java
class Solution {
    public int minimumTotal(List<List<Integer>> triangle) {
        // 三角形的行数
        int n = triangle.size();

        // 状态数组
        // dp[i][j]表示从顶点到坐标(i,j)的最小路径和
        int[][] dp = new int[n][n];

        // 边界值
        dp[0][0] = triangle.get(0).get(0);

        // 状态转移
        for (int i=1;i<n;i++) {
            // 上一行的长度
            int len = triangle.get(i-1).size();
            for(int j=0;j<=i;j++) {
                // 当前的dp值只能从dp[i-1][j]和dp[i-1][j-1]转移而来
                // i-1一定不会越界，需要判断j和j-1是否越界，如果越界了就设置为极大值
                int pre1 = j >= 0 && j < len ? dp[i-1][j] : Integer.MAX_VALUE;
                int pre2 = j-1 >=0 && j-1 < len ? dp[i-1][j-1] : Integer.MAX_VALUE;
                // 当前dp = 两个dp的较小值 + 当前结点值
                dp[i][j] = Math.min(pre1, pre2) + triangle.get(i).get(j);
            }
        }

        // 找到dp最后一行的最大值返回即可
        int res = Integer.MAX_VALUE;
        for(int i=0;i<dp[n-1].length;i++) {
            res = Math.min(res, dp[n-1][i]);
        }

        return res;
    }
}
```

### 2.2 Kotlin

```kotlin
class Solution {
    fun minimumTotal(triangle: List<List<Int>>): Int {
        // 三角形的行数
        val n = triangle.size

        // 状态数组
        // dp[i][j]表示从顶点到坐标(i,j)的最小路径和
        val dp = Array(n) { IntArray(n) }

        // 边界值
        dp[0][0] = triangle[0][0]

        // 状态转移
        for (i in 1 until n) {
            // 上一行的长度
            val len = triangle[i - 1].size
            for (j in 0..i) {
                // 当前的dp值只能从dp[i-1][j]和dp[i-1][j-1]转移而来
                // i-1一定不会越界，需要判断j和j-1是否越界，如果越界了就设置为极大值
                val pre1 = if (j >= 0 && j < len) dp[i - 1][j] else Integer.MAX_VALUE
                val pre2 = if (j - 1 >= 0 && j - 1 < len) dp[i - 1][j - 1] else Integer.MAX_VALUE
                // 当前dp = 两个dp的较小值 + 当前结点值
                dp[i][j] = Math.min(pre1, pre2) + triangle[i][j]
            }
        }

        // 找到dp最后一行的最大值返回即可
        var res = Integer.MAX_VALUE
        for (i in 0 until dp[n - 1].size) {
            res = Math.min(res, dp[n - 1][i])
        }

        return res
    }
}
```

## 3. 参考

* [https://leetcode-cn.com/problems/triangle/](https://leetcode-cn.com/problems/triangle/)

## 4. 笔记

![](https://777blog.oss-cn-shanghai.aliyuncs.com/leetcode/leetcode-120.jpg)

