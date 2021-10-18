# LEETCODE 5. 最长回文子串

## 1. [问题](https://leetcode-cn.com/problems/longest-palindromic-substring/)

给定一个字符串 `s`，找到 `s` 中最长的回文子串。你可以假设 `s` 的最大长度为 1000。

**示例 1：**

```
输入: "babad"
输出: "bab"
注意: "aba" 也是一个有效答案。
```

**示例 2：**

```
输入: "cbbd"
输出: "bb"
```

## 2. 标签

* 字符串
* 动态规划

## 3. 解法 - 动态规划

### 3.1 Java

```java
class Solution {
    public String longestPalindrome(String s) {
        // 字符串长度
        int n = s.length();
        // 状态转移数组
        // dp[i][j] 表示 s[i,j] 是否为回文串
        boolean[][] dp = new boolean[n][n];
        // 最长回文子串
        String ans = "";
        // l 是当前判断的字符串的长度减 1
        for (int l = 0; l < n; ++l) {
            // i为子串的左端点，j为子串的右端点
            for (int i = 0; i + l < n; ++i) {
                // 右端点 j
                int j = i + l;
                // 如果字符串长度为 1，显然为回文串
                if (l == 0) {
                    dp[i][j] = true;
                    // 如果字符串长度为 2，如果两个字符相等，就为回文串
                } else if (l == 1) {
                    dp[i][j] = (s.charAt(i) == s.charAt(j));
                } else {
                    // 如果字符串长度大于 2，那么只要判断【首尾字符是否相等，中间的字符串是否为回文串】即可
                    dp[i][j] = (s.charAt(i) == s.charAt(j) && dp[i + 1][j - 1]);
                }

                // 不停的更新最长的子串即可
                if (dp[i][j] && l + 1 > ans.length()) {
                    ans = s.substring(i, i + l + 1); // substring(i, j+1)也可以，一个意思
                }
            }
        }
        return ans;
    }
}


class Solution {
    public String longestPalindrome(String s) {
        int n = s.length();
        // dp[i][j] s[i,j] is huiwen?
        boolean[][] dp = new boolean[n][n];
        
        String res = "";
        
        // 长度为len的字符串
        for(int len=1;len<=n;len++) {
            // 遍历左端点
            for (int left=0;left+len-1<n;left++) {
                // 找到右端点
                int right = left + len - 1;
                
                // 开始判断是否为回文字符串
                if (len == 1) {
                    dp[left][right] = true;
                } else if (len == 2) {
                    if (s.charAt(left) == s.charAt(right)) {
                        dp[left][right] = true;
                    } else {
                        dp[left][right] = false;
                    }
                } else {
                    if (s.charAt(left) == s.charAt(right)) {
                        dp[left][right] = dp[left+1][right-1];
                    } else {
                        dp[left][right] = false;
                    }
                } 
                
                if (dp[left][right] == true && len > res.length()) {
                    res = s.substring(left, right+1);
                }
            }
        }
        return res;
    }
}
```

### 3.2 复杂度分析

* 时间复杂度 `O(n^2)` ：其中 n 是字符串的长度。动态规划的状态总数为 `O(n^2)`，对于每个状态，我们需要转移的时间为 `O(1)`。
* 空间复杂度 `O(n^2)` ：状态转移数组 dp 占用的空间。

## 4. 参考

* [https://leetcode-cn.com/problems/longest-palindromic-substring/](https://leetcode-cn.com/problems/longest-palindromic-substring/)
* [https://leetcode-cn.com/problems/longest-palindromic-substring/solution/zui-chang-hui-wen-zi-chuan-by-leetcode-solution/](https://leetcode-cn.com/problems/longest-palindromic-substring/solution/zui-chang-hui-wen-zi-chuan-by-leetcode-solution/)
