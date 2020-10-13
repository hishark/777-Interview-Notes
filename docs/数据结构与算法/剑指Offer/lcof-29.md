---
title: 29. 顺时针打印矩阵
date: 2020-10-03 15:00:20
tags:
- leetcode
- lcof
- java
- kotlin
- 数组
categories: 算法笔记
---
# 29. 顺时针打印矩阵
## 1. [问题](https://leetcode-cn.com/problems/shun-shi-zhen-da-yin-ju-zhen-lcof/)

输入一个矩阵，按照从外向里以顺时针的顺序依次打印出每一个数字。

示例 1：
```
输入：matrix = [[1,2,3],[4,5,6],[7,8,9]]
输出：[1,2,3,6,9,8,7,4,5]
```
<!--more-->
示例 2：
```
输入：matrix = [[1,2,3,4],[5,6,7,8],[9,10,11,12]]
输出：[1,2,3,4,8,12,11,10,9,5,6,7]
```

限制：

- 0 <= matrix.length <= 100
- 0 <= matrix[i].length <= 100

## 2. 解法

### 2.1 Java

```java
class Solution {
    public int[] spiralOrder(int[][] matrix) {
        // 空值处理
        if(matrix.length==0) 
            return new int[0];

        // 初始化边界和结果数组
        int left = 0, right = matrix[0].length - 1;
        int top = 0, bottom = matrix.length - 1;
        int[] res = new int[matrix[0].length * matrix.length];

				// 结果数组下标
        int index = 0;
        // 按照方向进行打印
        while (true) {
            // 从左到右
            // 1. 按照边界打印
            for (int i=left;i<=right;i++)
                res[index++] = matrix[top][i];
            // 2. 上边界收缩（下移）
            top++;
            // 3. 判断收缩后的上边界和下边界是否相遇
            if (top > bottom)
                break;

            // 从上到下
            // 1. 按照边界打印
            for (int i=top;i<=bottom;i++)
                res[index++] = matrix[i][right];
            // 2. 右边界收缩（左移）
            right--;
            // 3. 判断收缩后的右边界和左边界是否相遇
            if (left > right)
                break;

            // 从右到左
            // 1. 按照边界打印
            for (int i=right;i>=left;i--)
                res[index++] = matrix[bottom][i];
            // 2. 下边界收缩（上移)
            bottom--;
            // 3. 判断收缩后的下边界和上边界是否相遇
            if (top > bottom)
                break;

            // 从下到上
            // 1. 按照边界打印
            for (int i=bottom;i>=top;i--)
                res[index++] = matrix[i][left];
            // 2. 左边界收缩（右移）
            left++;
            // 3. 判断收缩后的左边界和右边界是否相遇
            if(left > right) 
                break;
        }
        return res;

    }
}
```

### 2.2 Kotlin

```kotlin
class Solution {
    fun spiralOrder(matrix: Array<IntArray>): IntArray {
        // 空值处理
        if(matrix.size==0) 
            return IntArray(0)

        // 初始化边界和结果数组
        var left = 0
        var right = matrix[0].size - 1
        var top = 0
        var bottom = matrix.size - 1
        var res = IntArray(matrix[0].size * matrix.size)

        // 结果数组下标
        var index = 0
        while (true) {
            // 从左到右
            // 1. 按照边界打印
            for (i in left..right)
                res[index++] = matrix[top][i]
            // 2. 上边界收缩（下移）
            top++
            // 3. 判断收缩后的上边界和下边界是否相遇
            if (top > bottom)
                break

            // 从上到下
            // 1. 按照边界打印
            for (i in top..bottom)
                res[index++] = matrix[i][right];
            // 2. 右边界收缩（左移）
            right--
            // 3. 判断收缩后的右边界和左边界是否相遇
            if (left > right)
                break

            // 从右到左
            // 1. 按照边界打印
            for (i in right downTo left)
                res[index++] = matrix[bottom][i]
            // 2. 下边界收缩（上移)
            bottom--
            // 3. 判断收缩后的下边界和上边界是否相遇
            if (top > bottom)
                break

            // 从下到上
            // 1. 按照边界打印
            for (i in bottom downTo top)
                res[index++] = matrix[i][left]
            // 2. 左边界收缩（右移）
            left++
            // 3. 判断收缩后的左边界和右边界是否相遇
            if(left > right) 
                break
        }
        return res
    }
}
```

## 3. 参考

- [《剑指 Offer（第 2 版）》：面试题29. 顺时针打印矩阵](https://leetcode-cn.com/problems/shun-shi-zhen-da-yin-ju-zhen-lcof)
- [Krahets：面试题29. 顺时针打印矩阵（模拟、设定边界，清晰图解）](https://leetcode-cn.com/problems/shun-shi-zhen-da-yin-ju-zhen-lcof/solution/mian-shi-ti-29-shun-shi-zhen-da-yin-ju-zhen-she-di/)

<!-- ## 4. 学习草稿
![](https://777blog.oss-cn-shanghai.aliyuncs.com/blog%20pic/IMG_4304.JPG)
 -->
