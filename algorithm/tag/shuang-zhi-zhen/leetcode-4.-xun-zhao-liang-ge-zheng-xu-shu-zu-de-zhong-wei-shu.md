# leetcode-4.-xun-zhao-liang-ge-zheng-xu-shu-zu-de-zhong-wei-shu

## 1. [问题](https://leetcode-cn.com/problems/median-of-two-sorted-arrays/)

给定两个大小为 m 和 n 的正序（从小到大）数组 nums1 和 nums2。请你找出并返回这两个正序数组的中位数。

进阶：你能设计一个时间复杂度为 O\(log \(m+n\)\) 的算法解决此问题吗？

**示例 1：**

```text
输入：nums1 = [1,3], nums2 = [2]
输出：2.00000
解释：合并数组 = [1,2,3] ，中位数 2
```

**示例 2：**

```text
输入：nums1 = [1,2], nums2 = [3,4]
输出：2.50000
解释：合并数组 = [1,2,3,4] ，中位数 (2 + 3) / 2 = 2.5
```

**示例 3：**

```text
输入：nums1 = [0,0], nums2 = [0,0]
输出：0.00000
```

**示例 4：**

```text
输入：nums1 = [], nums2 = [1]
输出：1.00000
```

**示例 5：**

```text
输入：nums1 = [2], nums2 = []
输出：2.00000
```

提示：

* nums1.length == m 
* nums2.length == n 
* 0 &lt;= m &lt;= 1000 
* 0 &lt;= n &lt;= 1000 
* 1 &lt;= m + n &lt;= 2000
*  -10^6 &lt;= nums1\[i\], nums2\[i\] &lt;= 10^6

## 2. 标签

* 数组
* 二分查找
* 分治算法
* 双指针

## 3. 解法 - 双指针

### 3.1 Java

```java
class Solution {
    public double findMedianSortedArrays(int[] nums1, int[] nums2) {
        /**
         * 只需要找到中位数的位置即可
         */

        // 两个数组的长度
        int m = nums1.length;
        int n = nums2.length;

        // 两个数组的总长度
        int len = m + n;

        /**
         * 判断中位数时需要对数组长度的奇偶情况进行分类
         *  1. 如果是奇数，要知道第 (len+1)/2 个数，共需要遍历 int(len/2)+1 次
         *  2. 如果是偶数，要知道第 len/2 个数和第 len/2+1个数，共需要遍历 len/2+1 次
         * 所以遍历的话，奇偶情况都是 len/2+1 次
         * 
         * 返回中位数的话：
         *  1. 奇数需要最后一次遍历的结果
         *  2. 偶数需要最后一次和上一次遍历的结果
         * 
         * 所以这里使用两个变量：
         *  1. cur 保存当前循环的结果
         *  2. pre 保存上一次循环的结果
         */
        int pre = -1;
        int cur = -1;

        // 双指针，分别指向两个数组
        int mPointer = 0;
        int nPointer = 0;

        for (int i=0;i<=len/2;i++) {
            // 更新 pre
            pre = cur;

            /**
             * 如果 mPointer < m && nums1[mPointer] < nums2[nPointer]，就可以右移
             * 如果 nPointer >= n 说明已经越界，就不需要执行 nums1[mPointer] < nums2[nPointer] 
             */

            if (mPointer < m && (nPointer >= n || nums1[mPointer] < nums2[nPointer])) {
                // 如果 nums1[mPointer] < nums2[nPointer]，那么 nums1 数组的指针右移
                cur = nums1[mPointer++];
            } else {
                // 如果 nums1[mPointer] >= nums2[nPointer]，那么 nums2 数组的指针右移
                // 总而言之是数字更小的那一个数组的指针进行右移
                cur = nums2[nPointer++];
            }

        }

        /**
         * 位运算判断奇偶：
         *  1. n&1=0 说明 n 为偶数
         *  2. n&1=1 说明 n 为奇数
         * 
         * 这里：
         *  1. 如果len为偶数，将最后一次和上一次遍历的结果求平均数即可
         *  2. 如果len为奇数，直接返回最后一次遍历的结果即可
         */
        if ((len & 1) == 0)
            return (pre + cur) / 2.0; // 记得是 2.0 不是 2
        else
            return cur;
    }
}
```

