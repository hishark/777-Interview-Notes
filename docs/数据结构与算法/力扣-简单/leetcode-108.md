---
title: 108. 将有序数组转换为二叉搜索树
date: 2020-07-03 17:42:12
tags:
- 树
- DFS
- leetcode
- java
categories: 算法笔记
notshow: true
---
# 108. 将有序数组转换为二叉搜索树
## [1. 问题](https://leetcode-cn.com/problems/convert-sorted-array-to-binary-search-tree/)
将一个按照升序排列的有序数组，转换为一棵高度平衡二叉搜索树。

本题中，一个高度平衡二叉树是指一个二叉树每个节点 的左右两个子树的高度差的绝对值不超过 1。

示例:
```
给定有序数组: [-10,-3,0,5,9],
一个可能的答案是：[0,-3,9,-10,null,5]，它可以表示下面这个高度平衡二叉搜索树：
      0
     / \
   -3   9
   /   /
 -10  5
```
<!--more-->

## 2. 解法 - DFS
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
    public TreeNode sortedArrayToBST(int[] nums) {
        return dfs(nums, 0, nums.length - 1);
    }
    
    public TreeNode dfs(int[] nums, int left, int right) {
        // 如果左大于右，返回null
        if (left>right)
            return null;
        
        // 找中点
        int mid = left + (right - left) / 2;
        
        // 中点位置的元素作为根结点
        TreeNode root = new TreeNode(nums[mid]);
        
        // 递归构建左子树
        root.left = dfs(nums, left, mid - 1);
        
        // 递归构建右子树
        root.right = dfs(nums, mid + 1, right);

        // 返回根结点
        return root;
    }
}
```

## 3. 参考
- [https://leetcode-cn.com/problems/convert-sorted-array-to-binary-search-tree/](https://leetcode-cn.com/problems/convert-sorted-array-to-binary-search-tree/)
- [https://leetcode-cn.com/problems/convert-sorted-array-to-binary-search-tree/solution/jian-dan-di-gui-bi-xu-miao-dong-by-sweetiee/](https://leetcode-cn.com/problems/convert-sorted-array-to-binary-search-tree/solution/jian-dan-di-gui-bi-xu-miao-dong-by-sweetiee/)
- [https://leetcode-cn.com/problems/convert-sorted-list-to-binary-search-tree/solution/you-xu-lian-biao-zhuan-huan-er-cha-sou-suo-shu-by-/](https://leetcode-cn.com/problems/convert-sorted-list-to-binary-search-tree/solution/you-xu-lian-biao-zhuan-huan-er-cha-sou-suo-shu-by-/)

## 4. 笔记
![](https://777blog.oss-cn-shanghai.aliyuncs.com/blog%20pic/leetcode-108.jpg)