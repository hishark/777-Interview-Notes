---
title: 95. 不同的二叉搜索树 II
date: '2020-07-21T16:38:46.000Z'
tags:
  - leetcode
  - java
  - kotlin
  - 树
  - 动态规划
  - 递归
categories: 算法笔记
notshow: true
---

# leetcode-95

## 1. [问题](https://leetcode-cn.com/problems/unique-binary-search-trees-ii/)

给定一个整数 n，生成所有由 1 ... n 为节点所组成的 二叉搜索树 。

示例：

```text
输入：3
输出：
[
  [1,null,3,2],
  [3,2,null,1],
  [3,1,null,null,2],
  [2,1,3],
  [1,null,2,null,3]
]
解释：
以上的输出对应以下 5 种不同结构的二叉搜索树：

   1         3     3      2      1
    \       /     /      / \      \
     3     2     1      1   3      2
    /     /       \                 \
   2     1         2                 3
```

提示：

* 0 &lt;= n &lt;= 8

## 2. 解法 - 递归

### 2.1 Java

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    public List<TreeNode> generateTrees(int n) {
        if (n==0)
            return new ArrayList<>();
        else 
            return generateTrees(1, n);
    }

    public List<TreeNode> generateTrees(int start, int end) {
        List<TreeNode> allTress = new ArrayList<>();

        // 递归出口，此时不存在一棵BST，直接返回null
        if (start > end) {
            allTress.add(null);
            return allTress;
        }

        // 枚举[start, end]中的值作为根节点
        for (int i=start;i<=end;i++) {
            // 左子树
            List<TreeNode> leftTrees = generateTrees(start, i-1);

            // 右子树
            List<TreeNode> rightTrees = generateTrees(i+1, end);

            // 遍历左右子树，和根节点i生成一棵BST
            for (TreeNode leftTree: leftTrees) {
                for (TreeNode rightTree: rightTrees) {
                    // 根节点
                    TreeNode root = new TreeNode(i);
                    // 左子树
                    root.left = leftTree;
                    // 右子树
                    root.right = rightTree;

                    allTress.add(root);
                }
            }
        }

        return allTress;
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
    fun generateTrees(n: Int): List<TreeNode?> {
        return if (n == 0)
            mutableListOf<TreeNode?>()
        else
            generateTrees(1, n)
    }

    fun generateTrees(start: Int, end: Int): List<TreeNode?> {
        val allTress = mutableListOf<TreeNode?>()

        // 递归出口，此时不存在一棵BST，直接返回null
        if (start > end) {
            allTress.add(null)
            return allTress
        }

        // 枚举[start, end]中的值作为根节点
        for (i in start..end) {
            // 左子树
            val leftTrees = generateTrees(start, i - 1)

            // 右子树
            val rightTrees = generateTrees(i + 1, end)

            // 遍历左右子树，和根节点i生成一棵BST
            for (leftTree in leftTrees) {
                for (rightTree in rightTrees) {
                    // 根节点
                    val root = TreeNode(i)
                    // 左子树
                    root.left = leftTree
                    // 右子树
                    root.right = rightTree

                    allTress.add(root)
                }
            }
        }

        return allTress
    }
}
```

## 3. 参考

* [https://leetcode-cn.com/problems/unique-binary-search-trees-ii/](https://leetcode-cn.com/problems/unique-binary-search-trees-ii/)
* [https://leetcode-cn.com/problems/unique-binary-search-trees-ii/solution/bu-tong-de-er-cha-sou-suo-shu-ii-by-leetcode-solut/](https://leetcode-cn.com/problems/unique-binary-search-trees-ii/solution/bu-tong-de-er-cha-sou-suo-shu-ii-by-leetcode-solut/)

## 4. 笔记

![](https://777blog.oss-cn-shanghai.aliyuncs.com/leetcode/leetcode-95-1.jpg) ![](https://777blog.oss-cn-shanghai.aliyuncs.com/leetcode/leetcode-95-2.jpg)

