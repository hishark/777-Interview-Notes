---
title: 329. 矩阵中的最长递增路径
date: '2020-07-27T23:12:28.000Z'
tags:
  - leetcode
  - java
  - kotlin
  - DFS
  - 记忆化
categories: 算法笔记
notshow: true
---

# 329. 矩阵中的最长递增路径

## 1. [问题](https://leetcode-cn.com/problems/longest-increasing-path-in-a-matrix)

给定一个整数矩阵，找出最长递增路径的长度。

对于每个单元格，你可以往上，下，左，右四个方向移动。 你不能在对角线方向上移动或移动到边界外（即不允许环绕）。

示例 1:

```text
输入: nums = 
[
  [9,9,4],
  [6,6,8],
  [2,1,1]
] 
输出: 4 
解释: 最长递增路径为 [1, 2, 6, 9]。
```

示例 2:

```text
输入: nums = 
[
  [3,4,5],
  [3,2,6],
  [2,2,1]
] 
输出: 4 
解释: 最长递增路径是 [3, 4, 5, 6]。注意不允许在对角线方向上移动。
```

## 2. 解法 - DFS

### 2.1 Java

```java
class Solution {
    // 方向数组
    public int[][] dir = {{-1, 0}, {1, 0}, {0, -1}, {0, 1}};

    // 矩阵行列数
    public int rows;
    public int cols;

    public int longestIncreasingPath(int[][] matrix) {
        // 空矩阵直接返回0
        if(matrix == null || matrix.length == 0)
            return 0;

        // 矩阵行列数
        rows = matrix.length;
        cols = matrix[0].length;

        // 记忆数组，存储已经计算过的路径长度
        int[][] memo = new int[rows][cols];

        // 最终结果
        int res = 0;

        for(int i=0;i<rows;i++) {
            for(int j=0;j<cols;j++) {
                res = Math.max(res, dfs(i, j, memo, matrix));
            }
        }

        return res;
    }


    // 计算第row行第col列节点的最长递增路径
    public int dfs(int row, int col, int[][] memo, int[][] matrix) {
        // 先判断当前节点是否计算过，如果计算过就直接返回结果
        if (memo[row][col] != 0) {
            return memo[row][col];
        }

        // 计算路径长度，自身+1
        memo[row][col]++;

        // 深度优先搜索 - 上下左右
        for (int[] direction: dir) {
            // 下一个节点的行列下标
            int newRow = row + direction[0];
            int newCol = col + direction[1];

            // 如果节点的下标没有越界，且值比当前节点的值更大，那么就可以继续向深处搜索
            if (newRow >= 0 && newRow < rows && newCol >= 0 && newCol < cols && matrix[newRow][newCol] > matrix[row][col]) {
                // 比较memo[row][col]和继续搜索后得到的递增路径，更新为较大的路径
                memo[row][col] = Math.max(memo[row][col], dfs(newRow, newCol, memo, matrix) + 1);
            }
        }

        return memo[row][col];
    }
}
```

### 2.2 Kotlin

```kotlin
class Solution {
    // 方向数组
    var dir = arrayOf(intArrayOf(-1, 0), intArrayOf(1, 0), intArrayOf(0, -1), intArrayOf(0, 1))

    // 矩阵行列数
    var rows: Int = 0
    var cols: Int = 0

    fun longestIncreasingPath(matrix: Array<IntArray>?): Int {
        // 空矩阵直接返回0
        if (matrix == null || matrix.size == 0)
            return 0

        // 矩阵行列数
        rows = matrix.size
        cols = matrix[0].size

        // 记忆数组，存储已经计算过的路径长度
        val memo = Array(rows) { IntArray(cols) }

        // 最终结果
        var res = 0

        for (i in 0 until rows) {
            for (j in 0 until cols) {
                res = Math.max(res, dfs(i, j, memo, matrix))
            }
        }

        return res
    }


    // 计算第row行第col列节点的最长递增路径
    fun dfs(row: Int, col: Int, memo: Array<IntArray>, matrix: Array<IntArray>): Int {
        // 先判断当前节点是否计算过，如果计算过就直接返回结果
        if (memo[row][col] != 0) {
            return memo[row][col]
        }

        // 计算路径长度，自身+1
        memo[row][col]++

        // 深度优先搜索 - 上下左右
        for (direction in dir) {
            // 下一个节点的行列下标
            val newRow = row + direction[0]
            val newCol = col + direction[1]

            // 如果节点的下标没有越界，且值比当前节点的值更大，那么就可以继续向深处搜索
            if (newRow >= 0 && newRow < rows && newCol >= 0 && newCol < cols && matrix[newRow][newCol] > matrix[row][col]) {
                // 比较memo[row][col]和继续搜索后得到的递增路径，更新为较大的路径
                memo[row][col] = Math.max(memo[row][col], dfs(newRow, newCol, memo, matrix) + 1)
            }
        }

        return memo[row][col]
    }
}
```

## 3. 参考

* [https://leetcode-cn.com/problems/longest-increasing-path-in-a-matrix](https://leetcode-cn.com/problems/longest-increasing-path-in-a-matrix)
* [https://leetcode-cn.com/problems/longest-increasing-path-in-a-matrix/solution/ju-zhen-zhong-de-zui-chang-di-zeng-lu-jing-by-le-2/](https://leetcode-cn.com/problems/longest-increasing-path-in-a-matrix/solution/ju-zhen-zhong-de-zui-chang-di-zeng-lu-jing-by-le-2/)

## 4. 笔记

![](https://777blog.oss-cn-shanghai.aliyuncs.com/leetcode/leetcode-329-1.jpg) ![](https://777blog.oss-cn-shanghai.aliyuncs.com/leetcode/leetcode-329-2.jpg)

