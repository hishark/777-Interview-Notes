# LEETCODE 958. 二叉树的完全性检验

## 1. [问题](https://leetcode-cn.com/problems/check-completeness-of-a-binary-tree/)

给定一个二叉树，确定它是否是一个完全二叉树。

百度百科中对完全二叉树的定义如下：

若设二叉树的深度为 h，除第 h 层外，其它各层 (1～h-1) 的结点数都达到最大个数，第 h 层所有的结点都连续集中在最左边，这就是完全二叉树。（注：第 h 层可能包含 1\~ 2h 个节点。）

示例 1：

```
输入：[1,2,3,4,5,6] 
输出：true 
解释：最后一层前的每一层都是满的（即，结点值为 {1} 和 {2,3} 的两层），且最后一层中的所有结点（{4,5,6}）都尽可能地向左。 
```

示例 2：

```
输入：[1,2,3,4,5,null,7] 
输出：false 
解释：值为 7 的结点没有尽可能靠向左侧。
```

提示：

* 树中将会有 1 到 100 个结点。

## 2. 标签

* 二叉树
* 完全二叉树
* BFS

## 3. 解法

### 3.1 Java

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
  	// 判断一个树是否为完全二叉树，BFS判断下标即可。
    public boolean isCompleteTree(TreeNode root) {
      	// 新建一个List用来存储所有的结点
        List<ANode> nodes = new ArrayList();
      	// 从根节点开始层序遍历，这里因为需要获取到指定编码的结点，所以用list
        nodes.add(new ANode(root, 1));
      	// 初始化当前遍历的结点下标
        int i = 0;
      	// 列表不为0就一直找下去
        while (i < nodes.size()) {
          	// 获取当前遍历的结点，且让下标自增
            ANode anode = nodes.get(i++);
            // 这里要记得判断一下node是否存在，可能为空，为空的话显然没有左右孩子
            if (anode.node != null) {
                // 注意【2 * anode.code 别手快写成了 2 * i】
                nodes.add(new ANode(anode.node.left, anode.code * 2));
                nodes.add(new ANode(anode.node.right, anode.code * 2 + 1));
            }
        }
  
        // 整棵树都遍历完了之后，判断最后一个结点的编码是否等于列表的长度
        // 若等于，说明是一颗完全二叉树
        // 若不等于 说明不是一颗完全二叉树
        return nodes.get(i-1).code == nodes.size();
    }
}

// 自定义一个结点，node就是当前结点，code就是他的编码，根为1 左子树为2*1=2 右子树为2*1+1=3
// 同理推算剩下的所有子树
class ANode {  // Annotated Node
    TreeNode node;
    int code;
    ANode(TreeNode node, int code) {
        this.node = node;
        this.code = code;
    }
}
```

## 4. 参考

* [https://leetcode-cn.com/problems/check-completeness-of-a-binary-tree/solution/er-cha-shu-de-wan-quan-xing-jian-yan-by-leetcode/](https://leetcode-cn.com/problems/check-completeness-of-a-binary-tree/solution/er-cha-shu-de-wan-quan-xing-jian-yan-by-leetcode/)
