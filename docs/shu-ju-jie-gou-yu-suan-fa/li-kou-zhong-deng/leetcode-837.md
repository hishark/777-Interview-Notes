---
title: 837. 新21点
date: '2020-06-09T14:53:44.000Z'
tags:
  - 动态规划
  - leetcode
  - java
  - kotlin
categories: 算法笔记
notshow: true
---

# leetcode-837

## [1. 问题](https://leetcode-cn.com/problems/new-21-game/)

爱丽丝参与一个大致基于纸牌游戏 “21点” 规则的游戏，描述如下：

爱丽丝以 0 分开始，并在她的得分少于 K 分时抽取数字。 抽取时，她从 \[1, W\] 的范围中随机获得一个整数作为分数进行累计，其中 W 是整数。 每次抽取都是独立的，其结果具有相同的概率。

当爱丽丝获得不少于 K 分时，她就停止抽取数字。 爱丽丝的分数不超过 N 的概率是多少？

示例 1：

> 输入：N = 10, K = 1, W = 10 输出：1.00000 说明：爱丽丝得到一张卡，然后停止。  示例 2： 输入：N = 6, K = 1, W = 10 输出：0.60000 说明：爱丽丝得到一张卡，然后停止。 在 W = 10 的 6 种可能下，她的得分不超过 N = 6 分。

示例 3：

> 输入：N = 21, K = 17, W = 10 输出：0.73278 提示：
>
> * 0 &lt;= K &lt;= N &lt;= 10000
> * 1 &lt;= W &lt;= 10000
> * 如果答案与正确答案的误差不超过10^-5，则该答案将被视为正确答案通过。
> * 此问题的判断限制时间已经减少。

## 2. 解法 - 动态规划

### 2.1 Java

```java
class Solution {
    public double new21Game(int N, int K, int W) {
        // 状态数组 - dp[x]表示手上牌面为x的获胜概率
        double[] dp = new double[K+W];
        double s = 0.0;
        // 填格子：[k, k+w-1]
        for (int i=K;i<=K+W-1;i++) {
            dp[i] = (i<=N ? 1.0 : 0.0);
            s += dp[i];
        }

        // 填格子：[0, k-1] 从右往左填
        // s每次减去前一个区间的最后一个，然后加上自己
        for (int i=K-1;i>=0;i--) {
            dp[i] = s/W;
            s = s - dp[i+W] + dp[i];
        }

        return dp[0];
    }
}
```

### 2.2 Kotlin

```kotlin
class Solution {
    fun new21Game(N: Int, K: Int, W: Int): Double {
        // 状态数组 - dp[x]表示手上牌面为x的获胜概率
        var dp = DoubleArray(K+W)
        var s = 0.0
        // 填格子：[k, k+w-1]
        for(i in K..K+W-1){
            dp[i] = if(i<=N) 1.0 else 0.0
            s += dp[i]
        }

        // 填格子：[0, k-1] 从右往左填
        // s每次减去前一个区间的最后一个，然后加上自己
        for(i in K-1 downTo 0){
            dp[i] = s/W;
            s = s - dp[i+W] + dp[i];
        }

        return dp[0]
    }
}
```

## 3. 参考

* [https://leetcode-cn.com/problems/new-21-game](https://leetcode-cn.com/problems/new-21-game)
* [https://leetcode-cn.com/problems/new-21-game/solution/huan-you-bi-zhe-geng-jian-dan-de-ti-jie-ma-tian-ge/](https://leetcode-cn.com/problems/new-21-game/solution/huan-you-bi-zhe-geng-jian-dan-de-ti-jie-ma-tian-ge/)

## 4. 学习草稿

![](https://777blog.oss-cn-shanghai.aliyuncs.com/blog%20pic/IMG_3924%202.JPEG)

