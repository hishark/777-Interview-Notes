# LCOF 33. 二叉搜索树的后序遍历序列

## 1. [问题](https://leetcode-cn.com/problems/er-cha-sou-suo-shu-de-hou-xu-bian-li-xu-lie-lcof)

输入一个整数数组，判断该数组是不是某二叉搜索树的后序遍历结果。如果是则返回 true，否则返回 false。假设输入的数组的任意两个数字都互不相同。

参考以下这颗二叉搜索树：

```text
     5
    / \
   2   6
  / \
 1   3
```

示例 1：

```text
输入: [1,6,3,2,5]
输出: false
```

示例 2：

```text
输入: [1,3,2,6,5]
输出: true
```

提示：

* 数组长度 &lt;= 1000

## 2. 解法 - 分治 递归

> 一棵二叉搜索树是一棵有根二叉树并且对于所有结点满足特殊的性质：对于树中任意一个结点，它的权值必然大于等于所有左子树结点的权值，小于等于所有右子树结点的权值。
>
> 二叉搜索树的左、右子树也分别为二叉搜索树。

### 2.1 Java

```java
class Solution {
    public boolean verifyPostorder(int[] postorder) {
        return recursion(postorder, 0, postorder.length - 1);
    }

    // 判断后序遍历 postorder[i, j] 是否满足二叉搜索树的定义
    boolean recursion(int[] postorder, int i, int j) {
        // 递归终止条件，此时树种结点数量 <= 1，无需判断正确性，直接返回 true
        if (i >= j)
            return true;

        // 工具人 p，初始化为 i，用于找结点
        int p = i;

        /**
         * 根据后序遍历的特性，j 即根结点的位置
         * 此时需要找到第一个大于根结点的结点
         * 将位置记录为 m
         * 该位置用于划分左子树区间[i,m-1]和右子树区间[m,j-1]
         * 
         */
        while (postorder[p] < postorder[j])
            p++;
        int m = p;

        /**
         * 接下来判断是否为二叉搜索树
         * 1. 左子树区间[i,m-1]内所有的结点都应该小于根结点 postorder[j]
         *    在之前找 m 位置的时候其实已经保证了这一点，所以无需再次判断
         * 2. 右子树区间[m,j-1]内所有的结点都应该大于根结点 postorder[j]
         *    遍历[p,j]，遇到小于等于根结点就跳出。
         *    最后看 p 是否等于 j 来判断是否为二叉搜索树
         *      a) 若 p == j，则是二叉搜索树
         *      b) 若 p != j，则不是二叉搜索树
         */
        while (postorder[p] > postorder[j])
            p++;

        // 递归判断当前树的左子树和右子树是否满足二叉搜索树的定义
        return p == j && recursion(postorder, i, m - 1) && recursion(postorder, m, j - 1);
    }
}
```

### 2.2 Kotlin

```kotlin
class Solution {
    fun verifyPostorder(postorder: IntArray): Boolean {
        return recursion(postorder, 0, postorder.size - 1)
    }

    // 判断后序遍历 postorder[i, j] 是否满足二叉搜索树的定义
    fun recursion(postorder: IntArray, i: Int, j: Int): Boolean {
        // 递归终止条件，此时树种结点数量 <= 1，无需判断正确性，直接返回 true
        if (i >= j)
            return true

        // 工具人 p，初始化为 i，用于找结点
        var p = i

        /**
         * 根据后序遍历的特性，j 即根结点的位置
         * 此时需要找到第一个大于根结点的结点
         * 将位置记录为 m
         * 该位置用于划分左子树区间[i,m-1]和右子树区间[m,j-1]
         *
         */
        while (postorder[p] < postorder[j])
            p++
        val m = p

        /**
         * 接下来判断是否为二叉搜索树
         * 1. 左子树区间[i,m-1]内所有的结点都应该小于根结点 postorder[j]
         * 在之前找 m 位置的时候其实已经保证了这一点，所以无需再次判断
         * 2. 右子树区间[m,j-1]内所有的结点都应该大于根结点 postorder[j]
         * 遍历[p,j]，遇到小于等于根结点就跳出。
         * 最后看 p 是否等于 j 来判断是否为二叉搜索树
         * a) 若 p == j，则是二叉搜索树
         * b) 若 p != j，则不是二叉搜索树
         */
        while (postorder[p] > postorder[j])
            p++

        // 递归判断当前树的左子树和右子树是否满足二叉搜索树的定义
        return p == j && recursion(postorder, i, m - 1) && recursion(postorder, m, j - 1)
    }
}
```

### 2.3 复杂度分析

* 时间复杂度 `O(N^2)`：每次递归调用 `recursion` 就能揪出一个根节点，总共有 N 个结点，因此递归需要占用 `O(N)`。最差情况下，当树退化成为链表，每轮递归都需要遍历树种所有的结点，占用 `O(N)`。所以总的时间复杂度为 `O(N^2)`。
* 空间复杂度 `O(N)`：最差情况下，当树退化成为链表，递归深度将达到 N。

## 3. 参考

* [https://leetcode-cn.com/problems/er-cha-sou-suo-shu-de-hou-xu-bian-li-xu-lie-lcof](https://leetcode-cn.com/problems/er-cha-sou-suo-shu-de-hou-xu-bian-li-xu-lie-lcof)
* [https://leetcode-cn.com/problems/er-cha-sou-suo-shu-de-hou-xu-bian-li-xu-lie-lcof/solution/mian-shi-ti-33-er-cha-sou-suo-shu-de-hou-xu-bian-6/](https://leetcode-cn.com/problems/er-cha-sou-suo-shu-de-hou-xu-bian-li-xu-lie-lcof/solution/mian-shi-ti-33-er-cha-sou-suo-shu-de-hou-xu-bian-6/)

## 4. 标签

* 树
* 栈
* 分治
* 递归

