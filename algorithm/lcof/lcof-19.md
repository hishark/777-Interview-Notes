---
title: 19. 正则表达式匹配
date: '2020-09-10T16:51:19.000Z'
tags:
  - 动态规划
  - leetcode
  - lcof
  - java
  - kotlin
categories: 算法笔记
---

# \*19. 正则表达式匹配

## 1. [问题](https://leetcode-cn.com/problems/zheng-ze-biao-da-shi-pi-pei-lcof)

请实现一个函数用来匹配包含 '.' 和 '\*' 的正则表达式。模式中的字符 '.' 表示任意一个字符，而 '\*' 表示它前面的字符可以出现任意次（含0次）。在本题中，匹配是指字符串的所有字符匹配整个模式。例如，字符串 "aaa" 与模式 "a.a" 和 "ab_ac_a" 匹配，但与 "aa.a" 和 "ab\*a" 均不匹配。

示例 1:

```text
输入:
s = "aa"
p = "a"
输出: false
解释: "a" 无法匹配 "aa" 整个字符串。
```

示例 2:

```text
输入:
s = "aa"
p = "a*"
输出: true
解释: 因为 '*' 代表可以匹配零个或多个前面的那一个元素, 在这里前面的元素就是 'a'。因此，字符串 "aa" 可被视为 'a' 重复了一次。
```

示例 3:

```text
输入:
s = "ab"
p = ".*"
输出: true
解释: ".*" 表示可匹配零个或多个（'*'）任意字符（'.'）。
```

示例 4:

```text
输入:
s = "aab"
p = "c*a*b"
输出: true
解释: 因为 '*' 表示零个或多个，这里 'c' 为 0 个, 'a' 被重复一次。因此可以匹配字符串 "aab"。
```

示例 5:

```text
输入:
s = "mississippi"
p = "mis*is*p*."
输出: false
s 可能为空，且只包含从 a-z 的小写字母。
p 可能为空，且只包含从 a-z 的小写字母以及字符 . 和 *，无连续的 '*'。
```

## 2. 解法 - 动态规划

> 还有一种递归解法，暂时搁置。

### 2.1 Java

```java
class Solution {
    public boolean isMatch(String A, String B) {
        /**
         * 解题思路
         * 
         * 假设字符串为A，正则表达式为B，假设A的长度为n，B的长度为m 要判断A和B是否可以匹配，可以根据B的最后一个字符来分类讨论： 1.
         * B的最后一个字符是普通字符，就只要看A[n-1]和B[m-1]是否相等 a.
         * 若A[n-1]=B[m-1]，那么就看A[0,n-2]和B[0,m-2]是否匹配 b. 若A[n-1]!=B[m-1]，那么可以得出，A和B无法匹配 2.
         * 若B的最后一个字符是「.」，由于它可以匹配任何字符，所以直接看A[0,n-2]和B[0,m-2]是否匹配 3.
         * 若B的最后一个字符是「*」，假设B[m-2]=c，那么c可以重复0次或者多次，这些连续的c组合成为c* a.
         * 如果A[n-1]不是c，那么B的最后两个字符就没有任何作用了，A和B能否匹配取决于A[0,n-1]和B[0,m-3]是否能匹配 b.
         * 如果A[n-1]是多个c中的最后一个，这种情况下A[n-1]为c或者「.」，因为有多个c，所以A[n-1]匹配成功之后往前挪一个字符，继续看A[0,n-2]和B[0,m-1]是否匹配
         */

        int n = A.length();
        int m = B.length();

        /**
         * 状态数组 dp[i][j]表示A的前i个字符和B的前j个字符能否匹配成功
         * 数组长度开[n+1][m+1]，这样方便处理空串，题目所求结果就是dp[n][m]
         */

        boolean[][] dp = new boolean[n + 1][m + 1];

        /**
         * 边界条件 1. 空字符串和空正则表达式，可匹配，dp[0][0]=true 2. 空字符串和非空正则表达式，不一定是false，需要推算，比如A=""
         * B="a*b*c*"时就是匹配的 3. 非空字符串和空正则表达式，一定不匹配，dp[1][0]=dp[2][0]=...=dp[n][0]=false
         * 4. 非空字符串和非空正则表达式，需要推算。
         */
        dp[0][0] = true;
        for (int i = 1; i <= n; i++) {
            dp[i][0] = false;
        }

        // 状态转移
        for (int i = 0; i <= n; i++) {
            for (int j = 0; j <= m; j++) {
                // 正则表达式为空，也就是j为0的边界情况都已经在上面赋值过了
                // 正则表达式非空，j不为0
                if (j != 0) {
                    // 正则表达式非空时，要分为两种情况，看B最后一个字符是不是「*」
                    // 若B最后一个字符不为「*」
                    if (B.charAt(j - 1) != '*') {
                        if (i >= 1 && (A.charAt(i - 1) == B.charAt(j - 1) || B.charAt(j - 1) == '.'))
                            dp[i][j] = dp[i - 1][j - 1];
                    } else {
                        // 若B最后一个字符为「*」，分两种情况，也就是解题思路中的3.a和3.b
                        // 碰到c*，如果不看*的话，那么正则表达式B的最后两个字符没有起作用，砍掉这两个字符
                        if (j >= 2)
                            dp[i][j] = dp[i][j - 2];

                        // 碰到c*，如果要看*的话，不管正则表达式B，字符串A往前移一个字符dp[i][j] = dp[i-1][j]
                        if (i >= 1 && j >= 2 && (A.charAt(i - 1) == B.charAt(j - 2) || B.charAt(j - 2) == '.'))
                            dp[i][j] |= dp[i - 1][j];

                        // 使用「 | 」是因为以上两种情况只要有一种情况匹配就算是匹配

                    }
                }
            }
        }

        return dp[n][m];
    }
}
```

