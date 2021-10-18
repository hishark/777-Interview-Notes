# 36. 二叉搜索树与双向链表【DFS】

## 1. [问题](https://leetcode-cn.com/problems/er-cha-sou-suo-shu-yu-shuang-xiang-lian-biao-lcof)

输入一棵二叉搜索树，将该二叉搜索树转换成一个**排序**的**循环双向链表**。要求不能创建任何新的节点，只能调整树中节点指针的指向。

为了让您更好地理解问题，以下面的二叉搜索树为例：

![](<../../.gitbook/assets/image (4).png>)

我们希望将这个二叉搜索树转化为双向循环链表。链表中的每个节点都有一个前驱和后继指针。对于双向循环链表，第一个节点的前驱是最后一个节点，最后一个节点的后继是第一个节点。

下图展示了上面的二叉搜索树转化成的链表。“head” 表示指向链表中有最小元素的节点。

![](<../../.gitbook/assets/image (5).png>)

特别地，我们希望可以就地完成转换操作。当转化完成以后，树中节点的左指针需要指向前驱，树中节点的右指针需要指向后继。还需要返回链表中的第一个节点的指针。

## 2. 标签

* 链表
* 分治
* 二叉搜索树

## 3. 解法 - DFS

### 3.1 Java

> 中序遍历二叉搜索树，可以得到一个递增序列。

```java
/*
// Definition for a Node.
class Node {
    public int val;
    public Node left;
    public Node right;

    public Node() {}

    public Node(int _val) {
        val = _val;
    }

    public Node(int _val,Node _left,Node _right) {
        val = _val;
        left = _left;
        right = _right;
    }
};
*/
class Solution {

    // 假设当前遍历结点为 cur，那么 pre 是 cur 的前一个结点
    // head 为头结点
    Node pre, head;

    public Node treeToDoublyList(Node root) {
        // 判空
        if (root== null)
            return null;

        // 中序遍历访问树的各个结点，同时在遍历过程中连接前后结点
        dfs(root);

        // 构建头尾结点的引用指向
        // dfs 结束时，head 指向链表中的头结点，pre 指向尾结点，互相指向即可
        head.left = pre;
        pre.right = head;
        
        return head;
    }

    // 中序遍历二叉搜索树，可以得到一个递增序列
    public void dfs(Node cur) {
        // 递归出口
        if (cur == null)
            return;

        // 中序遍历：左，根，右
        // 左左左
        dfs(cur.left);

        // 根根根
        // 若 pre 为空，说明正在访问链表头结点，记为 head
        if (pre == null) 
            head = cur;
        else// 若 pre 不为空，将 pre 和 cur 分两步双向连接即可
            pre.right = cur; // step1

        // step2
        cur.left = pre;

        // 调整 pre 的指向
        // ***别漏了这一步
        pre = cur;

        // 右右右
        dfs(cur.right);
    }
}
```

### 3.2 复杂度分析

* 时间复杂度 `O(N)` ：N 是二叉树的结点数，中序遍历需要访问所有结点。
* 空间复杂度 `O(N)` ：在最差情况下，也就是当树退化为链表后，递归深度达到 N ，系统需要占用 `O(N)` 大小的栈空间。

## 5. 参考

* [https://leetcode-cn.com/problems/er-cha-sou-suo-shu-yu-shuang-xiang-lian-biao-lcof/](https://leetcode-cn.com/problems/er-cha-sou-suo-shu-yu-shuang-xiang-lian-biao-lcof/)
* [https://leetcode-cn.com/problems/er-cha-sou-suo-shu-yu-shuang-xiang-lian-biao-lcof/solution/mian-shi-ti-36-er-cha-sou-suo-shu-yu-shuang-xian-5/](https://leetcode-cn.com/problems/er-cha-sou-suo-shu-yu-shuang-xiang-lian-biao-lcof/solution/mian-shi-ti-36-er-cha-sou-suo-shu-yu-shuang-xian-5/)
