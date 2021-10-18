# LEETCODE 442. 数组中重复的数据

## [题目](https://leetcode-cn.com/problems/find-all-duplicates-in-an-array/)

略

## 解法

```java
import java.util.List;

class Solution {
    public List<Integer> findDuplicates(int[] nums) {
        /**
         *  由条件1 ≤ a[i] ≤ n，可知出 nums 中的所有值可以和其索引有对应关系
         *  nums[i] 的正负值可表示数字 i+1 是否出现，若出现则将其变为负数，即 nums[i] = -nums[i]。默认为正整数，即未出现。
         */
        List<Integer> res = new ArrayList<>();
        for (int num: nums) {
            int absNum = Math.abs(num);
            // 当 nums[ absNum - 1]为负数时，表示 absNum 已经出现过一次了
            if (nums[absNum-1] < 0) {
                res.add(absNum);
            } else {
            // 当 nums[ abdNum - 1]为正数时，表示 absNum 还没有出现过
                nums[absNum-1] *= -1;
            }
        }
        return res;
    }
}
```

## 参考

* [https://leetcode-cn.com/problems/find-all-duplicates-in-an-array/solution/you-ya-shi-xian-yuan-di-ha-xi-qiao-yong-p8p43/](https://leetcode-cn.com/problems/find-all-duplicates-in-an-array/solution/you-ya-shi-xian-yuan-di-ha-xi-qiao-yong-p8p43/)



