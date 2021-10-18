# LEETCODE 560. 和为K的子数组

## 1. [问题](https://leetcode-cn.com/problems/subarray-sum-equals-k/)

给定一个整数数组和一个整数 **k，**你需要找到该数组中和为 **k **的连续的子数组的个数。

**示例 1 :**

```
输入:nums = [1,1,1], k = 2
输出: 2 , [1,1] 与 [1,1] 为两种不同的情况。
```

**说明 :**

1. 数组的长度为 \[1, 20,000]。
2. 数组中元素的范围是 \[-1000, 1000] ，且整数 **k **的范围是 \[-1e7, 1e7]。

## 2. 标签

* 数组
* 哈希表
* 前缀和

## 3. 解法 - 枚举

### 3.1 Java

```java
public class Solution {
    public int subarraySum(int[] nums, int k) {
        // 和为K的子数组总数
        int count = 0;
        // 遍历整个数组
        for (int start = 0; start < nums.length; start++) {
            // 当前子数组的和
            int sum = 0;
            // 计算[start, end]的和
            for (int end = start; end >= 0; end--) {
                // 每遍历一个数字就加起来
                sum += nums[end];
                // 找到了和为 k 的子数组，计数器加一
                if (sum == k) {
                    count++;
                }
            }
        }
        // 返回即可
        return count;
    }
}
```

### 3.2 复杂度分析

* 时间复杂度 `O(n^2)` ：其中 n 为数组的长度。
* 空间复杂度 `O(1)` ：只需要常数空间存放若干变量。

## 4. 解法 - **前缀和 哈希表**

### 4.1 Java

```java
public class Solution {
    public int subarraySum(int[] nums, int k) {
        // 和为 K 的子数组个数
        int count = 0;
        // 前缀和
        int pre = 0;
        // 哈希表，以和为键，以出现的次数为对应的值
        // 记录 pre 出现的次数，从左往右一边更新 map 一边一边计算值
        HashMap<Integer, Integer> map = new HashMap<>();
        // 初始化
        map.put(0, 1);
        // 遍历数组
        for (int i = 0; i < nums.length; i++) {
            /**
             * 计算前缀和
             *  pre[i] 表示 [0,i] 的总和
             *  pre[i] = pre[i-1] + nums[i]
             *  [j, i]的和为 k 即为：pre[i] - pre[j-1] = k
             *  所以 pre[j-1] = pre[i] - k
             *  找到符合上面这个式子的所有 j 即可
             */
            pre += nums[i];
            
            // 如果 map 里已经包含了这样的j，直接加上出现的次数即可
            if (map.containsKey(pre - k)) {
                count += map.get(pre - k);
            }
            // 每计算一个前缀和，都往 map 里放
            // 已有的就在原有的次数上加 1
            // 没有的就直接初始化为 1
            map.put(pre, map.getOrDefault(pre, 0) + 1);
        }
        // 返回即可
        return count;
    }
}
```

### 4.2 复杂度分析

* 时间复杂度 `O(n)` ：其中 n 为数组的长度，需要遍历一遍数组。
* 空间复杂度 `O(n)` ：其中 n 为数组的长度。哈希表在最坏情况下可能有 n 个不同的键值，因此需要 O(n) 的空间复杂度。

## 5. 参考

* [https://leetcode-cn.com/problems/subarray-sum-equals-k/](https://leetcode-cn.com/problems/subarray-sum-equals-k/)
* [https://leetcode-cn.com/problems/subarray-sum-equals-k/solution/he-wei-kde-zi-shu-zu-by-leetcode-solution/](https://leetcode-cn.com/problems/subarray-sum-equals-k/solution/he-wei-kde-zi-shu-zu-by-leetcode-solution/)
