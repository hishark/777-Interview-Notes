---
title: 990. 等式方程的可满足性
date: '2020-06-10T00:50:10.000Z'
tags:
  - kotlin
  - java
  - leetcode
  - 并查集
  - 图
categories: 算法笔记
notshow: true
---

# leetcode-990

## [1. 问题](https://leetcode-cn.com/problems/satisfiability-of-equality-equations/)

给定一个由表示变量之间关系的字符串方程组成的数组，每个字符串方程 equations\[i\] 的长度为 4，并采用两种不同的形式之一："a==b" 或 "a!=b"。在这里，a 和 b 是小写字母（不一定不同），表示单字母变量名。

只有当可以将整数分配给变量名，以便满足所有给定的方程时才返回 true，否则返回 false。

示例 1：

> 输入：\["a==b","b!=a"\] 输出：false 解释：如果我们指定，a = 1 且 b = 1，那么可以满足第一个方程，但无法满足第二个方程。没有办法分配变量同时满足这两个方程。

示例 2：

> 输入：\["b==a","a==b"\] 输出：true 解释：我们可以指定 a = 1 且 b = 1 以满足这两个方程。

示例 3：

> 输入：\["a==b","b==c","a==c"\] 输出：true

示例 4：

> 输入：\["a==b","b!=c","c==a"\] 输出：false

示例 5：

> 输入：\["c==c","b==d","x!=z"\] 输出：true

提示

* 1 &lt;= equations.length &lt;= 500
* equations\[i\].length == 4
* equations\[i\]\[0\] 和 equations\[i\]\[3\] 是小写字母
* equations\[i\]\[1\] 要么是 '='，要么是 '!'
* equations\[i\]\[2\] 是 '='

## 2. 解法 - 并查集

### 2.1 Java

```java
class Solution {
    public boolean equationsPossible(String[] equations) {
        // 初始化parent数组
        // parent[i] = j 表示 i的父节点为j
        // 最开始所有节点的父节点都为自己
        int[] parent = new int[26];
        for (int i=0;i<26;i++) {
            // 26个英文字母
            parent[i] = i;
        }

        // 遍历等式
        for(String equation: equations) {
            // equation[0]为变量1
            // equation[3]为变量2
            // equation[1]用于判断是等式还是不等式
            if (equation.charAt(1) == '=') {
                int index1 = equation.charAt(0) - 'a';
                int index2 = equation.charAt(3) - 'a';
                // 由于二者相等，所以同属于一个连通分量，合并即可
                union(parent, index1, index2);
            }
        }

        // 遍历不等式
        for(String equation: equations) {
            if (equation.charAt(1) == '!') {
                int index1 = equation.charAt(0) - 'a';
                int index2 = equation.charAt(3) - 'a';
                // 由于二者不相等，所以不属于同一个连通分量，所以根节点必定不相同。
                // 如果相同的话就出现矛盾，返回false
                if (findRoot(parent, index1) == findRoot(parent, index2)) {
                    return false;
                }
            }
        }

        return true;
    }

    // 合并两个变量
    // 把【变量1的根节点的父节点】指向【变量2的根节点】
    public void union(int[] parent, int index1, int index2) {
        parent[findRoot(parent, index1)] = findRoot(parent, index2);
    }

    // 查找当前节点的根节点
    // 沿着父节点一路向上查找
    public int findRoot(int[] parent, int index) {
        // parent[i] = j 表示 i的父节点为j
        // i!=j时表示还不是根节点
        // 只有根节点的父节点为自己
        while (parent[index] != index) {
            // 更新【父节点】为【父节点的父节点】
            parent[index] = parent[parent[index]];
            // 更新当前节点为【父节点】
            index = parent[index];
        }
        return index;
    }
}
```

### 2.2 Kotlin

```kotlin
class Solution {
    fun equationsPossible(equations: Array<String>): Boolean {
        // 初始化parent数组
        // parent[i] = j 表示 i的父节点为j
        // 最开始所有节点的父节点都为自己
        var parent = IntArray(26)
        for (i in 0..25) {
            // 26个英文字母
            parent[i] = i
        }

        // 遍历等式
        for( equation in equations) {
            // equation[0]为变量1
            // equation[3]为变量2
            // equation[1]用于判断是等式还是不等式
            if (equation[1] == '=') {
                var index1 = equation[0] - 'a'
                var index2 = equation[3] - 'a'
                // 由于二者相等，所以同属于一个连通分量，合并即可
                union(parent, index1, index2)
            }
        }

        // 遍历不等式
        for(equation in equations) {
            if (equation[1] == '!') {
                var index1 = equation[0] - 'a'
                var index2 = equation[3] - 'a'
                // 由于二者不相等，所以不属于同一个连通分量，所以根节点必定不相同。
                // 如果相同的话就出现矛盾，返回false
                if (findRoot(parent, index1) == findRoot(parent, index2)) {
                    return false
                }
            }
        }

        return true
    }

    // 合并两个变量
    // 把【变量1的根节点的父节点】指向【变量2的根节点】
    fun union(parent: IntArray, index1: Int, index2: Int) {
        parent[findRoot(parent, index1)] = findRoot(parent, index2)
    }

    // 查找当前节点的根节点
    // 沿着父节点一路向上查找
    fun findRoot(parent: IntArray, i: Int): Int {
        // parent[i] = j 表示 i的父节点为j
        // i!=j时表示还不是根节点
        // 只有根节点的父节点为自己
        var index = i
        while (parent[index] != index) {
            // 更新【父节点】为【父节点的父节点】
            parent[index] = parent[parent[index]]
            // 更新当前节点为【父节点】
            index = parent[index]
        }
        return index
    }
}
```

## 3. 参考

* [力扣：990. 等式方程的可满足性](https://leetcode-cn.com/problems/satisfiability-of-equality-equations)
* [力扣官方题解：等式方程的可满足性](https://leetcode-cn.com/problems/satisfiability-of-equality-equations/solution/deng-shi-fang-cheng-de-ke-man-zu-xing-by-leetcode-/)

## 4. 学习草稿

![](https://777blog.oss-cn-shanghai.aliyuncs.com/blog%20pic/IMG_4221%202.JPG) \*倒数第二行，【所在连通分量】删去

