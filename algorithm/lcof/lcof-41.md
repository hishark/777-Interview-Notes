# 41. 数据流中的中位数

## 1. [问题](https://leetcode-cn.com/problems/shu-ju-liu-zhong-de-zhong-wei-shu-lcof/)

如何得到一个数据流中的中位数？如果从数据流中读出奇数个数值，那么中位数就是所有数值排序之后位于中间的数值。如果从数据流中读出偶数个数值，那么中位数就是所有数值排序之后中间两个数的平均值。

例如，

\[2,3,4\] 的中位数是 3

\[2,3\] 的中位数是 \(2 + 3\) / 2 = 2.5

设计一个支持以下两种操作的数据结构：

void addNum\(int num\) - 从数据流中添加一个整数到数据结构中。 

double findMedian\(\) - 返回目前所有元素的中位数。 

**示例 1：**

```text
输入：
["MedianFinder","addNum","addNum","findMedian","addNum","findMedian"]
[[],[1],[2],[],[3],[]]
输出：[null,null,null,1.50000,null,2.00000]
```

**示例 2：**

```text
输入：
["MedianFinder","addNum","findMedian","addNum","findMedian"]
[[],[2],[],[3],[]]
输出：[null,null,2.00000,null,2.50000]
```

**限制：**

* 最多会对 `addNum、findMedian` 进行 `50000` 次调用。

## 2. 标签

* 堆
* 设计

## 3. 解法

### 3.1 Java

```java
class MedianFinder {
    // 使用一个小顶堆和一个大顶堆来分别保存较大的一半和较小的一半
    PriorityQueue<Integer> minHeap, maxHeap;

    /** initialize your data structure here. */
    public MedianFinder() {
        // PriorityQueue 默认为小顶堆
        // minHeap 为小顶堆。用于保存较大的一半数字
        minHeap = new PriorityQueue<>();
        // maxHeap 为大顶堆，需要重写 Comparator。用于保存较小的一半数字
        maxHeap = new PriorityQueue<>((x, y) -> (y - x));
        // 重写 Comparator 完整的写法：
        // maxHeap = new PriorityQueue<Integer>(new Comparator<Integer>() {
        //     public int compare(Integer x, Integer y) {
        //         return y - x;
        //     }
        // });
    }
    
    public void addNum(int num) {
        // 需要保持两个堆的平衡，最大堆的大小要始终等于最小堆的大小，或者等于最小堆的大小 + 1
        // 首先向最大堆中插入元素
        maxHeap.offer(num);
        // 最大堆中插入完，就从最大堆中取出最大的元素，插入最小堆中
        minHeap.offer(maxHeap.poll());
        // 此时如果两个堆不平衡，就把最小堆的元素放到最大堆里去
        if (minHeap.size() > maxHeap.size()) 
            maxHeap.offer(minHeap.poll());
    }
    
    public double findMedian() {
        // 如果两个堆的大小相等，就取出两个堆的堆顶元素求平均值
        if (maxHeap.size() == minHeap.size()) 
            return (maxHeap.peek() + minHeap.peek()) * 0.5;
        // 若两个堆的大小不相等，直接取出最大堆的堆顶元素即可
        return maxHeap.peek();
    }
}

/**
 * Your MedianFinder object will be instantiated and called as such:
 * MedianFinder obj = new MedianFinder();
 * obj.addNum(num);
 * double param_2 = obj.findMedian();
 */
```

### 3.2 Kotlin

```kotlin
class MedianFinder {
    // 使用一个小顶堆和一个大顶堆来分别保存较大的一半和较小的一半
    var minHeap: PriorityQueue<Int>
    var maxHeap: PriorityQueue<Int>

    /** initialize your data structure here.  */
    init {
        // PriorityQueue 默认为小顶堆
        // minHeap 为小顶堆。用于保存较大的一半数字
        minHeap = PriorityQueue()
        // maxHeap 为大顶堆，需要重写 Comparator。用于保存较小的一半数字
        maxHeap = PriorityQueue { x, y -> y!! - x!! }
    }

    fun addNum(num: Int) {
        // 需要保持两个堆的平衡，最大堆的大小要始终等于最小堆的大小，或者等于最小堆的大小 + 1
        // 首先向最大堆中插入元素
        maxHeap.offer(num)
        // 最大堆中插入完，就从最大堆中取出最大的元素，插入最小堆中
        minHeap.offer(maxHeap.poll())
        // 此时如果两个堆不平衡，就把最小堆的元素放到最大堆里去
        if (minHeap.size > maxHeap.size)
            maxHeap.offer(minHeap.poll())
    }

    fun findMedian(): Double {
        // 若两个堆的大小相等，就取出两个堆的堆顶元素求平均值
        // 若两个堆的大小不相等，直接取出最大堆的堆顶元素即可
        return if (maxHeap.size == minHeap.size) (maxHeap.peek() + minHeap.peek()) * 0.5 else maxHeap.peek().toDouble()
        
    }
}

/**
 * Your MedianFinder object will be instantiated and called as such:
 * var obj = MedianFinder()
 * obj.addNum(num)
 * var param_2 = obj.findMedian()
 */
```

### 3.3 复杂度分析

* 时间复杂度：获取堆顶元素 `O(1)` ，堆的插入和弹出使用 `O(logN)` 。
* 空间复杂度 `O(N)` ：其中 N 为数据流中的元素个数，小顶堆和大顶堆最多同时保存 N 个元素。

## 4. 参考

* [https://leetcode-cn.com/problems/shu-ju-liu-zhong-de-zhong-wei-shu-lcof/](https://leetcode-cn.com/problems/shu-ju-liu-zhong-de-zhong-wei-shu-lcof/)
* [https://leetcode-cn.com/problems/shu-ju-liu-zhong-de-zhong-wei-shu-lcof/solution/mian-shi-ti-41-shu-ju-liu-zhong-de-zhong-wei-shu-y/](https://leetcode-cn.com/problems/shu-ju-liu-zhong-de-zhong-wei-shu-lcof/solution/mian-shi-ti-41-shu-ju-liu-zhong-de-zhong-wei-shu-y/)
* [https://leetcode-cn.com/problems/shu-ju-liu-zhong-de-zhong-wei-shu-lcof/solution/you-xian-dui-lie-wu-fei-hua-jian-dan-yi-dong-by-je/](https://leetcode-cn.com/problems/shu-ju-liu-zhong-de-zhong-wei-shu-lcof/solution/you-xian-dui-lie-wu-fei-hua-jian-dan-yi-dong-by-je/)

