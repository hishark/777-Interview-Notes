# 68 - I. 二叉搜索树的最近公共祖先

## 1. [问题](https://leetcode-cn.com/problems/er-cha-sou-suo-shu-de-zui-jin-gong-gong-zu-xian-lcof/)

给定一个二叉搜索树, 找到该树中两个指定节点的最近公共祖先。

百度百科中最近公共祖先的定义为：“对于有根树 T 的两个结点 p、q，最近公共祖先表示为一个结点 x，满足 x 是 p、q 的祖先且 x 的深度尽可能大（一个节点也可以是它自己的祖先）。”

例如，给定如下二叉搜索树： `root = [6,2,8,0,4,7,9,null,null,3,5]`

![](../../.gitbook/assets/image%20%2816%29.png)

**示例 1：**

```text
输入: root = [6,2,8,0,4,7,9,null,null,3,5], p = 2, q = 8
输出: 6 
解释: 节点 2 和节点 8 的最近公共祖先是 6。
```

**示例 2：**

```text
输入: root = [6,2,8,0,4,7,9,null,null,3,5], p = 2, q = 4
输出: 2
解释: 节点 2 和节点 4 的最近公共祖先是 2, 因为根据定义最近公共祖先节点可以为节点本身。
```

**说明：**

* 所有节点的值都是唯一的。
* p、q 为不同节点且均存在于给定的二叉搜索树中。

## 2. 标签

* 二叉搜索树
* 递归
* 迭代

## 3. 解法 - 迭代

### 3.1 Java

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
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        // 结点为空时结束循环
        while (root != null) {
            // 如果 p 和 q 都在 root 的右子树中
            if (p.val > root.val && q.val > root.val) {
                // 接下来就往右子树遍历
                root = root.right; 
            // 如果 p 和 q 都在 root 的左子树中
            } else if (p.val < root.val && q.val < root.val) {
                // 接下来就往左子树遍历
                root = root.left;
            } else {
                /**
                 * 剩下三种情况：
                 *  1. p.val == root.val，q 在 root 的左子树或者右子树中
                 *  2. q.val == root.val，p 在 root 的左子树或者右子树中
                 *  3. p 和 q 分别在 root 的不同侧
                 * 这三种情况都说明 root 是 p 和 q 的最近公共祖先
                 * 找到了结果，终止循环即可
                 */
                break;
            }
        }
        // 返回最近公共祖先
        return root;
    }
}
```

### 3.2 复杂度分析

* 时间复杂度 `O(N)` ：其中 N 为二叉树的结点数，当树为满二叉树时，二叉搜索树的层数最小为 logN，当树退化为链表时，二叉搜索树的层数为 N。每循环一轮，排除一层，所以时间复杂度为 `O(N)`。
* 空间复杂度 `O(1)` ：只使用了常数大小的额外空间。

## 4. 解法 - 递归

### 4.1 Java

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
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        // 如果 p 和 q 都在 root 的右子树中
        if (p.val > root.val && q.val > root.val) {
            // 开始递归右子树并返回
            return lowestCommonAncestor(root.right, p, q);
        }

        // 如果 p 和 q 都在 root 的左子树中
        if (p.val < root.val && q.val < root.val) {
            // 开始递归左子树并返回
            return lowestCommonAncestor(root.left, p, q);
        }

        /**
         * 剩下三种情况：
         *  1. p.val == root.val，q 在 root 的左子树或者右子树中
         *  2. q.val == root.val，p 在 root 的左子树或者右子树中
         *  3. p 和 q 分别在 root 的不同侧
         * 这三种情况都说明 root 是 p 和 q 的最近公共祖先
         */
        return root;
    }
}
```

### 4.2 复杂度分析

* 时间复杂度 `O(N)` ：其中 N 为二叉树的结点数，当树为满二叉树时，二叉搜索树的层数最小为 logN，当树退化为链表时，二叉搜索树的层数为 N。每循环一轮，排除一层，所以时间复杂度为 `O(N)`。
* 空间复杂度 `O(N)` ：其中 N 为树的层数，最差情况下当树退化为链表时，递归深度达到树的层数 N。

## 5. 参考

* [https://leetcode-cn.com/problems/er-cha-sou-suo-shu-de-zui-jin-gong-gong-zu-xian-lcof/](https://leetcode-cn.com/problems/er-cha-sou-suo-shu-de-zui-jin-gong-gong-zu-xian-lcof/)
* [https://leetcode-cn.com/problems/er-cha-sou-suo-shu-de-zui-jin-gong-gong-zu-xian-lcof/solution/mian-shi-ti-68-i-er-cha-sou-suo-shu-de-zui-jin-g-7/](https://leetcode-cn.com/problems/er-cha-sou-suo-shu-de-zui-jin-gong-gong-zu-xian-lcof/solution/mian-shi-ti-68-i-er-cha-sou-suo-shu-de-zui-jin-g-7/)

