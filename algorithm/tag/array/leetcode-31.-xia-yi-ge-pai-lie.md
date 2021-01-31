# LEETCODE 31. 下一个排列

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

## 3. 解法 - 两遍扫描

### 3.1 Java

```java
class Solution {
    /**
     * 下一个排列
     * @param nums
     * 
     * 注意到下一个排列总是比当前排列要大，除非该排列已经是最大的排列。
     * 希望能够找到一个大于当前序列的新序列，且变大的幅度尽可能小。
     *  1. 将左边的较小数和右边的较大数交换，以使当前排列变大
     *  2. 要让较小数尽量靠右，而较大数尽可能小。
     *  3. 交换完成后，较大数右边的数需要按照升序重新排列，这样可以保证变大的幅度尽可能小。
     */
    public void nextPermutation(int[] nums) {
        /**
         * 首先从后向前查找第一个顺序对(i,i+1)。满足 nums[i] < nums[i+1]。
         * 这样较小数就是 nums[i]，此时[i+1,n)一定为降序
         * 
         * 这里是为了满足较小数尽量靠右。
         */
        int i = nums.length - 2;
        while (i >= 0 && nums[i] >= nums[i + 1]) {
            i--;
        }

        /**
         * 找到顺序对后，就在 [i+1,n) 中从后向前查找第一个元素 j 
         * 满足 nums[i] < nums[j]。这样较大数即为 nums[j]。
         * 
         * 由于[i+1,n)为降序，所以这样子是为了使较大数尽可能小。
         */
        if (i >= 0) {
            int j = nums.length - 1;
            while (j >= 0 && nums[i] >= nums[j]) {
                j--;
            }
            // 找到了 i 和 j 之后，交换二者。
            swap(nums, i, j);
        }
        // 按照升序重新排列较大数右边的数，这样可以保证变大的幅度尽可能小。
        reverse(nums, i + 1);
    }

    /**
     * 交换 nums 数组中下标为 i 和 j 的数字
     * @param nums
     * @param i
     * @param j
     */
    public void swap(int[] nums, int i, int j) {
        int temp = nums[i];
        nums[i] = nums[j];
        nums[j] = temp;
    }

    /**
     * 翻转 nums 数组指定区间的数字
     * @param nums
     * @param start 起始位置
     */
    public void reverse(int[] nums, int start) {
        int left = start, right = nums.length - 1;
        while (left < right) {
            swap(nums, left, right);
            left++;
            right--;
        }
    }
}
```

### 3.2 复杂度分析

* 时间复杂度 `O(N)` ：其中 N 为给定序列的长度。我们至多只需要扫描两次序列，以及进行一次反转操作。
* 空间复杂度 `O(1)` ：变量仅占用了常数大小的存储空间。

## 4. 参考

* [https://leetcode-cn.com/problems/next-permutation/](https://leetcode-cn.com/problems/next-permutation/)
* [https://leetcode-cn.com/problems/next-permutation/solution/xia-yi-ge-pai-lie-by-leetcode-solution/](https://leetcode-cn.com/problems/next-permutation/solution/xia-yi-ge-pai-lie-by-leetcode-solution/)

