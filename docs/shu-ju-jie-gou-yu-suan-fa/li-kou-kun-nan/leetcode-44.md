---
title: 44. 通配符匹配
date: 2020-07-05T17:29:21.000Z
tags:
  - leetcode
  - java
  - 动态规划
categories: 算法笔记
notshow: true
---

# 44. 通配符匹配

## [1. 问题](https://leetcode-cn.com/problems/wildcard-matching/)

给定一个字符串 \(s\) 和一个字符模式 \(p\) ，实现一个支持 '?' 和 '\*' 的通配符匹配。

'?' 可以匹配任何单个字符。 '\*' 可以匹配任意字符串（包括空字符串）。 两个字符串完全匹配才算匹配成功。

说明:

* s 可能为空，且只包含从 a-z 的小写字母。
* p 可能为空，且只包含从 a-z 的小写字母，以及字符 ? 和 \*。

示例 1:

> 输入: s = "aa" p = "a" 输出: false 解释: "a" 无法匹配 "aa" 整个字符串。

示例 2:

> 输入: s = "aa" p = "_" 输出: true 解释: '_' 可以匹配任意字符串。

示例 3:

> 输入: s = "cb" p = "?a" 输出: false 解释: '?' 可以匹配 'c', 但第二个 'a' 无法匹配 'b'。

示例 4:

> 输入: s = "adceb" p = "_a_b" 输出: true 解释: 第一个 '_' 可以匹配空字符串, 第二个 '_' 可以匹配字符串 "dce".

示例 5:

> 输入: s = "acdcb" p = "a\*c?b" 输出: false

## 2. 解法 - 动态规划

### 2.1 Java

```java
//dp
class Solution {
    public boolean isMatch(String s, String p) {
        // 两个串的长度
        int lenP = p.length();
        int lenS = s.length();

        // 状态数组
        // dp[i][j]表示p的前i个字符和s的前j个字符是否匹配
        boolean[][] dp = new boolean[lenP+1][lenS+1];

        // 空串匹配成功
        dp[0][0] = true;

        // 由于*可以匹配空串，所以需要考虑p以若干个*开头的情况
        for(int i=1;i<=lenP;i++) {
            if (p.charAt(i-1) != '*') {
                break;
            }
            dp[i][0] = true;
        }

        for (int i=1;i<=lenP;i++) {
            for (int j=1;j<=lenS;j++) {
                // p和s的当前字符可匹配
                // p的i-1对应dp的i
                if (p.charAt(i-1) == s.charAt(j-1) || p.charAt(i-1) == '?') {
                    dp[i][j] = dp[i-1][j-1];
                } else if (p.charAt(i-1) == '*') {
                    // dp[i-1][j]表示*匹配了空串
                    // dp[i][j-1]表示*匹配了当前位置的字符
                    // | 是不短路的或
                    dp[i][j] = dp[i-1][j] | dp[i][j-1];
                }
            }
        }

        return dp[lenP][lenS];
    }
}
```

## 3. 参考

* [https://leetcode-cn.com/problems/wildcard-matching](https://leetcode-cn.com/problems/wildcard-matching)
* [https://leetcode-cn.com/problems/wildcard-matching/solution/zi-fu-chuan-dong-tai-gui-hua-bi-xu-miao-dong-by-sw/](https://leetcode-cn.com/problems/wildcard-matching/solution/zi-fu-chuan-dong-tai-gui-hua-bi-xu-miao-dong-by-sw/)

## 4. 笔记

![](https://777blog.oss-cn-shanghai.aliyuncs.com/blog%20pic/leetcode44-1.jpg) ![](https://777blog.oss-cn-shanghai.aliyuncs.com/blog%20pic/leetcode44-2.jpg)

