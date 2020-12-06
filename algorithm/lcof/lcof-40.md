# 40. 最小的k个数

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

## 3. 解法 - 大根堆

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
         * 遍历数组的时候，若堆的大小小于 k，就直接把数字放进去 若堆的大小已经为 k，需要判断当前数字和堆顶数字的大小： 
         *  1. 若当前数字 >= 堆顶数字，那么这个数就直接跳过 
         *  2. 若当前数字 < 堆顶数字，那么就先把堆顶数字 poll 掉，然后把当前数字放入堆中
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
            if (arr[i] < maxHeap.peek()) {
                // 就把堆顶数字送出去
                maxHeap.poll();
                // 并把当前数字放入堆中
                maxHeap.offer(arr[i]);
            }
            // 如果「当前遍历的数字」 >=「堆顶数字」，直接跳过即可
            // 总之就是不断送走k个数里最大的数字，剩下的就是k个最小的数了
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

## 4. 解法 - 快排

> 注意找前 K 大/前 K 小问题不需要对整个数组进行 O\(NlogN\) 的排序！ 例如本题，直接通过快排切分排好第 K 小的数（下标为 K-1），那么它左边的数就是比它小的另外 K-1 个数。

### 4.1 Java

```java
class Solution {
    public int[] getLeastNumbers(int[] arr, int k) {
        // 首先做一下判空
        if ((k == 0) || (arr.length == 0)) {
            return new int[0];
        }

        // 通过快排切分排好第 K 小的数（下标为 K-1），那么它左边的数就是比它小的另外 K-1 个数。
        // 最后一个参数表示我们要找的是下标为k-1的数
        return quickSort(arr, 0, arr.length - 1, k - 1);
    }

    // 快速排序
    private int[] quickSort(int[] nums, int left, int right, int k) {
        // 每切分1次，找到排序后下标为pivot的元素，
        int pivot = partition(nums, left, right);

        // 如果pivot恰好等于k就返回pivot以及pivot左边所有的数。（左边的数都比pivot小）
        if (pivot == k) {
            return Arrays.copyOf(nums, pivot + 1);
        }

        // 否则根据下标pivot与k的大小关系来决定继续切分左段还是右段。
        // pivot更大，说明k在pivot的左边，所以继续切分左边
        // pivot更小，说明k在pivot的右边，所以继续切分右边
        return (pivot > k) ? quickSort(nums, left, pivot - 1, k)
                           : quickSort(nums, pivot + 1, right, k);
    }

    public int partition(int[] arr, int left, int right) {
        //一般设置最左边的为基准数
        int pivotKey = arr[left];

        //基准数的位置
        int pivotPointer = left;

        //右指针找比基准数小的，左指针找比基准数大的，然后进行交换
        while (left < right) {
            // 先移动右指针，原因http://www.cnblogs.com/wxisme/p/5243631.html
            while ((left < right) && (arr[right] >= pivotKey)) {
                right--;
            }

            //↑右指针找到了第一个比基准数小的数，就停止循环，并把小的数移动到左边
            arr[left] = arr[right];

            while ((left < right) && (arr[left] <= pivotKey)) {
                left++;
            }

            //↑左指针找到了第一个比基准数大的数，就停止循环，并把大的数移动到右边
            arr[right] = arr[left];
        }

        //把基准值赋值给两个指针碰头的地方，也就是中间
        // 退出上面循环的时候，left=right
        arr[left] = pivotKey; //所以left换成right是一样的

        //把这个位置返回，以给下一次划分使用，划分左半边就-1，划分右半边就+1
        return left; //这里换成right也ok
    }
}
```

### 4.2 复杂度分析

> 关于复杂度：[https://leetcode-cn.com/problems/zui-xiao-de-kge-shu-lcof/solution/3chong-jie-fa-miao-sha-topkkuai-pai-dui-er-cha-sou/296015](https://leetcode-cn.com/problems/zui-xiao-de-kge-shu-lcof/solution/3chong-jie-fa-miao-sha-topkkuai-pai-dui-er-cha-sou/296015)

* 时间复杂度 `O(n^2)` ：期望为 O\(n\) ，最坏情况下，每次的划分点都是最大值或最小值，一共需要划分 n - 1 次，而一次划分需要线性的时间复杂度O\(n\)，所以最坏情况下时间复杂度为 O\(n^2\)。
* 空间复杂度 `O(n)` ：期望为 O\(logn\)，递归调用的期望深度为 O\(logn\)，每层需要的空间为 O\(1\)，只有常数个变量。最坏情况下需要划分 n 次，递归调用最深达到 n−1 层，而每层由于需要 O\(1\) 的空间，所以一共需要 O\(n\) 的空间复杂度。

## 5. 参考

* [https://leetcode-cn.com/problems/zui-xiao-de-kge-shu-lcof/solution/](https://leetcode-cn.com/problems/zui-xiao-de-kge-shu-lcof/solution/)
* [https://leetcode-cn.com/problems/zui-xiao-de-kge-shu-lcof/solution/zui-xiao-de-kge-shu-by-leetcode-solution/](https://leetcode-cn.com/problems/zui-xiao-de-kge-shu-lcof/solution/zui-xiao-de-kge-shu-by-leetcode-solution/)
* [https://leetcode-cn.com/problems/zui-xiao-de-kge-shu-lcof/solution/3chong-jie-fa-miao-sha-topkkuai-pai-dui-er-cha-sou/](https://leetcode-cn.com/problems/zui-xiao-de-kge-shu-lcof/solution/3chong-jie-fa-miao-sha-topkkuai-pai-dui-er-cha-sou/)

