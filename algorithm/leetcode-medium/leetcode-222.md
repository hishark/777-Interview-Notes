# 222. 完全二叉树的节点个数

## 1. [问题](https://leetcode-cn.com/problems/count-complete-tree-nodes/)

给出一个完全二叉树，求出该树的节点个数。

**说明：**

[完全二叉树](https://baike.baidu.com/item/%E5%AE%8C%E5%85%A8%E4%BA%8C%E5%8F%89%E6%A0%91/7773232?fr=aladdin)的定义如下：在完全二叉树中，除了最底层节点可能没填满外，其余每层节点数都达到最大值，并且最下面一层的节点都集中在该层最左边的若干位置。若最底层为第 h 层，则该层包含 1~ 2h 个节点。

**示例:**

```text
输入: 
    1
   / \
  2   3
 / \  /
4  5 6

输出: 6
```

## 2. 标签

* 树
* 二分查找
* 位运算
* 递归
* 深度优先搜索

## 3. 解法 - DFS

### 3.1 Java

```java

```

### 3.2 Kotlin

```kotlin

```

### 3.3 复杂度分析

* 时间复杂度 `O(N)` ：N 为树的结点数量，计算树的深度需要遍历到所有的结点。
* 空间复杂度 `O(N)` ：最差情况下，当树退化为链表，递归的深度会达到 N。

## 4. 参考

* [https://leetcode-cn.com/problems/count-complete-tree-nodes/](https://leetcode-cn.com/problems/count-complete-tree-nodes/)
* [https://leetcode-cn.com/problems/count-complete-tree-nodes/solution/wan-quan-er-cha-shu-de-jie-dian-ge-shu-by-leetco-2/](https://leetcode-cn.com/problems/count-complete-tree-nodes/solution/wan-quan-er-cha-shu-de-jie-dian-ge-shu-by-leetco-2/)

