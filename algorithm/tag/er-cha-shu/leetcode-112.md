---
title: 112. 路径总和
date: '2020-07-07T15:35:03.000Z'
tags:
  - leetcode
  - java
  - kotlin
  - 树
  - 递归
  - BFS
categories: 算法笔记
notshow: true
---

# LEETCODE 112. 路径总和

## 1. [问题](https://leetcode-cn.com/problems/path-sum/)

给定一个二叉树和一个目标和，判断该树中是否存在根节点到叶子节点的路径，这条路径上所有节点值相加等于目标和。

说明: 叶子节点是指没有子节点的节点。

示例:

```text
给定如下二叉树，以及目标和 sum = 22，

              5
             / \
            4   8
           /   / \
          11  13  4
         /  \      \
        7    2      1
返回 true, 因为存在目标和为 22 的根节点到叶子节点的路径 5->4->11->2。
```

## 2. 解法1 - 递归

### 2.1 Java

```java
class Solution {
    public boolean hasPathSum(TreeNode root, int sum) {
        if(root==null)
            return false;
        if(root.left==null && root.right==null && sum-root.val==0)
            return true;
        return hasPathSum(root.left, sum-root.val) || hasPathSum(root.right, sum-root.val);//记得减去root.val
    }
}
```

### 2.2 Kotlin

```kotlin
class Solution {
    fun hasPathSum(root: TreeNode?, sum: Int): Boolean {
        if(root == null) 
            return false
        if(root.left == null && root.right == null && sum - root.`val` == 0) 
            return true
        return hasPathSum(root.left, sum - root.`val`) || hasPathSum(root.right, sum - root.`val`)
    }
}
```

## 3. 解法2 - BFS

### 3.1 Java

```java
class Solution {
    public boolean hasPathSum(TreeNode root, int sum) {
        // 空树
        if (root == null) 
            return false;


        // 定义两个队列，一个存储要遍历的节点，一个存储根节点到这些节点的路径和
        // 两个队列的值一一对应
        Queue<TreeNode> queueNode = new LinkedList<TreeNode>();
        Queue<Integer> queueValue = new LinkedList<Integer>();

        // 初始化，将根节点入队
        queueNode.offer(root);
        queueValue.offer(root.val);

        // 队列不为空时一直循环计算
        while (!queueNode.isEmpty()) {
            // 取出队头节点
            TreeNode curNode = queueNode.poll();
            int curVal = queueValue.poll();

            // 如果此节点为叶子结点
            // 判断该节点的值是否等于sum，若等于就返回true
            if (curNode.left == null && curNode.right == null) {
                if (curVal == sum) 
                    return true;
                // 只要节点为叶子结点就直接continue
                continue;
            }

            // 若当前节点的左子树不为空，就让左子树入队
            if (curNode.left != null) {
                queueNode.offer(curNode.left);
                queueValue.offer(curNode.left.val + curVal); // 千万别忘记加上curVal！在累积和啊！
            }

            // 若当前节点的右子树不为空，就让右子树入队
            if (curNode.right != null) {
                queueNode.offer(curNode.right);
                queueValue.offer(curNode.right.val + curVal);
            }
        }

        // 如果整个while循环都没找到符合条件的路径和，表示不存在，返回false
        return false;
    }
}
```

### 3.2 Kotlin

```kotlin
class Solution {
    fun hasPathSum(root: TreeNode?, sum: Int): Boolean {
        // 空树
        if (root == null) 
            return false

        // 定义两个队列，一个存储要遍历的节点，一个存储根节点到这些节点的路径和
        // 两个队列的值一一对应
        var queueNode = LinkedList<TreeNode>()
        var queueValue = LinkedList<Int>()

        // 初始化，将根节点入队
        queueNode.offer(root)
        queueValue.offer(root.`val`)

        // 队列不为空时一直循环计算
        while (!queueNode.isEmpty()) {
            // 取出队头节点
            val curNode = queueNode.poll()
            val curVal = queueValue.poll()

            // 如果此节点为叶子结点
            // 判断该节点的值是否等于sum，若等于就返回true
            if (curNode.left == null && curNode.right == null) {
                if (curVal == sum) 
                    return true
                // 只要节点为叶子结点就直接continue
                continue
            }

            // 若当前节点的左子树不为空，就让左子树入队
            if (curNode.left != null) {
                queueNode.offer(curNode.left)
                queueValue.offer(curNode.left.`val` + curVal) // 千万别忘记加上curVal！在累积和啊！
            }

            // 若当前节点的右子树不为空，就让右子树入队
            if (curNode.right != null) {
                queueNode.offer(curNode.right)
                queueValue.offer(curNode.right.`val` + curVal)
            }
        }

        // 如果整个while循环都没找到符合条件的路径和，表示不存在，返回false
        return false
    }
}
```

## 4. 参考

* [https://leetcode-cn.com/problems/path-sum](https://leetcode-cn.com/problems/path-sum)
* [https://leetcode-cn.com/problems/path-sum/solution/lu-jing-zong-he-by-leetcode-solution/](https://leetcode-cn.com/problems/path-sum/solution/lu-jing-zong-he-by-leetcode-solution/)

## 5. 笔记

![](https://777blog.oss-cn-shanghai.aliyuncs.com/leetcode/leetcode-112.jpg)

