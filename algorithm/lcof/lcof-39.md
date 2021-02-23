# \*39. 数组中出现次数超过一半的数字【哈希/摩尔投票】

## 1. [问题](https://leetcode-cn.com/problems/shu-zu-zhong-chu-xian-ci-shu-chao-guo-yi-ban-de-shu-zi-lcof/)

数组中有一个数字出现的次数超过数组长度的一半，请找出这个数字。

你可以假设数组是非空的，并且给定的数组总是存在多数元素。

**示例 1：**

```text
输入: [1, 2, 3, 2, 2, 2, 5, 4, 2]
输出: 2
```

**限制：**

* `1 <= 数组长度 <= 50000`

## 2. 标签

* 位运算
* 分治

## 3. 解法 - 摩尔投票法

### 3.1 Java

```java

// 摩尔投票法
// ref: https://leetcode-cn.com/problems/shu-zu-zhong-chu-xian-ci-shu-chao-guo-yi-ban-de-shu-zi-lcof/solution/mian-shi-ti-39-shu-zu-zhong-chu-xian-ci-shu-chao-3/
class Solution {
    public int majorityElement(int[] nums) {
        // 众数（本题的众数定义为数组中出现次数超过一半的数，并不是传统意义的众数）
        int mode = 0;
        // 票数和
        int votes = 0;

        // 遍历所有数字
        for (int num : nums) {
            // 当票数和为 0 时，就假设当前数字是众数 mode
            // 所以是先假设第一个数组是众数
            if (votes == 0)
                mode = num;

            // 如果当前数字是众数，票数+1，反之票数-1
            if (num == mode)
                votes += 1;
            else
                votes -= 1;

        }

        return mode;
    }
}
```

### 3.2 Kotlin

```kotlin
class Solution {
    fun majorityElement(nums: IntArray): Int {
        // 众数
        var mode = 0
        // 票数和
        var votes = 0

        // 遍历所有数字
        for (num in nums) {
            // 当票数和为 0 时，就假设当前数字是众数 mode
            if (votes == 0)
                mode = num

            // 如果当前数字是众数，票数+1，反之票数-1
            if (num == mode)
                votes += 1
            else
                votes -= 1

        }

        return mode
    }
}
```

### 3.3 复杂度分析

* 时间复杂度 `O(N)` ：N 为数组的长度。
* 空间复杂度 `O(1)` ：变量仅仅使用常数大小的额外存储空间。

## 4. 参考

* [https://leetcode-cn.com/problems/shu-zu-zhong-chu-xian-ci-shu-chao-guo-yi-ban-de-shu-zi-lcof/](https://leetcode-cn.com/problems/shu-zu-zhong-chu-xian-ci-shu-chao-guo-yi-ban-de-shu-zi-lcof/)
* [https://leetcode-cn.com/problems/shu-zu-zhong-chu-xian-ci-shu-chao-guo-yi-ban-de-shu-zi-lcof/solution/mian-shi-ti-39-shu-zu-zhong-chu-xian-ci-shu-chao-3/](https://leetcode-cn.com/problems/shu-zu-zhong-chu-xian-ci-shu-chao-guo-yi-ban-de-shu-zi-lcof/solution/mian-shi-ti-39-shu-zu-zhong-chu-xian-ci-shu-chao-3/)

