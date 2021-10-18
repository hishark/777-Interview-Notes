# LCOF 32 - II. 从上到下打印二叉树 II

## 1. [问题](https://leetcode-cn.com/problems/cong-shang-dao-xia-da-yin-er-cha-shu-ii-lcof/)

从上到下按层打印二叉树，同一层的节点按从左到右的顺序打印，每一层打印到一行。

例如: 给定二叉树: `[3,9,20,null,null,15,7]`,

```
    3
   / \
  9  20
    /  \
   15   7
```

返回其层次遍历结果：

```
[
  [3],
  [9,20],
  [15,7]
]
```

提示：

* 节点总数 <= 1000

## 2. 解法

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
    public List<List<Integer>> levelOrder(TreeNode root) {
        // 判空
        if (root == null)
            return new ArrayList<>();

        // BFS 需要使用队列存储遍历结点
        Queue<TreeNode> queue = new LinkedList<>();
        // 首先把根结点放入队列
        queue.offer(root);
        // 最终的遍历结果
        List<List<Integer>> resList = new ArrayList<>();

        // 队列为空时停止循环
        while (!queue.isEmpty()) {
            // 记录下队列此时的长度，用于
            int curSize = queue.size();
            // 工具人 i
            int i = 0;
            // 当前层次的遍历结果
            List<Integer> curList = new ArrayList<>();
            // 对此时队列中的所有结点依次进行判断
            while (i < curSize) {
                // 取出队头结点作为当前结点
                TreeNode curNode = queue.poll();
                // 把当前结点加入当前层次的遍历结果数组
                curList.add(curNode.val);

                // 判断当前结点的左右结点是否为空
                // 如果不为空，就把节点加入到队列中，用于之后的遍历
                if(curNode.left != null)
                    queue.offer(curNode.left);
                if(curNode.right != null)
                    queue.offer(curNode.right);

                // 工具人自增
                i++;
            }

            // 把当前层次的遍历结果放入最终结果中，继续下一层的遍历
            resList.add(curList);
        }

        // 返回即可
        return resList;
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
    fun levelOrder(root: TreeNode?): List<List<Int>> {
        // 判空
        if (root == null)
            return ArrayList()

        // BFS 需要使用队列存储遍历结点
        val queue = LinkedList<TreeNode>()
        // 首先把根结点放入队列
        queue.offer(root)
        // 最终的遍历结果
        val resList = ArrayList<List<Int>>()

        // 队列为空时停止循环
        while (!queue.isEmpty()) {
            // 记录下队列此时的长度，用于
            val curSize = queue.size
            // 工具人 i
            var i = 0
            // 当前层次的遍历结果
            val curList = ArrayList<Int>()
            // 对此时队列中的所有结点依次进行判断
            while (i < curSize) {
                // 取出队头结点作为当前结点
                val curNode = queue.poll()
                // 把当前结点加入当前层次的遍历结果数组
                curList.add(curNode.`val`)

                // 判断当前结点的左右结点是否为空
                // 如果不为空，就把节点加入到队列中，用于之后的遍历
                if (curNode.left != null)
                    queue.offer(curNode.left)
                if (curNode.right != null)
                    queue.offer(curNode.right)

                // 工具人自增
                i++
            }

            // 把当前层次的遍历结果放入最终结果中，继续下一层的遍历
            resList.add(curList)
        }

        // 返回即可
        return resList
    }
}
```

### 2.3 复杂度分析

* 时间复杂度 `O(N)`： N 是二叉树的结点数，BFS 需要循环 N 次。
* 空间复杂度 `O(N)`： 最差的情况下，即树为平衡二叉树时，最多有 `N/2` 个结点同时在 `queue` 中，需要使用 `O(N)` 大小的额外空间。

> 平衡树(Balance Tree，BT) 指的是，任意节点的子树的高度差都小于等于1。

## 3. 参考

* [https://leetcode-cn.com/problems/cong-shang-dao-xia-da-yin-er-cha-shu-ii-lcof/](https://leetcode-cn.com/problems/cong-shang-dao-xia-da-yin-er-cha-shu-ii-lcof/)
* [https://leetcode-cn.com/problems/cong-shang-dao-xia-da-yin-er-cha-shu-ii-lcof/solution/mian-shi-ti-32-ii-cong-shang-dao-xia-da-yin-er-c-5/](https://leetcode-cn.com/problems/cong-shang-dao-xia-da-yin-er-cha-shu-ii-lcof/solution/mian-shi-ti-32-ii-cong-shang-dao-xia-da-yin-er-c-5/)

## 4. 标签

* BFS
* 树
