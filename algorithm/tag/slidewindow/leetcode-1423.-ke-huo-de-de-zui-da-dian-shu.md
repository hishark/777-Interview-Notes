# LEETCODE 1423. 可获得的最大点数

## 1. [问题](https://leetcode-cn.com/problems/maximum-points-you-can-obtain-from-cards/)

几张卡牌 排成一行，每张卡牌都有一个对应的点数。点数由整数数组 cardPoints 给出。

每次行动，你可以从行的开头或者末尾拿一张卡牌，最终你必须正好拿 k 张卡牌。

你的点数就是你拿到手中的所有卡牌的点数之和。

给你一个整数数组 cardPoints 和整数 k，请你返回可以获得的最大点数。

示例 1：

```text
输入：cardPoints = [1,2,3,4,5,6,1], k = 3
输出：12
解释：第一次行动，不管拿哪张牌，你的点数总是 1 。但是，先拿最右边的卡牌将会最大化你的可获得点数。最优策略是拿右边的三张牌，最终点数为 1 + 6 + 5 = 12 。
```

示例 2：

```text
输入：cardPoints = [2,2,2], k = 2
输出：4
解释：无论你拿起哪两张卡牌，可获得的点数总是 4 。
```

示例 3：

```text
输入：cardPoints = [9,7,7,9,7,7,9], k = 7
输出：55
解释：你必须拿起所有卡牌，可以获得的点数为所有卡牌的点数之和。 
```

示例 4：

```text
输入：cardPoints = [1,1000,1], k = 1
输出：1
解释：你无法拿到中间那张卡牌，所以可以获得的最大点数为 1 。 
```

示例 5：

```text
输入：cardPoints = [1,79,80,1,1,1,200,1], k = 3
输出：202
```

## 2. 标签

* 数组
* 滑动窗口

## 3. 解法 - 滑动窗口

### 3.1 Java

```java
class Solution {
    public int maxScore(int[] cardPoints, int k) {
        // 数组长度
        int n = cardPoints.length;
        /**
         * 由于只能从开头和末尾拿 k 张牌，所以最后剩下的一定是连续的 n - k 张牌 
         * 可以通过求剩余卡牌点数之和的最小值，来求出拿走卡牌点数之和的最大值。
         * 
         * 滑动窗口的大小为 n - k 
         * 问题转换为：求滑动窗口内点数之和的最小值
         */
        int windowSize = n - k;

        // 滑动窗口当前的点数之和
        int curSum = 0;

        // 滑动窗口点数之和的初始值为前 n - k 个数字的点数之和
        for (int i = 0; i < windowSize; i++) {
            curSum += cardPoints[i];
        }

        // 滑动窗口点数之和的最小值
        int minSum = curSum;

        // 遍历数组，移动滑动窗口
        for (int i = windowSize; i < n; i++) {
            // 滑动窗口每向右移动一格
            // 增加从右侧进入窗口的数字 cardPoints[i]
            // 减少从左侧离开窗口的数字 cardPoints[i - windowSize]
            curSum += cardPoints[i] - cardPoints[i - windowSize];
            // 更新最小值
            minSum = Math.min(minSum, curSum);
        }
        // 拿走的卡牌数字之和最大值 = 数组之和 - 滑动窗口数字之和最小值
        return Arrays.stream(cardPoints).sum() - minSum;
    }
}
```

### 3.2 复杂度分析

* 时间复杂度 `O(n)` ：其中 n 是数组 cardPoints 的长度。
* 空间复杂度 `O(1)` ：仅占用了常数大小的存储空间。

## 4. 参考

* [https://leetcode-cn.com/problems/maximum-points-you-can-obtain-from-cards/](https://leetcode-cn.com/problems/maximum-points-you-can-obtain-from-cards/)
* [https://leetcode-cn.com/problems/maximum-points-you-can-obtain-from-cards/solution/ke-huo-de-de-zui-da-dian-shu-by-leetcode-7je9/](https://leetcode-cn.com/problems/maximum-points-you-can-obtain-from-cards/solution/ke-huo-de-de-zui-da-dian-shu-by-leetcode-7je9/)

