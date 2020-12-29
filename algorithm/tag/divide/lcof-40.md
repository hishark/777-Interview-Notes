# LCOF 40. 最小的k个数

## 1. [问题](https://leetcode-cn.com/problems/zui-xiao-de-kge-shu-lcof/)

输入整数数组 `arr` ，找出其中最小的 `k` 个数。例如，输入4、5、1、6、2、7、3、8这8个数字，则最小的4个数字是1、2、3、4。

示例1：

```text
输入：arr = [3,2,1], k = 2
输出：[1,2] 或者 [2,1]
```

示例2：

```text
输入：arr = [0,1,2,1], k = 1
输出：[0]
```

限制：

* `0 <= k <= arr.length <= 10000`
* `0 <= arr[i] <= 10000`

## 2. 标签

* 堆
* 分治

### 3. 解法 - 大根堆

### 3.1 Java

```java
class Solution {
    public int[] getLeastNumbers(int[] arr, int k) {
        // 数组中最小的 k 个数
        int[] ans = new int[k];

        // 判空
        if (k == 0)
            return ans;

        /**
         * Java中默认的为小根堆，实现大根堆需要重写一下 Comparator 题目要求前 k 小的数字，所以需要使用一个容量为 k 的大根堆
         * 
         * 遍历数组的时候，若堆的大小小于 k，就直接把数字放进去 若堆的大小已经为 k，需要判断当前数字和堆顶数字的大小： 1. 若当前数字 >=
         * 堆顶数字，那么这个数就直接跳过 2. 若当前数字 < 堆顶数字，那么就先把堆顶数字 poll 掉，然后把当前数字放入堆中
         * 
         */
        PriorityQueue<Integer> maxHeap = new PriorityQueue<Integer>(new Comparator<Integer>() {
            public int compare(Integer num1, Integer num2) {
                return num2 - num1;
            }
        });

        // 首先，先把数字的前 k 个数字全部怼入堆中
        for (int i = 0; i < k; i++) {
            maxHeap.offer(arr[i]);
        }

        // 接着继续遍历数组中剩下的数字
        for (int i = k; i < arr.length; i++) {
            // 如果「当前遍历的数字」 <「堆顶数字」
            if (maxHeap.peek() > arr[i]) {
                // 就把堆顶数字送出去
                maxHeap.poll();
                // 并把当前数字放入堆中
                maxHeap.offer(arr[i]);
            }
            // 如果「当前遍历的数字」 >=「堆顶数字」，直接跳过即可
        }

        // 此时，大根堆中已经存好了前 k 小的数字们，放入结果数组即可
        for (int i = 0; i < k; i++)
            ans[i] = maxHeap.poll();

        return ans;
    }
}
```

### 3.2 Kotlin

```kotlin
class Solution {
    fun getLeastNumbers(arr: IntArray, k: Int): IntArray {
        // 数组中最小的 k 个数
        val ans = IntArray(k)

        // 判空
        if (k == 0)
            return ans

        /**
         * Java中默认的为小根堆，实现大根堆需要重写一下 Comparator 题目要求前 k 小的数字，所以需要使用一个容量为 k 的大根堆
         *
         * 遍历数组的时候，若堆的大小小于 k，就直接把数字放进去 若堆的大小已经为 k，需要判断当前数字和堆顶数字的大小： 1. 若当前数字 >=
         * 堆顶数字，那么这个数就直接跳过 2. 若当前数字 < 堆顶数字，那么就先把堆顶数字 poll 掉，然后把当前数字放入堆中
         *
         */
        val maxHeap = PriorityQueue(Comparator<Int> { num1, num2 -> num2!! - num1!! })

        // 首先，先把数字的前 k 个数字全部怼入堆中
        for (i in 0 until k) {
            maxHeap.offer(arr[i])
        }

        // 接着继续遍历数组中剩下的数字
        for (i in k until arr.size) {
            // 如果「当前遍历的数字」 <「堆顶数字」
            if (maxHeap.peek() > arr[i]) {
                // 就把堆顶数字送出去
                maxHeap.poll()
                // 并把当前数字放入堆中
                maxHeap.offer(arr[i])
            }
            // 如果「当前遍历的数字」 >=「堆顶数字」，直接跳过即可
        }

        // 此时，大根堆中已经存好了前 k 小的数字们，放入结果数组即可
        for (i in 0 until k)
            ans[i] = maxHeap.poll()

        return ans
    }
}
```

### 3.3 复杂度分析

* 时间复杂度 `O(nlogk)` ：其中 n 是数组的长度。大根堆实时维护前 k 小的数字，插入删除操作都是 `O(logk)` 的时间复杂度，最坏情况下数组中所有的数字都要被插入堆中，所以总共是 `O(nlogk)` 的时间复杂度。
* 空间复杂度 `O(k)` ：大根堆的大小为 k 。

## 4. 参考

* [https://leetcode-cn.com/problems/zui-xiao-de-kge-shu-lcof/solution/](https://leetcode-cn.com/problems/zui-xiao-de-kge-shu-lcof/solution/)
* [https://leetcode-cn.com/problems/zui-xiao-de-kge-shu-lcof/solution/zui-xiao-de-kge-shu-by-leetcode-solution/](https://leetcode-cn.com/problems/zui-xiao-de-kge-shu-lcof/solution/zui-xiao-de-kge-shu-by-leetcode-solution/)
* [https://leetcode-cn.com/problems/zui-xiao-de-kge-shu-lcof/solution/3chong-jie-fa-miao-sha-topkkuai-pai-dui-er-cha-sou/](https://leetcode-cn.com/problems/zui-xiao-de-kge-shu-lcof/solution/3chong-jie-fa-miao-sha-topkkuai-pai-dui-er-cha-sou/)

