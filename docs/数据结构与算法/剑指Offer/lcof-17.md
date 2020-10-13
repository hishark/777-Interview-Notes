---
title: 17. 打印从1到最大的n位数
date: 2020-09-09 10:09:41
tags:
- 数学
- leetcode
- lcof
- java
- kotlin
categories: 算法笔记
---
# 17. 打印从1到最大的n位数
## 1. [问题](https://leetcode-cn.com/problems/da-yin-cong-1dao-zui-da-de-nwei-shu-lcof/)
输入数字 n，按顺序打印出从 1 到最大的 n 位十进制数。比如输入 3，则打印出 1、2、3 一直到最大的 3 位数 999。

<!--more-->

示例 1:
```
输入: n = 1
输出: [1,2,3,4,5,6,7,8,9]
```

说明：

- 用返回一个整数列表来代替打印
- n 为正整数

## 2. 解法 - 无脑法
> 考虑大数好复杂哦现在不想看，先搁置：[分治解法/全排列 清晰图解](https://leetcode-cn.com/problems/da-yin-cong-1dao-zui-da-de-nwei-shu-lcof/solution/mian-shi-ti-17-da-yin-cong-1-dao-zui-da-de-n-wei-2/)

### 2.1 Java
```java
class Solution {
    public int[] printNumbers(int n) {
        int max = 0;
        while (n != 0) {
            max = max * 10 + 9;
            n--;
        }
        int[] ans = new int[max];
        for (int i=1;i<=max;i++) {
            ans[i-1] = i;
        }
        return ans;
    }
}
```

### 2.2 Kotlin
```kotlin
class Solution {
    fun printNumbers(n: Int): IntArray {
        var n = n
        var max = 0
        while (n != 0) {
            max = max * 10 + 9
            n--
        }
        val ans = IntArray(max)
        for (i in 1..max) {
            ans[i - 1] = i
        }
        return ans
    }
}
```

## 3. 参考
- [https://leetcode-cn.com/problems/da-yin-cong-1dao-zui-da-de-nwei-shu-lcof/](https://leetcode-cn.com/problems/da-yin-cong-1dao-zui-da-de-nwei-shu-lcof/)
