# \*59 - I. 滑动窗口的最大值【滑动窗口】

## 1. [问题](https://leetcode-cn.com/problems/hua-dong-chuang-kou-de-zui-da-zhi-lcof/)

给定一个数组 `nums` 和滑动窗口的大小 `k`，请找出所有滑动窗口里的最大值。

**示例：**

```text
输入: nums = [1,3,-1,-3,5,3,6,7], 和 k = 3
输出: [3,3,5,5,6,7] 
解释: 

  滑动窗口的位置                最大值
---------------               -----
[1  3  -1] -3  5  3  6  7       3
 1 [3  -1  -3] 5  3  6  7       3
 1  3 [-1  -3  5] 3  6  7       5
 1  3  -1 [-3  5  3] 6  7       5
 1  3  -1  -3 [5  3  6] 7       6
 1  3  -1  -3  5 [3  6  7]      7
```

**提示：**

* 你可以假设 _k_ 总是有效的，在输入数组不为空的情况下，1 ≤ k ≤ 输入数组的大小。

## 2. 标签

* 队列
* 滑动窗口

## 3. 解法 - 滑动窗口

### 3.1 Java

> 还需要回头琢磨琢磨\#TODO

```java
class Solution {
    public int[] maxSlidingWindow(int[] nums, int k) {
        // 判空
        if (nums.length == 0 || k == 0)
            return new int[0];
        
        // 双端队列
        Deque<Integer> deque = new LinkedList<>();
        
        // 结果数组
        // 该数组的长度为滑动窗口的个数
        // 也就是【数组长度 - 滑动窗口的大小 + 1】
        int[] res = new int[nums.length - k + 1];
        
        // 开始遍历所有窗口，i 为窗口的左边界，j 为窗口的右边界
        // 形成窗口后的每一轮中，nums[i-1]为被删除元素，nums[j]为要添加的元素
        // 未形成窗口时，nums[j]为要添加的元素
        for (int j=0, i=1-k;j<nums.length;i++,j++) {
            // i>0说明此时已经形成了窗口，且窗口正在右移，需要删除一个元素
            // 如果队首元素等于被删除的元素，那么队首元素直接出队（队首元素是窗口内的最大元素）
            // 这一步是为了保证 deque 里只包含窗口内的元素
            if (i>0 && deque.peekFirst() == nums[i-1]) {
                deque.removeFirst();
            }
            
            // 删除deque内所有小于nums[j]的元素，以保持deque递减
            while(!deque.isEmpty() && deque.peekLast() < nums[j])
                deque.removeLast();
            
            // 把要添加的元素加入到队列中
            deque.addLast(nums[j]);
            
            // 如果此时形成了滑动窗口，队首元素即最大值，添加至结果数组
            if (i >= 0)
                res[i] = deque.peekFirst();
        }
        return res;
    }
}
```

### 3.2 Kotlin

```kotlin
class Solution {
    fun maxSlidingWindow(nums: IntArray, k: Int): IntArray {
        // 判空
        if (nums.size == 0 || k == 0)
            return IntArray(0)

        // 双端队列
        val deque = LinkedList<Int>()

        // 结果数组
        // 该数组的长度为滑动窗口的个数
        // 也就是【数组长度 - k + 1】
        val res = IntArray(nums.size - k + 1)

        // 开始遍历所有窗口，i 为窗口的左边界，j 为窗口的右边界
        // 形成窗口后的每一轮中，nums[i-1]为被删除元素，nums[j]为要添加的元素
        // 未形成窗口时，nums[j]为要添加的元素
        var j = 0
        var i = 1 - k
        while (j < nums.size) {
            // i>0说明此时已经形成了窗口，且窗口正在右移，需要删除一个元素
            // 如果队首元素等于被删除的元素，那么队首元素直接出队（队首元素是窗口内的最大元素）
            // 这一步是为了保证 deque 里只包含窗口内的元素
            if (i > 0 && deque.peekFirst() == nums[i - 1]) {
                deque.removeFirst()
            }

            // 删除deque内所有小于nums[j]的元素，以保持deque递减
            while (!deque.isEmpty() && deque.peekLast() < nums[j])
                deque.removeLast()

            // 把要添加的元素加入到队列中
            deque.addLast(nums[j])

            // 如果此时形成了滑动窗口，队首元素即最大值，添加至结果数组
            if (i >= 0)
                res[i] = deque.peekFirst()
            i++
            j++
        }
        return res
    }
}
```

### 3.3 复杂度分析

* 时间复杂度 `O(N)` ：其中 N 是数组 nums 的长度。线性遍历数组需要 `O(N)`。每个元素最多入队和出队一次，因此队列 deque 占用 `O(2N)` 。
* 空间复杂度 `O(k)` ：队列 deque 中最多同时存储 k 个元素，即窗口的大小。

## 4. 参考

* [https://leetcode-cn.com/problems/hua-dong-chuang-kou-de-zui-da-zhi-lcof/](https://leetcode-cn.com/problems/hua-dong-chuang-kou-de-zui-da-zhi-lcof/)
* [https://leetcode-cn.com/problems/hua-dong-chuang-kou-de-zui-da-zhi-lcof/solution/mian-shi-ti-59-i-hua-dong-chuang-kou-de-zui-da-1-6/](https://leetcode-cn.com/problems/hua-dong-chuang-kou-de-zui-da-zhi-lcof/solution/mian-shi-ti-59-i-hua-dong-chuang-kou-de-zui-da-1-6/)

