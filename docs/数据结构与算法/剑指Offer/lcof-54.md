---
title: 54. 二叉搜索树的第k大节点
date: 2020-08-06 15:13:14
tags:
- 树
- leetcode
- lcof
- java
- kotlin
categories: 算法笔记
notshow: true
---
# 54. 二叉搜索树的第k大节点
## 1. [问题](https://leetcode-cn.com/problems/er-cha-sou-suo-shu-de-di-kda-jie-dian-lcof/)
给定一棵二叉搜索树，请找出其中第k大的节点。
<!--more-->

示例 1:
```
输入: root = [3,1,4,null,2], k = 1
   3
  / \
 1   4
  \
   2
输出: 4
```

示例 2:
```
输入: root = [5,3,6,2,4,null,null,1], k = 3
       5
      / \
     3   6
    / \
   2   4
  /
 1
输出: 4
```

限制：

- 1 ≤ k ≤ 二叉搜索树元素个数



## 2. 解法 - 中序遍历

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
    int ans, kk;
    public int kthLargest(TreeNode root, int k) {
        // kk作为全局变量使用
        kk = k;
        // 对二叉搜索树进行中序遍历
        dfs(root);
        // 返回结果
        return ans;
    }

    // 中序遍历的遍历：右根左
    public void dfs(TreeNode root) {
        if (root ==  null)
            return;

        // 右
        dfs(root.right);

        // 找到了第k大的元素，记录下来
        if (--kk == 0)
            ans = root.val;

        // kk已经找到了，返回即可
        if (kk == 0)
            return;

        // 左
        dfs(root.left);
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
    var ans: Int = 0
    var kk: Int = 0
    fun kthLargest(root: TreeNode, k: Int): Int {
        // kk作为全局变量使用
        kk = k
        // 对二叉搜索树进行中序遍历
        dfs(root)
        // 返回结果
        return ans
    }

    // 中序遍历的遍历：右根左
    fun dfs(root: TreeNode?) {
        if (root == null)
            return

        // 右
        dfs(root.right)

        // 找到了第k大的元素，记录下来
        if (--kk == 0)
            ans = root.`val`

        // kk已经找到了，返回即可
        if (kk == 0)
            return

        // 左
        dfs(root.left)
    }
}
```

## 3. 参考
- [https://leetcode-cn.com/problems/er-cha-sou-suo-shu-de-di-kda-jie-dian-lcof/](https://leetcode-cn.com/problems/er-cha-sou-suo-shu-de-di-kda-jie-dian-lcof/)
- [https://leetcode-cn.com/problems/er-cha-sou-suo-shu-de-di-kda-jie-dian-lcof/solution/mian-shi-ti-54-er-cha-sou-suo-shu-de-di-k-da-jie-d/](https://leetcode-cn.com/problems/er-cha-sou-suo-shu-de-di-kda-jie-dian-lcof/solution/mian-shi-ti-54-er-cha-sou-suo-shu-de-di-k-da-jie-d/)

## 4. 笔记
![](https://777blog.oss-cn-shanghai.aliyuncs.com/leetcode/lcof-54.jpg)