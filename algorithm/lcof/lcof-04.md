---
title: 04. 二维数组中的查找
date: '2020-08-11T20:07:31.000Z'
tags:
  - 数组
  - 双指针
  - leetcode
  - lcof
  - java
  - kotlin
categories: 算法笔记
notshow: true
---

# 04. 二维数组中的查找

## 1. [问题](https://leetcode-cn.com/problems/er-wei-shu-zu-zhong-de-cha-zhao-lcof/)

在一个 n \* m 的二维数组中，每一行都按照从左到右递增的顺序排序，每一列都按照从上到下递增的顺序排序。请完成一个函数，输入这样的一个二维数组和一个整数，判断数组中是否含有该整数。

示例:

```text
现有矩阵 matrix 如下：

[
  [1,   4,  7, 11, 15],
  [2,   5,  8, 12, 19],
  [3,   6,  9, 16, 22],
  [10, 13, 14, 17, 24],
  [18, 21, 23, 26, 30]
]
```

给定 target = 5，返回 true。

给定 target = 20，返回 false。

限制：

* 0 &lt;= n &lt;= 1000
* 0 &lt;= m &lt;= 1000

## 2. 解法

### 2.1 Java

```java
class Solution {
    public boolean findNumberIn2DArray(int[][] matrix, int target) {
        // 判空
        if (matrix.length == 0) {
            return false;
        }
        // 从右上角开始搜索
        // 当前值和target相等就返回true
        // target < 当前值，就剔除当前列，往左移动一列
        // target > 当前值，就剔除当前行，往下移动一行
        int row = 0;
        int col = matrix[0].length - 1;

        while (row < matrix.length && col >= 0) {
            if(matrix[row][col] == target)
                return true;
            else if (target < matrix[row][col])
                col--;
            else if (target > matrix[row][col])
                row++;
        }

        return false;
    }
}
```

### 2.2 Kotlin

```kotlin
class Solution {
    fun findNumberIn2DArray(matrix: Array<IntArray>, target: Int): Boolean {
        // 判空
        if (matrix.size == 0) {
            return false
        }
        // 从右上角开始搜索
        // 当前值和target相等就返回true
        // target < 当前值，就剔除当前列，往左移动一列
        // target > 当前值，就剔除当前行，往下移动一行
        var row = 0
        var col = matrix[0].size - 1

        while (row < matrix.size && col >= 0) {
            if (matrix[row][col] == target)
                return true
            else if (target < matrix[row][col])
                col--
            else if (target > matrix[row][col])
                row++
        }

        return false
    }
}
```

## 3. 参考

* [https://leetcode-cn.com/problems/er-wei-shu-zu-zhong-de-cha-zhao-lcof](https://leetcode-cn.com/problems/er-wei-shu-zu-zhong-de-cha-zhao-lcof)
* [《剑指Offer（第2版）》](https://book.douban.com/subject/27008702/)

## 4. 笔记

![](https://777blog.oss-cn-shanghai.aliyuncs.com/leetcode/lcof-04.jpg)

