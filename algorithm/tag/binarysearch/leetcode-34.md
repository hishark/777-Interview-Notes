# LEETCODE 34. 在排序数组中查找元素的第一个和最后一个位置

## 1. [问题](https://leetcode-cn.com/problems/find-first-and-last-position-of-element-in-sorted-array/)

给定一个按照升序排列的整数数组 nums，和一个目标值 target。找出给定目标值在数组中的开始位置和结束位置。

你的算法时间复杂度必须是 O(log n) 级别。

如果数组中不存在目标值，返回 \[-1, -1]。

示例 1:

```
输入: nums = [5,7,7,8,8,10], target = 8
输出: [3,4]
```

示例 2:

```
输入: nums = [5,7,7,8,8,10], target = 6
输出: [-1,-1]
```

## 2. 标签

* 数组
* 二分查找

## 3. 解法 - 二分查找

### 3.1 Java

```java
class Solution {
    public int[] searchRange(int[] nums, int target) {
        int[] targetRange = {-1, -1};
        
        int leftIndex = getIndex(nums, target, true);
        
        // 如果越界了或者值对不上，就返回 -1 -1
        if (leftIndex == nums.length || nums[leftIndex] != target) {
            return targetRange;
        }

        //成功找到了左边界
        targetRange[0] = leftIndex;
        // 有左一定有右
        // -1 是因为 在 getIndex() 中 right 为 nums.length
        targetRange[1] = getIndex(nums, target, false) - 1;

        return targetRange;

    }

    /**
     * 返回左右索引值
     * @param nums 数组
     * @param target 目标值
     * @param flag flag为true时递归查询左区间，flag为false时递归查询右区间
     * @return
     */
    public int getIndex(int[] nums, int target, boolean flag) {
        int left = 0;
        int right = nums.length;
        
        while (left < right) {
            int mid = left + (right - left) / 2;
            if (nums[mid] > target || (flag && nums[mid] == target)) {
                right = mid;
            } else {
                left = mid + 1;
            }
        }

        return left;
    }

}
```

### 3.2 Kotlin

```kotlin
class Solution {
    fun searchRange(nums: IntArray, target: Int): IntArray {
        val targetRange = intArrayOf(-1, -1)

        val leftIndex = getIndex(nums, target, true)

        // 如果越界了或者值对不上，就返回 -1 -1
        if (leftIndex == nums.size || nums[leftIndex] != target) {
            return targetRange
        }

        //成功找到了左边界
        targetRange[0] = leftIndex
        // 有左一定有右
        // -1 是因为 在 getIndex() 中 right 为 nums.size
        targetRange[1] = getIndex(nums, target, false) - 1

        return targetRange

    }

    /**
     * 返回左右索引值
     * @param nums 数组
     * @param target 目标值
     * @param flag flag为true时递归查询左区间，flag为false时递归查询右区间
     * @return
     */
    fun getIndex(nums: IntArray, target: Int, flag: Boolean): Int {
        var left = 0
        var right = nums.size

        while (left < right) {
            val mid = left + (right - left) / 2
            if (nums[mid] > target || flag && nums[mid] == target) {
                right = mid
            } else {
                left = mid + 1
            }
        }

        return left
    }

}
```

### 3.3 复杂度分析

* 时间复杂度 `O(logn)` ：由于二分查找每次将搜索区间大约划分为两等分，所以至多有 $$\lceil \log_{2}n\rceil$$次迭代。二分查找的过程被调用了两次，所以总的时间复杂度是对数级别的。
* 空间复杂度 `O(1)` ：所有计算过程都是原地进行的。

## 4. 参考

* [https://leetcode-cn.com/problems/find-first-and-last-position-of-element-in-sorted-array/](https://leetcode-cn.com/problems/find-first-and-last-position-of-element-in-sorted-array/)
* [https://leetcode-cn.com/problems/find-first-and-last-position-of-element-in-sorted-array/solution/zai-pai-xu-shu-zu-zhong-cha-zhao-yuan-su-de-di-yi-/](https://leetcode-cn.com/problems/find-first-and-last-position-of-element-in-sorted-array/solution/zai-pai-xu-shu-zu-zhong-cha-zhao-yuan-su-de-di-yi-/)
