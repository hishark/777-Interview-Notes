---
title: 63. 不同路径 II
date: '2020-07-06T15:28:08.000Z'
tags:
  - leetcode
  - java
  - kotlin
  - 动态规划
categories: 算法笔记
notshow: true
---

# LEETCODE 63. 不同路径 II

## 1. [问题](https://leetcode-cn.com/problems/unique-paths-ii/)

一个机器人位于一个 m x n 网格的左上角 （起始点在下图中标记为“Start” ）。

机器人每次只能向下或者向右移动一步。机器人试图达到网格的右下角（在下图中标记为“Finish”）。

现在考虑网格中有障碍物。那么从左上角到右下角将会有多少条不同的路径？

![](../../../.gitbook/assets/image.png)

网格中的障碍物和空位置分别用 1 和 0 来表示。

说明：m 和 n 的值均不超过 100。

示例 1:

```text
输入:
[
  [0,0,0],
  [0,1,0],
  [0,0,0]
]
输出: 2
解释:
3x3 网格的正中间有一个障碍物。
从左上角到右下角一共有 2 条不同的路径：
1. 向右 -> 向右 -> 向下 -> 向下
2. 向下 -> 向下 -> 向右 -> 向右
```

## 2. 解法 - 动态规划

### 2.1 Java

```java
class Solution {
    public int uniquePathsWithObstacles(int[][] obstacleGrid) {
        // 数组长度
        int x = obstacleGrid.length;
        int y = obstacleGrid[0].length;

        // 状态数组
        int[][] dp = new int[x][y];

        // 边界条件
        dp[0][0] = obstacleGrid[0][0] == 0 ? 1 : 0;

        // 状态转移
        for (int i=0;i<x;i++) {
            for (int j=0;j<y;j++) {
                if(i==0 && j==0)
                    continue;
                else if(obstacleGrid[i][j] == 1)
                    dp[i][j] = 0;
                else 
                    dp[i][j] = (i - 1 >= 0 ? dp[i-1][j] : 0) + (j-1 >= 0 ? dp[i][j-1] : 0);
            }
        }

        return dp[x-1][y-1];

    }
}
```

### 2.2 Kotlin

```kotlin
class Solution {
    fun uniquePathsWithObstacles(obstacleGrid: Array<IntArray>): Int {
        // 数组长度
        var x = obstacleGrid.size
        var y = obstacleGrid[0].size

        // 状态数组
        var dp = Array(x){IntArray(y)}

        // 边界条件
        dp[0][0] = if (obstacleGrid[0][0] == 0) 1 else 0

        // 状态转移  
        for (i in 0..x-1) {
            for (j in 0..y-1) {
                if(i==0 && j==0)
                    continue
                else if(obstacleGrid[i][j] == 1)
                    dp[i][j] = 0
                else 
                    dp[i][j] = (if(i - 1 >= 0) dp[i-1][j] else 0) + (if(j-1 >= 0) dp[i][j-1] else 0)
            }
        }

        return dp[x-1][y-1]
    }
}
```

## 3. 参考

* [https://leetcode-cn.com/problems/unique-paths-ii/](https://leetcode-cn.com/problems/unique-paths-ii/)

## 4. 笔记

![](https://777blog.oss-cn-shanghai.aliyuncs.com/leetcode/leetcode-63.jpg)

