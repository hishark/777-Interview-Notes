# LEETCODE 33. 搜索旋转排序数组

## 1. [问题](https://leetcode-cn.com/problems/search-in-rotated-sorted-array/)

给你一个整数数组 nums ，和一个整数 target 。

该整数数组原本是按升序排列，但输入时在预先未知的某个点上进行了旋转。（例如，数组 \[0,1,2,4,5,6,7] 可能变为 \[4,5,6,7,0,1,2] ）。

请你在数组中搜索 target ，如果数组中存在这个目标值，则返回它的索引，否则返回 -1 。

**示例 1：**

```
输入：nums = [4,5,6,7,0,1,2], target = 0
输出：4
```

**示例 2：**

```
输入：nums = [4,5,6,7,0,1,2], target = 3
输出：-1
```

**示例 3：**

```
输入：nums = [1], target = 0
输出：-1
```

提示：

* 1 <= nums.length <= 5000 
* \-10^4 <= nums\[i] <= 10^4 
* nums 中的每个值都 独一无二 
* nums 肯定会在某个点上旋转 
* \-10^4 <= target <= 10^4

## 2. 标签

* 数组
* 二分查找

## 3. 解法 - 二分查找

> 二分查找的等号我吐啦

### 3.1 Java

```java
// ref: https://leetcode-cn.com/problems/search-in-rotated-sorted-array/solution/sou-suo-xuan-zhuan-pai-xu-shu-zu-by-leetcode-solut/
class Solution {
    public int search(int[] nums, int target) {
        // 数组长度
        int len = nums.length;

        // 判空
        if (len == 0)
            return -1;

        // 边界情况
        if (len == 1)
            return nums[0] == target ? 0 : -1;

        // 二分查找时使用的两个指针
        int left = 0;
        int right = len - 1;

        while (left <= right) {
            // 找中点
            int mid = left + (right - left) / 2;

            // 找到了就直接返回
            if (nums[mid] == target)
                return mid;

            /**
             * 判断 mid 分割出来的两个部分：
             *  1. [left, mid]
             *  2. [mid+1, right]
             * 哪个部分是有序的
             */
            // 假设 mid = 6
            // [4,5,6,7,0,1,2] -> 左[4,5,6,7]  右[0,1,2]
            // 以上面这个数组为例
            // nums[mid] 和 nums[0]做比较主要是想判断 nums[mid] 处于旋转后的左还是右
            if (nums[0] <= nums[mid]) {
                // 如果 mid 处于左
                // 那么就在左边的数组进行二分查找
                if (nums[0] <= target && target < nums[mid]) {
                    right = mid - 1;
                } else {
                    left = mid + 1;
                }
            } else {
                // 如果 mid 处于右
                // 那么就在右边的数组进行二分查找
                if (nums[mid] < target && target <= nums[len - 1]) {
                    left = mid + 1;
                } else {
                    right = mid - 1;
                }

            }
        }
        // 找不到，返回 -1
        return -1;
    }
}
```

### 3.2 Kotlin

```kotlin
class Solution {
    fun search(nums: IntArray, target: Int): Int {
        // 数组长度
        val len = nums.size

        // 判空
        if (len == 0)
            return -1

        // 边界情况
        if (len == 1)
            return if (nums[0] == target) 0 else -1

        // 二分查找时使用的两个指针
        var left = 0
        var right = len - 1

        while (left <= right) {
            // 找中点
            val mid = left + (right - left) / 2

            // 找到了就直接返回
            if (nums[mid] == target)
                return mid

            /**
             * 判断 mid 分割出来的两个部分：
             * 1. [left, mid]
             * 2. [mid+1, right]
             * 哪个部分是有序的
             */
            // 假设 mid = 6
            // [4,5,6,7,0,1,2] -> 左[4,5,6,7]  右[0,1,2]
            // 以上面这个数组为例
            // nums[mid] 和 nums[0]做比较主要是想判断 nums[mid] 处于旋转后的左还是右
            if (nums[0] <= nums[mid]) {
                // 如果 mid 处于左
                // 那么就在左边的数组进行二分查找
                if (nums[0] <= target && target < nums[mid]) {
                    right = mid - 1
                } else {
                    left = mid + 1
                }
            } else {
                // 如果 mid 处于右
                // 那么就在右边的数组进行二分查找
                if (nums[mid] < target && target <= nums[len - 1]) {
                    left = mid + 1
                } else {
                    right = mid - 1
                }

            }
        }
        // 找不到，返回 -1
        return -1
    }
}
```

### 3.3 复杂度分析

* 时间复杂度 `O(logn)` ：搜索空间每次循环都会减少一半，二分查找的时间复杂度为对数级别。
* 空间复杂度 `O(1)` ：变量仅占用了常数大小的额外存储空间。

## 4. 参考

* [https://leetcode-cn.com/problems/search-in-rotated-sorted-array/](https://leetcode-cn.com/problems/search-in-rotated-sorted-array/)
* [https://leetcode-cn.com/problems/search-in-rotated-sorted-array/solution/sou-suo-xuan-zhuan-pai-xu-shu-zu-by-leetcode-solut/](https://leetcode-cn.com/problems/search-in-rotated-sorted-array/solution/sou-suo-xuan-zhuan-pai-xu-shu-zu-by-leetcode-solut/)
