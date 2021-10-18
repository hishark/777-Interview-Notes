# 53 - I. 在排序数组中查找数字 I【二分查找】

## 1. [问题](https://leetcode-cn.com/problems/zai-pai-xu-shu-zu-zhong-cha-zhao-shu-zi-lcof/)

统计一个数字在排序数组中出现的次数。

示例 1：

```
输入: nums = [5,7,7,8,8,10], target = 8
输出: 2
```

示例 2：

```
输入: nums = [5,7,7,8,8,10], target = 6
输出: 0
```

限制：

* `0 <= 数组长度 <= 50000`

## 2. 标签

* 数组
* 二分查找

## 3. 解法 - 二分查找

> 本题要求统计数字 `target` 的出现次数，可转化为：使用二分法分别找到 左边界 `left` 和 右边界`right` ，易得数字 `target` 的数量为 `right - left - 1`。

### 3.1 Java

```java
class Solution {
    public int search(int[] nums, int target) {
        // 二分查找的左右边界
        int left = 0;
        int right = nums.length - 1;

        // target不一定只有一个，所以需要查找target的右边界
        while (left <= right) {
            int mid = left + (right - left) / 2;
            //这里是“小于等于”，目的是为了确定右边界
            //当nums[mid]等于target时
            //因为不确定右边还有没有target，所以需要收缩左边界，去右边再继续查找
            if (nums[mid] <= target)
                left = mid + 1;
            else
                right = mid - 1;
        }

        // target的右边界
        // numRight指向了最后一个target的下一个位置
        int numRight = left;

        // 二分查找的左右边界
        left = 0;
        right = nums.length - 1;

        // target不一定只有一个，所以需要查找target的左边界
        while (left <= right) {
            int mid = left + (right - left) / 2;
            // 这里是“大于等于”，目的是确定左边界
            // 当nums[mid]等于target时
            // 因为不确定左边还有没有target，所以需要收缩右边界，去左边再继续查找
            if (nums[mid] >= target)
                right = mid - 1;
            else
                left = mid + 1; 
        }

        // target的左边界
        int numLeft = right;

        // target的左右边界相减即可得到target的出现次数
        return numRight - numLeft - 1;
    }
}
```

### 3.2 Kotlin

```kotlin
class Solution {
    fun search(nums: IntArray, target: Int): Int {
        // 二分查找的左右边界
        var left = 0
        var right = nums.size - 1

        // target不一定只有一个，所以需要查找target的右边界
        while (left <= right) {
            val mid = left + (right - left) / 2
            if (nums[mid] <= target)
                left = mid + 1
            else
                right = mid - 1
        }

        // target的右边界
        val numRight = left

        // 二分查找的左右边界
        left = 0
        right = nums.size - 1

        // target不一定只有一个，所以需要查找target的左边界
        while (left <= right) {
            val mid = left + (right - left) / 2
            if (nums[mid] < target)
                left = mid + 1
            else
                right = mid - 1
        }

        // target的左边界
        val numLeft = right

        // target的左右边界相减即可得到target的出现次数
        return numRight - numLeft - 1
    }
}
```

### 3.3 复杂度分析

* 时间复杂度 `O(logN)` ：二分查找的时间复杂度为对数级别。
* 空间复杂度 `O(1)` ：几个变量，只占用常数大小的额外空间。

## 4. 参考

* [https://leetcode-cn.com/problems/zai-pai-xu-shu-zu-zhong-cha-zhao-shu-zi-lcof/](https://leetcode-cn.com/problems/zai-pai-xu-shu-zu-zhong-cha-zhao-shu-zi-lcof/)
* [https://leetcode-cn.com/problems/zai-pai-xu-shu-zu-zhong-cha-zhao-shu-zi-lcof/solution/mian-shi-ti-53-i-zai-pai-xu-shu-zu-zhong-cha-zha-5/](https://leetcode-cn.com/problems/zai-pai-xu-shu-zu-zhong-cha-zhao-shu-zi-lcof/solution/mian-shi-ti-53-i-zai-pai-xu-shu-zu-zhong-cha-zha-5/)
