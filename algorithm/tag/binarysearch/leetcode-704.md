# LEETCODE 704. 二分查找

## 1. [问题](https://leetcode-cn.com/problems/binary-search/)

给定一个 n 个元素有序的（升序）整型数组 nums 和一个目标值 target ，写一个函数搜索 nums 中的 target，如果目标值存在返回下标，否则返回 -1。

示例 1:

```
输入: nums = [-1,0,3,5,9,12], target = 9
输出: 4
解释: 9 出现在 nums 中并且下标为 4
```

示例 2:

```
输入: nums = [-1,0,3,5,9,12], target = 2
输出: -1
解释: 2 不存在 nums 中因此返回 -1
```

提示：

1. 你可以假设 nums 中的所有元素是不重复的。 
2. n 将在 \[1, 10000]之间。 
3. nums 的每个元素都将在 \[-9999, 9999]之间。

## 2. 标签

* 二分查找

## 3. 解法

### 3.1 Java

```java
class Solution {
    public int search(int[] nums, int target) {
        // 目标值的下标
        int index = 0;
        // 左右边界
        int left = 0;
        int right = nums.length - 1;
        
        // 注意是小于等于
        while (left <= right) {
            index = left + (right - left) / 2;
            if (nums[index] == target)
                return index;
            else if (nums[index] > target)
                right = index - 1;
            else
                left = index + 1; 
        }
        // 没找到
        return -1;
    }
}
```

### 3.2 Kotlin

```kotlin
class Solution {
    fun search(nums: IntArray, target: Int): Int {
        // 目标值的下标
        var index = 0
        // 左右边界
        var left = 0
        var right = nums.size - 1

        // 注意是小于等于
        while (left <= right) {
            index = left + (right - left) / 2
            if (nums[index] == target)
                return index
            else if (nums[index] > target)
                right = index - 1
            else
                left = index + 1
        }
        // 没找到
        return -1
    }
}
```

### 3.3 复杂度分析

* 时间复杂度 `O(logn)` ：搜索空间每次循环都会减少一半，二分查找的时间复杂度为对数级别。
* 空间复杂度 `O(1)` ：变量仅占用了常数大小的额外存储空间。

## 4. 参考

* [https://leetcode-cn.com/problems/binary-search/](https://leetcode-cn.com/problems/binary-search/)
