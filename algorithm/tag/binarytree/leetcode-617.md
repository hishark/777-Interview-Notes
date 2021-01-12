# LEETCODE 617. 合并二叉树

## 1. [问题](https://leetcode-cn.com/problems/merge-two-binary-trees/)

给定两个二叉树，想象当你将它们中的一个覆盖到另一个上时，两个二叉树的一些节点便会重叠。

你需要将他们合并为一个新的二叉树。合并的规则是如果两个节点重叠，那么将他们的值相加作为节点合并后的新值，否则不为 NULL 的节点将直接作为新二叉树的节点。

示例1：

```text
输入: 
	Tree 1                     Tree 2                  
          1                         2                             
         / \                       / \                            
        3   2                     1   3                        
       /                           \   \                      
      5                             4   7                  
输出: 
合并后的树:
	     3
	    / \
	   4   5
	  / \   \ 
	 5   4   7
```

**注意:** 合并必须从两个树的根节点开始。

## 2. 标签

* 二叉树
* DFS

## 3. 解法 - DFS

### 3.1 Java

```java
class Solution {
    public TreeNode mergeTrees(TreeNode t1, TreeNode t2) {
        // 有一个结点为空，就返回另一个结点
        if (t1 == null) {
            return t2;
        }
        if (t2 == null) {
            return t1;
        }
        // 两个结点都不为空，将两个结点的值相加即可
        TreeNode root = new TreeNode(t1.val + t2.val);
        // 合并了当前结点后，还要对该结点的左右子树分别进行合并
        root.left = mergeTrees(t1.left, t2.left);
        root.right = mergeTrees(t1.right, t2.right);
        // 返回根结点
        return root;
    }
}
```

### 3.2 复杂度分析

* 时间复杂度 `O(min(m,n))` ：其中 m 和 n 分别是两个二叉树的节点个数。
* 空间复杂度 `O(min(m,n))` ：其中 m 和 n 分别是两个二叉树的节点个数。

## 4. 参考

* [https://leetcode-cn.com/problems/merge-two-binary-trees/](https://leetcode-cn.com/problems/merge-two-binary-trees/)
* [https://leetcode-cn.com/problems/merge-two-binary-trees/solution/he-bing-er-cha-shu-by-leetcode-solution/](https://leetcode-cn.com/problems/merge-two-binary-trees/solution/he-bing-er-cha-shu-by-leetcode-solution/)

