# LEETCODE 852. 山脉数组的峰顶索引

## 1. [问题](https://leetcode-cn.com/problems/peak-index-in-a-mountain-array/)

我们把符合下列属性的数组 A 称作山脉：

* A.length &gt;= 3 
* 存在 0 &lt; i &lt; A.length - 1 使得A\[0\] &lt; A\[1\] &lt; ... A\[i-1\] &lt; A\[i\] &gt; A\[i+1\] &gt; ... &gt; A\[A.length - 1\] 

给定一个确定为山脉的数组，返回任何满足 A\[0\] &lt; A\[1\] &lt; ... A\[i-1\] &lt; A\[i\] &gt; A\[i+1\] &gt; ... &gt; A\[A.length - 1\] 的 i 的值。

**示例 1：**

```text
输入：[0,1,0]
输出：1
```

**示例 2：**

```text
输入：[0,2,1,0]
输出：1
```

**提示：**

1. `3 <= A.length <= 10000`
2. 0 &lt;= A\[i\] &lt;= 10^6
3. A 是如上定义的山脉

## 2. 标签

* 二分查找

## 3. 解法 - 二分查找

### 3.1 Java

```java
// ref: https://leetcode-cn.com/problems/peak-index-in-a-mountain-array/solution/shan-mai-shu-zu-de-feng-ding-suo-yin-by-leetcode/

class Solution {
    public int peakIndexInMountainArray(int[] arr) {
        /**
         * 将山脉数组中所有满足 A[i] < A[i+1]的 i 点标记为 True 不满足的标记为 False 那么一个山脉数组可以标记为 [True,
         * True, ... , True, False , ... , False]
         */
        int left = 0;
        int right = arr.length - 1;

        while (left < right) {
            // 找中点
            int mid = left + (right - left) / 2;

            if (arr[mid] < arr[mid + 1]) {
                left = mid + 1;
            } else {
                // 由于题目限制，不存在连续相等的数字
                // 所以这里一定是发生突变的地方，更新右边界即可
                right = mid;
            }
        }

        return left;
    }
}
```

### 3.2 Kotlin

```kotlin
class Solution {
    fun peakIndexInMountainArray(arr: IntArray): Int {
        /**
         * 将山脉数组中所有满足 A[i] < A[i+1]的 i 点标记为 True 不满足的标记为 False 那么一个山脉数组可以标记为 [True,
         * True, ... , True, False , ... , False]
         */
        var left = 0
        var right = arr.size - 1

        while (left < right) {
            // 找中点
            val mid = left + (right - left) / 2

            if (arr[mid] < arr[mid + 1]) {
                left = mid + 1
            } else {
                // 由于题目限制，不存在连续相等的数字
                // 所以这里一定是 arr[mid] > arr[mid+1]
                right = mid
            }
        }

        return left
    }
}
```

### 3.3 复杂度分析

* 时间复杂度 `O(logn)` ：搜索空间每次循环都会减少一半，二分查找的时间复杂度为对数级别。
* 空间复杂度 `O(1)` ：变量仅占用了常数大小的额外存储空间。

## 4. 参考

* [https://leetcode-cn.com/problems/peak-index-in-a-mountain-array/](https://leetcode-cn.com/problems/peak-index-in-a-mountain-array/)
* [https://leetcode-cn.com/problems/peak-index-in-a-mountain-array/solution/shan-mai-shu-zu-de-feng-ding-suo-yin-by-leetcode/](https://leetcode-cn.com/problems/peak-index-in-a-mountain-array/solution/shan-mai-shu-zu-de-feng-ding-suo-yin-by-leetcode/)

