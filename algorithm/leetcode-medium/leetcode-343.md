---
title: 343. 整数拆分
date: '2020-07-30T13:43:57.000Z'
tags:
  - leetcode
  - java
  - kotlin
  - 动态规划
categories: 算法笔记
notshow: true
---

# 343. 整数拆分

## 1. [问题](https://leetcode-cn.com/problems/integer-break)

给定一个正整数 n，将其拆分为至少两个正整数的和，并使这些整数的乘积最大化。 返回你可以获得的最大乘积。

示例 1:

```text
输入: 2
输出: 1
解释: 2 = 1 + 1, 1 × 1 = 1。
```

示例 2:

```text
输入: 10
输出: 36
解释: 10 = 3 + 3 + 4, 3 × 3 × 4 = 36。
```

说明: 你可以假设 n 不小于 2 且不大于 58。 

## 2. 解法 - 动态规划

### 2.1 Java

```java
class Solution {
    public int integerBreak(int n) {
        // 状态数组
        // dp[i]表示正整数i的最大乘积
        int[] dp = new int[n + 1];

        // 边界条件
        // 0和1都是不可拆分的
        dp[0] = dp[1] = 0;

        // 状态转移方程
        for (int i=2;i<=n;i++) {
            int curMax = 0;
            for (int j=1;j<=i-1;j++) {
                // 假设i拆分出的第一个整数为j，剩下的部分为i-j，那么存在两种情况
                // 1. i-j不再继续拆分，那么乘积就是 j*(i-j)
                // 2. i-j继续拆分，拆成什么样随便他，反正乘积就是 j*dp[i-j]
                // 二者取较大值即可
                curMax = Math.max(curMax, Math.max(j * (i - j), j * dp[i - j]));
            }
            dp[i] = curMax;
        }

        return dp[n];
    }
}
```

### 2.2 Kotlin

```kotlin
class Solution {
    fun integerBreak(n: Int): Int {
        // 状态数组
        // dp[i]表示正整数i的最大乘积
        val dp = IntArray(n + 1)

        // 边界条件
        // 0和1都是不可拆分的
        dp[1] = 0
        dp[0] = dp[1]

        // 状态转移方程
        for (i in 2..n) {
            var curMax = 0
            for (j in 1..i - 1) {
                // 假设i拆分出的第一个整数为j，剩下的部分为i-j，那么存在两种情况
                // 1. i-j不再继续拆分，那么乘积就是 j*(i-j)
                // 2. i-j继续拆分，拆成什么样随便他，反正乘积就是 j*dp[i-j]
                // 二者取较大值即可
                curMax = Math.max(curMax, Math.max(j * (i - j), j * dp[i - j]))
            }
            dp[i] = curMax
        }

        return dp[n]
    }
}
```

## 3. 参考

* [https://leetcode-cn.com/problems/integer-break](https://leetcode-cn.com/problems/integer-break)
* [https://leetcode-cn.com/problems/integer-break/solution/zheng-shu-chai-fen-by-leetcode-solution/](https://leetcode-cn.com/problems/integer-break/solution/zheng-shu-chai-fen-by-leetcode-solution/)

## 4. 笔记

![](https://777blog.oss-cn-shanghai.aliyuncs.com/leetcode/leetcode-343-1.jpg) ![](https://777blog.oss-cn-shanghai.aliyuncs.com/leetcode/leetcode-343-2.jpg)

