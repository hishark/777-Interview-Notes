# LEETCODE 239. 滑动窗口最大值

## 1. [问题](https://leetcode-cn.com/problems/sliding-window-maximum/)

给你一个整数数组 nums，有一个大小为 k 的滑动窗口从数组的最左侧移动到数组的最右侧。你只可以看到在滑动窗口内的 k 个数字。滑动窗口每次只向右移动一位。

返回滑动窗口中的最大值。

**示例 1：**

> 通过下面的解释可以明显看出，对于长度为 n 的数组 nums ，滑动窗口的数量为 `n−k+1`。

```text
输入：nums = [1,3,-1,-3,5,3,6,7], k = 3
输出：[3,3,5,5,6,7]
解释：
滑动窗口的位置                最大值
---------------               -----
[1  3  -1] -3  5  3  6  7       3
 1 [3  -1  -3] 5  3  6  7       3
 1  3 [-1  -3  5] 3  6  7       5
 1  3  -1 [-3  5  3] 6  7       5
 1  3  -1  -3 [5  3  6] 7       6
 1  3  -1  -3  5 [3  6  7]      7
```

**示例 2：**

```text
输入：nums = [1], k = 1
输出：[1]
```

**示例 3：**

```text
输入：nums = [1,-1], k = 1
输出：[1,-1]
```

**示例 4：**

```text
输入：nums = [9,11], k = 2
输出：[11]
```

**示例 5：**

```text
输入：nums = [4,-2], k = 2
输出：[4]
```

**提示：**

* `1 <= nums.length <= 105`
* `-104 <= nums[i] <= 104`
* `1 <= k <= nums.length`

## 2. 标签

* 堆
* 队列
* 滑动窗口

## 3. 解法 - 大根堆

> 还有一点糊涂 \#TODO

### 3.1 Java

```java
class Solution {
    public int[] maxSlidingWindow(int[] nums, int k) {
        // 数组大小
        int n = nums.length;
        // 大根堆
        PriorityQueue<int[]> pq = new PriorityQueue<int[]>(new Comparator<int[]>() {
            public int compare(int[] pair1, int[] pair2) {
                return pair1[0] != pair2[0] ? pair2[0] - pair1[0] : pair2[1] - pair1[1];
            }
        });
        // 为了方便判断堆顶元素与滑动窗口的位置关系
        // 可以在优先队列中存储二元组 (num,index)，表示元素 num 在数组中的下标为 index。
        // 先把数组中的前 k 个数字放入大根堆
        for (int i = 0; i < k; ++i) {
            pq.offer(new int[]{nums[i], i});
        }
        // 滑动窗口的最大值
        int[] ans = new int[n - k + 1];
        // 取出大根堆的堆顶元素，即第一个滑动窗口内的最大值
        ans[0] = pq.peek()[0];
        // 继续遍历余下的滑动窗口
        for (int i = k; i < n; i++) {
            // 继续把 (num, index) 放入大根堆
            pq.offer(new int[]{nums[i], i});
            // 查看此时的堆顶元素（即此时堆内的最大值）的下标 pq.peek()[1]
            // 把下标不在滑动窗口内的元素都删去
            while (pq.peek()[1] <= i - k) {
                pq.poll();
            }
            // 此时的堆顶元素即为当前滑动窗口的最大值
            ans[i - k + 1] = pq.peek()[0];
        }
        // 返回结果即可
        return ans;
    }
}
```

### 3.2 复杂度分析

* 时间复杂度 `O(nlogn)` ：其中 n 是数组 nums 的长度。在最坏情况下，数组 nums 中的元素单调递增，那么最终优先队列将会包含了所有元素，没有元素被移除。由于将一个元素放入优先队列的时间复杂度为 `O(logn)`，因此总时间复杂度为 `O(nlogn)`。
* 空间复杂度 `O(n)` ：即优先队列需要使用的空间。这里所有的空间复杂度分析都不考虑返回的答案所需要的 O\(n\) 空间，只计算额外的空间使用。

## 4. 参考

* [https://leetcode-cn.com/problems/sliding-window-maximum/](https://leetcode-cn.com/problems/sliding-window-maximum/)
* [https://leetcode-cn.com/problems/sliding-window-maximum/solution/hua-dong-chuang-kou-zui-da-zhi-by-leetco-ki6m/](https://leetcode-cn.com/problems/sliding-window-maximum/solution/hua-dong-chuang-kou-zui-da-zhi-by-leetco-ki6m/)

