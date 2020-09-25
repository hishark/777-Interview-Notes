---
title: 32. 最长有效括号
date: 2020-07-04 17:22:37
tags:
- leetcode
- java
- 字符串
- 栈
- 动态规划
categories: 算法笔记
notshow: true
---
## [1. 问题](https://leetcode-cn.com/problems/longest-valid-parentheses/)
给定一个只包含 '(' 和 ')' 的字符串，找出最长的包含有效括号的子串的长度。

示例 1:
>输入: "(()"
输出: 2
解释: 最长有效括号子串为 "()"
<!--more-->
示例 2:
>输入: ")()())"
输出: 4
解释: 最长有效括号子串为 "()()"

## 2. 解法
### 2.1 栈
```java
// 栈解法
class Solution {
    public int longestValidParentheses(String s) {
        Stack<Integer> stack = new Stack<>();
        int res = 0;
        int len = 0;
        int maxLen = 0;
        char[] strs = s.toCharArray();
        // 初始化栈，表示最长子串只能从0开始
        stack.push(-1);

        for (int i=0;i<strs.length;i++) {
            if (strs[i] == '(') {
                // 如果当前括号为左括号，直接入栈
                stack.push(i);
            } else {
                // 如果当前括号为右括号
                // 首先将栈顶元素出栈
                stack.pop();

                // 接着判断此时栈是否为空
                if (stack.empty()) {
                    // 如果栈为空，说明刚刚出栈的是右括号
                    // 直接把当前右括号的下标入栈即可
                    stack.push(i);
                } else {
                    // 如果栈不为空，说明刚刚出栈的是左括号
                    // 计算此时子串的长度
                    // 子串长度 = 当前下标 - 栈顶元素（即相匹配的左括号下标）
                    len = i - stack.peek();
                    // 更新最长子串长度
                    maxLen = Math.max(len, maxLen);
                }
            }
        }

        return maxLen;
    }
}
```

### 2.2 动态规划
```java
// 动态规划解法
class Solution {
    public int longestValidParentheses(String str) {
        // 状态数组
        // 初始值全都是0
        int[] dp = new int[str.length()];
        
        char[] s = str.toCharArray();
        
        int maxLen = 0;
        
        // 所有'('的dp值直接为0
        // ')'的dp值需要进一步计算
        // 从i=1开始遍历，因为i=0一个人无法凑出一对
        for (int i=1;i<s.length;i++) {
            // 如果s[i]=')'且s[i-1]='(' 那么配对成功
            if (s[i] == ')' && s[i-1] == '(') {
                
                dp[i] = ( i >=2 ? dp[i-2] : 0 ) + 2;
            } else if (s[i] == ')' && s[i-1] == ')') {// 如果s[i]和s[i-1]都是')' 画个图缕清一下关系就成了
                // 如果s[i-dp[i-1]-1]='(' 那么和s[i]配对成功
                if ( i - dp[i-1] >= 1 && s[i - dp[i-1] - 1] == '(') {
                    // i-dp[i-1]>=2 是为了保证 i-dp[i-1]-2不越界
                    dp[i] = dp[i - 1] + ( i - dp[i-1] >= 2 ? dp[i - dp[i-1] -2] : 0) + 2;
                }
                
            }
            maxLen = Math.max(maxLen, dp[i]);
        }
        
        return maxLen;
    }
}
```

## 3. 参考
- [https://leetcode-cn.com/problems/longest-valid-parentheses](https://leetcode-cn.com/problems/longest-valid-parentheses)
- [https://leetcode-cn.com/problems/longest-valid-parentheses/solution/zui-chang-you-xiao-gua-hao-by-leetcode-solution/](https://leetcode-cn.com/problems/longest-valid-parentheses/solution/zui-chang-you-xiao-gua-hao-by-leetcode-solution/)

## 4. 笔记
![](https://777blog.oss-cn-shanghai.aliyuncs.com/blog%20pic/leetcode32-1.jpg)
![](https://777blog.oss-cn-shanghai.aliyuncs.com/blog%20pic/leetcode32-2.jpg)
![](https://777blog.oss-cn-shanghai.aliyuncs.com/blog%20pic/leetcode32-3.jpg)
![](https://777blog.oss-cn-shanghai.aliyuncs.com/blog%20pic/leetcode32-4.jpg)