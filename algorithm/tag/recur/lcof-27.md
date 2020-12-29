# LCOF 27. 二叉树的镜像

## 1. [问题](https://leetcode-cn.com/problems/er-cha-shu-de-jing-xiang-lcof/)

请完成一个函数，输入一个二叉树，该函数输出它的镜像。

例如输入：

```text
     4
   /   \
  2     7
 / \   / \
1   3 6   9
```

镜像输出：

```text
     4
   /   \
  7     2
 / \   / \
9   6 3   1
```

示例 1：

```text
输入：root = [4,2,7,1,3,6,9]
输出：[4,7,2,9,6,3,1]
```

限制：

* 0 &lt;= 节点个数 &lt;= 1000

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
//递归
class Solution {
    public TreeNode mirrorTree(TreeNode root) {
        // 递归出口：遍历到叶子结点时返回空
        if (root == null)
            return null;

        // 利用工具人tmp暂存一下左子树
        TreeNode tmp = root.left;
        // 递归右子树，把返回值作为root的左子树
        root.left = mirrorTree(root.right);
        // 递归左子树，把返回值作为root的右子树
        root.right = mirrorTree(tmp);
        // 返回根节点
        return root;
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
    fun mirrorTree(root: TreeNode?): TreeNode? {
        // 递归出口：遍历到叶子结点时返回空
        if (root == null)
            return null

        // 利用工具人tmp暂存一下左子树
        val tmp = root.left
        // 递归右子树，把返回值作为root的左子树
        root.left = mirrorTree(root.right)
        // 递归左子树，把返回值作为root的右子树
        root.right = mirrorTree(tmp)
        // 返回根节点
        return root
    }
}
```

### 2.3 复杂度分析

* 时间复杂度`O(N)`：其中N为二叉树的结点数量，建立二叉树的镜像需要遍历树中所有的结点，占用`O(N)`时间。
* 空间复杂度`O(N)`：当处于最差情况时，即当二叉树退化为链表时，递归时系统需要使用`O(N)`大小的栈空间。

## 3. 解法 - 辅助栈

> 可以用辅助栈或者队列。

### 3.1 Java

```java
//辅助栈
class Solution {
    public TreeNode mirrorTree(TreeNode root) {
        // 特判，根为空直接返回空
        if(root == null) 
            return null;

        // 辅助栈
        Stack<TreeNode> stack = new Stack<>();

        // 初始化，添加根结点
        stack.add(root);

        // 当辅助栈为空时跳出循环
        while(!stack.isEmpty()) {
            // 先把当前结点pop出来
            TreeNode curNode = stack.pop();

            // 如果当前节点的左结点不为空，就把左节点加入到辅助栈中
            if(curNode.left != null) 
                stack.add(curNode.left);
            // 如果当前节点的右结点不为空，就把右节点加入到辅助栈中
            if(curNode.right != null) 
                stack.add(curNode.right);
            
            // 交换当前结点的左右结点
            TreeNode tmp = curNode.left;
            curNode.left = curNode.right;
            curNode.right = tmp;
        }

        // 返回root，此时已经完成镜像
        return root;
    }
}
```

### 3.2 Kotlin

```kotlin
// 辅助栈
class Solution {
    fun mirrorTree(root: TreeNode?): TreeNode? {
        // 特判，根为空直接返回空
        if (root == null)
            return null

        // 辅助栈
        val stack = Stack<TreeNode>()

        // 初始化，添加根结点
        stack.add(root)

        // 当辅助栈为空时跳出循环
        while (!stack.isEmpty()) {
            // 先把当前结点pop出来
            val curNode = stack.pop()

            // 如果当前节点的左结点不为空，就把左节点加入到辅助栈中
            if (curNode.left != null)
                stack.add(curNode.left)
            // 如果当前节点的右结点不为空，就把右节点加入到辅助栈中
            if (curNode.right != null)
                stack.add(curNode.right)

            // 交换当前结点的左右结点
            val tmp = curNode.left
            curNode.left = curNode.right
            curNode.right = tmp
        }

        // 返回root，此时已经完成镜像
        return root
    }
}
```

### 3.3 复杂度分析

* 时间复杂度`O(N)`：其中N为二叉树的结点数量，建立二叉树镜像需要遍历树的所有结点，占用`O(N)`时间。
* 空间复杂度`O(N)`：当处于最差情况下，即该二叉树为满二叉树时，辅助栈最多同时存储`N/2`个节点，占用`O(N)`额外空间。

## 4. 参考

* [https://leetcode-cn.com/problems/er-cha-shu-de-jing-xiang-lcof/](https://leetcode-cn.com/problems/er-cha-shu-de-jing-xiang-lcof/)
* [https://leetcode-cn.com/problems/er-cha-shu-de-jing-xiang-lcof/solution/mian-shi-ti-27-er-cha-shu-de-jing-xiang-di-gui-fu-/](https://leetcode-cn.com/problems/er-cha-shu-de-jing-xiang-lcof/solution/mian-shi-ti-27-er-cha-shu-de-jing-xiang-di-gui-fu-/)

