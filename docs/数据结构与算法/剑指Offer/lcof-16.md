---
title: 16. 数值的整数次方
date: 2020-09-04 18:49:46
tags:
- 递归
- 分治
- 二进制
- 位运算
- leetcode
- lcof
- java
- kotlin
categories: 算法笔记
---
# 16. 数值的整数次方
## 1. [问题](https://leetcode-cn.com/problems/shu-zhi-de-zheng-shu-ci-fang-lcof)
实现函数double Power(double base, int exponent)，求base的exponent次方。不得使用库函数，同时不需要考虑大数问题。

<!--more-->

示例 1:
```
输入: 2.00000, 10
输出: 1024.00000
```

示例 2:
```
输入: 2.10000, 3
输出: 9.26100
```

示例 3:
```
输入: 2.00000, -2
输出: 0.25000
解释: 2-2 = 1/22 = 1/4 = 0.25
```

说明:

- -100.0 < x < 100.0
- n 是 32 位有符号整数，其数值范围是 [−2^31, 2^31 − 1]。


## 2. 解法 - 分治 递归
n 的范围是[−2^31, 2^31 − 1]，当 n = -2^31 时，执行 -n 操作会导致越界，所以需要将 n 转换成 long 类型来计算。

>可以用右移运算符代替除以2，用位与运算符代替求余符号（%）来判断一个数是奇数还是偶数，位运算的效率比乘除法及求余运算的效率要高很多。


### 2.1 Java
```java
// 分治算法 递归
class Solution {
    public double myPow(double x, int n) {
        /**
         * 求 x ^ n
         * n 的范围是 [−2^31, 2^31 − 1] 即 int 的范围
         * 但是 -n 操作会导致越界，所以需要将 n 转换成 long 类型来计算
         */
        long N = n;
        
        // 下面3个N别不小心写成n啦
        if (N < 0) {
            return 1 / myPow(x, -N);
        }
        return myPow(x, N);
    }

    public double myPow(double x, long n) {
        // 边界处理
        if (n == 0)
            return 1;

        if (x == 1)
            return 1;

        // 奇偶次幂分别处理
        // 偶次幂
        if (n % 2 == 0) {
            // 分治 - 分
            double square = myPow(x, n / 2);
            // 分治 - 合
            return  square * square;
        } else { // 奇次幂
            // 分治 - 分
            double square = myPow(x, (n - 1) / 2);
            // 分治 - 合
            return square * square * x;
        }
    }
}
```

### 2.2 Kotlin
```kotlin
// 分治算法 递归
class Solution {
    fun myPow(x: Double, n: Int): Double {
        /**
         * 求 x ^ n
         * n 的范围是 [−2^31, 2^31 − 1] 即 int 的范围
         * 但是 -n 操作会导致越界，所以需要将 n 转换成 long 类型来计算
         */
        val N = n.toLong()

        // 下面3个N别不小心写成n啦
        return if (N < 0) {
            1 / myPow(x, -N)
        } else myPow(x, N)
    }

    fun myPow(x: Double, n: Long): Double {
        // 边界处理
        if (n == 0L)
            return 1.0

        if (x == 1.0)
            return 1.0

        // 奇偶次幂分别处理
        // 偶次幂
        if (n % 2 == 0L) {
            // 分治 - 分
            val square = myPow(x, n / 2)
            // 分治 - 合
            return square * square
        } else { // 奇次幂
            // 分治 - 分
            val square = myPow(x, (n - 1) / 2)
            // 分治 - 合
            return square * square * x
        }
    }
}
```

## 3. 解法 - [快速幂](https://baike.baidu.com/item/%E5%BF%AB%E9%80%9F%E5%B9%82/5500243?fr=aladdin)
n 的范围是[−2^31, 2^31 − 1]，当 n = -2^31 时，执行 -n 操作会导致越界，所以需要将n转换成long类型来计算。

### 3.1 Java
```java
class Solution {
    public double myPow(double x, int n) {
        /**
         * 求 x ^ n
         * n 的范围是 [−2^31, 2^31 − 1] 即 int 的范围
         * 但是 -n 操作会导致越界，所以需要将 n 转换成 long 类型来计算
         */
        long N = n;

        if(N < 0) {
            x = 1 / x;
            N = -N;
        }

        /**
         * 把指数 n 看成二进制数，比如 11 的二进制为 1011
         * 11 = 1*2^3 + 0*2^2 + 1*2^1 + 1*2^0
         * x^11 = x^(2^3) * x^(2^1) * x^(2^0)
         */
        double ans = 1;
        // 指数不为0
        while (N > 0) {
            // 将N转换为二进制数，从最低位开始
            // 如果当前位的二进制为1，那么就需要给 ans 乘上当前的 x
            if (N % 2 == 1) {
                ans *= x;
            }

            // x每一轮循环都要通过累乘来增加
            x *= x; // 假设 x 的初始值为3，那么x的值为：3^(2^0), 3^(2^1), 3^(2^2) ...
            // 解决完当前二进制位，将 N/2 继续求下一位
            N /= 2; // 这里也可以用右移来代替：N >>= 1;
        }
        return ans;
    }
}
```

### 3.2 Kotlin
```kotlin
class Solution {
    fun myPow(x: Double, n: Int): Double {
        var x = x
        /**
         * 求 x ^ n
         * n 的范围是 [−2^31, 2^31 − 1] 即 int 的范围
         * 但是 -n 操作会导致越界，所以需要将 n 转换成 long 类型来计算
         */
        var N = n.toLong()

        if (N < 0) {
            x = 1 / x
            N = -N
        }

        /**
         * 把指数 n 看成二进制数，比如 11 的二进制为 1011
         * 11 = 1*2^3 + 0*2^2 + 1*2^1 + 1*2^0
         * x^11 = x^(2^3) * x^(2^1) * x^(2^0)
         */
        var ans = 1.0
        // 指数不为0
        while (N > 0) {
            // 将N转换为二进制数，从最低位开始
            // 如果当前位的二进制为1，那么就需要给 ans 乘上当前的 x
            if (N % 2 == 1L) {
                ans *= x
            }

            // x每一轮循环都要通过累乘来增加
            x *= x // 假设 x 的初始值为3，那么x的值为：3^(2^0), 3^(2^1), 3^(2^2) ...
            // 解决完当前二进制位，将 N/2 继续求下一位
            N /= 2 // 这里也可以用右移来代替：N >>= 1
        }
        return ans
    }
}
```

## 4. 参考
- [https://leetcode-cn.com/problems/shu-zhi-de-zheng-shu-ci-fang-lcof](https://leetcode-cn.com/problems/shu-zhi-de-zheng-shu-ci-fang-lcof)
- [https://leetcode-cn.com/problems/shu-zhi-de-zheng-shu-ci-fang-lcof/solution/di-gui-xie-fa-fen-zhi-si-xiang-yu-fei-di-gui-xie-f/](https://leetcode-cn.com/problems/shu-zhi-de-zheng-shu-ci-fang-lcof/solution/di-gui-xie-fa-fen-zhi-si-xiang-yu-fei-di-gui-xie-f/)
- [《剑指Offer（第2版）》](https://book.douban.com/subject/27008702/)