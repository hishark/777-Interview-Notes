---
title: 9. 回文数
date: 2020-06-10 13:13:29
tags:
- leetcode
- java
- kotlin
- 数学
categories: 算法笔记
notshow: true
---
## [1. 问题](https://leetcode-cn.com/problems/palindrome-number/)
判断一个整数是否是回文数。回文数是指正序（从左向右）和倒序（从右向左）读都是一样的整数。

示例 1:
>输入: 121
输出: true
<!--more-->
示例 2:
>输入: -121
输出: false
解释: 从左向右读, 为 -121 。 从右向左读, 为 121- 。因此它不是一个回文数。

示例 3:
>输入: 10
输出: false
解释: 从右向左读, 为 01 。因此它不是一个回文数。

进阶:
你能不将整数转为字符串来解决这个问题吗？

## 2. 解法
### 2.1 Java
```java
class Solution {
    public boolean isPalindrome(int x) {
        // 临界情况处理
        // 1. 负数一定不是回文数
        if (x<0) return false;
        // 2. 大于0且个位数为0的数一定不是回文数
        if (x>0 && x%10==0) return false;

        // 对后半部分的数字进行反转，反转后得到的数字为xr
        // 循环结束条件：x <= xr 
        int xr = 0;
        while (x > xr) {
            // 取x的最后一位
            xr = xr*10 + x%10;
            x/=10;
        }

        // 循环结束后，得到了新的x和xr，接下来比较x和xr即可
        // 当x为奇数时，比较x和xr/10是否相同，若相同，则x为回文数
        // 当x为偶数时，比较x和xr是否相同，若相同，则x为回文数
        return x == xr/10 || x == xr;
    }
}
```
### 2.2 Kotlin
```kotlin
class Solution {
    fun isPalindrome(xx: Int): Boolean {
        // 临界情况处理
        // 1. 负数一定不是回文数
        var x = xx
        if (x<0) return false
        // 2. 大于0且个位数为0的数一定不是回文数
        if ((x>0) and (x%10==0)) return false

        // 对后半部分的数字进行反转，反转后得到的数字为xr
        // 循环结束条件：x <= xr 
        var xr = 0
        while (x > xr) {
            // 取x的最后一位
            xr = xr*10 + x%10
            x /= 10
        }

        // 循环结束后，得到了新的x和xr，接下来比较x和xr即可
        // 当x为奇数时，比较x和xr/10是否相同，若相同，则x为回文数
        // 当x为偶数时，比较x和xr是否相同，若相同，则x为回文数
        return (x == xr/10) or (x == xr)
    }
}
```
## 3. 参考
- [力扣：9. 回文数](https://leetcode-cn.com/problems/palindrome-number/)
- [力扣官方题解：回文数](https://leetcode-cn.com/problems/palindrome-number/solution/hui-wen-shu-by-leetcode-solution/)

## 4. 学习草稿
![](https://777blog.oss-cn-shanghai.aliyuncs.com/blog%20pic/leetcode9.JPG)
