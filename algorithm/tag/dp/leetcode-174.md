# LEETCODE 174. 地下城游戏

## 1. [问题](https://leetcode-cn.com/problems/dungeon-game/)

一些恶魔抓住了公主（P）并将她关在了地下城的右下角。地下城是由 M x N 个房间组成的二维网格。我们英勇的骑士（K）最初被安置在左上角的房间里，他必须穿过地下城并通过对抗恶魔来拯救公主。

骑士的初始健康点数为一个正整数。如果他的健康点数在某一时刻降至 0 或以下，他会立即死亡。

有些房间由恶魔守卫，因此骑士在进入这些房间时会失去健康点数（若房间里的值为负整数，则表示骑士将损失健康点数）；其他房间要么是空的（房间里的值为 0），要么包含增加骑士健康点数的魔法球（若房间里的值为正整数，则表示骑士将增加健康点数）。

为了尽快到达公主，骑士决定每次只向右或向下移动一步。

编写一个函数来计算确保骑士能够拯救到公主所需的最低初始健康点数。

例如，考虑到如下布局的地下城，如果骑士遵循最佳路径`右 -> 右 -> 下 -> 下`，则骑士的初始健康点数至少为 7。

```
-2 (K)    -3       3
-5        -10       1
10        30      -5 (P)
```

说明:

* 骑士的健康点数没有上限。
* 任何房间都可能对骑士的健康点数造成威胁，也可能增加骑士的健康点数，包括骑士进入的左上角房间以及公主被监禁的右下角房间。

## 2. 解法 - 动态规划

### 2.1 Java

```java
class Solution {
    public int calculateMinimumHP(int[][] dungeon) {
        // 重点：从右下往左上计算
        int n = dungeon.length;
        int m = dungeon[0].length;

        // 状态数组
        // dp[i][j]表示从(i,j)到终点的最低初始值
        int[][] dp = new int[n+1][m+1];

        // 无效值赋值为最大值
        for (int i=0;i<=n;i++) {
            Arrays.fill(dp[i], Integer.MAX_VALUE);
        }

        // 计算dp[n-1][m-1]时要用到的两个值，需要赋值为1
        dp[n-1][m] = dp[n][m-1] = 1;

        // 状态方程
        for (int i=n-1;i>=0;i--) {
            for (int j=m-1;j>=0;j--) {
                int min = Math.min(dp[i+1][j], dp[i][j+1]);
                dp[i][j] = Math.max(min - dungeon[i][j], 1);
            }
        }

        return dp[0][0];
    }
}
```

### 2.2 Kotlin

```kotlin
class Solution {
    fun calculateMinimumHP(dungeon: Array<IntArray>): Int {
        // 重点：从右下往左上计算
        val n = dungeon.size
        val m = dungeon[0].size

        // 状态数组
        // dp[i][j]表示从(i,j)到终点的最低初始值
        val dp = Array(n + 1) { IntArray(m + 1) }

        // 无效值赋值为最大值
        for (i in 0..n) {
            Arrays.fill(dp[i], Integer.MAX_VALUE)
        }

        // 计算dp[n-1][m-1]时要用到的两个值，需要赋值为1
        dp[n][m - 1] = 1
        dp[n - 1][m] = 1

        // 状态方程
        for (i in n - 1 downTo 0) {
            for (j in m - 1 downTo 0) {
                val min = Math.min(dp[i + 1][j], dp[i][j + 1])
                dp[i][j] = Math.max(min - dungeon[i][j], 1)
            }
        }

        return dp[0][0]
    }
}
```

## 3. 参考

* [https://leetcode-cn.com/problems/dungeon-game/](https://leetcode-cn.com/problems/dungeon-game/)
* [https://leetcode-cn.com/problems/dungeon-game/solution/di-xia-cheng-you-xi-by-leetcode-solution/](https://leetcode-cn.com/problems/dungeon-game/solution/di-xia-cheng-you-xi-by-leetcode-solution/)

## 4. 笔记

![](https://777blog.oss-cn-shanghai.aliyuncs.com/leetcode/leetcode-174-1.jpg) ![](https://777blog.oss-cn-shanghai.aliyuncs.com/leetcode/leetcode-174-2.jpg)
