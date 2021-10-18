# 44. 数字序列中某一位的数字【找规律】

## 1. [问题](https://leetcode-cn.com/problems/shu-zi-xu-lie-zhong-mou-yi-wei-de-shu-zi-lcof/)

数字以0123456789101112131415…的格式序列化到一个字符序列中。在这个序列中，第5位（从下标0开始计数）是5，第13位是1，第19位是4，等等。

请写一个函数，求任意第n位对应的数字。

**示例 1：**

```
输入：n = 3
输出：3
```

**示例 2：**

```
输入：n = 11
输出：0
```

**限制：**

* `0 <= n < 2^31`

## 2. 标签

* 数学
* 找规律

## 3. 解法

> 吐了，找规律我阵亡。

### 3.1 Java

```java
class Solution {
    public int findNthDigit(int n) {
        // 数字的位数，比如 777 的位数为 3
        int digit = 1;

        // 放弃了，为什么要有找规律这种玩意- -
    }
}
```

### 3.2 Kotlin

```kotlin
class Solution {
    fun findNthDigit(n: Int): Int {
        // 数字的位数，比如 777 的位数为 3
        val digit = 1

        // 放弃了，为什么要有找规律这种玩意- -
    }
}
```

### 3.3 复杂度分析

* 时间复杂度 `O(?)` ：你猜。
* 空间复杂度 `O(?)` ：你再猜。

## 4. 参考

* [https://leetcode-cn.com/problems/shu-zi-xu-lie-zhong-mou-yi-wei-de-shu-zi-lcof/](https://leetcode-cn.com/problems/shu-zi-xu-lie-zhong-mou-yi-wei-de-shu-zi-lcof/)
* [https://leetcode-cn.com/problems/shu-zi-xu-lie-zhong-mou-yi-wei-de-shu-zi-lcof/solution/mian-shi-ti-44-shu-zi-xu-lie-zhong-mou-yi-wei-de-6/](https://leetcode-cn.com/problems/shu-zi-xu-lie-zhong-mou-yi-wei-de-shu-zi-lcof/solution/mian-shi-ti-44-shu-zi-xu-lie-zhong-mou-yi-wei-de-6/)
