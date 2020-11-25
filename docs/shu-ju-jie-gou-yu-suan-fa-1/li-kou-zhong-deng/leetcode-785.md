---
title: 785. 判断二分图
date: '2020-07-16T16:31:19.000Z'
tags:
  - leetcode
  - java
  - kotlin
  - BFS
  - DFS
  - 图
categories: 算法笔记
notshow: true
---

# 785. 判断二分图

## 1. [问题](https://leetcode-cn.com/problems/is-graph-bipartite)

给定一个无向图graph，当这个图为二分图时返回true。

如果我们能将一个图的节点集合分割成两个独立的子集A和B，并使图中的每一条边的两个节点一个来自A集合，一个来自B集合，我们就将这个图称为二分图。

graph将会以邻接表方式给出，graph\[i\]表示图中与节点i相连的所有节点。每个节点都是一个在0到graph.length-1之间的整数。这图中没有自环和平行边： graph\[i\] 中不存在i，并且graph\[i\]中没有重复的值。 

示例 1:

```text
输入: [[1,3], [0,2], [1,3], [0,2]]
输出: true
解释: 
无向图如下:
0----1
|    |
|    |
3----2
我们可以将节点分成两组: {0, 2} 和 {1, 3}。
```

示例 2:

```text
输入: [[1,2,3], [0,2], [0,1,3], [0,2]]
输出: false
解释: 
无向图如下:
0----1
| \  |
|  \ |
3----2
我们不能将节点分割成两个独立的子集。
```

注意:

* graph 的长度范围为 \[1, 100\]。
* graph\[i\] 中的元素的范围为 \[0, graph.length - 1\]。
* graph\[i\] 不会包含 i 或者有重复的值。
* 图是无向的: 如果j 在 graph\[i\]里边, 那么 i 也会在 graph\[j\]里边。

## 2. 解法 - DFS

### 2.1 Java

```java
class Solution {
    public boolean isBipartite(int[][] graph) {
        // 0-未访问 1和-1分别代表一种颜色
        int[] visited = new int[graph.length];

        // 遍历所有结点
        // 如果当前结点没有被染过色，就从这个结点开始dfs染色
        for(int i=0;i<graph.length;i++) {
            if(visited[i]==0 && !dfs(graph, i, 1, visited)){
                return false;
            }
        }

        // 走完所有的连通域都没有返回false，那就是个二分图啦
        return true;
    }


    // 返回值的含义：是否为二分图
    public boolean dfs(int[][] graph, int curNode, int color, int[] visited) {
        // 如果已经染过色，就判断染过的色和当前要染的色是不是同一个色
        if (visited[curNode] != 0) {
            // 这个就是边界条件，如果两个色相同，说明一直在正确染色
            // 如果两个色不相同，说明染色错误，直接返回false，不是二分图
            return visited[curNode] == color;
        }

        // 当前结点没染过色，就染color
        visited[curNode] = color;
        // 然后把与curNode相连接的结点全部染成另外一个色-color
        for (int other: graph[curNode]) {
            // 一旦出现了不符合二分图性质的边，就返回false
            if(!dfs(graph, other, -color, visited))
                return false;
        }

        // 走到最后了就返回true，的确是个二分图
        return true;
    }
}
```

### 2.2 Kotlin

```kotlin
class Solution {
    fun isBipartite(graph: Array<IntArray>): Boolean {
        // 0-未访问 1和-1分别代表一种颜色
        val visited = IntArray(graph.size)

        // 遍历所有结点
        // 如果当前结点没有被染过色，就从这个结点开始dfs染色
        for (i in graph.indices) {
            if (visited[i] == 0 && !dfs(graph, i, 1, visited)) {
                return false
            }
        }

        // 走完所有的连通域都没有返回false，那就是个二分图啦
        return true
    }


    // 返回值的含义：是否为二分图
    fun dfs(graph: Array<IntArray>, curNode: Int, color: Int, visited: IntArray): Boolean {
        // 如果已经染过色，就判断染过的色和当前要染的色是不是同一个色
        if (visited[curNode] != 0) {
            // 这个就是边界条件，如果两个色相同，说明一直在正确染色
            // 如果两个色不相同，说明染色错误，直接返回false，不是二分图
            return visited[curNode] == color
        }

        // 当前结点没染过色，就染color
        visited[curNode] = color
        // 然后把与curNode相连接的结点全部染成另外一个色-color
        for (other in graph[curNode]) {
            // 一旦出现了不符合二分图性质的边，就返回false
            if (!dfs(graph, other, -color, visited))
                return false
        }

        // 走到最后了就返回true，的确是个二分图
        return true
    }
}
```

## 3. 参考

* [https://leetcode-cn.com/problems/is-graph-bipartite](https://leetcode-cn.com/problems/is-graph-bipartite)
* [https://leetcode-cn.com/problems/is-graph-bipartite/solution/bfs-dfs-bing-cha-ji-san-chong-fang-fa-pan-duan-er-/](https://leetcode-cn.com/problems/is-graph-bipartite/solution/bfs-dfs-bing-cha-ji-san-chong-fang-fa-pan-duan-er-/)

## 4. 笔记

![](https://777blog.oss-cn-shanghai.aliyuncs.com/leetcode/leetcode-785-1.jpg) ![](https://777blog.oss-cn-shanghai.aliyuncs.com/leetcode/leetcode-785-2.jpg)

