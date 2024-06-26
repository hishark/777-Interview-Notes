# LCOF 10-I. 斐波那契数列

## 1. [问题](https://leetcode-cn.com/problems/fei-bo-na-qi-shu-lie-lcof/)

写一个函数，输入 n ，求斐波那契（Fibonacci）数列的第 n 项。斐波那契数列的定义如下：

F(0) = 0, F(1) = 1 F(N) = F(N - 1) + F(N - 2), 其中 N > 1. 斐波那契数列由 0 和 1 开始，之后的斐波那契数就是由之前的两数相加而得出。

答案需要取模 1e9+7（1000000007），如计算初始结果为：1000000008，请返回 1。 

示例 1：

```
输入：n = 2
输出：1
```

示例 2：

```
输入：n = 5
输出：5
```

提示：

* 0 <= n <= 100

## 2. 解法 - 递归

### 2.1 Java

```java
// 递归超时了
class Solution {
    public int fib(int n) {
        if (n==0 || n==1)
            return n;
        int[] res = new int[n+1];
        res[0] = 0;
        res[1] = 1;
        for(int i=2;i<=n;i++)
            res[i] = (res[i-1] + res[i-2]) % 1000000007;
        return res[n];
    }
}
```

### 2.2 Kotlin

```kotlin
// 递归超时了
class Solution {
    fun fib(n: Int): Int {
        if (n == 0 || n == 1)
            return n
        val res = IntArray(n + 1)
        res[0] = 0
        res[1] = 1
        for (i in 2..n)
            res[i] = (res[i - 1] + res[i - 2]) % 1000000007
        return res[n]
    }
}
```

## 3. 参考

* [https://leetcode-cn.com/problems/fei-bo-na-qi-shu-lie-lcof/](https://leetcode-cn.com/problems/fei-bo-na-qi-shu-lie-lcof/)
