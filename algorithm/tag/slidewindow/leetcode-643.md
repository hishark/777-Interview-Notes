# LEETCODE 643. 子数组最大平均数 I

## 1. [问题](https://leetcode-cn.com/problems/maximum-average-subarray-i/)

给定 `n` 个整数，找出平均数最大且长度为 `k` 的连续子数组，并输出该最大平均数。

**示例：**

```text
输入：[1,12,-5,-6,50,3], k = 4
输出：12.75
解释：最大平均数 (12-5-6+50)/4 = 51/4 = 12.75
```

**提示：**

* 1 &lt;= `k` &lt;= `n` &lt;= 30,000。
* 所给数据范围 \[-10,000，10,000\]。

## 2. 标签

* 数组
* 滑动窗口

## 3. 解法 - 滑动窗口

### 3.1 Java

```java
class Solution {
    public double findMaxAverage(int[] nums, int k) {
        // 滑动窗口中的数字总和
        int windoSum = 0;
        // 数组长度
        int n = nums.length;
        // 初始化窗口
        for (int i = 0; i < k; i++) {
            windoSum += nums[i];
        }
        // 初始化子数组最大和
        int maxSum = windoSum;
        // 遍历之后的数字，不停的向右滑动窗口
        for (int i = k; i < n; i++) {
            // 把老窗口的第一个数字删掉，再加上当前的数字，就形成了新的窗口
            windoSum = windoSum - nums[i - k] + nums[i];
            // 更新子数组最大和
            maxSum = Math.max(maxSum, windoSum);
        }
        // 除一下就是最大平均数
        // 别忘了 1.0，返回值类型是 double
        return 1.0 * maxSum / k;
    }
}
```

### 3.2 复杂度分析

* 时间复杂度 `O(n)` ：其中 n 是数组 nums 的长度。遍历数组一次。
* 空间复杂度 `O(1)` ：几个变量仅占用常数大小的存储空间。

## 4. 参考

* [https://leetcode-cn.com/problems/maximum-average-subarray-i/](https://leetcode-cn.com/problems/maximum-average-subarray-i/)
* [https://leetcode-cn.com/problems/maximum-average-subarray-i/solution/zi-shu-zu-zui-da-ping-jun-shu-i-by-leetc-us1k/](https://leetcode-cn.com/problems/maximum-average-subarray-i/solution/zi-shu-zu-zui-da-ping-jun-shu-i-by-leetc-us1k/)

