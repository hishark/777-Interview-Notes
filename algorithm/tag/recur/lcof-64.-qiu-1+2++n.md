# LCOF 64. 求1+2+…+n

## 1. [问题](https://leetcode-cn.com/problems/qiu-12n-lcof/)

求 `1+2+...+n` ，要求不能使用乘除法、for、while、if、else、switch、case等关键字及条件判断语句（A?B:C）。

**示例 1：**

```text
输入: n = 3
输出: 6
```

**示例 2：**

```text
输入: n = 9
输出: 45
```

**限制：**

* `1 <= n <= 10000`

## 2. 标签

* 位运算
* 递归

## 3. 解法

> 递归时一般都会使用条件判断语句来决定递归的出口，由于题目限制无法使用，我们可以使用逻辑运算符的短路性质来决定递归的出口。

### 3.1 Java

```java
class Solution {
    public int sumNums(int n) {
        /**
         * A && B
         * A: n > 0
         * B: n += sumNums(n - 1)
         * 可以将判断是否为递归的出口看作 A 部分
         * 将递归的主体函数看作 B 部分
         *  1. 如果不是递归出口，也就是 n > 0，那么返回 True，继续执行 B 部分，进行递归
         *  2. 如果是递归出口，也就是 n == 0，那么返回 False，短路，不再执行 B 部分，结束递归
         */
        boolean flag = n > 0 && (n += sumNums(n - 1)) > 0;
        return n;
    }
}
```

### 3.2 Kotlin

```kotlin
？
```

### 3.3 复杂度分析

* 时间复杂度 `O(n)` ：递归函数总共递归了 n 次，每次递归中计算操作的时间复杂度为 `O(1)`，因此总时间复杂度为 `O(n)`。
* 空间复杂度 `O(n)` ：递归函数的空间复杂度取决于递归调用栈的深度，这里深度为 `O(n)`。

## 4. 参考

* [https://leetcode-cn.com/problems/qiu-12n-lcof/](https://leetcode-cn.com/problems/qiu-12n-lcof/)
* [https://leetcode-cn.com/problems/qiu-12n-lcof/solution/qiu-12n-by-leetcode-solution/](https://leetcode-cn.com/problems/qiu-12n-lcof/solution/qiu-12n-by-leetcode-solution/)
* [https://leetcode-cn.com/problems/qiu-12n-lcof/solution/mian-shi-ti-64-qiu-1-2-nluo-ji-fu-duan-lu-qing-xi-/](https://leetcode-cn.com/problems/qiu-12n-lcof/solution/mian-shi-ti-64-qiu-1-2-nluo-ji-fu-duan-lu-qing-xi-/)

