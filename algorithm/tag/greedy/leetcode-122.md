# LEETCODE 122. 买卖股票的最佳时机 II

## 1. [问题](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-ii/)

给定一个数组，它的第 i 个元素是一支给定股票第 i 天的价格。

设计一个算法来计算你所能获取的最大利润。你可以尽可能地完成更多的交易（多次买卖一支股票）。

注意：你不能同时参与多笔交易（你必须在再次购买前出售掉之前的股票）。

**示例 1:**

```
输入: [7,1,5,3,6,4]
输出: 7
解释: 在第 2 天（股票价格 = 1）的时候买入，在第 3 天（股票价格 = 5）的时候卖出, 这笔交易所能获得利润 = 5-1 = 4 。
     随后，在第 4 天（股票价格 = 3）的时候买入，在第 5 天（股票价格 = 6）的时候卖出, 这笔交易所能获得利润 = 6-3 = 3 。
```

**示例 2:**

```
输入: [1,2,3,4,5]
输出: 4
解释: 在第 1 天（股票价格 = 1）的时候买入，在第 5 天 （股票价格 = 5）的时候卖出, 这笔交易所能获得利润 = 5-1 = 4 。
     注意你不能在第 1 天和第 2 天接连购买股票，之后再将它们卖出。
     因为这样属于同时参与了多笔交易，你必须在再次购买前出售掉之前的股票。
```

**示例 3:**

```
输入: [7,6,4,3,1]
输出: 0
解释: 在这种情况下, 没有交易完成, 所以最大利润为 0。
```

**提示：**

* `1 <= prices.length <= 3 * 10 ^ 4`
* `0 <= prices[i] <= 10 ^ 4`

## 2. 标签

* 贪心
* 动态规划

## 3. 解法 - 贪心

> 因为交易次数不受限，如果可以把所有的上坡全部收集到，一定是利益最大化的。
>
> ——[seven](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-ii/solution/mai-mai-gu-piao-de-zui-jia-shi-ji-ii-by-leetcode-s/658886)

### 3.1 Java

```java
class Solution {
    public int maxProfit(int[] prices) {
        // 最大利润
        int maxprofit = 0;
        // 总共的天数
        int days = prices.length;
        // 遍历每一天的价格
        for (int i = 1; i < days; i++) {
            // 如果当天的价格比前一天更高，说明可以带来更大的价值，就加到结果里去
            maxprofit += Math.max(0, prices[i] - prices[i - 1]);
        }
        // 返回最大利润
        return maxprofit;
    }
}
```

### 3.2 复杂度分析

* 时间复杂度 `O(n)` ：其中 n 为数组长度，遍历一遍数组即可。
* 空间复杂度 `O(1)` ：仅使用了常数空间存放变量。

## 3. 解法 - 动态规划

> 每一天的状态只与前一天的状态有关，而与更早的状态都无关，因此我们不必存储这些无关的状态，只需要将 dp\[i−1]\[0] 和 dp\[i−1]\[1] 存放在两个变量中，通过它们计算出 dp\[i]\[0] 和 dp\[i]\[1] 并存回对应的变量，以便于第 i+1i+1 天的状态转移即可。
>
> 可以通过上述操作优化空间复杂度至 `O(1)`。

### 3.1 Java

```java
class Solution {
    public int maxProfit(int[] prices) {
        // 总共的天数
        int n = prices.length;

        // 状态数组
        // 每天交易结束后只可能存在手里有一支股票或者没有股票的状态
        // dp[i][0] 表示第 i 天后交易完手里没有股票的最大利润
        // dp[i][1] 表示第 i 天交易完后手里持有一支股票的最大利润
        // i 从 0 开始
        int[][] dp = new int[n][2];

        // 边界值
        dp[0][0] = 0;
        dp[0][1] = -prices[0];
        
        // 遍历剩下的价格
        for (int i = 1; i < n; ++i) {
            // 【前一天手里没股票的最大利润，前一天手里有股票然后今天卖掉的总利润】二者取较大值即为【今天手里没股票的最大利润】
            dp[i][0] = Math.max(dp[i - 1][0], dp[i - 1][1] + prices[i]);
            // 【前一天手里有股票今天没卖的利润，前一天手里没股票今天买了一只股票的利润】二者取较大值即为【今天手里有股票的最大利润】
            dp[i][1] = Math.max(dp[i - 1][1], dp[i - 1][0] - prices[i]);
        }

        // 最后返回最后一天的利润即可
        // dp[n-1][0] 肯定是要比 dp[n-1][1] 更大的，手里压着一个股票没卖出去肯定钱更少嘛
        return dp[n - 1][0];
    }
}
```

### 3.2 复杂度分析

* 时间复杂度 `O(n)` ：其中 n 为数组的长度。一共有 2n 个状态，每次状态转移的时间复杂度为 `O(1)`，因此时间复杂度为 `O(2n)` 即 `O(n)`。
* 空间复杂度 `O(n)` ：我们需要开辟 `O(n)` 空间存储动态规划中的所有状态。如果使用空间优化，空间复杂度可以优化至 O(1)。

## 4. 参考

* [https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-ii/](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-ii/)
* [https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-ii/solution/mai-mai-gu-piao-de-zui-jia-shi-ji-ii-by-leetcode-s/](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-ii/solution/mai-mai-gu-piao-de-zui-jia-shi-ji-ii-by-leetcode-s/)
