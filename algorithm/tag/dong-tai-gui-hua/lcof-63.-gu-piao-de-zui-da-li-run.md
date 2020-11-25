# lcof-63.-gu-piao-de-zui-da-li-run

## 1. [问题](https://leetcode-cn.com/problems/gu-piao-de-zui-da-li-run-lcof/)

假设把某股票的价格按照时间先后顺序存储在数组中，请问买卖该股票一次可能获得的最大利润是多少？

**示例 1:**

```text
输入: [7,1,5,3,6,4]
输出: 5
解释: 在第 2 天（股票价格 = 1）的时候买入，在第 5 天（股票价格 = 6）的时候卖出，最大利润 = 6-1 = 5 。
     注意利润不能是 7-1 = 6, 因为卖出价格需要大于买入价格。
```

**示例 2:**

```text
输入: [7,6,4,3,1]
输出: 0
解释: 在这种情况下, 没有交易完成, 所以最大利润为 0。
```

**限制：**

* `0 <= 数组长度 <= 10^5`

## 2. 标签

* 动态规划

## 3. 解法 - 动态规划

### 3.1 Java

```java
class Solution {
    public int maxProfit(int[] prices) {
        // 判空
        if (prices.length == 0)
            return 0;

        // 状态数组
        // dp[i] 表示以 prices[i] 结尾的子数组的最大利润（也就是前i天的最大利润）
        int[] dp = new int[prices.length];
        
        // 前几日的最低价格
        int minPrice = Integer.MAX_VALUE;
        // 股票的最大利润
        int maxProfit = 0;

        // 边界值
        dp[0] = 0;

        for (int i=1;i<prices.length;i++) {
            // 遍历的同时更新股票的最低价格
            minPrice = Math.min(minPrice, prices[i]);
            // 当前最大利润为【前一天的最大利润】和【当日股价 - 前几日中的最低股价】中的较大者
            dp[i] = Math.max(dp[i-1], prices[i] - minPrice);
            // 更新最大利润
            maxProfit = Math.max(dp[i], maxProfit);
        }

        return maxProfit;
    }
}
```

### 3.2 Kotlin

```kotlin
class Solution {
    fun maxProfit(prices: IntArray): Int {
        // 判空
        if (prices.size == 0)
            return 0

        // 状态数组
        // dp[i] 表示以 prices[i] 结尾的子数组的最大利润（也就是前i天的最大利润）
        val dp = IntArray(prices.size)

        // 前几日的最低价格
        var minPrice = Integer.MAX_VALUE
        // 股票的最大利润
        var maxProfit = 0

        // 边界值
        dp[0] = 0

        for (i in 1 until prices.size) {
            // 遍历的同时更新股票的最低价格
            minPrice = Math.min(minPrice, prices[i])
            // 当前最大利润为【前一天的最大利润】和【当日股价 - 前几日中的最低股价】中的较大者
            dp[i] = Math.max(dp[i - 1], prices[i] - minPrice)
            // 更新最大利润
            maxProfit = Math.max(dp[i], maxProfit)
        }

        return maxProfit
    }
}
```

### 3.3 复杂度分析

* 时间复杂度 `O(N)` ：其中 N 为 prices 的长度，需要遍历整个数组。
* 空间复杂度 `O(N)` ：dp 数组占用了 O\(N\) 的额外空间。

**效率优化**：

> 由于 `dp[i]` 只和 `dp[i-1]、prices[i]、minPrice` 有关，所以可以直接使用一个变量代替 `dp` 数组，这样可以将空间复杂度从 `O(N)` 降低至 `O(1)` ，修改后的代码如下：

```java
class Solution {
    public int maxProfit(int[] prices) {
        // 前几日的股票最低价格
        int minPrice = Integer.MAX_VALUE;
        // 股票的最大利润
        int maxProfit = 0;

        // 遍历股价
        for (int price : prices) {
            // 更新股票最低价格
            minPrice = Math.min(minPrice, price);
            // 更新最大利润，当前最大利润为【前一天的最大利润】和【当日股价 - 前几日中的最低股价】中的较大者
            maxProfit = Math.max(maxProfit, price - minPrice);
        }

        return maxProfit;
    }
}
```

## 4. 参考

* [https://leetcode-cn.com/problems/gu-piao-de-zui-da-li-run-lcof/](https://leetcode-cn.com/problems/gu-piao-de-zui-da-li-run-lcof/)
* [https://leetcode-cn.com/problems/gu-piao-de-zui-da-li-run-lcof/solution/mian-shi-ti-63-gu-piao-de-zui-da-li-run-dong-tai-2/](https://leetcode-cn.com/problems/gu-piao-de-zui-da-li-run-lcof/solution/mian-shi-ti-63-gu-piao-de-zui-da-li-run-dong-tai-2/)

