# LEETCODE 238. 除自身以外数组的乘积

## [1. 问题](https://leetcode-cn.com/problems/product-of-array-except-self/)

给你一个长度为 n 的整数数组 nums，其中 n > 1，返回输出数组 output ，其中 output\[i] 等于 nums 中除 nums\[i] 之外其余各元素的乘积。

**示例:**

> 输入: \[1,2,3,4] 输出: \[24,12,8,6]

**提示：** 题目数据保证数组之中任意元素的全部前缀元素和后缀（甚至是整个数组）的乘积都在 32 位整数范围内。

**说明:** 请不要使用除法，且在 O(n) 时间复杂度内完成此题。

**进阶：** 你可以在常数空间复杂度内完成这个题目吗？（ 出于对空间复杂度分析的目的，输出数组不被视为额外空间。） 

## 2. 解法 - 左右乘积列表

### 2.1 Java

```java
class Solution {
    public int[] productExceptSelf(int[] nums) {
        // 结果数组
        int[] output = new int[nums.length];

        // 【从左往右】第一轮循环，存前缀之积
        // 【最左边的数】的前缀之积为1
        output[0] = 1;
        for(int i=1;i<nums.length;i++) {
            // 前缀之积 = 前一个数 * 前一个数的前缀之积
            output[i] = nums[i-1] * output[i-1];
        }

        // 初始化一个整型变量R，用于存后缀之积。【最右边的数】的后缀之积为1
        int R = 1;
        // 【从右往左】第二轮循环，将output里的数与后缀之积相乘，并同时更新R
        for(int i=nums.length-1;i>=0;i--) {
            output[i] *= R;
            R *= nums[i];
        }

        return output;
    }
}
```

### 2.2 Kotlin

```java
class Solution {
    fun productExceptSelf(nums: IntArray): IntArray {
        // 结果数组
        var output = IntArray(nums.size)

        // 【从左往右】第一轮循环，存前缀之积
        // 【最左边的数】的前缀之积为1
        output[0] = 1
        for(i in 1 until nums.size) {
            // 前缀之积 = 前一个数 * 前一个数的前缀之积
            output[i] = nums[i-1] * output[i-1]
        }

        // 初始化一个整型变量R，用于存后缀之积。【最右边的数】的后缀之积为1
        var R = 1
        // 【从右往左】第二轮循环，将output里的数与后缀之积相乘，并同时更新R                
        for(i in nums.size-1 downTo 0) {
            output[i] *= R
            R *= nums[i]
        }

        return output
    }
}
```

## 3. 参考

* [力扣：238. 除自身以外数组的乘积](https://leetcode-cn.com/problems/product-of-array-except-self)
* [力扣官方题解：除自身以外数组的乘积](https://leetcode-cn.com/problems/product-of-array-except-self/solution/chu-zi-shen-yi-wai-shu-zu-de-cheng-ji-by-leetcode-/)

## 4. 学习草稿

![](https://777blog.oss-cn-shanghai.aliyuncs.com/blog%20pic/IMG\_4303.JPG) \*忘记写了，为什么第一个数的前缀之积是1，最后一个数的后缀之积是1呢？首先看第一个数，第一个数的output应该是前缀之积✖️后缀之积，而后缀之积很明显是后面所有数字的乘积，同时output也是后面所有数字的乘积，所以前缀之积就是1。后缀之积同理！
