# LCOF 68 - II. 二叉树的最近公共祖先

## 1. [问题](https://leetcode-cn.com/problems/er-cha-shu-de-zui-jin-gong-gong-zu-xian-lcof/) <a href="1-wen-ti" id="1-wen-ti"></a>

‌给定一个二叉树, 找到该树中两个指定节点的最近公共祖先。

[百度百科](https://baike.baidu.com/item/%E6%9C%80%E8%BF%91%E5%85%AC%E5%85%B1%E7%A5%96%E5%85%88/8918834?fr=aladdin)中最近公共祖先的定义为：“对于有根树 T 的两个结点 p、q，最近公共祖先表示为一个结点 x，满足 x 是 p、q 的祖先且 x 的深度尽可能大（一个节点也可以是它自己的祖先）。”

例如，给定如下二叉树: root = \[3,5,1,6,2,0,8,null,null,7,4]

![](<../../../.gitbook/assets/image (8).png>)

**示例 1:**

```
输入: root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 1
输出: 3
解释: 节点 5 和节点 1 的最近公共祖先是节点 3。
```

**示例 2:**

```
输入: root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 4
输出: 5
解释: 节点 5 和节点 4 的最近公共祖先是节点 5。因为根据定义最近公共祖先节点可以为节点本身。
```

**说明:**

* 所有节点的值都是唯一的。
* p、q 为不同节点且均存在于给定的二叉树中。

## 2. 标签‌ <a href="2-biao-qian" id="2-biao-qian"></a>

* 树
* DFS
* 递归

## 3. 解法 <a href="3-jie-fa" id="3-jie-fa"></a>

### 3.1 Java <a href="3-1-java" id="3-1-java"></a>

```java
​/**
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
        /**
         * 递归终止条件：
         *  1. 递归越过叶子结点，直接返回 null
         *  2. 当 root 等于 p 或者 q 时，root 即最近公共祖先，直接返回
         */
        if (root == null || root == p || root == q)
            return root;

        // 递归左子树
        TreeNode leftTree = lowestCommonAncestor(root.left, p, q);

        // 递归右子树
        TreeNode rightTree = lowestCommonAncestor(root.right, p, q);

        // 根据 leftTree 和 rightTree 的值，可以分为四种情况
        // 1. 同时为空，说明 root 的左右子树都不包含 p 和 q
        if (leftTree == null && rightTree == null)
            return null;

        // 2. 只有 leftTree 为空，说明 p 和 q 都不在 root 的左子树中，直接返回 rightTree
        if (leftTree == null)
            return rightTree;

        // 3. 只有 rightTree 为空，说明 p 和 q 都不在 root 的右子树中，直接返回 leftTree
        if (rightTree == null)
            return leftTree;

        // 4. 同时不为空，说明 p 和 q 处于 root 的不同侧，因此 root 就是最近公共祖先，返回即可
        return root;
    }
}
```

### 3.2 复杂度分析 <a href="33-fu-za-du-fen-xi" id="33-fu-za-du-fen-xi"></a>

* 时间复杂度 `O(N)` ：其中 N 为二叉树的结点数，最差情况下，二叉树退化为链表时，需要递归遍历树的所有结点。
* 空间复杂度 `O(N)` ：最差情况下，当二叉树退化为链表时，递归深度达到 N，系统需要使用 `O(N)` 大小的额外存储空间。

## 4. 参考 <a href="4-can-kao" id="4-can-kao"></a>

* [https://leetcode-cn.com/problems/er-cha-shu-de-zui-jin-gong-gong-zu-xian-lcof/](https://leetcode-cn.com/problems/er-cha-shu-de-zui-jin-gong-gong-zu-xian-lcof/)
* [https://leetcode-cn.com/problems/er-cha-shu-de-zui-jin-gong-gong-zu-xian-lcof/solution/mian-shi-ti-68-ii-er-cha-shu-de-zui-jin-gong-gon-7/](https://leetcode-cn.com/problems/er-cha-shu-de-zui-jin-gong-gong-zu-xian-lcof/solution/mian-shi-ti-68-ii-er-cha-shu-de-zui-jin-gong-gon-7/)​