### 3.2 Kotlin

```kotlin
class Solution {
    fun findMedianSortedArrays(nums1: IntArray, nums2: IntArray): Double {
        /**
         * 只需要找到中位数的位置即可
         */

        // 两个数组的长度
        val m = nums1.size
        val n = nums2.size

        // 两个数组的总长度
        val len = m + n

        /**
         * 判断中位数时需要对数组长度的奇偶情况进行分类
         * 1. 如果是奇数，要知道第 (len+1)/2 个数，共需要遍历 int(len/2)+1 次
         * 2. 如果是偶数，要知道第 len/2 个数和第 len/2+1个数，共需要遍历 len/2+1 次
         * 所以遍历的话，奇偶情况都是 len/2+1 次
         *
         * 返回中位数的话：
         * 1. 奇数需要最后一次遍历的结果
         * 2. 偶数需要最后一次和上一次遍历的结果
         *
         * 所以这里使用两个变量：
         * 1. cur 保存当前循环的结果
         * 2. pre 保存上一次循环的结果
         */
        var pre = -1
        var cur = -1

        // 双指针，分别指向两个数组
        var mPointer = 0
        var nPointer = 0

        for (i in 0..len / 2) {
            // 更新 pre
            pre = cur

            /**
             * 如果 mPointer < m && nums1[mPointer] < nums2[nPointer]，就可以右移
             * 如果 nPointer >= n 说明已经越界，就不需要执行 nums1[mPointer] < nums2[nPointer]
             */

            if (mPointer < m && (nPointer >= n || nums1[mPointer] < nums2[nPointer])) {
                // 如果 nums1[mPointer] < nums2[nPointer]，那么 nums1 数组的指针右移
                cur = nums1[mPointer++]
            } else {
                // 如果 nums1[mPointer] >= nums2[nPointer]，那么 nums2 数组的指针右移
                // 总而言之是数字更小的那一个数组的指针进行右移
                cur = nums2[nPointer++]
            }

        }

        /**
         * 位运算判断奇偶：
         * 1. n&1=0 说明 n 为偶数
         * 2. n&1=1 说明 n 为奇数
         *
         * 这里：
         * 1. 如果len为偶数，将最后一次和上一次遍历的结果求平均数即可
         * 2. 如果len为奇数，直接返回最后一次遍历的结果即可
         */
        return if (len and 1 == 0)
            (pre + cur) / 2.0 // 记得是 2.0 不是 2
        else
            cur.toDouble()
    }
}
```

### 3.3 复杂度分析

* 时间复杂度 `O(m+n)` ：遍历 `len/2+1` 次，`len=m+n`，所以时间复杂度是 `O(m+n)`。
* 空间复杂度 `O(1)` ：几个变量仅占用常数大小的存储空间。

## 4. 解法 - 二分查找\#TODO

### 4.1 Java

```java

```

### 4.2 Kotlin

```kotlin

```

### 4.3 复杂度分析

* 时间复杂度 `O()` ：
* 空间复杂度 `O()` ：

## 5. 参考

* [https://leetcode-cn.com/problems/median-of-two-sorted-arrays/](https://leetcode-cn.com/problems/median-of-two-sorted-arrays/)
* [https://leetcode-cn.com/problems/median-of-two-sorted-arrays/solution/xun-zhao-liang-ge-you-xu-shu-zu-de-zhong-wei-s-114/](https://leetcode-cn.com/problems/median-of-two-sorted-arrays/solution/xun-zhao-liang-ge-you-xu-shu-zu-de-zhong-wei-s-114/)
* [https://leetcode-cn.com/problems/median-of-two-sorted-arrays/solution/xiang-xi-tong-su-de-si-lu-fen-xi-duo-jie-fa-by-w-2/](https://leetcode-cn.com/problems/median-of-two-sorted-arrays/solution/xiang-xi-tong-su-de-si-lu-fen-xi-duo-jie-fa-by-w-2/)

