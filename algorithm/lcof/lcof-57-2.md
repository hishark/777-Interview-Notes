# 57 - II. 和为s的连续正数序列【双指针】

## 1. [问题](https://leetcode-cn.com/problems/he-wei-sde-lian-xu-zheng-shu-xu-lie-lcof/)

输入一个正整数 target ，输出所有和为 target 的连续正整数序列（至少含有两个数）。

序列内的数字由小到大排列，不同序列按照首个数字从小到大排列。

**示例 1：**

```text
输入：target = 9
输出：[[2,3,4],[4,5]]
```

**示例 2：**

```text
输入：target = 15
输出：[[1,2,3,4,5],[4,5,6],[7,8]]
```

**限制：**

* `1 <= target <= 10^5`

## 2. 标签

* 数组
* 双指针
* 滑动窗口

## 3. 解法 - 双指针

> 这里也是在滑动窗口嘛，和[另一个](https://leetcode-cn.com/problems/he-wei-sde-lian-xu-zheng-shu-xu-lie-lcof/solution/shi-yao-shi-hua-dong-chuang-kou-yi-ji-ru-he-yong-h/)有些区别，下次再看看。

### 3.1 Java

```java
class Solution {
    public int[][] findContinuousSequence(int target) {
        // 最终结果
        List<int[]> resList = new ArrayList<int[]>();
        
        // 当前枚举区间为 [start, end]
        int start = 1;
        int end = 2;
        while (start < end) {
            // 序列之和，使用求和公式
            int sum = (start + end) * (end - start + 1) / 2;

            // 如果等于 target，就找到了一个合法序列，加入结果列表
            if (sum == target) {
                // 当前合法序列
                int[] curRes = new int[end - start + 1];
                for (int i = start; i <= end; ++i) {
                    curRes[i - start] = i;
                }
                // 添加到结果列表中
                resList.add(curRes);
                // 以 start 为起点的合法序列最多只有一个，所以需要枚举下一个起点，将 start 右移
                start++;
            } else if (sum < target) {
                // 序列之和比目标更小，说明还可以将 end 右移，以获得更大的值
                end++;
            } else {
                // 序列之和比目标更大，说明以 start 为起点不存在一个 end 使得 sum = target
                // 此时应该枚举下一个起点，将 start 右移
                start++;
            }
        }
        // 循环结束，得到所有的合法序列
        return resList.toArray(new int[resList.size()][]);
    }
}
```

### 3.2 Kotlin

```kotlin
class Solution {
    fun findContinuousSequence(target: Int): Array<IntArray> {
        // 最终结果
        val resList = ArrayList<IntArray>()
        
        // 当前枚举区间为 [start, end]
        var start = 1
        var end = 2
        while (start < end) {
            // 序列之和，使用求和公式
            val sum = (start + end) * (end - start + 1) / 2

            // 如果等于 target，就找到了一个合法序列，加入结果列表
            if (sum == target) {
                // 当前合法序列
                val curRes = IntArray(end - start + 1)
                for (i in start..end) {
                    curRes[i - start] = i
                }
                // 添加到结果列表中
                resList.add(curRes)
                // 以 start 为起点的合法序列最多只有一个，所以需要枚举下一个起点，将 start 右移
                start++
            } else if (sum < target) {
                // 序列之和比目标更小，说明还可以将 end 右移，以获得更大的值
                end++
            } else {
                // 序列之和比目标更大，说明以 start 为起点不存在一个 end 使得 sum = target
                // 此时应该枚举下一个起点，将 start 右移
                start++
            }
        }
        // 循环结束，得到所有的合法序列
        return resList.toTypedArray()
    }
}
```

### 3.3 复杂度分析

* 时间复杂度 `O(target)` ：由于题目要求序列长度至少大于 2，所以枚举的上界为 $$\lfloor \frac{target}{2} \rfloor$$ 。又由于两个指针一直单调增加，最多移动 $$\lfloor \frac{target}{2} \rfloor$$ 次，所以时间复杂度为 `O(target)` 。
* 空间复杂度 `O(1)` ：只使用到了常数大小的额外空间。

> 为啥是这个上界 - - 先搁着

## 4. 解法 - 滑动窗口 \#TODO

### 4.1 Java

```java

```

### 4.2 Kotlin

```kotlin

```

### 4.3 复杂度分析

* 时间复杂度 `O()` ：
* 空间复杂度 `O()` ：

## 5. 参考

* [https://leetcode-cn.com/problems/he-wei-sde-lian-xu-zheng-shu-xu-lie-lcof/](https://leetcode-cn.com/problems/he-wei-sde-lian-xu-zheng-shu-xu-lie-lcof/)
* [https://leetcode-cn.com/problems/he-wei-sde-lian-xu-zheng-shu-xu-lie-lcof/solution/mian-shi-ti-57-ii-he-wei-sde-lian-xu-zheng-shu-x-2/](https://leetcode-cn.com/problems/he-wei-sde-lian-xu-zheng-shu-xu-lie-lcof/solution/mian-shi-ti-57-ii-he-wei-sde-lian-xu-zheng-shu-x-2/)
* [https://leetcode-cn.com/problems/he-wei-sde-lian-xu-zheng-shu-xu-lie-lcof/solution/shi-yao-shi-hua-dong-chuang-kou-yi-ji-ru-he-yong-h/](https://leetcode-cn.com/problems/he-wei-sde-lian-xu-zheng-shu-xu-lie-lcof/solution/shi-yao-shi-hua-dong-chuang-kou-yi-ji-ru-he-yong-h/)

