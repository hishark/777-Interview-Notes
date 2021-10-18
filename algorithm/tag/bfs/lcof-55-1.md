# LCOF 55 - I. 二叉树的深度

## 1. [问题](https://leetcode-cn.com/problems/er-cha-shu-de-shen-du-lcof/)

输入一棵二叉树的根节点，求该树的深度。从根节点到叶节点依次经过的节点（含根、叶节点）形成树的一条路径，最长路径的长度为树的深度。

例如：

给定二叉树 `[3,9,20,null,null,15,7]`，

```
    3
   / \
  9  20
    /  \
   15   7
```

返回它的最大深度 3 。

**提示：**

* `节点总数 <= 10000`

## 2. 标签

* 树
* DFS
* BFS

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
// dfs
class Solution {
    public int maxDepth(TreeNode root) {
        if(root == null)
            return 0;
        return Math.max(maxDepth(root.left), maxDepth(root.right)) + 1;
    }
}
```

### 3.2 Kotlin

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
    fun maxDepth(root: TreeNode?): Int {
        return if (root == null) 0 else Math.max(maxDepth(root.left), maxDepth(root.right)) + 1
    }
}
```

### 3.3 复杂度分析

* 时间复杂度 `O(N)` ：N 为树的结点数量，计算树的深度需要遍历到所有的结点。
* 空间复杂度 `O(N)` ：最差情况下，当树退化为链表，递归的深度会达到 N。

## 4. 解法 - BFS

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
// bfs
class Solution {
    public int maxDepth(TreeNode root) {
        // 判空
        if (root == null)
            return 0;

        // 使用队列存储节点
        Queue<TreeNode> queue = new LinkedList<>();

        // 初始化，先令根节点入队
        queue.offer(root);

        // 二叉树深度，最后要返回的结果
        int depth = 0;

        while (!queue.isEmpty()) {
            // 当前层次的节点数目
            int curSize = queue.size();
            // 遍历当前层次的所有节点，并将他们的子节点都入队
            int i = 0;
            while (i < curSize) {
                TreeNode curNode = queue.poll();
                // 左右子树存在的话就将其入队
                if (curNode.left != null)
                    queue.offer(curNode.left);
                if (curNode.right != null)
                    queue.offer(curNode.right);
                i++;
            }
            // 遍历完一个层次，就将深度++
            depth++;

        }

        return depth;
    }
}
```

### 4.2 Kotlin

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
    fun maxDepth(root: TreeNode?): Int {
        // 判空
        if (root == null)
            return 0

        // 使用队列存储节点
        val queue = LinkedList<TreeNode>()

        // 初始化，先令根节点入队
        queue.offer(root)

        // 二叉树深度，最后要返回的结果
        var depth = 0

        while (!queue.isEmpty()) {
            // 当前层次的节点数目
            val curSize = queue.size
            // 遍历当前层次的所有节点，并将他们的子节点都入队
            var i = 0
            while (i < curSize) {
                val curNode = queue.poll()
                // 左右子树存在的话就将其入队
                if (curNode.left != null)
                    queue.offer(curNode.left)
                if (curNode.right != null)
                    queue.offer(curNode.right)
                i++
            }
            // 遍历完一个层次，就将深度++
            depth++

        }

        return depth
    }
}
```

### 4.3 复杂度分析

* 时间复杂度 `O(N)` ：N 为树的结点数量，计算树的深度需要遍历到所有结点。
* 空间复杂度 `O(N)`：最差情况下，树为满二叉树时，最多会有 `N/2` 个结点在 `queue` 中，需要占用 `O(N)` 大小的额外空间。

> 假设满二叉树的层数为 k ，那么总结点数为 $$2^k-1$$ ，叶子结点的个数为 $$2^{k-1}$$ 。

## 5. 参考

* [https://leetcode-cn.com/problems/er-cha-shu-de-shen-du-lcof/](https://leetcode-cn.com/problems/er-cha-shu-de-shen-du-lcof/)
* [https://leetcode-cn.com/problems/er-cha-shu-de-shen-du-lcof/solution/mian-shi-ti-55-i-er-cha-shu-de-shen-du-xian-xu-bia/](https://leetcode-cn.com/problems/er-cha-shu-de-shen-du-lcof/solution/mian-shi-ti-55-i-er-cha-shu-de-shen-du-xian-xu-bia/)
