# LEETCODE 97. 交错字符串

## 1. [问题](https://leetcode-cn.com/problems/interleaving-string)

给定三个字符串 s1, s2, s3, 验证 s3 是否是由 s1 和 s2 交错组成的。

示例 1：

```
输入：s1 = "aabcc", s2 = "dbbca", s3 = "aadbbcbcac"
输出：true
```

示例 2：

```
输入：s1 = "aabcc", s2 = "dbbca", s3 = "aadbbbaccc"
输出：false
```

## 2. 解法 - 动态规划

### 2.1 Java

```java
class Solution {
    public boolean isInterleave(String s1, String s2, String s3) {
        // 状态数组
        int len1 = s1.length();
        int len2 = s2.length();
        boolean[][] dp = new boolean[len1+1][len2+1];

        if (len1 + len2 != s3.length())
            return false;

        // 边界条件
        dp[0][0] = true;

        // 状态转移方程
        for (int i=0;i<=len1;i++) {
            for (int j=0;j<=len2;j++) {
                if (i > 0)
                    dp[i][j] =  dp[i][j] || dp[i-1][j] && s1.charAt(i-1) == s3.charAt(i+j-1);

                if (j > 0)
                    dp[i][j] = dp[i][j] || dp[i][j-1] && s2.charAt(j-1) == s3.charAt(i+j-1);
            }
        }

        return dp[len1][len2];
    }
}
```

### 2.2 Kotlin

```kotlin
class Solution {
    fun isInterleave(s1: String, s2: String, s3: String): Boolean {
        // 状态数组
        val len1 = s1.length
        val len2 = s2.length
        val dp = Array(len1 + 1) { BooleanArray(len2 + 1) }

        if (len1 + len2 != s3.length)
            return false

        // 边界条件
        dp[0][0] = true

        // 状态转移方程
        for (i in 0..len1) {
            for (j in 0..len2) {
                if (i > 0)
                    dp[i][j] = dp[i][j] || dp[i - 1][j] && s1[i - 1] == s3[i + j - 1]

                if (j > 0)
                    dp[i][j] = dp[i][j] || dp[i][j - 1] && s2[j - 1] == s3[i + j - 1]
            }
        }

        return dp[len1][len2]
    }
}
```

## 3. 参考

* [https://leetcode-cn.com/problems/interleaving-string](https://leetcode-cn.com/problems/interleaving-string)
* [https://leetcode-cn.com/problems/interleaving-string/solution/jiao-cuo-zi-fu-chuan-by-leetcode-solution/](https://leetcode-cn.com/problems/interleaving-string/solution/jiao-cuo-zi-fu-chuan-by-leetcode-solution/)

## 4. 笔记

![](https://777blog.oss-cn-shanghai.aliyuncs.com/leetcode/leetcode-97.jpg)