### 2.2 Kotlin

```kotlin
class Solution {
    fun isMatch(A: String, B: String): Boolean {
        /**
         * 解题思路
         *
         * 假设字符串为A，正则表达式为B，假设A的长度为n，B的长度为m 要判断A和B是否可以匹配，可以根据B的最后一个字符来分类讨论： 1.
         * B的最后一个字符是普通字符，就只要看A[n-1]和B[m-1]是否相等 a.
         * 若A[n-1]=B[m-1]，那么就看A[0,n-2]和B[0,m-2]是否匹配 b. 若A[n-1]!=B[m-1]，那么可以得出，A和B无法匹配 2.
         * 若B的最后一个字符是「.」，由于它可以匹配任何字符，所以直接看A[0,n-2]和B[0,m-2]是否匹配 3.
         * 若B的最后一个字符是「*」，假设B[m-2]=c，那么c可以重复0次或者多次，这些连续的c组合成为c* a.
         * 如果A[n-1]不是c，那么B的最后两个字符就没有任何作用了，A和B能否匹配取决于A[0,n-1]和B[0,m-3]是否能匹配 b.
         * 如果A[n-1]是多个c中的最后一个，这种情况下A[n-1]为c或者「.」，因为有多个c，所以A[n-1]匹配成功之后往前挪一个字符，继续看A[0,n-2]和B[0,m-1]是否匹配
         */

        val n = A.length
        val m = B.length

        /**
         * 状态数组 dp[i][j]表示A的前i个字符和B的前j个字符能否匹配成功
         * 数组长度开[n+1][m+1]，这样方便处理空串，题目所求结果就是dp[n][m]
         */

        val dp = Array(n + 1) { BooleanArray(m + 1) }

        /**
         * 边界条件 1. 空字符串和空正则表达式，可匹配，dp[0][0]=true 2. 空字符串和非空正则表达式，不一定是false，需要推算，比如A=""
         * B="a*b*c*"时就是匹配的 3. 非空字符串和空正则表达式，一定不匹配，dp[1][0]=dp[2][0]=...=dp[n][0]=false
         * 4. 非空字符串和非空正则表达式，需要推算。
         */
        dp[0][0] = true
        for (i in 1..n) {
            dp[i][0] = false
        }

        // 状态转移
        for (i in 0..n) {
            for (j in 0..m) {
                // 正则表达式为空，也就是j为0的边界情况都已经在上面赋值过了
                // 正则表达式非空，j不为0
                if (j != 0) {
                    // 正则表达式非空时，要分为两种情况，看B最后一个字符是不是「*」
                    // 若B最后一个字符不为「*」
                    if (B[j - 1] != '*') {
                        if (i >= 1 && (A[i - 1] == B[j - 1] || B[j - 1] == '.'))
                            dp[i][j] = dp[i - 1][j - 1]
                    } else {
                        // 若B最后一个字符为「*」，分两种情况，也就是解题思路中的3.a和3.b
                        // 碰到c*，如果不看*的话，那么正则表达式B的最后两个字符没有起作用，砍掉这两个字符
                        if (j >= 2)
                            dp[i][j] = dp[i][j - 2]

                        // 碰到c*，如果要看*的话，不管正则表达式B，字符串A往前移一个字符dp[i][j] = dp[i-1][j]
                        if (i >= 1 && j >= 2 && (A[i - 1] == B[j - 2] || B[j - 2] == '.'))
                            dp[i][j] = dp[i][j] or dp[i - 1][j]

                        // 使用「 | 」是因为以上两种情况只要有一种情况匹配就算是匹配

                    }
                }
            }
        }

        return dp[n][m]
    }
}
```

## 3. 参考

* [https://leetcode-cn.com/problems/zheng-ze-biao-da-shi-pi-pei-lcof/](https://leetcode-cn.com/problems/zheng-ze-biao-da-shi-pi-pei-lcof/)
* [https://leetcode-cn.com/problems/zheng-ze-biao-da-shi-pi-pei-lcof/solution/zhu-xing-xiang-xi-jiang-jie-you-qian-ru-shen-by-je/](https://leetcode-cn.com/problems/zheng-ze-biao-da-shi-pi-pei-lcof/solution/zhu-xing-xiang-xi-jiang-jie-you-qian-ru-shen-by-je/)

