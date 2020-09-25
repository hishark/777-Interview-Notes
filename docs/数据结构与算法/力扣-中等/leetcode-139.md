---
title: 139. 单词拆分
date: 2020-06-30 11:01:38
tags:
- leetcode
- java
- 动态规划
categories: 算法笔记
notshow: true
---
## [1. 问题](https://leetcode-cn.com/problems/word-break/)
给定一个非空字符串 s 和一个包含非空单词列表的字典 wordDict，判定 s 是否可以被空格拆分为一个或多个在字典中出现的单词。

说明：
- 拆分时可以重复使用字典中的单词。
- 你可以假设字典中没有重复的单词。

示例 1：
>输入: s = "leetcode", wordDict = ["leet", "code"]
输出: true
解释: 返回 true 因为 "leetcode" 可以被拆分成 "leet code"。
<!--more-->

示例 2：
>输入: s = "applepenapple", wordDict = ["apple", "pen"]
输出: true
解释: 返回 true 因为 "applepenapple" 可以被拆分成 "apple pen apple"。注意你可以重复使用字典中的单词。

示例 3：
>输入: s = "catsandog", wordDict = ["cats", "dog", "sand", "and", "cat"]
输出: false

## 2. 解法
```java
class Solution {
    public boolean wordBreak(String s, List<String> wordDict) {
        int length = s.length();
        Set<String> dictSet = new HashSet(wordDict);

        // 状态数组
        boolean[] dp = new boolean[length+1];

        // 边界条件
        dp[0] = true;

        // 状态方程
        for (int i=1;i<=length;i++) {
            for (int j=0;j<i;j++) {
                dp[i] = dp[j] && dictSet.contains(s.substring(j, i));
                if(dp[i]==true)
                    break;
            }
        }
        return dp[length];
    }

}
```

## 3. 参考
- https://leetcode-cn.com/problems/word-break
- https://leetcode-cn.com/problems/word-break/solution/dan-ci-chai-fen-by-leetcode-solution/

## 4. 笔记
![](https://777blog.oss-cn-shanghai.aliyuncs.com/blog%20pic/leetcode139.jpg)