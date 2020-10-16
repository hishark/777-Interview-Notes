---
title: 309. 最佳买卖股票时机含冷冻期
date: '2020-07-10T15:55:42.000Z'
tags:
  - leetcode
  - java
  - kotlin
  - 动态规划
categories: 算法笔记
notshow: true
---

# leetcode-309

## 1. [问题](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-with-cooldown/)

给定一个整数数组，其中第 i 个元素代表了第 i 天的股票价格 。​

设计一个算法计算出最大利润。在满足以下约束条件下，你可以尽可能地完成更多的交易（多次买卖一支股票）:

* 你不能同时参与多笔交易（你必须在再次购买前出售掉之前的股票）。
* 卖出股票后，你无法在第二天买入股票 \(即冷冻期为 1 天\)。

示例:

```text
输入: [1,2,3,0,2]
输出: 3 
解释: 对应的交易状态为: [买入, 卖出, 冷冻期, 买入, 卖出]
```

## 2. 解法

### 2.1 Java

```java
class Solution {
    public int maxProfit(int[] prices) {
        if(prices.length == 0)
            return 0;

        // 总天数
        int n = prices.length;

        // 状态数组
        // max(dp[i][0], dp[i][1], dp[i][2])表示第i天结束之后的累计最大收益
        int[][] dp = new int[n][3];

        // 边界值
        dp[0][0] = -prices[0];
        dp[0][1] = 0;
        dp[0][2] = 0;

        // 状态转移方程
        for (int i=1;i<n;i++) {
            // 目前持有一支股票
            // 这支股票可能是前一天持有的 dp[i-1][0]
            // 也可能是今天刚买的，那么前一天一定不处于冷冻期 dp[i-1][2] - prices[i]
            dp[i][0] = Math.max(dp[i-1][0], dp[i-1][2] - prices[i]);

            // 目前没股票，在冷冻期
            // 在冷冻期说明当日卖出了一支股票，所以前一天一定有一支股票
            dp[i][1] = dp[i-1][0] + prices[i];

            // 目前没股票，也不在冷冻期
            // 说明当日即没有买也没有卖，啥也没干，那么前一天什么状态都有可能
            dp[i][2] = Math.max(dp[i-1][0], Math.max(dp[i-1][1], dp[i-1][2]));
        }

        // 最后一天手里还有股票也没啥意思了，所以只要取dp[n - 1][1]和dp[n - 1][2]里的较大值就可以了
        return Math.max(dp[n-1][1], dp[n-1][2]);
    }
}
```

### 2.2 Kotlin

```kotlin
class Solution {
    fun maxProfit(prices: IntArray): Int {
        if (prices.size == 0)
            return 0

        // 总天数
        val n = prices.size

        // 状态数组
        // max(dp[i][0], dp[i][1], dp[i][2])表示第i天结束之后的累计最大收益
        val dp = Array(n) { IntArray(3) }

        // 边界值
        dp[0][0] = -prices[0]
        dp[0][1] = 0
        dp[0][2] = 0

        // 状态转移方程
        for (i in 1 until n) {
            // 目前持有一支股票
            // 这支股票可能是前一天持有的 dp[i-1][0]
            // 也可能是今天刚买的，那么前一天一定不处于冷冻期 dp[i-1][2] - prices[i]
            dp[i][0] = Math.max(dp[i - 1][0], dp[i - 1][2] - prices[i])

            // 目前没股票，在冷冻期
            // 在冷冻期说明当日卖出了一支股票，所以前一天一定有一支股票
            dp[i][1] = dp[i - 1][0] + prices[i]

            // 目前没股票，也不在冷冻期
            // 说明当日即没有买也没有卖，啥也没干，那么前一天什么状态都有可能
            dp[i][2] = Math.max(dp[i - 1][0], Math.max(dp[i - 1][1], dp[i - 1][2]))
        }

        // 最后一天手里还有股票也没啥意思了，所以只要取dp[n - 1][1]和dp[n - 1][2]里的较大值就可以了
        return Math.max(dp[n - 1][1], dp[n - 1][2])
    }
}
```

## 3. 参考

* [https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-with-cooldown/](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-with-cooldown/)
* [https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-with-cooldown/solution/zui-jia-mai-mai-gu-piao-shi-ji-han-leng-dong-qi-4/](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-with-cooldown/solution/zui-jia-mai-mai-gu-piao-shi-ji-han-leng-dong-qi-4/)

## 4. 笔记

![](https://777blog.oss-cn-shanghai.aliyuncs.com/leetcode/leetcode-309-1.jpg) ![](https://777blog.oss-cn-shanghai.aliyuncs.com/leetcode/leetcode-309-2.jpg) ![](https://777blog.oss-cn-shanghai.aliyuncs.com/leetcode/leetcode-309-3.jpg)

