# LCOF 07. 重建二叉树

## 1. [问题](https://leetcode-cn.com/problems/zhong-jian-er-cha-shu-lcof/)

输入某二叉树的前序遍历和中序遍历的结果，请重建该二叉树。假设输入的前序遍历和中序遍历的结果中都不含重复的数字。

例如，给出

```
前序遍历 preorder = [3,9,20,15,7]
中序遍历 inorder = [9,3,15,20,7]
```

返回如下的二叉树：

```
    3
   / \
  9  20
    /  \
   15   7
```

限制：

* 0 <= 节点个数 <= 5000

## 2. 解法 - 递归

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
    // 存储中序遍历中各个结点的下标
    Map<Integer, Integer> indexMap = new HashMap<Integer, Integer>();

    public TreeNode buildTree(int[] preorder, int[] inorder) {
        // 判空
        if (preorder.length == 0)
            return null;

        // 将中序遍历中所有结点的下标存储到map中
        // 为什么这里要存储中序遍历的结点下标？
        // 因为需要先在中序遍历中得到左右子树的中序遍历下标范围和结点数量，然后根据左右子树的结点数量才能在前序遍历中确定左右子树的前序遍历下标范围。
        for(int i=0;i<inorder.length;i++) {
            indexMap.put(inorder[i], i);
        }

        // 结点数量
        int size = preorder.length;

        // 重建二叉树
        TreeNode root = buildTree(preorder, 0, size - 1, inorder, 0, size - 1);
        return root;
    }

    // 前序遍历下标范围[preStart, preEnd]
    // 中序遍历下标范围[inStart, inEnd]
    public TreeNode buildTree(int[] preorder, int preStart, int preEnd, int[] inorder, int inStart, int inEnd) {
        // 判断前序遍历的下标范围的start和end的关系

        // 开始大于结束，说明当前二叉树中没有结点，返回null即可
        if (preStart > preEnd)
            return null;

        // 另外两种情况都需要先确定根节点
        // 已知前序遍历的第一个节点就是根节点
        int rootValue = preorder[preStart];
        TreeNode root = new TreeNode(rootValue);

        // 开始等于结束，则当前的二叉树中恰好有一个节点，即根节点
        if (preStart == preEnd) {
            return root;
        } else {
            // 开始小于结束，说明当前二叉树中有多个结点。
            // 先在中序遍历中确定左右子树的结点数量
            int rootIndex = indexMap.get(rootValue); //根节点在中序遍历中的下标
            int leftNodeNum = rootIndex - inStart; //根节点下标 - 中序遍历起点 = 左子树结点数量
            int rightNodeNum = inEnd - rootIndex; //中序遍历终点 - 根节点下标 = 右子树结点数量

            // 递归重建左右子树
            // 参数意义：
            // 前序遍历，左子树的前序起点下标，前序终点下标，中序遍历，左子树的中序起点下标，中序终点下标
            TreeNode leftTree = buildTree(preorder, preStart + 1, preStart + leftNodeNum, inorder, inStart, inStart + leftNodeNum - 1); // 最后一个参数也可以是rootIndex - 1
            // 参数意义：
            // 前序遍历，右子树的前序起点下标，前序终点下标，中序遍历，右子树的中序起点下标，中序终点下标
            TreeNode rightTree = buildTree(preorder, preEnd - rightNodeNum + 1, preEnd, inorder, rootIndex + 1, inEnd);

            // 根节点的左右结点即左右子树的根节点
            root.left = leftTree;
            root.right = rightTree;

            // 返回根节点
            return root;

        }
    }
}
```

## 3. 参考

* [https://leetcode-cn.com/problems/zhong-jian-er-cha-shu-lcof/](https://leetcode-cn.com/problems/zhong-jian-er-cha-shu-lcof/)
* [https://leetcode-cn.com/problems/zhong-jian-er-cha-shu-lcof/solution/mian-shi-ti-07-zhong-jian-er-cha-shu-by-leetcode-s/](https://leetcode-cn.com/problems/zhong-jian-er-cha-shu-lcof/solution/mian-shi-ti-07-zhong-jian-er-cha-shu-by-leetcode-s/)

## 4. 笔记

![](<../../../.gitbook/assets/image (18).png>)
