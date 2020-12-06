# 66. 构建乘积数组

## 1. [问题](https://leetcode-cn.com/problems/gou-jian-cheng-ji-shu-zu-lcof/)

给定一个数组 A\[0,1,…,n-1\]，请构建一个数组 B\[0,1,…,n-1\]，其中 B 中的元素 B\[i\]=A\[0\]×A\[1\]×…×A\[i-1\]×A\[i+1\]×…×A\[n-1\]。不能使用除法。

**示例:**

```text
输入: [1,2,3,4,5]
输出: [120,60,40,30,24]
```

**提示：**

* 所有元素乘积之和不会溢出 32 位整数
* `a.length <= 100000`

## 2. 标签

* 找规律
* DP

## 3. 解法

> 本质DP，看[DP的代码](https://leetcode-cn.com/problems/gou-jian-cheng-ji-shu-zu-lcof/solution/mian-shi-ti-66-gou-jian-cheng-ji-shu-zu-biao-ge-fe/417592)会更清晰易懂一些。

### 3.1 Java

```java
class Solution {
    public int[] constructArr(int[] a) {
        // 判空
        if (a.length == 0)
            return new int[0];

        // 创建 b 数组
        int[] b = new int[a.length];
        // 赋初值
        b[0] = 1;
        // 工具人 tmp
        int tmp = 1;
        /**
         * 去看K佬画的表格 第一个循环是在计算「下三角」部分的值
         */
        for (int i = 1; i < a.length; i++) {
            b[i] = b[i - 1] * a[i - 1];
        }
        // 第二个循环是在计算「上三角」部分的值
        for (int i = a.length - 2; i >= 0; i--) {
            tmp *= a[i + 1];
            b[i] *= tmp;
        }
        
        return b;
    }
}
```

### 3.2 Kotlin

```kotlin
class Solution {
    fun constructArr(a: IntArray): IntArray {
        // 判空
        if (a.size == 0)
            return IntArray(0)

        // 创建 b 数组
        val b = IntArray(a.size)
        // 赋初值
        b[0] = 1
        // 工具人 tmp
        var tmp = 1
        /**
         * 去看K佬画的表格 第一个循环是在计算「下三角」部分的值
         */
        for (i in 1 until a.size) {
            b[i] = b[i - 1] * a[i - 1]
        }
        // 第二个循环是在计算「上三角」部分的值
        for (i in a.size - 2 downTo 0) {
            tmp *= a[i + 1]
            b[i] *= tmp
        }

        return b
    }
}
```

### 3.3 复杂度分析

* 时间复杂度 `O(N)` ：其中 N 为数组的长，总共需要遍历两边数组。
* 空间复杂度 `O(1)` ：变量 tmp 仅使用了常数大小的额外空间。（数组 b 作为返回值不考虑到复杂度内）。

> 哇还能这样不考虑的吗

## 4. 参考

* [https://leetcode-cn.com/problems/gou-jian-cheng-ji-shu-zu-lcof/](https://leetcode-cn.com/problems/gou-jian-cheng-ji-shu-zu-lcof/)
* [https://leetcode-cn.com/problems/gou-jian-cheng-ji-shu-zu-lcof/solution/mian-shi-ti-66-gou-jian-cheng-ji-shu-zu-biao-ge-fe/](https://leetcode-cn.com/problems/gou-jian-cheng-ji-shu-zu-lcof/solution/mian-shi-ti-66-gou-jian-cheng-ji-shu-zu-biao-ge-fe/)

