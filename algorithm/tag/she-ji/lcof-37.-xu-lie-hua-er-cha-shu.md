# LCOF 37. 序列化二叉树

## 1. [问题](https://leetcode-cn.com/problems/xu-lie-hua-er-cha-shu-lcof/)

请实现两个函数，分别用来序列化和反序列化二叉树。

示例：

```text
你可以将以下二叉树：

    1
   / \
  2   3
     / \
    4   5

序列化为 "[1,2,3,null,null,4,5]"
```

## 2. 标签

* 树
* 设计
* 层序遍历
* 队列

## 3. 解法

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
public class Codec {

    // Encodes a tree to a single string.
    // 把树序列化为字符串
    public String serialize(TreeNode root) {
        // 判空
        if (root == null)
            return "[]";

        // 结果字符串
        StringBuilder ans = new StringBuilder("[");

        // 层序遍历需要使用队列 
        Queue<TreeNode> queue = new LinkedList<>();
        // 先把根结点放入队列
        queue.add(root);

        // 队列为空时停止循环
        while (!queue.isEmpty()) {
            // 取出队头结点作为当前结点
            TreeNode curNode = queue.poll();
            // 当前结点不为空就将其加入结果列表
            if (curNode != null) {
                ans.append(curNode.val + ",");
                // 并将当前结点的左右结点加入队列，等待下一层的遍历
                queue.add(curNode.left);
                queue.add(curNode.right);
            } else {
                // 当前结点为空时就加入 null
                ans.append("null,");
            }

            // 删除最后一个逗号
            ans.deleteCharAt(ans.length() - 1);
            // 加上中括号作为结尾
            ans.append("]");
        }

        // 返回结果
        return ans.toString();
    }

    // Decodes your encoded data to tree.
    // 把字符串反序列化为一棵树
    public TreeNode deserialize(String data) {
        // 判空
        if (data.equals("[]"))
            return null;

        // 从字符串中解析出所有的结点值
        String[] nodeValues = data.substring(1, data.length() - 1).split(",");

        // 使用 nodeValues 中的第一个值来创建树的根结点
        TreeNode root = new TreeNode(Integer.parseInt(nodeValues[0]));

         // 利用队列按层来构建二叉树
         Queue<TreeNode> queue = new LinkedList<>();
         // 先把刚刚构建的根结点放入队列
         queue.add(root);

        // 用于遍历 nodeValues 的索引
        int i = 1;

        // 队列为空时停止循环
        while (!queue.isEmpty()) {
            // 取出当前结点
            TreeNode curNode = queue.poll();

            // 判断 nodeValues 的当前值是否为空，不为空时就为当前结点 curNode 构建左右子树
            // 构建 curNode 的左子树
            if (!nodeValues[i].equals("null")) {
                curNode.left = new TreeNode(Integer.parseInt(nodeValues[i]));
                // 将当前结点的左结点放入队列，以进行再往下一层的构建
                queue.add(curNode.left);
            }
            // 这个索引自增千万别顺手放到上面的括号里了，nodeValues当前值为空的时候也需要对索引进行自增操作
            i++;

            // 构建 curNode 的右子树
            if (!nodeValues[i].equals("null")) {
                curNode.right = new TreeNode(Integer.parseInt(nodeValues[i]));
                // 将当前结点的右结点放入队列，以进行再往下一层的构建
                queue.add(curNode.right);
            }
            // 这个索引自增千万别顺手放到上面的括号里了，nodeValues当前值为空的时候也需要对索引进行自增操作
            i++;
        }

        return root;
    }
}

// Your Codec object will be instantiated and called as such:
// Codec codec = new Codec();
// codec.deserialize(codec.serialize(root));
```

### 3.2 复杂度分析

**序列化 `serialize`**

* 时间复杂度 `O(N)` ：N 为二叉树的结点数，层序遍历会按层访问到所有的结点。
* 空间复杂度 `O(N)` ：最差情况下，树为完全二叉树时，最多会有 `N/2` 个结点在 `queue` 中，需要占用 `O(N)` 大小的额外空间。

> 假设完全二叉树的层数为 k ，那么总结点数为 `2^(k-1)` ，叶子结点的个数为 `2^k - 1`。

**反序列化 `deserialize`**

* 时间复杂度 `O(N)` ：N 为二叉树的结点数，按层构建二叉树需要遍历 nodeValues，其长度最大为 `2N + 1` 。
  * _为啥 2N+1 \#TODO_
* 空间复杂度 `O(N)` ：最差情况下，树为完全二叉树时，最多会有 `N/2` 个结点在 `queue` 中，需要占用 `O(N)` 大小的额外空间。

## 4. 参考

* [https://leetcode-cn.com/problems/xu-lie-hua-er-cha-shu-lcof/](https://leetcode-cn.com/problems/xu-lie-hua-er-cha-shu-lcof/)
* [https://leetcode-cn.com/problems/xu-lie-hua-er-cha-shu-lcof/solution/mian-shi-ti-37-xu-lie-hua-er-cha-shu-ceng-xu-bian-/](https://leetcode-cn.com/problems/xu-lie-hua-er-cha-shu-lcof/solution/mian-shi-ti-37-xu-lie-hua-er-cha-shu-ceng-xu-bian-/)

