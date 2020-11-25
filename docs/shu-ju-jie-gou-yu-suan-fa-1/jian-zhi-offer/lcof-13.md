---
title: 13. 机器人的运动范围
date: '2020-08-27T21:13:59.000Z'
tags:
  - DFS
  - leetcode
  - lcof
  - java
  - kotlin
categories: 算法笔记
---

# 13. 机器人的运动范围

## 1. [问题](https://leetcode-cn.com/problems/ji-qi-ren-de-yun-dong-fan-wei-lcof/)

地上有一个m行n列的方格，从坐标 \[0,0\] 到坐标 \[m-1,n-1\] 。一个机器人从坐标 \[0, 0\] 的格子开始移动，它每次可以向左、右、上、下移动一格（不能移动到方格外），也不能进入行坐标和列坐标的数位之和大于k的格子。例如，当k为18时，机器人能够进入方格 \[35, 37\] ，因为3+5+3+7=18。但它不能进入方格 \[35, 38\]，因为3+5+3+8=19。请问该机器人能够到达多少个格子？ 

示例 1：

```text
输入：m = 2, n = 3, k = 1
输出：3
```

示例 2：

```text
输入：m = 3, n = 1, k = 0
输出：1
```

提示：

* 1 &lt;= n,m &lt;= 100
* 0 &lt;= k &lt;= 20

## 2. 解法

### 2.1 Java

```java
/**
 * 搜索矩阵：
 *  递归 —— 深度优先搜索
 *  队列 —— 广度优先搜索
 * 
 * 递归出口：
 *  越界，数位之和不合法，已访问
 * 
 * 记录已访问
 * 
 * 解决子问题，返回当前问题的结果
 * 
 * 
 * Ref：
 * https://leetcode-cn.com/problems/ji-qi-ren-de-yun-dong-fan-wei-lcof/solution/ji-qi-ren-de-yun-dong-fan-wei-by-leetcode-solution/
 * https://leetcode-cn.com/problems/ji-qi-ren-de-yun-dong-fan-wei-lcof/
 */
class Solution {
    public int movingCount(int m, int n, int k) {
        boolean[][] visited = new boolean[m][n];
        return dfs(m, n, 0, 0, k, visited);
    }

    public int dfs(int m, int n, int i, int j, int k, boolean[][] visited) {
        // 递归出口：越界，数位之和不合法，已访问
        if (i < 0 || i >= m || j < 0 || j >= n || digitCount(i, j) > k || visited[i][j]) 
            return 0;

        // 当前位置已访问
        visited[i][j] = true;

        // 解决子问题，返回当前问题的结果
        return 1 + dfs(m, n, i + 1, j, k, visited) +  dfs(m, n, i - 1, j, k, visited)
                 + dfs(m, n, i, j + 1, k, visited) + dfs(m, n, i, j - 1, k, visited);
    }

    // 计算x和y的数位之和
    public int digitCount(int x, int y) {
        int sum = 0;
        while (x != 0 || y != 0 ) {
            sum += x%10;
            x /= 10;
            sum += y%10;
            y /= 10;
        }
        return sum;
    }
}
```

### 2.2 Kotlin

```kotlin
/**
 * 搜索矩阵：
 * 递归 —— 深度优先搜索
 * 队列 —— 广度优先搜索
 *
 * 递归出口：
 * 越界，数位之和不合法，已访问
 *
 * 记录已访问
 *
 * 解决子问题，返回当前问题的结果
 *
 *
 * Ref：
 * https://leetcode-cn.com/problems/ji-qi-ren-de-yun-dong-fan-wei-lcof/solution/ji-qi-ren-de-yun-dong-fan-wei-by-leetcode-solution/
 * https://leetcode-cn.com/problems/ji-qi-ren-de-yun-dong-fan-wei-lcof/
 */
class Solution {
    fun movingCount(m: Int, n: Int, k: Int): Int {
        val visited = Array(m) { BooleanArray(n) }
        return dfs(m, n, 0, 0, k, visited)
    }

    fun dfs(m: Int, n: Int, i: Int, j: Int, k: Int, visited: Array<BooleanArray>): Int {
        // 递归出口：越界，数位之和不合法，已访问
        if (i < 0 || i >= m || j < 0 || j >= n || digitCount(i, j) > k || visited[i][j])
            return 0

        // 当前位置已访问
        visited[i][j] = true

        // 解决子问题，返回当前问题的结果
        return (1 + dfs(m, n, i + 1, j, k, visited) + dfs(m, n, i - 1, j, k, visited)
                + dfs(m, n, i, j + 1, k, visited) + dfs(m, n, i, j - 1, k, visited))
    }

    // 计算x和y的数位之和
    fun digitCount(x: Int, y: Int): Int {
        var x = x
        var y = y
        var sum = 0
        while (x != 0 || y != 0) {
            sum += x % 10
            x /= 10
            sum += y % 10
            y /= 10
        }
        return sum
    }
}
```

## 3. 参考

* [https://leetcode-cn.com/problems/ji-qi-ren-de-yun-dong-fan-wei-lcof/](https://leetcode-cn.com/problems/ji-qi-ren-de-yun-dong-fan-wei-lcof/)
* [https://leetcode-cn.com/problems/ji-qi-ren-de-yun-dong-fan-wei-lcof/solution/ji-qi-ren-de-yun-dong-fan-wei-by-leetcode-solution/](https://leetcode-cn.com/problems/ji-qi-ren-de-yun-dong-fan-wei-lcof/solution/ji-qi-ren-de-yun-dong-fan-wei-by-leetcode-solution/)

