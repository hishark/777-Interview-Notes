---
title: 14-I. 剪绳子
date: '2020-09-01T11:19:52.000Z'
tags:
  - 数学
  - 动态规划
  - 贪心
  - leetcode
  - lcof
  - java
  - kotlin
categories: 算法笔记
---

# 14-I. 剪绳子

## 1. [问题](https://leetcode-cn.com/problems/jian-sheng-zi-lcof/)

给你一根长度为 n 的绳子，请把绳子剪成整数长度的 m 段（m、n都是整数，n&gt;1并且m&gt;1），每段绳子的长度记为 k\[0\],k\[1\]...k\[m-1\] 。请问 k\[0\]k\[1\]...k\[m-1\] 可能的最大乘积是多少？例如，当绳子的长度是8时，我们把它剪成长度分别为2、3、3的三段，此时得到的最大乘积是18。 

示例 1：

```text
输入: 2
输出: 1
解释: 2 = 1 + 1, 1 × 1 = 1
```

示例 2:

```text
输入: 10
输出: 36
解释: 10 = 3 + 3 + 4, 3 × 3 × 4 = 36
```

提示：

* 2 &lt;= n &lt;= 58

## 2. 解法 - 动态规划

> 时间复杂度：O\(n^2\) 空间复杂度：O\(n\)

### 2.1 Java

```java
class Solution {
    public int cuttingRope(int n) {
        // 边界值
        if (n < 2)
            return 0; // return n;
        else if (n == 2)
            return 1;
        else if (n == 3)
            return 2;

        // 状态数组
        // dp[n]表示把长度为n的绳子剪成若干段之后各段长度乘积的最大值
        // 特殊处理：如果某个长度的绳子，剪了一下之后，其中一段的长度在[0,3]的区间内，就不要再剪这一段了
        // 因为剪了之后，乘积会变小，而res[i]是长度为i的绳子剪成若干段后能获得的最大乘积
        // 所以dp[0],dp[1],dp[2],dp[3]要单独处理
        int[] dp = new int[n+1];
        dp[0] = 0;
        dp[1] = 1;
        dp[2] = 2;
        dp[3] = 3;

        // 状态转移方程
        // dp[n]表示把长度为n的绳子剪成若干段之后各段长度乘积的最大值
        // dp[n] = max(dp[j] * dp[n-j]) 其中j的范围为：[1,n-1]
        for (int i=4;i<=n;i++) {
            // 当前绳子长度为i
            // 乘积的最大值↓
            int maxValue = 0;

            // j从1开始是因为剪一刀子下去长度最少为1
            // j最大为i因为当前绳子的长度为i
            // 这里的循环条件可以改为j<=i/2，因为i/2之后算出来的就是重复的乘积了，当n特别特别大的时候，只算到i/2可以节省时间
            for(int j=1;j<=i;j++) {
                // 当前乘积
                int product = dp[j] * dp[i-j];
                if (product > maxValue)
                    maxValue = product;                
            }
            // 把最大值存入dp数组
            dp[i] = maxValue;
        }

        // 返回结果
        return dp[n];
    }
}
```

### 2.2 Kotlin

```kotlin
class Solution {
    fun cuttingRope(n: Int): Int {
        // 边界值
        if (n < 2)
            return 0
        else if (n == 2)
            return 1
        else if (n == 3)
            return 2

        // 状态数组
        // dp[n]表示把长度为n的绳子剪成若干段之后各段长度乘积的最大值
        // 特殊处理：如果某个长度的绳子，剪了一下之后，其中一段的长度在[0,3]的区间内，就不要再剪这一段了
        // 因为剪了之后，乘积会变小，而res[i]是长度为i的绳子剪成若干段后能获得的最大乘积
        // 所以dp[0],dp[1],dp[2],dp[3]要单独处理
        val dp = IntArray(n + 1)
        dp[0] = 0
        dp[1] = 1
        dp[2] = 2
        dp[3] = 3

        // 状态转移方程
        // dp[n]表示把长度为n的绳子剪成若干段之后各段长度乘积的最大值
        // dp[n] = max(dp[j] * dp[n-j]) 其中j的范围为：[1,n-1]
        for (i in 4..n) {
            // 当前绳子长度为i
            // 乘积的最大值↓
            var maxValue = 0

            // j从1开始是因为剪一刀子下去长度最少为1
            // j最大为i因为当前绳子的长度为i
            // 这里的循环条件可以改为j<=i/2，因为i/2之后算出来的就是重复的乘积了，当n特别特别大的时候，只算到i/2可以节省时间
            for (j in 1..i) {
                // 当前乘积
                val product = dp[j] * dp[i - j]
                if (product > maxValue)
                    maxValue = product
            }
            // 把最大值存入dp数组
            dp[i] = maxValue
        }

        // 返回结果
        return dp[n]
    }
}
```

