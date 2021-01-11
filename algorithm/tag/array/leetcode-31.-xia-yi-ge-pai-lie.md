# \*LEETCODE 31. 下一个排列

## 1. [问题](https://leetcode-cn.com/problems/next-permutation/)

实现获取 下一个排列 的函数，算法需要将给定数字序列重新排列成字典序中下一个更大的排列。

如果不存在下一个更大的排列，则将数字重新排列成最小的排列（即升序排列）。

必须 原地 修改，只允许使用额外常数空间。

示例 1：

```text
输入：nums = [1,2,3]
输出：[1,3,2]
```

示例 2：

```text
输入：nums = [3,2,1]
输出：[1,2,3]
```

示例 3：

```text
输入：nums = [1,1,5]
输出：[1,5,1]
```

示例 4：

```text
输入：nums = [1]
输出：[1]
```

**提示：**

* `1 <= nums.length <= 100`
* `0 <= nums[i] <= 100`

## 2. 标签

* 数组

## 3. 解法

### 3.1 Java

```java

```

### 3.2 复杂度分析

* 时间复杂度 `O(N)` ：其中 N 为给定序列的长度。我们至多只需要扫描两次序列，以及进行一次反转操作。
* 空间复杂度 `O(1)` ：变量仅占用了常数大小的存储空间。

## 4. 参考

* [https://leetcode-cn.com/problems/next-permutation/](https://leetcode-cn.com/problems/next-permutation/)
* [https://leetcode-cn.com/problems/next-permutation/solution/xia-yi-ge-pai-lie-by-leetcode-solution/](https://leetcode-cn.com/problems/next-permutation/solution/xia-yi-ge-pai-lie-by-leetcode-solution/)

