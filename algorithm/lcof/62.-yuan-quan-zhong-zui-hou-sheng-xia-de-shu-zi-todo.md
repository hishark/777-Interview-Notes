# 62. 圆圈中最后剩下的数字

## 1. [问题](https://leetcode-cn.com/problems/yuan-quan-zhong-zui-hou-sheng-xia-de-shu-zi-lcof/)

0,1,...,n - 1 这 n 个数字排成一个圆圈，从数字 0 开始，每次从这个圆圈里删除第 m 个数字。求出这个圆圈里剩下的最后一个数字。

例如，0、1、2、3、4 这 5 个数字组成一个圆圈，从数字 0 开始每次删除第 3 个数字，则删除的前 4 个数字依次是 2、0、4、1，因此最后剩下的数字是 3。

**示例 1：**

```text
输入: n = 5, m = 3
输出: 3
```

**示例 2：**

```text
输入: n = 10, m = 17
输出: 2
```

**限制：**

* `1 <= n <= 10^5`
* `1 <= m <= 10^6`

## 2. 标签

* 数学

## 3. 解法 - 约瑟夫环

### 3.1 Java

```java
class Solution {
    public int lastRemaining(int n, int m) {
        // 倒推
        // 最后一轮只剩下一个元素了，它的下标一定为0
        int res = 0;
        // 最后一轮只剩下两个人，所以从 2 开始反推
        for (int i = 2; i <= n; i++) {
            res = (res + m) % i;
        }
        return res;
    }
}
```

### 3.2 Kotlin

```kotlin
class Solution {
    fun lastRemaining(n: Int, m: Int): Int {
        var res = 0
        // 最后一轮只剩下两个人，所以从 2 开始反推
        for (i in 2..n) {
            res = (res + m) % i
        }
        return res
    }
}
```

### 3.3 复杂度分析

* 时间复杂度 `O(n)` ：循环花费了 `O(n)` 的时间。
* 空间复杂度 `O(1)` ：变量只占用了常数大小的额外存储空间。

## 4. 参考

* [https://leetcode-cn.com/problems/yuan-quan-zhong-zui-hou-sheng-xia-de-shu-zi-lcof/](https://leetcode-cn.com/problems/yuan-quan-zhong-zui-hou-sheng-xia-de-shu-zi-lcof/)
* [https://leetcode-cn.com/problems/yuan-quan-zhong-zui-hou-sheng-xia-de-shu-zi-lcof/solution/yuan-quan-zhong-zui-hou-sheng-xia-de-shu-zi-by-lee/](https://leetcode-cn.com/problems/yuan-quan-zhong-zui-hou-sheng-xia-de-shu-zi-lcof/solution/yuan-quan-zhong-zui-hou-sheng-xia-de-shu-zi-by-lee/)

