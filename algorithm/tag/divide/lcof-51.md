# LCOF 51. 数组中的逆序对

## 1. [问题](https://leetcode-cn.com/problems/shu-zu-zhong-de-ni-xu-dui-lcof/)

在数组中的两个数字，如果前面一个数字大于后面的数字，则这两个数字组成一个逆序对。输入一个数组，求出这个数组中的逆序对的总数。

**示例 1:**

```
输入: [7,5,6,4]
输出: 5
```

**限制：**

* `0 <= 数组长度 <= 50000`

## 2. 标签

* 归并排序
* 分治算法

## 3. 解法 - 归并排序

### 3.1 Java

```java
// 待琢磨
class Solution {
    public int reversePairs(int[] nums) {
        // 数组长度
        int length = nums.length;

        // 判空
        if (length < 2)
            return 0;

        // 复制一个数组
        int[] copy = new int[length];
        for (int i = 0; i < length; i++)
            copy[i] = nums[i];

        int[] temp = new int[length];
        return reversePairs(copy, 0, length - 1, temp);

    }

    // 计算逆序对数目并排序
    private int reversePairs(int[] nums, int left, int right, int[] temp) {
        // 判空
        if (left == right) {
            return 0;
        }

        // 中点
        int mid = left + (right - left) / 2;
        // nums[left, mid]中的逆序对
        int leftPairs = reversePairs(nums, left, mid, temp);
        // nums[mid+1, right]中的逆序对
        int rightPairs = reversePairs(nums, mid + 1, right, temp);

        // 左边数组的最后一个 比 右边数组的第一个 还要小
        // 说明两个数组之间没有逆序对，直接把两个分数组中的逆序对数目加起来即可
        if (nums[mid] <= nums[mid + 1]) {
            return leftPairs + rightPairs;
        }

        // 如果两个分数组中存在逆序对，归并排序并计算其逆序对的数目
        int crossPairs = mergeAndCount(nums, left, mid, right, temp);
        // 全部加到一起就是总的逆序对数目
        return leftPairs + rightPairs + crossPairs;
    }

    // nums[left, mid] 和 nums[mid+1, right]都是有序的
    // 归并排序的同时计算逆序对的数目
    private int mergeAndCount(int[] nums, int left, int mid, int right, int[] temp) {
        // 归并排序需要使用到一个临时数组
        for (int i = left; i <= right; i++) {
            temp[i] = nums[i];
        }

        // 指针 i 指向 nums[left, mid]
        int i = left;
        // 指针 j 指向 nums[mid+1, right]
        int j = mid + 1;

        // 逆序对的数目
        int count = 0;

        for (int k = left; k <= right; k++) {
            // 指针 i 遍历完了 nums[left, mid]
            // 接着遍历右边的数组
            if (i == mid + 1) {
                nums[k] = temp[j];
                j++;
                // 指针 j 遍历完了 nums[mid+1, right]
                // 接着遍历左边的数组
            } else if (j == right + 1) {
                nums[k] = temp[i];
                i++;
                // 不是逆序对，继续遍历
            } else if (temp[i] <= temp[j]) {
                nums[k] = temp[i];
                i++;
                // temp[i] > temp[j] 发现逆序对，计算逆序对的数目
            } else {
                nums[k] = temp[j];
                j++;
                count += (mid - i + 1);
            }
        }
        return count;
    }
}
```

### 3.2 Kotlin

```kotlin
// 待琢磨
class Solution {
    fun reversePairs(nums: IntArray): Int {
        // 数组长度
        val length = nums.size

        // 判空
        if (length < 2)
            return 0

        // 复制一个数组
        val copy = IntArray(length)
        for (i in 0 until length)
            copy[i] = nums[i]

        val temp = IntArray(length)
        return reversePairs(copy, 0, length - 1, temp)

    }

    // 计算逆序对数目并排序
    private fun reversePairs(nums: IntArray, left: Int, right: Int, temp: IntArray): Int {
        // 判空
        if (left == right) {
            return 0
        }

        // 中点
        val mid = left + (right - left) / 2
        // nums[left, mid]中的逆序对
        val leftPairs = reversePairs(nums, left, mid, temp)
        // nums[mid+1, right]中的逆序对
        val rightPairs = reversePairs(nums, mid + 1, right, temp)

        // 左边数组的最后一个 比 右边数组的第一个 还要小
        // 说明两个数组之间没有逆序对，直接把两个分数组中的逆序对数目加起来即可
        if (nums[mid] <= nums[mid + 1]) {
            return leftPairs + rightPairs
        }

        // 如果两个分数组中存在逆序对，归并排序并计算其逆序对的数目
        val crossPairs = mergeAndCount(nums, left, mid, right, temp)
        // 全部加到一起就是总的逆序对数目
        return leftPairs + rightPairs + crossPairs
    }

    // nums[left, mid] 和 nums[mid+1, right]都是有序的
    // 归并排序的同时计算逆序对的数目
    private fun mergeAndCount(nums: IntArray, left: Int, mid: Int, right: Int, temp: IntArray): Int {
        // 归并排序需要使用到一个临时数组
        for (i in left..right) {
            temp[i] = nums[i]
        }

        // 指针 i 指向 nums[left, mid]
        var i = left
        // 指针 j 指向 nums[mid+1, right]
        var j = mid + 1

        // 逆序对的数目
        var count = 0

        for (k in left..right) {
            // 指针 i 遍历完了 nums[left, mid]
            // 接着遍历右边的数组
            if (i == mid + 1) {
                nums[k] = temp[j]
                j++
                // 指针 j 遍历完了 nums[mid+1, right]
                // 接着遍历左边的数组
            } else if (j == right + 1) {
                nums[k] = temp[i]
                i++
                // 不是逆序对，继续遍历
            } else if (temp[i] <= temp[j]) {
                nums[k] = temp[i]
                i++
                // temp[i] > temp[j] 发现逆序对，计算逆序对的数目
            } else {
                nums[k] = temp[j]
                j++
                count += mid - i + 1
            }
        }
        return count
    }
}
```

### 3.3 复杂度分析

* 时间复杂度 `O(nlogn)` ：同归并排序。
* 空间复杂度 `O(n)` ：归并排序需要用到一个临时数组，占用 `O(n)` 大小的额外存储空间。

## 4. 参考

* [https://leetcode-cn.com/problems/shu-zu-zhong-de-ni-xu-dui-lcof/](https://leetcode-cn.com/problems/shu-zu-zhong-de-ni-xu-dui-lcof/)
* [https://leetcode-cn.com/problems/shu-zu-zhong-de-ni-xu-dui-lcof/solution/shu-zu-zhong-de-ni-xu-dui-by-leetcode-solution/](https://leetcode-cn.com/problems/shu-zu-zhong-de-ni-xu-dui-lcof/solution/shu-zu-zhong-de-ni-xu-dui-by-leetcode-solution/)
* [https://leetcode-cn.com/problems/shu-zu-zhong-de-ni-xu-dui-lcof/solution/bao-li-jie-fa-fen-zhi-si-xiang-shu-zhuang-shu-zu-b/](https://leetcode-cn.com/problems/shu-zu-zhong-de-ni-xu-dui-lcof/solution/bao-li-jie-fa-fen-zhi-si-xiang-shu-zhuang-shu-zu-b/)
