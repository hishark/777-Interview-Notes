# LEETCODE 75. 颜色分类

## 1. [问题](https://leetcode-cn.com/problems/sort-colors/)

给定一个包含红色、白色和蓝色，一共 n 个元素的数组，原地对它们进行排序，使得相同颜色的元素相邻，并按照红色、白色、蓝色顺序排列。

此题中，我们使用整数 0、 1 和 2 分别表示红色、白色和蓝色。

进阶：

* 你可以不使用代码库中的排序函数来解决这道题吗？ 
* 你能想出一个仅使用常数空间的一趟扫描算法吗？

**示例 1：**

```
输入：nums = [2,0,2,1,1,0]
输出：[0,0,1,1,2,2]
```

**示例 2：**

```
输入：nums = [2,0,1]
输出：[0,1,2]
```

**示例 3：**

```
输入：nums = [0]
输出：[0]
```

**示例 4：**

```
输入：nums = [1]
输出：[1]
```

**提示：**

* `n == nums.length`
* `1 <= n <= 300`
* `nums[i]` 为 `0`、`1` 或 `2`

## 2. 标签

* 数组
* 双指针

## 3. 解法 - 双指针

### 3.1 Java

```java
class Solution {
    public void sortColors(int[] nums) {
        // 数组长度
        int len = nums.length;

        /**
         * 使用 p0 来交换 0，使用 p2 来交换 2
         * 在遍历的过程中，找出所有的 0 交换到数组头部
         * 找出所有的 2 交换到数组尾部
         */
        int p0 = 0, p2 = len - 1;
        
        /**
         * p0 从左向右移动，p2 从右向左移动
         * 在从左向右遍历整个数组时，如果遍历的位置超过了 p2，即可停止遍历
         */
        for (int i = 0; i <= p2; i++) {
            /**
             * 如果找到了2，将 nums[i] 与 nums[p2] 交换
             * 可是这样就会导致一个问题，新的 nums[i] 可能是 0 或者 2
             * 如果是 0 的话，直接结束循环，交换即可
             * 如果是 1 的话，啥也不要做
             * 如果是 2 的话，就不断的与 p2 进行交换，直到 nums[i] 不为 2
             */
            while (i <= p2 && nums[i] == 2) {
                // 交换数字
                int temp = nums[i];
                nums[i] = nums[p2];
                nums[p2] = temp;
                // 别忘记将 p2 左移一个位置
                p2--;
            }
            // 如果找到了0，直接将 nums[i] 与 nums[p0] 交换
            if (nums[i] == 0) {
                // 交换数字
                int temp = nums[i];
                nums[i] = nums[p0];
                nums[p0] = temp;
                // 别忘记将 p0 右移一个位置
                p0++;
            }
        }
    }
}
```

### 3.2 复杂度分析

* 时间复杂度 `O(n)` ：其中 n 是数组 nums 的长度。
* 空间复杂度 `O(1)` ：原地算法，没有占用额外的存储空间。

## 4. 参考

* [https://leetcode-cn.com/problems/sort-colors/](https://leetcode-cn.com/problems/sort-colors/)
* [https://leetcode-cn.com/problems/sort-colors/solution/yan-se-fen-lei-by-leetcode-solution/](https://leetcode-cn.com/problems/sort-colors/solution/yan-se-fen-lei-by-leetcode-solution/)
