# LCOF 26. 树的子结构

## 1. [问题](https://leetcode-cn.com/problems/shu-de-zi-jie-gou-lcof/)

输入两棵二叉树A和B，判断B是不是A的子结构。\(约定空树不是任意一个树的子结构\)

B是A的子结构， 即 A中有出现和B相同的结构和节点值。

例如:

给定的树 A:

```text
     3
    / \
   4   5
  / \
 1   2
```

给定的树 B：

```text
   4 
  /
 1
```

返回 true，因为 B 与 A 的一个子树拥有相同的结构和节点值。

示例 1：

```text
输入：A = [1,2,3], B = [3,1]
输出：false
```

示例 2：

```text
输入：A = [3,4,5,1,2], B = [4,1]
输出：true
```

限制：

* 0 &lt;= 节点个数 &lt;= 10000

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
    /**
     * 
     * @param A
     * @param B
     * @return 判断B树是否是A树的子结构
     */
    public boolean isSubStructure(TreeNode A, TreeNode B) {
        /**
         * 特判：
         *  如果A为空树或者B为空树时，直接返回false
         */
        if (A == null || B == null)
            return false;

        /**
         * 判断B是否是A的子结构，需要判断：
         *  1. 以结点A为根节点的树是否包含树B recur(A, B)
         *  2. B树是否是A的左子树的子结构
         *  3. B树是否是A的右子树的子结构
         */
        return recur(A, B) || isSubStructure(A.left, B) || isSubStructure(A.right, B);
    }

    /**
     * 
     * @param A
     * @param B
     * @return 判断以结点A为根节点的树是否包括树B
     */
    boolean recur(TreeNode A, TreeNode B) {
        // 1. 当结点B为空，说明树B的遍历已经越过叶子结点，匹配完成，返回true
        if(B == null) 
            return true;

        // 2. 当结点A为空，说明树A的遍历已经越过叶子结点，此时说明至今未找到树B的子结构，匹配失败，返回false
        // 3. 当A和B的值不相等时，必然匹配失败，返回false
        if(A == null || A.val != B.val) 
            return false;

        // 以上三种情况都没发生，说明当前A和B结点的值相同，匹配成功，可以继续匹配下一个，接着遍历左右子树即可
        return recur(A.left, B.left) && recur(A.right, B.right);
    }
}
```

### 2.2 Kotlin

```kotlin
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 * int val;
 * TreeNode left;
 * TreeNode right;
 * TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    /**
     *
     * @param A
     * @param B
     * @return 判断B树是否是A树的子结构
     */
    fun isSubStructure(A: TreeNode?, B: TreeNode?): Boolean {
        /**
         * 特判：
         * 如果A为空树或者B为空树时，直接返回false
         */
        return if (A == null || B == null) false else recur(A, B) || isSubStructure(
            A.left,
            B
        ) || isSubStructure(A.right, B)

        /**
         * 判断B是否是A的子结构，需要判断：
         * 1. 以结点A为根节点的树是否包含树B recur(A, B)
         * 2. B树是否是A的左子树的子结构
         * 3. B树是否是A的右子树的子结构
         */
    }

    /**
     *
     * @param A
     * @param B
     * @return 判断以结点A为根节点的树是否包括树B
     */
    fun recur(A: TreeNode?, B: TreeNode?): Boolean {
        // 1. 当结点B为空，说明树B的遍历已经越过叶子结点，匹配完成，返回true
        if (B == null)
            return true

        // 2. 当结点A为空，说明树A的遍历已经越过叶子结点，此时说明至今未找到树B的子结构，匹配失败，返回false
        // 3. 当A和B的值不相等时，必然匹配失败，返回false
        return if (A == null || A.`val` !== B!!.`val`) false else recur(A.left, B.left) && recur(A.right, B.right)

        // 以上三种情况都没发生，说明当前A和B结点的值相同，匹配成功，可以继续匹配下一个，接着遍历左右子树即可
    }
}
```

### 2.3 复杂度分析

* 时间复杂度：`O(mn)`。其中m和n分别是A树和B树的结点数量，先序遍历树A占用O\(m\)，每次调用`recur(A, B)`判断占用O\(n\)。
* 空间复杂度：`O(m)`。当A树和B树都退化为链表时，递归的调用深度达到最大。m&lt;=n时，遍历A树和递归判断的总递归深度为m，当m&gt;n时，最差情况为遍历到A树的叶子结点，此时的总递归深度为m。

## 3. 参考

* [https://leetcode-cn.com/problems/shu-de-zi-jie-gou-lcof/](https://leetcode-cn.com/problems/shu-de-zi-jie-gou-lcof/)
* [https://leetcode-cn.com/problems/shu-de-zi-jie-gou-lcof/solution/mian-shi-ti-26-shu-de-zi-jie-gou-xian-xu-bian-li-p/](https://leetcode-cn.com/problems/shu-de-zi-jie-gou-lcof/solution/mian-shi-ti-26-shu-de-zi-jie-gou-xian-xu-bian-li-p/)

