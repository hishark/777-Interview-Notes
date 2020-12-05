---
title: 32 - I. 从上到下打印二叉树
date: '2020-10-13T23:16:20.000Z'
tags:
  - leetcode
  - lcof
  - java
  - 树
  - BFS
  - kotlin
categories: 算法笔记
---

# 32 - I. 从上到下打印二叉树

## 1. [问题](https://leetcode-cn.com/problems/cong-shang-dao-xia-da-yin-er-cha-shu-lcof/)

从上到下打印出二叉树的每个节点，同一层的节点按照从左到右的顺序打印。

例如: 给定二叉树: `[3,9,20,null,null,15,7]`,

```text
    3
   / \
  9  20
    /  \
   15   7
```

返回：

```text
[3,9,20,15,7]
```

提示：

* 节点总数 &lt;= 1000

## 2. 解法 - BFS

### 2.1 Java

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public int[] levelOrder(TreeNode root) {
        // 判空
        if (root == null)
            return new int[0];

        // BFS 需要使用队列
        Queue<TreeNode> queue = new LinkedList<>();
        // 先把根节点放入队列
        queue.offer(root);

        // 打印结果数组
        ArrayList<Integer> res = new ArrayList<>();

        // 队列为空时结束循环
        while (!queue.isEmpty()) {
            // 取出队头结点作为当前结点
            TreeNode curNode = queue.poll();
            // 先把当前结点放入结果数组
            res.add(curNode.val);
            // 然后开始判断当前结点的左右结点是否存在
            // 如果存在的话，将其放入队列
            if (curNode.left != null)
                queue.add(curNode.left);
            if (curNode.right != null )
                queue.add(curNode.right);
        }

        // 将ArrayList转换为int[]即可
        int[] finalRes = new int[res.size()];
        for(int i=0;i<res.size();i++) 
            finalRes[i] = res.get(i);

        // 返回最终结果
        return finalRes;
    }
}
```

### 2.2 Kotlin

```kotlin
/**
 * Example:
 * var ti = TreeNode(5)
 * var v = ti.`val`
 * Definition for a binary tree node.
 * class TreeNode(var `val`: Int) {
 *     var left: TreeNode? = null
 *     var right: TreeNode? = null
 * }
 */
class Solution {
    fun levelOrder(root: TreeNode?): IntArray {
        // 判空
        if (root == null)
            return IntArray(0)

        // BFS 需要使用队列
        val queue = LinkedList<TreeNode>()
        // 先把根节点放入队列
        queue.offer(root)

        // 打印结果数组
        val res = ArrayList<Int>()

        // 队列为空时结束循环
        while (!queue.isEmpty()) {
            // 取出队头结点作为当前结点
            val curNode = queue.poll()
            // 先把当前结点放入结果数组
            res.add(curNode.`val`)
            // 然后开始判断当前结点的左右结点是否存在
            // 如果存在的话，将其放入队列
            if (curNode.left != null)
                queue.add(curNode.left)
            if (curNode.right != null)
                queue.add(curNode.right)
        }

        // 将ArrayList转换为int[]即可
        val finalRes = IntArray(res.size)
        for (i in res.indices)
            finalRes[i] = res[i]

        // 返回最终结果
        return finalRes
    }
}
```

### 2.3 复杂度分析

* 时间复杂度 `O(N)`： N 是二叉树的结点数，BFS 需要循环 N 次。
* 空间复杂度 `O(N)`： 最差的情况下，即树为平衡二叉树时，最多有 `N/2` 个结点同时在 `queue` 中，需要使用 `O(N)` 大小的额外空间。

> 平衡树\(Balance Tree，BT\) 指的是，任意节点的子树的高度差都小于等于1。

## 3. 参考

* [https://leetcode-cn.com/problems/cong-shang-dao-xia-da-yin-er-cha-shu-lcof/](https://leetcode-cn.com/problems/cong-shang-dao-xia-da-yin-er-cha-shu-lcof/)
* [https://leetcode-cn.com/problems/cong-shang-dao-xia-da-yin-er-cha-shu-lcof/solution/mian-shi-ti-32-i-cong-shang-dao-xia-da-yin-er-ch-4/](https://leetcode-cn.com/problems/cong-shang-dao-xia-da-yin-er-cha-shu-lcof/solution/mian-shi-ti-32-i-cong-shang-dao-xia-da-yin-er-ch-4/)

## 4. 标签

* BFS
* 树

