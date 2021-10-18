# LEETCODE 128. 最长连续序列

## [1. 问题](https://leetcode-cn.com/problems/longest-consecutive-sequence/)

给定一个未排序的整数数组，找出最长连续序列的长度。

要求算法的时间复杂度为 O(n)。

示例:

> 输入: \[100, 4, 200, 1, 3, 2] 输出: 4 解释: 最长连续序列是 \[1, 2, 3, 4]。它的长度为 4。

## 2. 解法 - 哈希表

### 2.1 Java

```java
class Solution {
    public int longestConsecutive(int[] nums) {
        // 初始化哈希表
        Set<Integer> set = new HashSet<>();
        for (int num: nums)
            set.add(num);

        // 最长连续序列的长度
        int maxLength = 0;

        // 遍历哈希表
        for (int num: set) {
            int currentLength = 1;
            // 判断当前数字num的前一个数字num-1在哈希表中存不存在
            if (set.contains(num-1)) {
                // 如果存在，就跳过
                continue;
            } else {
                // 如果不存在，就开始匹配num+1、num+2、num+2……
                while (true) {
                    if (set.contains(num+1)) {
                        currentLength++;
                        num++;
                    } else{
                        break;
                    }
                }

            }
            // 更新最大值
            maxLength = Math.max(maxLength, currentLength);
        }

        return maxLength;
    }
}
```

### 2.2 Kotlin

```kotlin
import kotlin.math.max
class Solution {
    fun longestConsecutive(nums: IntArray): Int {
        // 初始化集合
        var set = mutableSetOf<Int>()
        for (num in nums)
            set.add(num)

        // 最长连续序列的长度
        var maxLength = 0;

        // 遍历哈希表
        for (n in set) {
            var num = n
            var currentLength = 1;
            // 判断当前数字num的前一个数字num-1在哈希表中存不存在
            if (set.contains(num-1)) {
                // 如果存在，就跳过
                continue
            } else {
                // 如果不存在，就开始匹配num+1、num+2、num+2……
                while (true) {
                    if (set.contains(num+1)) {
                        currentLength++
                        num++
                    } else{
                        break
                    }
                }

            }
            // 更新最大值
            maxLength = max(maxLength, currentLength)
        }

        return maxLength
    }
}
```

## 3. 参考

* [力扣：128. 最长连续序列](https://leetcode-cn.com/problems/longest-consecutive-sequence/)
* [力扣官方题解：最长连续序列](https://leetcode-cn.com/problems/longest-consecutive-sequence/solution/zui-chang-lian-xu-xu-lie-by-leetcode-solution/)

## 4. 学习草稿

![](https://777blog.oss-cn-shanghai.aliyuncs.com/blog%20pic/IMG\_4305.JPG)
