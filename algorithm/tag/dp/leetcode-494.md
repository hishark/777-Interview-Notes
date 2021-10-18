# LEETCODE 494. 目标和

## 1. [问题](https://leetcode-cn.com/problems/target-sum/)

给定一个非负整数数组，a1, a2, ..., an, 和一个目标数，S。现在你有两个符号 + 和 -。对于数组中的任意一个整数，你都可以从 + 或 -中选择一个符号添加在前面。

返回可以使最终数组和为目标数 S 的所有添加符号的方法数。

示例：

```
输入：nums: [1, 1, 1, 1, 1], S: 3
输出：5
解释：

-1+1+1+1+1 = 3
+1-1+1+1+1 = 3
+1+1-1+1+1 = 3
+1+1+1-1+1 = 3
+1+1+1+1-1 = 3

一共有5种方法让最终目标和为3。
```

**提示：**

* 数组非空，且长度不会超过 20 。
* 初始的数组的和不会超过 1000 。
* 保证返回的最终结果能被 32 位整数存下。

## 2. 标签

* DFS
* 动态规划
* 背包问题

## 3. 解法 - 递归

### 3.1 Java

```java
public class Solution {
    // 方法数
    int count = 0;
    public int findTargetSumWays(int[] nums, int S) {
        // 递归搜索
        recur(nums, 0, 0, S);
        // 返回即可
        return count;
    }
    /**
     * 递归枚举出所有的情况
     * @param nums 数组
     * @param i 当前枚举的数字下标
     * @param sum 当前的和
     * @param S 目标和
     */
    public void recur(int[] nums, int i, int sum, int S) {
        // 如果已经枚举到了数组的最后一个数字
        if (i == nums.length) {
            // 判断此时的和是否等于目标和
            // 等于的话就方法数+1
            if (sum == S)
                count++;
        // 还未枚举到最后一个数字，继续递归
        } else {
            // 枚举下一个数字：i + 1
            // 更新当前的和：sum +/- nums[i]
            recur(nums, i + 1, sum + nums[i], S);
            recur(nums, i + 1, sum - nums[i], S);
        }
    }
}
```

### 3.2 复杂度分析

* 时间复杂度 `O(2^N)` ：其中 N 是数组 `nums` 的长度。
* 空间复杂度 `O(N)` ：递归使用的栈空间大小。

## 4. 解法 - 动态规划

> 常见背包问题。

### 4.1 Java

```java
public class Solution {
    public int findTargetSumWays(int[] nums, int S) {
        /**
         * 状态数组
         * dp[i][j]表示用数组中的前i个元素，组成和为j的方法数
         */
        int[][] dp = new int[nums.length][2001];

        // 边界条件，此时 j 为 0
        dp[0][nums[0] + 1000] = 1;
        dp[0][-nums[0] + 1000] += 1;
        
        /**
         * 状态转移方程：
         *  dp[i][j] = dp[i - 1][j - nums[i]] + dp[i - 1][j + nums[i]]
         * 写成递推的形式：
         *  dp[i][j + nums[i]] += dp[i - 1][j]
         *  dp[i][j - nums[i]] += dp[i - 1][j]
         * 
         * 由于题干中说到数组中所有数的和不超过1000，所以 j 的最小值可以达到 -1000
         * 由于数组下标不允许为负数，所以数字的第二维增加 1000
         *  dp[i][j + nums[i] + 1000] += dp[i - 1][j + 1000]
         *  dp[i][j - nums[i] + 1000] += dp[i - 1][j + 1000]
         */
        for (int i = 1; i < nums.length; i++) {
            for (int sum = -1000; sum <= 1000; sum++) {
                // 如果数组中的前 i-1 个元素组成和为 sum 的方法数大于 0
                if (dp[i - 1][sum + 1000] > 0) {
                    // 那么就可以计算出数组中的前 i 个元素组成和为 sum + nums[i] 的方法数
                    dp[i][sum + nums[i] + 1000] += dp[i - 1][sum + 1000];
                    dp[i][sum - nums[i] + 1000] += dp[i - 1][sum + 1000];
                }
            }
        }
        return S > 1000 ? 0 : dp[nums.length - 1][S + 1000];
    }
}
```

### 4.2 复杂度分析

* 时间复杂度 `O(N*sum)` ：其中 N 是数组 `nums` 的长度。
* 空间复杂度 `O(N*sum)` 

## 5. 参考

* [https://leetcode-cn.com/problems/target-sum/](https://leetcode-cn.com/problems/target-sum/)
* [https://leetcode-cn.com/problems/target-sum/solution/mu-biao-he-by-leetcode/](https://leetcode-cn.com/problems/target-sum/solution/mu-biao-he-by-leetcode/)
