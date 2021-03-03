# LEETCODE 62. 不同路径

## 1. [问题](https://leetcode-cn.com/problems/unique-paths/)

一个机器人位于一个 m x n 网格的左上角 （起始点在下图中标记为 “Start” ）。

机器人每次只能向下或者向右移动一步。机器人试图达到网格的右下角（在下图中标记为 “Finish” ）。

问总共有多少条不同的路径？

![](../../../.gitbook/assets/image%20%2823%29.png)

示例 1：

```text
输入：m = 3, n = 7
输出：28
```

示例 2：

```text
输入：m = 3, n = 2
输出：3
解释：
从左上角开始，总共有 3 条路径可以到达右下角。
1. 向右 -> 向右 -> 向下
2. 向右 -> 向下 -> 向右
3. 向下 -> 向右 -> 向右
```

示例 3：

```text
输入：m = 7, n = 3
输出：28
```

示例 4：

```text
输入：m = 3, n = 3
输出：6
```

**提示：**

* `1 <= m, n <= 100`
* 题目数据保证答案小于等于 `2 * 109`

## 2. 标签

* 数组
* 动态规划

## 3. 解法 - 动态规划

### 3.1 Java

```java
class Solution {
    public int uniquePaths(int m, int n) {
        // 状态数组
        // dp[i][j] 表示从左上角走到 [i,j] 的路径总数
        int[][] dp = new int[m][n];
        // 初始化第一行，第一行的格子只能通过右移得到
        for (int i = 0; i < m; ++i) {
            dp[i][0] = 1;
        }
        // 初始化第一列，第一列的格子只能通过下移得到
        for (int j = 0; j < n; ++j) {
            dp[0][j] = 1;
        }
        // 遍历余下的所有格子
        for (int i = 1; i < m; ++i) {
            for (int j = 1; j < n; ++j) {
                // 从左上角走到 [i,j] 的路径数 = 左边的格子的路径数 + 上面的格子的路径数
                dp[i][j] = dp[i - 1][j] + dp[i][j - 1];
            }
        }
        // 返回右下角的路径数即可
        return dp[m - 1][n - 1];
    }
}
```

### 3.2 复杂度分析

* 时间复杂度 `O(mn)` ：双重循环。
* 空间复杂度 `O(mn)` ：即为存储所有状态需要的空间

## 4. 参考

* [https://leetcode-cn.com/problems/unique-paths/](https://leetcode-cn.com/problems/unique-paths/)
* [https://leetcode-cn.com/problems/unique-paths/solution/bu-tong-lu-jing-by-leetcode-solution-hzjf/](https://leetcode-cn.com/problems/unique-paths/solution/bu-tong-lu-jing-by-leetcode-solution-hzjf/)

