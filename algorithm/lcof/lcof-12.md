---
title: 12. 矩阵中的路径
date: '2020-08-27T21:09:07.000Z'
tags:
  - DFS
  - leetcode
  - lcof
  - java
  - kotlin
categories: 算法笔记
---

# 12. 矩阵中的路径【DFS】

## 1. [问题](https://leetcode-cn.com/problems/ju-zhen-zhong-de-lu-jing-lcof/)

请设计一个函数，用来判断在一个矩阵中是否存在一条包含某字符串所有字符的路径。路径可以从矩阵中的任意一格开始，每一步可以在矩阵中向左、右、上、下移动一格。如果一条路径经过了矩阵的某一格，那么该路径不能再次进入该格子。例如，在下面的 3 × 4 的矩阵中包含一条字符串“bfce”的路径（路径中的字母用加粗标出）。 

\[\["a","b","c","e"\], \["s","f","c","s"\], \["a","d","e","e"\]\]

但矩阵中不包含字符串“abfb”的路径，因为字符串的第一个字符b占据了矩阵中的第一行第二个格子之后，路径不能再次进入这个格子。

示例 1：

```text
输入：board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "ABCCED"
输出：true
```

示例 2：

```text
输入：board = [["a","b"],["c","d"]], word = "abcd"
输出：false
```

提示：

* 1 &lt;= board.length &lt;= 200
* 1 &lt;= board\[i\].length &lt;= 200

## 2. 标签

* DFS
* 剪枝

## 3. 解法 - DFS

### 3.1 Java

```java
class Solution {
    public boolean exist(char[][] board, String word) {
        // 字符串 - 字符数组
        char[] words = word.toCharArray();
        // 遍历所有字符，找到为止，没找到就返回false
        for(int i=0;i<board.length;i++){
            for(int j=0;j<board[0].length;j++){
                // 起点为[i, j]
                // 最后一个参数为字符串开始判断的位置，从 0 开始判断，一直到最后都合法就成啦
                if(dfs(board, words, i, j, 0))
                    return true;
            }
        }
        return false;
    }

    public boolean dfs(char[][] board, char[] word, int i, int j, int index) {
        // 越界，矩阵当前字符不等于字符串当前字符，不合法，返回false
        // （这里就是在剪枝）
        if (i < 0 || i >= board.length || j < 0 || j >= board[0].length || board[i][j] != word[index])
            return false;

        // 矩阵当前字符 = 字符串当前字符，且已经判断到了字符串的最后一个字符
        // 说明字符串已经全部匹配，合法，返回true
        if (index == word.length - 1)
            return true;

        // 记录下当前的字符，用于访问结束后恢复矩阵
        char curChar = board[i][j];

        // 已访问，标记为'/'
        board[i][j] = '/';

        // 上下左右都访问一下，只要有一条路成了就可以，所以用或
        boolean ans = dfs(board, word, i + 1, j, index + 1) || dfs(board, word, i - 1, j, index + 1) || 
                      dfs(board, word, i, j + 1, index + 1) || dfs(board, word, i , j - 1, index + 1);

        // 访问后还原矩阵
        board[i][j] = curChar;
        // 返回结果
        return ans;
    }
}
```

### 3.2 Kotlin

```kotlin
class Solution {
    fun exist(board: Array<CharArray>, word: String): Boolean {
        // 字符串 - 字符数组
        val words = word.toCharArray()
        // 遍历所有字符，找到为止，没找到就返回false
        for (i in board.indices) {
            for (j in 0 until board[0].size) {
                if (dfs(board, words, i, j, 0))
                    return true
            }
        }
        return false
    }

    fun dfs(board: Array<CharArray>, word: CharArray, i: Int, j: Int, index: Int): Boolean {
        // 越界，矩阵当前字符不等于字符串当前字符，不合法，返回false
        if (i < 0 || i >= board.size || j < 0 || j >= board[0].size || board[i][j] != word[index])
            return false

        // 矩阵当前字符=字符串当前字符，且已经是字符串最后一个字符，合法，返回true
        if (index == word.size - 1)
            return true

        // 记录下当前的字符，用于访问结束后恢复矩阵
        val curChar = board[i][j]

        // 已访问，标记为'/'
        board[i][j] = '/'

        // 上下左右都访问一下，只要有一条路成了就可以，所以用或
        val ans = dfs(board, word, i + 1, j, index + 1) || dfs(board, word, i - 1, j, index + 1) ||
                dfs(board, word, i, j + 1, index + 1) || dfs(board, word, i, j - 1, index + 1)

        // 访问后还原矩阵
        board[i][j] = curChar
        // 返回结果
        return ans
    }
}
```

### 3.3 复杂度分析

其中 M 和 N 分别为矩阵行列大小，K 为字符串 word 的长度。

* 时间复杂度 `O((3^K)MN)` ：最差情况下，需要遍历矩阵中所有长度为 K 的字符串，时间复杂度将达到 `O(3^K)`，矩阵汇总共有 MN 个起点，时间复杂度为 `O(MN)`。
  * 方案数计算：设字符串长度为 KK ，搜索中每个字符有上、下、左、右四个方向可以选择，舍弃回头（上个字符）的方向，剩下 33 种选择，因此方案数的复杂度为 O\(3^K\)O\(3 K \) 。
* 空间复杂度 `O(K)` ：搜索的过程中，递归深度不超过 K，因此栈空间占用 `O(K)`，最坏情况下 K=MN，递归深度将达到 MN，因此需要使用 O\(MN\) 的额外存储空间。

## 4. 参考

* [https://leetcode-cn.com/problems/ju-zhen-zhong-de-lu-jing-lcof/](https://leetcode-cn.com/problems/ju-zhen-zhong-de-lu-jing-lcof/)
* [https://leetcode-cn.com/problems/ju-zhen-zhong-de-lu-jing-lcof/solution/mian-shi-ti-12-ju-zhen-zhong-de-lu-jing-shen-du-yo/](https://leetcode-cn.com/problems/ju-zhen-zhong-de-lu-jing-lcof/solution/mian-shi-ti-12-ju-zhen-zhong-de-lu-jing-shen-du-yo/)

