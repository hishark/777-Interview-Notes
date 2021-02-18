# 53 - II. 0～n-1中缺失的数字【二分查找/位运算】

## 1. [问题](https://leetcode-cn.com/problems/que-shi-de-shu-zi-lcof/)

一个长度为 n - 1 的递增排序数组中的所有数字都是唯一的，并且每个数字都在范围 0 ～ n - 1 之内。在范围0 ～ n - 1 内的 n 个数字中有且只有一个数字不在该数组中，请找出这个数字。

**示例 1:**

```text
输入: [0,1,3]
输出: 2
```

**示例 2:**

```text
输入: [0,1,2,3,4,5,6,7,9]
输出: 8
```

**限制：**

* `1 <= 数组长度 <= 10000`

## 2. 标签

* 数组
* 二分查找
* 位运算

## 3. 解法 - 二分查找

### 3.1 Java

```java
class Solution {
    public int missingNumber(int[] nums) {
        // 数组最左端
        int left = 0;
        // 数组最右端
        int right = nums.length - 1;
        
        /**
         * 由题意，数组可以分为两部分：
         *  左子数组中每个 nums[i] = i
         *  右子数组中每个 nums[i] != i
         * 
         * 所以题目中想求的就是「右子数组的首位元素」对应的索引
         * 此处采用二分法来查找该元素
         */
        while (left<=right) {
            // 中点
            int mid = left + (right - left) / 2;

            if (nums[mid] == mid) {
                // 此时，「右子数组的首位元素」一定处于[mid + 1, right]中
                // 所以接下来应该开始搜索当前元素的右边
                left = mid + 1;
            } else {
                // 此时，「左子数组的末位元素」一定处于[left, mid - 1]中
                // 所以接下来应该开始搜索当前元素的左边
                right = mid - 1;
            }
        }
        // 跳出循环时，left 和 right 分别指向 “右子数组的首位元素” 和 “左子数组的末位元素” 
        // 返回 left 即可
        return left;
    }
}
```

### 3.2 Kotlin

```kotlin
class Solution {
    fun missingNumber(nums: IntArray): Int {
        // 数组最左端
        var left = 0
        // 数组最右端
        var right = nums.size - 1

        /**
         * 由题意，数组可以分为两部分：
         * 左子数组中每个 nums[i] = i
         * 右子数组中每个 nums[i] != i
         *
         * 所以题目中想求的就是「右子数组的首位元素」对应的索引
         * 此处采用二分法来查找该元素
         */
        while (left <= right) {
            // 中点
            val mid = left + (right - left) / 2

            if (nums[mid] == mid) {
                // 此时，「右子数组的首位元素」一定处于[mid + 1, right]中
                // 所以接下来应该开始搜索当前元素的右边
                left = mid + 1
            } else {
                // 此时，「左子数组的末位元素」一定处于[left, mid - 1]中
                // 所以接下来应该开始搜索当前元素的左边
                right = mid - 1
            }
        }
        // 跳出循环时，left 和 right 分别指向 “右子数组的首位元素” 和 “左子数组的末位元素” 
        // 返回 left 即可
        return left
    }
}
```

### 3.3 复杂度分析

* 时间复杂度 `O(logN)` ：二分查找的时间复杂度为对数级别。
* 空间复杂度 `O(1)` ：只使用了常数大小的存储空间。

## 4. 解法 - 位运算

> 异或运算：
>
> A ^ A = 0
>
> A ^ 0 = A
>
> 这个方法有点妙。

### 4.1 Java

```java
class Solution {
    public int missingNumber(int[] nums) {
        // 数组长度
        int n = nums.length;
        // 由于缺了一个数字，所以数组中一定会出现 n 这个数
        // 先设缺失的数字为 n
        int miss = n;

        for(int i=0;i<n;i++) {
            // 异或：a^a=0,a^0=a
            // i ^ nums[i]: 未缺失的数字和它对应的下标先全部抵消掉
            // miss设为n就是为了和n抵消
            // 最后只剩下了一个下标，就是缺失的那个数字的下标，即缺失的数字（缺失的数字本身和它的下标是一样的！）
            miss ^= (i ^ nums[i]);
        }
        return miss;
    }
}
```

### 4.2 复杂度分析

* 时间复杂度：O\(N\)
* 空间复杂度：O\(1\)

## 4. 参考

* [https://leetcode-cn.com/problems/que-shi-de-shu-zi-lcof/](https://leetcode-cn.com/problems/que-shi-de-shu-zi-lcof/)
* [https://leetcode-cn.com/problems/que-shi-de-shu-zi-lcof/solution/mian-shi-ti-53-ii-0n-1zhong-que-shi-de-shu-zi-er-f/](https://leetcode-cn.com/problems/que-shi-de-shu-zi-lcof/solution/mian-shi-ti-53-ii-0n-1zhong-que-shi-de-shu-zi-er-f/)

