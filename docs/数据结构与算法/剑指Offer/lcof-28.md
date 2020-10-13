---
title: 28. 对称的二叉树
date: 2020-10-02 00:11:26
tags: 
- leetcode
- java
- kotlin
- lcof
- 树
- 简单
categories: 算法笔记
---
# 28. 对称的二叉树
## 1. [问题](https://leetcode-cn.com/problems/dui-cheng-de-er-cha-shu-lcof)
请实现一个函数，用来判断一棵二叉树是不是对称的。如果一棵二叉树和它的镜像一样，那么它是对称的。

<!--more-->

例如，二叉树 [1,2,2,3,4,4,3] 是对称的。
```
    1
   / \
  2   2
 / \ / \
3  4 4  3
```

但是下面这个 [1,2,2,null,3,null,3] 则不是镜像对称的:
```
    1
   / \
  2   2
   \   \
   3    3
```
 

示例 1：
```
输入：root = [1,2,2,3,4,4,3]
输出：true
```

示例 2：
```
输入：root = [1,2,2,null,3,null,3]
输出：false
```

限制：

- 0 <= 节点个数 <= 1000


## 2. 解法

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
    public boolean isSymmetric(TreeNode root) {
        // 空树显然对称
        if (root == null)
            return true;
        // 非空树，检查左右子树是否对称
        return recursion(root.left, root.right);
    }

    // 检查L和R是否对称
    public boolean recursion(TreeNode L, TreeNode R) {
        // L和R同时越过叶子结点，为空，则该树从顶到底都对称，返回true
        if (L == null && R == null)
            return true;
        
        // 1. L和R只有一个越过叶子结点
        // 2. L的值和R的值不相等
        // 这两种情况下明显树不对称，返回false
        if ((L == null || R == null) || L.val != R.val)
            return false;
        
        // 判断L的left和R的right是否对称，L的right和R的left是否对称
        return recursion(L.left, R.right) && recursion(L.right, R.left);
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
    fun isSymmetric(root: TreeNode?): Boolean {
        // 空树显然对称
        // 非空树，检查左右子树是否对称
        return if (root == null) true else recursion(root.left, root.right)
    }

    // 检查L和R是否对称
    fun recursion(L: TreeNode?, R: TreeNode?): Boolean {
        // L和R同时越过叶子结点，为空，则该树从顶到底都对称，返回true
        if (L == null && R == null)
            return true

        // 1. L和R只有一个越过叶子结点
        // 2. L的值和R的值不相等
        // 这两种情况下明显树不对称，返回false
        return if (L == null || R == null || L.`val` !== R!!.`val`) false else recursion(
            L.left,
            R.right
        ) && recursion(L.right, R.left)// 判断L的left和R的right是否对称，L的right和R的left是否对称
    }
}
```

### 2.3 复杂度分析
- 时间复杂度O(N)：其中N是二叉树的结点数量，每次执行`recursion()`可以判断一对结点是否对称，所以最多调用`N/2`次`recursion()`方法。
- 空间复杂度O(N)：最差情况下二叉树退化为链表，系统需要占用O(N)大小的栈。

## 3. 参考
- [https://leetcode-cn.com/problems/dui-cheng-de-er-cha-shu-lcof](https://leetcode-cn.com/problems/dui-cheng-de-er-cha-shu-lcof)
- [https://leetcode-cn.com/problems/dui-cheng-de-er-cha-shu-lcof/solution/mian-shi-ti-28-dui-cheng-de-er-cha-shu-di-gui-qing/](https://leetcode-cn.com/problems/dui-cheng-de-er-cha-shu-lcof/solution/mian-shi-ti-28-dui-cheng-de-er-cha-shu-di-gui-qing/)