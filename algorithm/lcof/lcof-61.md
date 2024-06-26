# 61. 扑克牌中的顺子【Set/排序】

## 1. [问题](https://leetcode-cn.com/problems/bu-ke-pai-zhong-de-shun-zi-lcof/)

从扑克牌中随机抽5张牌，判断是不是一个顺子，即这5张牌是不是连续的。2～10为数字本身，A为1，J为11，Q为12，K为13，而大、小王为 0 ，可以看成任意数字。A 不能视为 14。

**示例 1:**

```
输入: [1,2,3,4,5]
输出: True
```

**示例 2:**

```
输入: [0,0,1,2,5]
输出: True
```

**限制：**

* 数组长度为 5 
* 数组的数取值为 \[0, 13] 

## 2. 标签

* 数组
* 排序
* 哈希表

## 3. 解法 - 集合 Set

### 3.1 Java

```java
class Solution {
    public boolean isStraight(int[] nums) {
        // 利用 Set 判断是否存在重复的牌
        Set<Integer> set = new HashSet<>();
        // 初始化：五张牌中的最大值和最小值
        int min = 14; // min 和 max 的初始值别搞反啦
        int max = 0;

        // 遍历五张扑克牌
        for (int num: nums) {
            // 大小王可以看作是任意数字，所以只要没有重复的牌
            // 同时【最大牌 - 最小牌 < 5】那么就是一个顺子
            if (num == 0)
                continue;

            // 存储最大的牌
            max = Math.max(max, num);

            // 存储最小的牌
            min = Math.min(min, num);

            // 如果出现了重复的牌，必定不是顺子！
            if (set.contains(num))
                return false;
             
            // 每遍历一个牌都放入 set（set会自动去重）
            set.add(num);
        }
        // 遍历完所有的牌之后，判断最大值和最小值的差
        return max - min < 5;
    }
}
```

### 3.2 Kotlin

```kotlin
class Solution {
    fun isStraight(nums: IntArray): Boolean {
        // 利用 Set 判断是否存在重复的牌
        val set = HashSet<Int>()
        // 初始化：五张牌中的最大值和最小值
        var min = 14
        var max = 0

        // 遍历五张扑克牌
        for (num in nums) {
            // 大小王可以看作是任意数字，所以只要没有重复的牌
            // 同时【最大牌 - 最小牌 < 5】那么就是一个顺子
            if (num == 0)
                continue

            // 存储最大的牌
            max = Math.max(max, num)

            // 存储最小的牌
            min = Math.min(min, num)

            // 如果出现了重复的牌，必定不是顺子！
            if (set.contains(num))
                return false

            // 每遍历一个牌都放入 set（set会自动去重）
            set.add(num)
        }
        // 遍历完所有的牌之后，判断最大值和最小值的差
        return max - min < 5
    }
}
```

### 3.3 复杂度分析

* 时间复杂度 `O(N)` ：其中 N 为数组 nums 的长度，遍历数组需要使用 `O(N)` 时间。
* 空间复杂度 `O(N)` ：集合 Set 只占用了 `O(N)` 的额外存储空间。

## 4. 解法 - 排序

### 4.1 Java

```java
class Solution {
    public boolean isStraight(int[] nums) {
        // 大小王的数量
        int kingNum = 0;
        // 对数组进行排序
        Arrays.sort(nums);
        
        for (int i=0;i<4;i++) {
            // 统计大小王的数量
            if (nums[i] == 0)
                kingNum++;
            // 判断是否有重复的牌，如果有的话直接返回 false
            else if (nums[i] == nums[i+1]) // 这里的逻辑别写成两个if了，因为可能会有两个连续的0！
                return false;
        }

        // 排序后，nums[4]是最大的牌
        // 统计好大小王的数量 kingNum 之后，nums[kingNum] 就是大小王之后最小的一张牌
        // 只要【最大牌 - 最小牌 < 5】就说明是一个顺子
        return nums[4] - nums[kingNum] < 5;
    } 
}

```

### 4.2 Kotlin

```kotlin
class Solution {
    fun isStraight(nums: IntArray): Boolean {
        // 大小王的数量
        var kingNum = 0
        // 对数组进行排序
        Arrays.sort(nums)

        for (i in 0..3) {
            // 统计大小王的数量
            if (nums[i] == 0)
                kingNum++
            else if (nums[i] == nums[i + 1])
                return false// 判断是否有重复的牌，如果有的话直接返回 false
        }

        // 排序后，nums[4]是最大的牌
        // 统计好大小王的数量 kingNum 之后，nums[kingNum] 就是大小王之后最小的一张牌
        // 只要【最大牌 - 最小牌 < 5】就说明是一个顺子
        return nums[4] - nums[kingNum] < 5
    }
}
```

### 4.3 复杂度分析

* 时间复杂度 `O(NlogN)` ：其中 N 为数组 nums 的长度，使用内置函数对数组进行排序需要占用 O(NlogN) 的时间。本题的 N 恒等于 5，所以时间复杂度为 `O(5log5) = O(1)` 。
* 空间复杂度 `O(1)` ：变量 kingNum 仅占用了常数大小的额外存储空间。

## 4. 参考

* [https://leetcode-cn.com/problems/bu-ke-pai-zhong-de-shun-zi-lcof/](https://leetcode-cn.com/problems/bu-ke-pai-zhong-de-shun-zi-lcof/)
* [https://leetcode-cn.com/problems/bu-ke-pai-zhong-de-shun-zi-lcof/solution/mian-shi-ti-61-bu-ke-pai-zhong-de-shun-zi-ji-he-se/](https://leetcode-cn.com/problems/bu-ke-pai-zhong-de-shun-zi-lcof/solution/mian-shi-ti-61-bu-ke-pai-zhong-de-shun-zi-ji-he-se/)
