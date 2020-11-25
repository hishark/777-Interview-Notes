# LCOF 14-II. 剪绳子 II

## 1. [问题](https://leetcode-cn.com/problems/jian-sheng-zi-ii-lcof/)

给你一根长度为 n 的绳子，请把绳子剪成整数长度的 m 段（m、n都是整数，n&gt;1并且m&gt;1），每段绳子的长度记为 k\[0\],k\[1\]...k\[m - 1\] 。请问 k\[0\]\*k\[1\]\*...\*k\[m - 1\] 可能的最大乘积是多少？例如，当绳子的长度是8时，我们把它剪成长度分别为2、3、3的三段，此时得到的最大乘积是18。

答案需要取模 1e9+7（1000000007），如计算初始结果为：1000000008，请返回 1。

示例 1：

```text
输入: 2
输出: 1
解释: 2 = 1 + 1, 1 × 1 = 1
```

示例 2:

```text
输入: 10
输出: 36
解释: 10 = 3 + 3 + 4, 3 × 3 × 4 = 36
```

提示：

* 2 &lt;= n &lt;= 1000

## 2. 解法 - 贪心

> 时间复杂度：O\(1\) 空间复杂度：O\(1\)

### 2.1 Java

```java
class Solution {
    public int cuttingRope(int n) {
        // 单独处理
        if (n == 2)
            return 1;
        if (n == 3)
            return 2;

        // 最大乘积
        long maxProduct = 1;

        // 取模
        int mod = (int)1e9 + 7;

        // n大于4的情况下不停地拆3出来
        while (n > 4) {
            // 拆一个3就乘一下
            maxProduct *= 3;
            // 每求出一个新的乘积就取模
            maxProduct %= mod;
            // 拆了一个3当然要剪去一个3
            n -= 3;
        }

        // 退出循环后，剩下的绳子长度只有可能是1，2，3
        // 不管是谁都没有必要拆，越拆越小，直接乘上即可
        return (int)(maxProduct * n % mod);

    }
}
```

### 2.2 Kotlin

```kotlin
class Solution {
    fun cuttingRope(n: Int): Int {
        var n = n
        // 单独处理
        if (n == 2)
            return 1
        if (n == 3)
            return 2

        // 最大乘积
        var maxProduct: Long = 1

        // 取模
        val mod = 1e9.toInt() + 7

        // n大于4的情况下不停地拆3出来
        while (n > 4) {
            // 拆一个3就乘一下
            maxProduct *= 3
            // 每求出一个新的乘积就取模
            maxProduct %= mod.toLong()
            // 拆了一个3当然要剪去一个3
            n -= 3
        }

        // 退出循环后，剩下的绳子长度只有可能是1，2，3
        // 不管是谁都没有必要拆，越拆越小，直接乘上即可
        return (maxProduct * n % mod).toInt()

    }
}
```

## 3. 参考

* [https://leetcode-cn.com/problems/jian-sheng-zi-ii-lcof/](https://leetcode-cn.com/problems/jian-sheng-zi-ii-lcof/)
* [https://leetcode-cn.com/problems/jian-sheng-zi-ii-lcof/solution/javatan-xin-si-lu-jiang-jie-by-henrylee4/](https://leetcode-cn.com/problems/jian-sheng-zi-ii-lcof/solution/javatan-xin-si-lu-jiang-jie-by-henrylee4/)

