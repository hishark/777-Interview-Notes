# LEETCODE 153. 寻找旋转排序数组中的最小值

## 1. [问题](https://leetcode-cn.com/problems/find-minimum-in-rotated-sorted-array/)

假设按照升序排序的数组在预先未知的某个点上进行了旋转。

( 例如，数组 \[0,1,2,4,5,6,7] 可能变为 \[4,5,6,7,0,1,2] )。

请找出其中最小的元素。

你可以假设数组中不存在重复元素。

示例 1:

```
输入: [3,4,5,1,2]
输出: 1
```

示例 2:

```
输入: [4,5,6,7,0,1,2]
输出: 0
```

## 2. 解法

### 2.1 Java

```java
class Solution {
    public int findMin(int[] nums) {
        // 如果只有一个数字就直接返回
        if (nums.length == 1)
            return nums[0];

        // 左右边界
        int left = 0;
        int right = nums.length - 1;

        // 如果第一个元素比最后一个元素小，说明没有旋转，直接返回第一个元素即可
        if (nums[left] < nums[right])
            return nums[0];

        // 二分查找
        while (left <= right) {

            // 中点
            int mid = left + (right - left) / 2;

            // 原数组为升序数组，所以一定满足nums[mid-1]<nums[mid]<nums[mid]+1，所以一旦出现矛盾，说明找到了【变化点】，也就找到了最小值
            // 注意一定要把nums[mid]和nums[mid+1]之间的比较放在前面，不然会出现越界异常
            //（比如只有两个元素的时候，mid=0，mid-1=-1，会造成越界）
            if (nums[mid] > nums[mid + 1])
                return nums[mid + 1];
            if (nums[mid - 1] > nums[mid])
                return nums[mid];

            // 【变化点】左边的元素都比nums[0]大，右边的元素都比nums[0]小
            // 比较nums[mid]和nums[0]的大小，以决定应该继续查找左区间还是右区间
            if (nums[mid] > nums[0]) {
                // nums[mid]更大，说明此时在【变化点】的左边，所以应该继续查找右区间
                left = mid + 1;
            } else {
                // 本题数组无重复元素，所以else里一定是nums[mid] < nums[0]
                // nums[mid]更小，说明此时在【变化点】的右边，所以应该继续查找左区间
                right = mid - 1;
            }

        }

        return -1;
    }
}
```

### 2.2 Kotlin

```kotlin
class Solution {
    fun findMin(nums: IntArray): Int {
        // 如果只有一个数字就直接返回
        if (nums.size == 1)
            return nums[0]

        // 左右边界
        var left = 0
        var right = nums.size - 1

        // 如果第一个元素比最后一个元素小，说明没有旋转，直接返回第一个元素即可
        if (nums[left] < nums[right])
            return nums[0]

        // 二分查找
        while (left <= right) {

            // 中点
            val mid = left + (right - left) / 2

            // 原数组为升序数组，所以一定满足nums[mid-1]<nums[mid]<nums[mid]+1，所以一旦出现矛盾，说明找到了【变化点】，也就找到了最小值
            // 注意一定要把nums[mid]和nums[mid+1]之间的比较放在前面，不然会出现越界异常
            //（比如只有两个元素的时候，mid=0，mid-1=-1，会造成越界）
            if (nums[mid] > nums[mid + 1])
                return nums[mid + 1]
            if (nums[mid - 1] > nums[mid])
                return nums[mid]

            // 【变化点】左边的元素都比nums[0]大，右边的元素都比nums[0]小
            // 比较nums[mid]和nums[0]的大小，以决定应该继续查找左区间还是右区间
            if (nums[mid] > nums[0]) {
                // nums[mid]更大，说明此时在【变化点】的左边，所以应该继续查找右区间
                left = mid + 1
            } else {
                // 本题数组无重复元素，所以else里一定是nums[mid] < nums[0]
                // nums[mid]更小，说明此时在【变化点】的右边，所以应该继续查找左区间
                right = mid - 1
            }

        }

        return -1
    }
}
```

## 3. 参考

* [https://leetcode-cn.com/problems/find-minimum-in-rotated-sorted-array/](https://leetcode-cn.com/problems/find-minimum-in-rotated-sorted-array/)
* [https://leetcode-cn.com/problems/find-minimum-in-rotated-sorted-array/solution/xun-zhao-xuan-zhuan-pai-lie-shu-zu-zhong-de-zui-xi/](https://leetcode-cn.com/problems/find-minimum-in-rotated-sorted-array/solution/xun-zhao-xuan-zhuan-pai-lie-shu-zu-zhong-de-zui-xi/)

## 4. 笔记

![](https://777blog.oss-cn-shanghai.aliyuncs.com/leetcode/leetcode-153-1.jpg) ![](https://777blog.oss-cn-shanghai.aliyuncs.com/leetcode/leetcode-153-2.jpg)
