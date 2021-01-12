# LEETCODE 448. 找到所有数组中消失的数字

## 1. [问题](https://leetcode-cn.com/problems/find-all-numbers-disappeared-in-an-array/)

给定一个范围在 1 ≤ a\[i\] ≤ n \( n = 数组大小 \) 的 整型数组，数组中的元素一些出现了两次，另一些只出现一次。

找到所有在 \[1, n\] 范围之间没有出现在数组中的数字。

您能在不使用额外空间且时间复杂度为O\(n\)的情况下完成这个任务吗? 你可以假定返回的数组不算在额外空间内。

示例:

```text
输入:
[4,3,2,7,8,2,3,1]

输出:
[5,6]
```

## 2. 标签

* 数组
* 哈希表

## 3. 解法 - 哈希表

### 3.1 Java

```java
class Solution {
    public List<Integer> findDisappearedNumbers(int[] nums) {
        
        // 使用哈希表记录数字是否出现
        HashMap<Integer, Boolean> hashmap = new HashMap<Integer, Boolean>();
        for (int i = 0; i < nums.length; i++) {
            hashmap.put(nums[i], true);
        }
        
        // 结果列表
        List<Integer> result = new LinkedList<Integer>();
        
        // 遍历数组找到没有出现的数字即可 
        for (int i = 1; i <= nums.length; i++) {
            if (!hashmap.containsKey(i)) {
                result.add(i);
            }
        }
        
        return result;
    }
}
```

### 3.2 复杂度分析

* 时间复杂度 `O(N)` 
* 空间复杂度 `O(N)` 

## 4. 解法 - 原地修改

### 4.1 Java

```java
class Solution {
    public List<Integer> findDisappearedNumbers(int[] nums) {
        // 遍历整个数组
        for (int i = 0; i < nums.length; i++) {
            // 把当前数字的值减去1作为新的索引
            int newIndex = Math.abs(nums[i]) - 1;
            // 判断新索引处的nums值是否大于0，如果大于0的话就变成负数
            // 此时，索引的数值（指下标的数值）即在数组中出现过的数字
            if (nums[newIndex] > 0) {
                nums[newIndex] *= -1;
            }
        }
        // 结果列表
        List<Integer> result = new LinkedList<Integer>();
        // 遍历数组
        for (int i = 1; i <= nums.length; i++) {
            // 如果nums没有变成负数，说明此处索引值没有出现过
            if (nums[i - 1] > 0) {
                result.add(i);
            }
        }
        // 返回结果即可
        return result;
    }
}
```

### 4.2 复杂度分析

* 时间复杂度 `O(N)` 
* 空间复杂度 `O(1)` 

## 5. 参考

* [https://leetcode-cn.com/problems/find-all-numbers-disappeared-in-an-array/](https://leetcode-cn.com/problems/find-all-numbers-disappeared-in-an-array/)
* [https://leetcode-cn.com/problems/find-all-numbers-disappeared-in-an-array/solution/zhao-dao-suo-you-shu-zu-zhong-xiao-shi-de-shu-zi-2/](https://leetcode-cn.com/problems/find-all-numbers-disappeared-in-an-array/solution/zhao-dao-suo-you-shu-zu-zhong-xiao-shi-de-shu-zi-2/)

