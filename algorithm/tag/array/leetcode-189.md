# LEETCODE 189. 旋转数组

## 1. [问题](https://leetcode-cn.com/problems/rotate-array/)

给定一个数组，将数组中的元素向右移动 _k_ 个位置，其中 _k_ 是非负数。

**示例 1:**

```text
输入: [1,2,3,4,5,6,7] 和 k = 3
输出: [5,6,7,1,2,3,4]
解释:
向右旋转 1 步: [7,1,2,3,4,5,6]
向右旋转 2 步: [6,7,1,2,3,4,5]
向右旋转 3 步: [5,6,7,1,2,3,4]
```

**示例 2:**

```text
输入: [-1,-100,3,99] 和 k = 2
输出: [3,99,-1,-100]
解释: 
向右旋转 1 步: [99,-1,-100,3]
向右旋转 2 步: [3,99,-1,-100]
```

**说明:**

* 尽可能想出更多的解决方案，至少有三种不同的方法可以解决这个问题。
* 要求使用空间复杂度为 O\(1\) 的 **原地** 算法。

## 2. 标签

* 数组
* 原地算法

## 3. 解法 - 借助新数组

### 3.1 Java

```java
class Solution {
    public void rotate(int[] nums, int k) {
        // 数组长度
        int len = nums.length;
        // 新数组
        int[] newNums = new int[len];
        
        // 巧妙利用取模运算符
        for(int i=0;i<len;i++){
            newNums[(i+k)%len] = nums[i];
        }

        // 把新数组的结果放回原数组即可
        for(int i=0;i<len;i++){
            nums[i] = newNums[i];
        }
    }
}
```

### 3.2 复杂度分析

* 时间复杂度 `O(n)` ：其中 n 为数组的长度。
* 空间复杂度 `O(n)` ：新数组所占用的空间。

## 4. 解法 - 原地翻转

要注意的其实是 k 可能会大于数组长度，所以需要对 k 进行取模运算。

### 4.1 Java

```java
class Solution {
    public void rotate(int[] nums, int k) {
        // 数组长度
        int length = nums.length;
        // k 可能会大于数组长度，所以要对其取模
        k %= length;
        // 首先把整个数组翻转一下
        reverse(nums, 0, length-1);
        // 再把[0,k]之间的数字翻转一下
        reverse(nums, 0, k-1);
        // 最后把[k,length-1]之间的数字翻转一下
        reverse(nums, k, length-1);
    }
    
    // 翻转数组
    public void reverse(int[] nums, int begin, int end){
        // 双指针
        while(begin < end){
            int temp = nums[begin];
            nums[begin] = nums[end];
            nums[end] = temp;
            begin++;
            end--;
        }
    }
}

```

### 4.2 复杂度分析

* 时间复杂度 `O(n)` ：其中 n 为数组的长度。每个元素被翻转两次，一共 n 个元素，因此总时间复杂度为 `O(2n)=O(n)`。
* 空间复杂度 `O(1)` ：原地算法，没有占用额外的存储空间。

## 5. 参考

* [https://leetcode-cn.com/problems/rotate-array/](https://leetcode-cn.com/problems/rotate-array/)
* [https://leetcode-cn.com/problems/rotate-array/solution/xuan-zhuan-shu-zu-by-leetcode-solution-nipk/](https://leetcode-cn.com/problems/rotate-array/solution/xuan-zhuan-shu-zu-by-leetcode-solution-nipk/)

