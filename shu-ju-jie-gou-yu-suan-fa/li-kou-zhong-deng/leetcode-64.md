---
title: 64. 最小路径和
date: '2020-07-23T13:29:07.000Z'
tags:
  - leetcode
  - java
  - kotlin
  - 动态规划
categories: 算法笔记
notshow: true
---

# leetcode-64

## 1. [问题](https://leetcode-cn.com/problems/minimum-path-sum)

给定一个包含非负整数的 m x n 网格，请找出一条从左上角到右下角的路径，使得路径上的数字总和为最小。

说明：每次只能向下或者向右移动一步。

示例:

```text
输入:
[
  [1,3,1],
  [1,5,1],
  [4,2,1]
]
输出: 7
解释: 因为路径 1→3→1→1→1 的总和最小。
```

## 2. 解法

### 2.1 Java

```java
class Solution {
    public int minPathSum(int[][] grid) {
        // 数组行列长度
        int m = grid.length;
        int n = grid[0].length;

        // 状态数组
        int[][] dp = new int[m][n];

        // 边界条件
        dp[0][0] = grid[0][0];

        // 状态转移方程
        for (int i=0;i<m;i++) {
            for (int j=0;j<n;j++) {
                // 防止越界
                if (i==0 && j==0)
                    continue;
                if (i - 1 < 0) {
                    dp[i][j] = dp[i][j-1] + grid[i][j];
                } else if (j - 1 < 0) {
                    dp[i][j] = dp[i-1][j] + grid[i][j];
                } else {
                    dp[i][j] = Math.min(dp[i][j-1] + grid[i][j], dp[i-1][j] + grid[i][j]);
                }

            }
        }

        return dp[m-1][n-1];
    }
}
```

### 2.2 Kotlin

```kotlin
class Solution {
    fun minPathSum(grid: Array<IntArray>): Int {
        // 数组行列长度
        val m = grid.size
        val n = grid[0].size

        // 状态数组
        val dp = Array(m) { IntArray(n) }

        // 边界条件
        dp[0][0] = grid[0][0]

        // 状态转移方程
        for (i in 0 until m) {
            for (j in 0 until n) {
                // 防止越界
                if (i == 0 && j == 0)
                    continue
                if (i - 1 < 0) {
                    dp[i][j] = dp[i][j - 1] + grid[i][j]
                } else if (j - 1 < 0) {
                    dp[i][j] = dp[i - 1][j] + grid[i][j]
                } else {
                    dp[i][j] = Math.min(dp[i][j - 1] + grid[i][j], dp[i - 1][j] + grid[i][j])
                }
            }
        }

        return dp[m - 1][n - 1]
    }
}
```

## 3. 参考

* [https://leetcode-cn.com/problems/minimum-path-sum](https://leetcode-cn.com/problems/minimum-path-sum)

## 4. 笔记

![](https://777blog.oss-cn-shanghai.aliyuncs.com/leetcode/leetcode-64.jpg)

