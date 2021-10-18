# 47. 礼物的最大价值【DP】

## 1. [问题](https://leetcode-cn.com/problems/li-wu-de-zui-da-jie-zhi-lcof/)

在一个 m\*n 的棋盘的每一格都放有一个礼物，每个礼物都有一定的价值（价值大于 0）。你可以从棋盘的左上角开始拿格子里的礼物，并每次向右或者向下移动一格、直到到达棋盘的右下角。给定一个棋盘及其上面的礼物的价值，请计算你最多能拿到多少价值的礼物？

**示例 1:**

```
输入: 
[
  [1,3,1],
  [1,5,1],
  [4,2,1]
]
输出: 12
解释: 路径 1→3→5→2→1 可以拿到最多价值的礼物
```

**提示：**

* `0 < grid.length <= 200`
* `0 < grid[0].length <= 200`

## 2. 标签

* 动态规划

## 3. 解法 - 动态规划

### 3.1 Java

```java
class Solution {
    public int maxValue(int[][] grid) {
        // 状态数组
        // dp[i][j] 表示从左上角开始到 [i,j] 时可以拿到的礼物的最大价值
        int row = grid.length;
        int col = grid[0].length;
        int[][] dp = new int[row][col];

        // 边界值
        dp[0][0] = grid[0][0];

        // 状态转移方程
        // 初始化第一行，第一行的每个格子只能靠左边的格子右移得到，因为上面没有格子了，无法通过下移得到第一行的格子
        for (int i=1;i<col;i++) {
            dp[0][i] = grid[0][i] + dp[0][i-1];
        }

        // 初始化第一列，第一列的每个格子只能靠上面的格子下移得到，因为左边没有格子了，无法通过右移得到第一列的格子
        for (int i=1;i<row;i++) {
            dp[i][0] = grid[i][0] + dp[i-1][0];
        }

        // 余下的格子，每个格子都可以往右、往下移动
        for (int i=1;i<row;i++) {
            for (int j=1;j<col;j++) {
                dp[i][j] = grid[i][j] + Math.max(dp[i][j-1], dp[i-1][j]);
            }
        }

        return dp[row - 1][col - 1];
    }
}
```

### 3.2 Kotlin

```kotlin
class Solution {
    fun maxValue(grid: Array<IntArray>): Int {
        // 状态数组
        // dp[i][j] 表示从左上角开始到 [i,j] 时可以拿到的礼物的最大价值
        val row = grid.size
        val col = grid[0].size
        val dp = Array(row) { IntArray(col) }

        // 边界值
        dp[0][0] = grid[0][0]

        // 状态转移方程
        // 初始化第一行，第一行的每个格子只能一直往右平移
        for (i in 1 until col) {
            dp[0][i] = grid[0][i] + dp[0][i - 1]
        }

        // 初始化第一列，第一列的每个格子只能一直往下平移
        for (i in 1 until row) {
            dp[i][0] = grid[i][0] + dp[i - 1][0]
        }

        // 余下的格子，每个格子都可以往右、往下移动
        for (i in 1 until row) {
            for (j in 1 until col) {
                dp[i][j] = grid[i][j] + Math.max(dp[i][j - 1], dp[i - 1][j])
            }
        }

        return dp[row - 1][col - 1]
    }
}
```

### 3.3 复杂度分析

* 时间复杂度 `O(MN)` ：其中 M 和 N 分别为矩阵的行列数，动态规划需要遍历整个矩阵。
* 空间复杂度 `O(MN)` ：dp 数组占用了 `O(MN)` 大小的额外存储空间。

## 4. 参考

* [https://leetcode-cn.com/problems/li-wu-de-zui-da-jie-zhi-lcof/](https://leetcode-cn.com/problems/li-wu-de-zui-da-jie-zhi-lcof/)
* [https://leetcode-cn.com/problems/li-wu-de-zui-da-jie-zhi-lcof/solution/mian-shi-ti-47-li-wu-de-zui-da-jie-zhi-dong-tai-gu/](https://leetcode-cn.com/problems/li-wu-de-zui-da-jie-zhi-lcof/solution/mian-shi-ti-47-li-wu-de-zui-da-jie-zhi-dong-tai-gu/)
