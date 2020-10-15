---
title: 34. 二叉树中和为某一值的路径
date: 2020-10-15 23:26:20
tags:
- leetcode
- lcof
- java
- 树
- DFS
- kotlin
categories: 算法笔记
---
# 34. 二叉树中和为某一值的路径
## 1. [问题](https://leetcode-cn.com/problems/er-cha-shu-zhong-he-wei-mou-yi-zhi-de-lu-jing-lcof)
输入一棵二叉树和一个整数，打印出二叉树中节点值的和为输入整数的所有路径。从树的根节点开始往下一直到叶节点所经过的节点形成一条路径。
 
<!--more-->

示例:
给定如下二叉树，以及目标和 sum = 22，
```
              5
             / \
            4   8
           /   / \
          11  13  4
         /  \    / \
        7    2  5   1
```

返回:
```
[
   [5,4,11,2],
   [5,8,4,5]
]
```

提示：

- 节点总数 <= 10000

## 2. 解法
### 2.1 Java
```java
import java.util.LinkedList;

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
    // 结果列表
    LinkedList<List<Integer>> res = new LinkedList<>();
    // 路径
    LinkedList<Integer> path = new LinkedList<>();

    public List<List<Integer>> pathSum(TreeNode root, int sum) {
        recursion(root, sum);
        return res;
    }

    public void recursion(TreeNode root, int sum) {
        // 判空
        if (root == null)
            return;

        // 首先把根结点加入到路径中
        path.add(root.val);
        // 路径和减去根结点的值
        sum -= root.val;

        // 此时需要判断一下路径和是否等于 0 且根结点不存在左右结点，若成立，把此时的路径添加到结果中
        if (sum == 0 && root.left == null & root.right == null)
            res.add(new LinkedList(path));
        
        // 递归左右子树
        recursion(root.left, sum);
        recursion(root.right, sum);

        // 回溯，删去此时路径中的最后一个结点
        path.removeLast();
    }
}
```

### 2.2 Kotlin
```kotlin
pending
```

### 2.3 复杂度分析
- 时间复杂度 `O(N)`：N 为二叉树的结点数，先序遍历需要遍历所有结点。
- 空间复杂度 `O(N)`：最差情况下，即当树退化为链表时，path 需要存储所有结点，占用 `O(N)` 额外空间。

## 3. 参考
- [https://leetcode-cn.com/problems/er-cha-shu-zhong-he-wei-mou-yi-zhi-de-lu-jing-lcof](https://leetcode-cn.com/problems/er-cha-shu-zhong-he-wei-mou-yi-zhi-de-lu-jing-lcof)
- [https://leetcode-cn.com/problems/er-cha-shu-zhong-he-wei-mou-yi-zhi-de-lu-jing-lcof/solution/mian-shi-ti-34-er-cha-shu-zhong-he-wei-mou-yi-zh-5/](https://leetcode-cn.com/problems/er-cha-shu-zhong-he-wei-mou-yi-zhi-de-lu-jing-lcof/solution/mian-shi-ti-34-er-cha-shu-zhong-he-wei-mou-yi-zh-5/)

## 4. 关键词

- 树
- DFS
- 回溯