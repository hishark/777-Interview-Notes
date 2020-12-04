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

## 2. 解法 - DFS

> m, n, k, visited 可以全部提出来做全局变量，简化一下代码。

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

        // 当前位置已访问 // 别忘记这里哈
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

### 2.3 复杂度分析

* 时间复杂度 `O(MN)`：最差情况下，机器人遍历矩阵所有单元格。
* 空间复杂度 `O(MN)`：最差情况下， `visited` 内存储矩阵中所有单元格的索引。

## 3. 解法 - BFS

> BFS/DFS：两者目标都是遍历整个矩阵，不同点在于**搜索顺序不同**。DFS 是**朝一个方向走到底**，再回退，以此类推；BFS 则是**按照“平推”的方式向前搜索**。
>
> BFS实现：通常利用队列实现广度优先遍历。

### 3.1 Java

```java
// bfs
class Solution {
    public int movingCount(int m, int n, int k) {
        // 访问矩阵
        boolean[][] visited = new boolean[m][n];
        // 结果
        int ans = 0;
        // 利用队列实现广度优先遍历
        Queue<int[]> queue= new LinkedList<int[]>();
        // 将机器人初始点 (0,0) 加入队列 queue
        // 四个数字分别代表：横坐标索引值，纵坐标索引值，数位之和
        queue.add(new int[] { 0, 0, 0 });
        // 终止条件：queue为空，说明已经遍历完所有可达解
        while(queue.size() > 0) {
            // 单元格出列，作为当前搜索的单元格
            int[] cur = queue.poll();
            // 得到该单元格的索引和数位之和
            int i = cur[0], j = cur[1], sum = cur[2];
            // 如果越界、不合法、已访问的话就跳过
            if(i >= m || j >= n || sum > k || visited[i][j]) 
                continue;
            // 标记当前单元格已被访问
            visited[i][j] = true;
            // 结果++
            ans++;
            // 把当前元素下方和右方的单元格加入队列
            // 下方单元格：横坐标索引，纵坐标索引，数位之和
            queue.add(new int[]{i, j+1, digitCount(i, j+1)});
            // 右方单元格：横坐标索引，纵坐标索引，数位之和
            queue.add(new int[]{i+1, j, digitCount(i+1, j)});
        }
        return ans;
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

### 3.2 复杂度分析

* 时间复杂度 `O(MN)`：最差情况下，机器人遍历矩阵所有单元格。
* 空间复杂度 `O(MN)`：最差情况下， `visited` 内存储矩阵所有单元格的索引。

## 3. 参考

* [https://leetcode-cn.com/problems/ji-qi-ren-de-yun-dong-fan-wei-lcof/](https://leetcode-cn.com/problems/ji-qi-ren-de-yun-dong-fan-wei-lcof/)
* [https://leetcode-cn.com/problems/ji-qi-ren-de-yun-dong-fan-wei-lcof/solution/ji-qi-ren-de-yun-dong-fan-wei-by-leetcode-solution/](https://leetcode-cn.com/problems/ji-qi-ren-de-yun-dong-fan-wei-lcof/solution/ji-qi-ren-de-yun-dong-fan-wei-by-leetcode-solution/)
* [https://leetcode-cn.com/problems/ji-qi-ren-de-yun-dong-fan-wei-lcof/solution/mian-shi-ti-13-ji-qi-ren-de-yun-dong-fan-wei-dfs-b/](https://leetcode-cn.com/problems/ji-qi-ren-de-yun-dong-fan-wei-lcof/solution/mian-shi-ti-13-ji-qi-ren-de-yun-dong-fan-wei-dfs-b/)

