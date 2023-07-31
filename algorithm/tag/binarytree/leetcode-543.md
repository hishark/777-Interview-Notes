# LEETCODE 543. 二叉树的直径

## 1. [问题](https://leetcode-cn.com/problems/diameter-of-binary-tree/)

给定一棵二叉树，你需要计算它的直径长度。一棵二叉树的直径长度是任意两个结点路径长度中的最大值。这条路径可能穿过也可能不穿过根结点。

示例 : 给定二叉树

```
          1
         / \
        2   3
       / \     
      4   5  
```

返回 **3**, 它的长度是路径 \[4,2,1,3] 或者 \[5,2,1,3]。

**注意：**两结点之间的路径长度是以它们之间边的数目表示。

## 2. 标签

* 二叉树
* DFS

## 3. 解法 - DFS

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
    // 二叉树的直径
    int maxNodeNum;

    public int diameterOfBinaryTree(TreeNode root) {
        // 最开始的时候只有根结点，所以为1
        maxNodeNum = 1;
        // 深度优先搜索整棵树
        dfs(root);
        // 结点数减去 1 就是路径长度啦
        return maxNodeNum - 1;
    }

    // 求二叉树的高度
    public int dfs(TreeNode root) {
        // 判空
        if (root == null) {
            return 0;
        }
        // 左子树的高度
        int left = dfs(root.left);
        // 右子树的高度
        int right = dfs(root.right);
        // 更新当前的最大直径节点数
        maxNodeNum = Math.max(maxNodeNum, left + right + 1);
        // 当前树的高度即左右子树的较大者 + 1
        return Math.max(left, right) + 1;
    }
}
```

### 3.2 复杂度分析

* 时间复杂度 `O(N)` ：其中 N 为二叉树的节点数，即遍历一棵二叉树的时间复杂度，每个结点只被访问一次。
* 空间复杂度 `O(H)` ：其中 H 为二叉树的高度。由于递归函数在递归过程中需要为每一层递归函数分配栈空间，所以这里需要额外的空间且该空间取决于递归的深度，而递归的深度显然为二叉树的高度，并且每次递归调用的函数里又只用了常数个变量，所以所需空间复杂度为 `O(H)`。

## 4. 参考

* [https://leetcode-cn.com/problems/diameter-of-binary-tree/](https://leetcode-cn.com/problems/diameter-of-binary-tree/)
* [https://leetcode-cn.com/problems/diameter-of-binary-tree/solution/er-cha-shu-de-zhi-jing-by-leetcode-solution/](https://leetcode-cn.com/problems/diameter-of-binary-tree/solution/er-cha-shu-de-zhi-jing-by-leetcode-solution/)
