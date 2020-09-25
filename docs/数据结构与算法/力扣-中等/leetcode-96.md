---
title: 96. 不同的二叉搜索树
date: 2020-07-15 16:24:48
tags:
- leetcode
- java
- 树
- 动态规划
categories: 算法笔记
notshow: true
---
## 1. [问题](https://leetcode-cn.com/problems/unique-binary-search-trees)
给定一个整数 n，求以 1 ... n 为节点组成的二叉搜索树有多少种？

示例:
```
输入: 3
输出: 5
解释:
给定 n = 3, 一共有 5 种不同结构的二叉搜索树:

   1         3     3      2      1
    \       /     /      / \      \
     3     2     1      1   3      2
    /     /       \                 \
   2     1         2                 3
```

<!--more-->

## 2. 解法 - 动态规划

### 2.1 Java
```java
class Solution {
    public int numTrees(int n) {
        // 状态数组
        int[] dp = new int[n+1];
        // 边界条件
        dp[0] = 1;
        dp[1] = 1;
        
        // 状态转移方程
        for(int i = 2; i <= n; i++)
            for(int j = 1; j <= i; j++) 
                dp[i] += dp[j-1] * dp[i-j];
        
        return dp[n];
    }
}
```

## 3. 参考
- [https://leetcode-cn.com/problems/unique-binary-search-trees/](https://leetcode-cn.com/problems/unique-binary-search-trees/)
- [https://leetcode-cn.com/problems/unique-binary-search-trees/solution/bu-tong-de-er-cha-sou-suo-shu-by-leetcode-solution/](https://leetcode-cn.com/problems/unique-binary-search-trees/solution/bu-tong-de-er-cha-sou-suo-shu-by-leetcode-solution/)

## 4. 笔记
![](https://777blog.oss-cn-shanghai.aliyuncs.com/leetcode/leetcode-96-1.jpg)
![](https://777blog.oss-cn-shanghai.aliyuncs.com/leetcode/leetcode-96-2.jpg)