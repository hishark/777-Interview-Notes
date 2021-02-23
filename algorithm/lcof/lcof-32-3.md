---
title: 32 - III. 从上到下打印二叉树 III
date: '2020-10-14T23:26:20.000Z'
tags:
  - leetcode
  - lcof
  - java
  - 树
  - BFS
  - kotlin
categories: 算法笔记
---

# 32 - III. 从上到下打印二叉树 III【BFS 双端队列】

## 1. [问题](https://leetcode-cn.com/problems/cong-shang-dao-xia-da-yin-er-cha-shu-iii-lcof)

请实现一个函数按照之字形顺序打印二叉树，即第一行按照从左到右的顺序打印，第二层按照从右到左的顺序打印，第三行再按照从左到右的顺序打印，其他行以此类推。

例如: 给定二叉树: \[3,9,20,null,null,15,7\],

```text
    3
   / \
  9  20
    /  \
   15   7
```

返回其层次遍历结果：

```text
[
  [3],
  [20,9],
  [15,7]
]
```

提示：

* 节点总数 &lt;= 1000

## 2. 解法 - BFS双端队列

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
    public List<List<Integer>> levelOrder(TreeNode root) {
        /**
         * 利用双端队列两头都可以添加元素的性质，假设打印列表tmp为双端队列，规定：
         * 1. 偶数层的结点添加到队列头部
         * 2. 奇数层的结点添加到队列尾部
         */
        // 借助队列存储将要遍历的结点
        Queue<TreeNode> queue = new LinkedList<>();

        // 层次遍历的结果
        List<List<Integer>> res = new ArrayList<>();

        // 判断当前处于什么层，初始化为奇数层
        boolean isOdd = true;

        // 判空
        if (root == null)
            return res;

        // 首先把根节点加入到队列中
        queue.add(root);

        // 队列为空时结束循环
        while (!queue.isEmpty()) {
            /**
             * 定义一个双端队列用于存储当前层次的打印结果：
             * 1. 偶数层的结点添加到队列头部
             * 2. 奇数层的结点添加到队列尾部
             */
            LinkedList<Integer> deque = new LinkedList<>();
            // 遍历当前层次的所有结点（即 queue 里的所有结点）
            for (int i=queue.size();i>0;i--) {
                // 取出 queue 的队头结点作为当前遍历结点
                TreeNode curNode = queue.poll();

                // 判断此时处于奇数层还是偶数层
                if (isOdd) 
                    deque.addLast(curNode.val); // 奇数层结点添加到双端队列尾部
                else 
                    deque.addFirst(curNode.val); // 偶数层结点添加到双端队列头部

                // 判断当前结点是否存在左右结点，如果存在就加入到 queue 中等下一层继续遍历
                if (curNode.left != null)
                    queue.add(curNode.left);
                if (curNode.right != null)
                    queue.add(curNode.right);
            }
            // 把当前层次的遍历结果加入到 res 中
            res.add(deque);
            // 奇变偶 偶变奇
            isOdd = !isOdd;
        }
        return res;
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
    fun levelOrder(root: TreeNode?): List<List<Int>> {
        /**
         * 利用双端队列两头都可以添加元素的性质，假设打印列表tmp为双端队列，规定：
         * 1. 偶数层的结点添加到队列头部
         * 2. 奇数层的结点添加到队列尾部
         */
        // 借助队列存储将要遍历的结点
        val queue = LinkedList<TreeNode>()

        // 层次遍历的结果
        val res = ArrayList<List<Int>>()

        // 判断当前处于什么层，初始化为奇数层
        var isOdd = true

        // 判空
        if (root == null)
            return res

        // 首先把根节点加入到队列中
        queue.add(root)

        // 队列为空时结束循环
        while (!queue.isEmpty()) {
            /**
             * 定义一个双端队列用于存储当前层次的打印结果：
             * 1. 偶数层的结点添加到队列头部
             * 2. 奇数层的结点添加到队列尾部
             */
            val deque = LinkedList<Int>()
            // 遍历当前层次的所有结点（即 queue 里的所有结点）
            for (i in queue.size downTo 1) {
                // 取出 queue 的队头结点作为当前遍历结点
                val curNode = queue.poll()

                // 判断此时处于奇数层还是偶数层
                if (isOdd)
                    deque.addLast(curNode.`val`) // 奇数层结点添加到双端队列尾部
                else
                    deque.addFirst(curNode.`val`) // 偶数层结点添加到双端队列头部

                // 判断当前结点是否存在左右结点，如果存在就加入到 queue 中等下一层继续遍历
                if (curNode.left != null)
                    queue.add(curNode.left)
                if (curNode.right != null)
                    queue.add(curNode.right)
            }
            // 把当前层次的遍历结果加入到 res 中
            res.add(deque)
            // 奇变偶 偶变奇
            isOdd = !isOdd
        }
        return res
    }
}
```

### 2.3 复杂度分析

* 时间复杂度 `O(N)`：N 为二叉树的结点数量，广度优先搜索需要循环 N 次，时间复杂度为`O(N)`。双端队列的队首队尾的添加和删除操作的时间复杂度均为`O(1)`。
* 空间复杂度 `O(N)`：最差情况下，树为满二叉树时，最多会有 `N/2` 个结点在 `queue` 中，需要占用 `O(N)` 大小的额外空间。

> 假设满二叉树的层数为 k ，那么总结点数为 $$2^k-1$$ ，叶子结点的个数为 $$2^{k-1}$$ 。

## 3. 参考

* [https://leetcode-cn.com/problems/cong-shang-dao-xia-da-yin-er-cha-shu-iii-lcof](https://leetcode-cn.com/problems/cong-shang-dao-xia-da-yin-er-cha-shu-iii-lcof)
* [https://leetcode-cn.com/problems/cong-shang-dao-xia-da-yin-er-cha-shu-iii-lcof/solution/mian-shi-ti-32-iii-cong-shang-dao-xia-da-yin-er--3/](https://leetcode-cn.com/problems/cong-shang-dao-xia-da-yin-er-cha-shu-iii-lcof/solution/mian-shi-ti-32-iii-cong-shang-dao-xia-da-yin-er--3/)

## 4. 标签

* BFS
* 树

