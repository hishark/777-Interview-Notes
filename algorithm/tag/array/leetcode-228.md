# LEETCODE 228. 汇总区间

## 1. [问题](https://leetcode-cn.com/problems/summary-ranges/)

给定一个无重复元素的有序整数数组 nums 。

返回 恰好覆盖数组中所有数字 的 最小有序 区间范围列表。也就是说，nums 的每个元素都恰好被某个区间范围所覆盖，并且不存在属于某个范围但不属于 nums 的数字 x 。

列表中的每个区间范围 \[a,b\] 应该按如下格式输出：

"a-&gt;b" ，如果 a != b "a" ，如果 a == b

示例 1：

```text
输入：nums = [0,1,2,4,5,7]
输出：["0->2","4->5","7"]
解释：区间范围是：
[0,2] --> "0->2"
[4,5] --> "4->5"
[7,7] --> "7"
```

示例 2：

```text
输入：nums = [0,2,3,4,6,8,9]
输出：["0","2->4","6","8->9"]
解释：区间范围是：
[0,0] --> "0"
[2,4] --> "2->4"
[6,6] --> "6"
[8,9] --> "8->9"
```

示例 3：

```text
输入：nums = []
输出：[]
```

示例 4：

```text
输入：nums = [-1]
输出：["-1"]
```

示例 5：

```text
输入：nums = [0]
输出：["0"]
```

提示：

* 0 &lt;= nums.length &lt;= 20 
* -2^31 &lt;= nums\[i\] &lt;= 2^31 - 1 
* nums 中的所有值都 互不相同 
* nums 按升序排列

## 2. 标签

* 数组

## 3. 解法 - 一次遍历

### 3.1 Java

```java
class Solution {
    public List<String> summaryRanges(int[] nums) {
        // 结果列表
        List<String> res = new ArrayList<String>();
        // 遍历下标
        int i = 0;
        // 数组长度
        int n = nums.length;
        // 对数组进行一次遍历
        while (i < n) {
            // 记下左边界
            int left = i;
            // 往右走
            i++;
            // 如果还在数组范围内，且数字连续，就一直往右
            while (i < n && nums[i] == nums[i - 1] + 1) {
                i++;
            }
            //记下右边界
            int right = i - 1;
            // 组成结果字符串
            StringBuffer curRange = new StringBuffer(Integer.toString(nums[left]));
            // 如果结果里只有一个数字，就不需要箭头啦
            if (left < right) {
                curRange.append("->");
                curRange.append(Integer.toString(nums[right]));
            }
            // 加入到最终结果列表中即可
            res.add(curRange.toString());
        }
        // 返回结果
        return res;
    }
}
```

### 3.2 复杂度分析

* 时间复杂度 `O(n)` ：其中 n 为数组的长度。
* 空间复杂度 `O(1)` ：除了用于输出的空间外，额外使用的空间为常数。
  * 力扣官方题解里计算空间复杂度好像都不管用于返回的空间哦，好滴。

## 4. 参考

* [https://leetcode-cn.com/problems/summary-ranges/](https://leetcode-cn.com/problems/summary-ranges/)
* [https://leetcode-cn.com/problems/summary-ranges/solution/hui-zong-qu-jian-by-leetcode-solution-6zrs/](https://leetcode-cn.com/problems/summary-ranges/solution/hui-zong-qu-jian-by-leetcode-solution-6zrs/)

