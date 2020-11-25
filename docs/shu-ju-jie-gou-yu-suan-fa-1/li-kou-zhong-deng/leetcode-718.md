---
title: 718. 最长重复子数组
date: '2020-07-01T17:17:03.000Z'
tags:
  - 动态规划
  - leetcode
  - java
categories: 算法笔记
notshow: true
---

# 718. 最长重复子数组

## [1. 问题](https://leetcode-cn.com/problems/maximum-length-of-repeated-subarray/)

给两个整数数组 A 和 B ，返回两个数组中公共的、长度最长的子数组的长度。

示例：

> 输入： A: \[1,2,3,2,1\] B: \[3,2,1,4,7\] 输出：3 解释： 长度最长的公共子数组是 \[3, 2, 1\] 。

提示：

* 1 &lt;= len\(A\), len\(B\) &lt;= 1000
* 0 &lt;= A\[i\], B\[i\] &lt; 100

## 2. 解法

### 2.1 暴力

```java
// 暴力法 - 计算最长公共前缀
// 这个方法会超时！
class Solution {
    public int findLength(int[] A, int[] B) {
        // 结果，最长重复子数组的长度
        int ans = 0;
        // 每次比较时最长公共前缀的长度
        int len = 0;
        for (int i=0;i<A.length;i++) {
            for (int j=0;j<B.length;j++) {
                len = 0;
                while(i+len<A.length && j+len<B.length && A[i+len] == B[j+len])
                    len++;
                ans = Math.max(ans, len);
            }
        }
        return ans;
    }
}
```

### 2.2 动态规划

```java
// 动态规划
class Solution {
    public int findLength(int[] A, int[] B) {
        // 状态数组
        // dp[i][j]表示A[i:]和B[j:]最长公共前缀的长度
        int[][] dp = new int[A.length+1][B.length+1];

        // 结果
        int ans = 0;

        for (int i=A.length-1;i>=0;i--) {
            for(int j=B.length-1;j>=0;j--) {
                // 状态转移方程
                // dp[i][j] = dp[i+1][j+1] + 1 (A[i]==B[j])
                // dp[i][j] = 0 (A[i]!=B[j])
                dp[i][j] = A[i]==B[j] ? dp[i+1][j+1] + 1 : 0;
                ans = Math.max(ans, dp[i][j]);
            }
        }

        return ans;
    }
}
```

## 3. 参考

* [https://leetcode-cn.com/problems/maximum-length-of-repeated-subarray](https://leetcode-cn.com/problems/maximum-length-of-repeated-subarray)
* [https://leetcode-cn.com/problems/maximum-length-of-repeated-subarray/solution/zui-chang-zhong-fu-zi-shu-zu-by-leetcode-solution/](https://leetcode-cn.com/problems/maximum-length-of-repeated-subarray/solution/zui-chang-zhong-fu-zi-shu-zu-by-leetcode-solution/)

## 4. 笔记

![](https://777blog.oss-cn-shanghai.aliyuncs.com/blog%20pic/leetcode718-1.jpg) ![](https://777blog.oss-cn-shanghai.aliyuncs.com/blog%20pic/leetcode718-2.jpg)

