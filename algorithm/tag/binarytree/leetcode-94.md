# LEETCODE 94. 二叉树的中序遍历

## 1. [问题](https://leetcode-cn.com/problems/binary-tree-inorder-traversal/)

给定一个二叉树的根节点 `root` ，返回它的 **中序** 遍历。

**示例 1：**

![](../../../.gitbook/assets/image%20%2826%29.png)

```text
输入：root = [1,null,2,3]
输出：[1,3,2]
```

**示例 2：**

```text
输入：root = []
输出：[]
```

**示例 3：**

```text
输入：root = [1]
输出：[1]
```

**示例 4：**

![](../../../.gitbook/assets/image%20%2824%29.png)

```text
输入：root = [1,2]
输出：[2,1]
```

**示例 5：**

![](../../../.gitbook/assets/image%20%2841%29.png)

```text
输入：root = [1,null,2]
输出：[1,2]
```

**提示：**

* 树中节点数目在范围 `[0, 100]` 内
* `-100 <= Node.val <= 100`

**进阶:** 递归算法很简单，你可以通过迭代算法完成吗？

## 2. 标签

* 二叉树
* 递归
* 栈

## 3. 解法 - 递归

### 3.1 Java

```java
class Solution {
    public List<Integer> inorderTraversal(TreeNode root) {
        // 中序遍历结果
        List<Integer> ans = new ArrayList<Integer>();
        // 递归
        inorder(root, ans);
        // 返回结果即可
        return ans;
    }

    /**
     * 中序遍历
     * @param root 树的根结点
     * @param ans 中序遍历的结果
     */
    public void inorder(TreeNode root, List<Integer> ans) {
        // 遍历到空结点时，结束递归
        if (root == null) {
            return;
        }
        // 中序遍历：左，根，右
        // 左
        inorder(root.left, ans);
        // 根
        ans.add(root.val);
        // 右
        inorder(root.right, ans);
    }
}
```

### 3.2 复杂度分析

* 时间复杂度 `O(n)` ：其中 n 为二叉树节点的个数。二叉树的遍历中每个节点会被访问一次且只会被访问一次。
* 空间复杂度 `O(n)` ：空间复杂度取决于递归的栈深度，而栈深度在二叉树为一条链的情况下会达到 O\(n\) 的级别。

## 4. 解法 - 栈

> 迭代

### 4.1 Java

```java

```

### 4.2 复杂度分析

* 时间复杂度 `O(n)` ：其中 n 为二叉树节点的个数。二叉树的遍历中每个节点会被访问一次且只会被访问一次。
* 空间复杂度 `O(n)` ：空间复杂度取决于栈深度，而栈深度在二叉树为一条链的情况下会达到 O\(n\) 的级别。

## 5. 参考

* [https://leetcode-cn.com/problems/binary-tree-inorder-traversal/](https://leetcode-cn.com/problems/binary-tree-inorder-traversal/)
* [https://leetcode-cn.com/problems/binary-tree-inorder-traversal/solution/er-cha-shu-de-zhong-xu-bian-li-by-leetcode-solutio/](https://leetcode-cn.com/problems/binary-tree-inorder-traversal/solution/er-cha-shu-de-zhong-xu-bian-li-by-leetcode-solutio/)

