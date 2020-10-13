---
title: 104. 二叉树的最大深度
date: 2020-07-28 17:05:27
tags:
- leetcode
- java
- kotlin
- 树
- DFS
- BFS
categories: 算法笔记
notshow: true
---
# 104. 二叉树的最大深度
## 1. [问题](https://leetcode-cn.com/problems/maximum-depth-of-binary-tree)
给定一个二叉树，找出其最大深度。

二叉树的深度为根节点到最远叶子节点的最长路径上的节点数。

说明: 叶子节点是指没有子节点的节点。

示例：
```
给定二叉树 [3,9,20,null,null,15,7]，

    3
   / \
  9  20
    /  \
   15   7
```
返回它的最大深度 3 。
<!--more-->

## 2. 解法 - DFS

### 2.1 Java
```java
class Solution {
    public int maxDepth(TreeNode root) {
        if (root == null) return 0;
        return Math.max(maxDepth(root.left) ,maxDepth(root.right)) + 1;
    }
}
```

### 2.2 Kotlin
```kotlin
class Solution {
    fun maxDepth(root: TreeNode?): Int {
        return if (root == null) 0 else Math.max(maxDepth(root.left), maxDepth(root.right)) + 1
    }
}
```

## 3. 解法 - BFS

### 3.1 Java
```java
class Solution {
    public int maxDepth(TreeNode root) {
        // 判空
        if(root == null) return 0;
    
        // 队列，一层层的搜索时，用于存放当前层的所有结点
        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);

        // 二叉树的层数
        int ans = 0;

        while(!queue.isEmpty()) {
            // 二叉树当前层的结点数目
            int curSize = queue.size();
            
            // 遍历当前层的所有结点，把它们的左右子结点都加入到队列里，用于下一次循环（外层）
            while(curSize!=0) {
                TreeNode cur = queue.poll();
                if(cur.left != null) {
                    queue.offer(cur.left); 
                }
                if(cur.right != null) {
                    queue.offer(cur.right); 
                }
                curSize--;
            }
            
            // 每遍历一层，就增加层数
            ans++;
        }

        // 二叉树的层数即二叉树的最大深度
        return ans;
    }

}
```

### 3.2 Kotlin
```kotlin
class Solution {
    fun maxDepth(root: TreeNode?): Int {
        // 判空
        if (root == null) return 0

        // 队列，一层层的搜索时，用于存放当前层的所有结点
        val queue = LinkedList<TreeNode>()
        queue.offer(root)

        // 二叉树的层数
        var ans = 0

        while (!queue.isEmpty()) {
            // 二叉树当前层的结点数目
            var curSize = queue.size

            // 遍历当前层的所有结点，把它们的左右子结点都加入到队列里，用于下一次循环（外层）
            while (curSize != 0) {
                val cur = queue.poll()
                if (cur.left != null) {
                    queue.offer(cur.left)
                }
                if (cur.right != null) {
                    queue.offer(cur.right)
                }
                curSize--
            }

            // 每遍历一层，就增加层数
            ans++
        }

        // 二叉树的层数即二叉树的最大深度
        return ans
    }

}
```

## 4. 参考
- [https://leetcode-cn.com/problems/maximum-depth-of-binary-tree](https://leetcode-cn.com/problems/maximum-depth-of-binary-tree)
- [https://leetcode-cn.com/problems/maximum-depth-of-binary-tree/solution/er-cha-shu-de-zui-da-shen-du-by-leetcode-solution/](https://leetcode-cn.com/problems/maximum-depth-of-binary-tree/solution/er-cha-shu-de-zui-da-shen-du-by-leetcode-solution/)

## 5. 笔记
![](https://777blog.oss-cn-shanghai.aliyuncs.com/leetcode/leetcode-104-1.jpg)
![](https://777blog.oss-cn-shanghai.aliyuncs.com/leetcode/leetcode-104-2.jpg)