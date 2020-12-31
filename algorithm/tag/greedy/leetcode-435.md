# \*LEETCODE 435. 无重叠区间

## 1. [问题](https://leetcode-cn.com/problems/non-overlapping-intervals/)

给定一个区间的集合，找到需要移除区间的最小数量，使剩余区间互不重叠。

注意:

* 可以认为区间的终点总是大于它的起点。 
* 区间 \[1,2\] 和 \[2,3\] 的边界相互“接触”，但没有相互重叠。

**示例 1:**

```text
输入: [ [1,2], [2,3], [3,4], [1,3] ]
输出: 1
解释: 移除 [1,3] 后，剩下的区间没有重叠。
```

**示例 2:**

```text
输入: [ [1,2], [1,2], [1,2] ]
输出: 2
解释: 你需要移除两个 [1,2] 来使剩下的区间没有重叠。
```

**示例 3:**

```text
输入: [ [1,2], [2,3] ]
输出: 0
解释: 你不需要移除任何区间，因为它们已经是无重叠的了。
```

## 2. 标签

* 贪心
* 动态规划

## 3. 解法 - 贪心

### 3.1 Java

```java
class Solution {
    public int eraseOverlapIntervals(int[][] intervals) {
        // 判空
        if (intervals.length == 0) {
            return 0;
        }
        // 按照右端点的大小，从小到大对区间排序
        Arrays.sort(intervals, new Comparator<int[]>() {
            public int compare(int[] interval1, int[] interval2) {
                return interval1[1] - interval2[1];
            }
        });

        // 区间的个数
        int n = intervals.length;
        // 最前面的区间的右端点
        int right = intervals[0][1];
        // 
        int ans = 1;
        // 遍历剩下的区间
        for (int i = 1; i < n; ++i) {
            // 如果【当前区间的左端点】在【前一个区间的右端点】之后
            // 那么就说明找到了一个不重合的且右端点最小的区间
            if (intervals[i][0] >= right) {
                ans++;
                // 保存当前区间的右端点，给下一次循环使用
                right = intervals[i][1];
            }
        }
        // 【区间总数】减去【不重叠的区间总数】就是【需要移除区间的最小数量】
        return n - ans;
    }
}
```

### 3.2 复杂度分析

* 时间复杂度 `O(nlogn)` ：其中 n 是区间的数量。我们需要 O\(nlogn\) 的时间对所有的区间按照右端点进行升序排序，并且需要 O\(n\) 的时间进行遍历。由于前者在渐进意义下大于后者，因此总时间复杂度为  O\(nlogn\)。
* 空间复杂度 `O(logn)` ：排序需要使用的栈空间。

## 4. 解法 - 动态规划

> 时间复杂度不咋地，先不看。

### 4.1 Java

```java

```

### 4.2 复杂度分析

* 时间复杂度 `O()` ：
* 空间复杂度 `O()` ：

## 5. 参考

* [https://leetcode-cn.com/problems/non-overlapping-intervals/](https://leetcode-cn.com/problems/non-overlapping-intervals/)
* [https://leetcode-cn.com/problems/non-overlapping-intervals/solution/wu-zhong-die-qu-jian-by-leetcode-solutio-cpsb/](https://leetcode-cn.com/problems/non-overlapping-intervals/solution/wu-zhong-die-qu-jian-by-leetcode-solutio-cpsb/)