## 3. 解法 - 贪心

> 时间复杂度：O\(1\) 空间复杂度：O\(1\)

### 3.1 Java

```java
// 贪心算法
class Solution {
    public int cuttingRope(int n) {
        // 按照如下策略来剪绳子：
        //  1. 当 n>=5 时 尽可能多地剪长度为3的绳子
        //  2. 当剩下的绳子长度为4时，把绳子剪成两段长度为2的绳子
        // 证明该思路的正确性：
        //  1. 首先当 n>=5 时，可以证明 2(n-2)>n 且 3(n-3)>n。
        //     也就是说当绳子剩下的长度大于或者等于5的时候，我们就把它剪成长度为3或者2的绳子段
        //     另外 n>=5 时 3(n-3)>=2(n-2)，所以应该尽可能地多剪长度为3的绳子段
        //  2. 当绳子的长度为4，由于2x2>1x3，所以剪成两段长度为2的绳子比较好

        // 几个边界值
        if (n < 2)
            return 0;// return n;
        if (n == 2)
            return 1;
        if (n == 3)
            return 2;

        // 尽可能多地剪去长度为3的绳子段
        // numOf3 是绳子段长度为3的绳子数量
        int numOf3 = n / 3;

        // 当绳子最后剩下的长度为4的时候，不能再剪去长度为3的绳子段
        // 此时更好的方法是剪成两段长度为2的绳子，因为2x2 > 3x1
        // 如果n减去所有的3剩下了1，说明有一个3可以和这个1加起来等于4，这个4可以拆成2和2，于是3的数量就减一。
        if (n - 3 * numOf3 == 1)
            numOf3 -= 1;   

        // numsOf2 是绳子段长度为2的绳子数量
        int numOf2 = (n - numOf3 * 3) / 2;

        // 最大乘积
        double maxProduct = Math.pow(3, numOf3) * Math.pow(2, numOf2);

        return (int)maxProduct;
    }
}
```

### 3.2 Kotlin

```kotlin
// 贪心算法
class Solution {
    fun cuttingRope(n: Int): Int {
        // 按照如下策略来剪绳子：
        //  1. 当 n>=5 时 尽可能多地剪长度为3的绳子
        //  2. 当剩下的绳子长度为4时，把绳子剪成两段长度为2的绳子
        // 证明该思路的正确性：
        //  1. 首先当 n>=5 时，可以证明 2(n-2)>n 且 3(n-3)>n。
        //     也就是说当绳子剩下的长度大于或者等于5的时候，我们就把它剪成长度为3或者2的绳子段
        //     另外 n>=5 时 3(n-3)>=2(n-2)，所以应该尽可能地多剪长度为3的绳子段
        //  2. 当绳子的长度为4，由于2x2>1x3，所以剪成两段长度为2的绳子比较好

        // 几个边界值
        if (n < 2)
            return 0
        if (n == 2)
            return 1
        if (n == 3)
            return 2

        // 尽可能多地剪去长度为3的绳子段
        // numOf3 是绳子段长度为3的绳子数量
        var numOf3 = n / 3

        // 当绳子最后剩下的程度为4的时候，不能再剪去长度为3的绳子段
        // 此时更好的方法是剪成两段长度为2的绳子，因为2x2 > 3x1
        // 如果n减去所有的3剩下了1，说明有一个3可以和这个1加起来等于4，这个4可以拆成2和2，于是3的数量就减一。
        if (n - 3 * numOf3 == 1)
            numOf3 -= 1

        // numsOf2 是绳子段长度为2的绳子数量
        val numOf2 = (n - numOf3 * 3) / 2

        // 最大乘积
        val maxProduct = Math.pow(3.0, numOf3.toDouble()) * Math.pow(2.0, numOf2.toDouble())

        return maxProduct.toInt()
    }
}
```

## 4. 参考

* [https://leetcode-cn.com/problems/jian-sheng-zi-lcof/](https://leetcode-cn.com/problems/jian-sheng-zi-lcof/)
* [https://leetcode-cn.com/problems/jian-sheng-zi-lcof/solution/zi-jie-ti-ku-jian-14-i-zhong-deng-jian-sheng-zi-1s/](https://leetcode-cn.com/problems/jian-sheng-zi-lcof/solution/zi-jie-ti-ku-jian-14-i-zhong-deng-jian-sheng-zi-1s/)
* [《剑指Offer（第2版）》](https://book.douban.com/subject/27008702/)

