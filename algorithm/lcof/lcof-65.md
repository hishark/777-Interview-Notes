# 65. 不用加减乘除做加法【位运算】

## 1. [问题](https://leetcode-cn.com/problems/bu-yong-jia-jian-cheng-chu-zuo-jia-fa-lcof/)

写一个函数，求两个整数之和，要求在函数体内不得使用 “+”、“-”、“\*”、“/” 四则运算符号。

**示例:**

```
输入: a = 1, b = 1
输出: 2
```

**提示：**

* `a`, `b` 均可能是负数或 0
* 结果不会溢出 32 位整数

## 2. 标签

* 位运算

## 3. 解法 - 位运算

### 3.1 Java

```java
class Solution {
    public int add(int a, int b) {
        /**
         * 【此处看一眼K佬题解里的表格就能秒懂了！】
         *     「无进位和」和「异或运算」规律相同
         *     「进位」和「与运算」规律相同，并需要左移一位
         * 注：
         *     1. 异或运算：两个位相同为 0，相异为 1
         *     2. 与运算：两个位都为 1时，结果才为 1
         */
        // 进位为 0 时结束循环
        while (b != 0) {
            // 进位
            int carry = (a & b) << 1;
            a ^= b; // a 是「无进位和」
            b = carry; // b 是「进位」
        }
        return a;
    }
}
```

### 3.2 Kotlin

```kotlin
class Solution {
    fun add(a: Int, b: Int): Int {
        var a = a
        var b = b
        /**
         * 【此处看一眼K佬题解里的表格就能秒懂了！】
         *     「无进位和」和「异或运算」规律相同
         *     「进位」和「与运算」规律相同，并需要左移一位
         * 注：
         *     1. 异或运算：两个位相同为 0，相异为 1
         *     2. 与运算：两个位都为 1时，结果才为 1
         */
        // 进位为 0 时结束循环
        while (b != 0) {
            // 进位
            val carry = a and b shl 1
            a = a xor b // a 是「无进位和」
            b = carry // b 是「进位」
        }
        return a
    }
}
```

### 3.3 复杂度分析

* 时间复杂度 `O(1)` ：每轮中的常数次位运算操作耗费 `O(1)` 时间，最差情况下需要循环 32 次，时间复杂度仍为 `O(1)`。
* 空间复杂度 `O(1)` ：使用常数大小的额外空间。

## 4. 参考

* [https://leetcode-cn.com/problems/bu-yong-jia-jian-cheng-chu-zuo-jia-fa-lcof/](https://leetcode-cn.com/problems/bu-yong-jia-jian-cheng-chu-zuo-jia-fa-lcof/)
* [https://leetcode-cn.com/problems/bu-yong-jia-jian-cheng-chu-zuo-jia-fa-lcof/solution/mian-shi-ti-65-bu-yong-jia-jian-cheng-chu-zuo-ji-7/](https://leetcode-cn.com/problems/bu-yong-jia-jian-cheng-chu-zuo-jia-fa-lcof/solution/mian-shi-ti-65-bu-yong-jia-jian-cheng-chu-zuo-ji-7/)
