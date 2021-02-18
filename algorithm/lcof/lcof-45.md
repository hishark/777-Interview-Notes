# 45. 把数组排成最小的数【排序】

## 1. [问题](https://leetcode-cn.com/problems/ba-shu-zu-pai-cheng-zui-xiao-de-shu-lcof/)

输入一个非负整数数组，把数组里所有数字拼接起来排成一个数，打印能拼接出的所有数字中最小的一个。

**示例 1:**

```text
输入: [10,2]
输出: "102"
```

**示例 2:**

```text
输入: [3,30,34,5,9]
输出: "3033459"
```

**提示:**

* `0 < nums.length <= 100`

**说明:**

* 输出结果可能非常大，所以你需要返回一个字符串而不是整数
* 拼接起来的数字可能会有前导 0，最后结果不需要去掉前导 0

## 2. 标签

* 数组
* 排序
* 字符串

## 3. 解法 - Arrays.sort

> 重写Arrays.sort排序规则

### 3.1 Java

```java
class Solution {
    public String minNumber(int[] nums) {
        // 把整数数组转换为字符串数组
        String[] strs = new String[nums.length];
        for (int i=0;i<nums.length;i++) {
            strs[i] = String.valueOf(nums[i]);
        }
        /**
         * Arrays.sort默认是对元素进行从小到大的排序
         * 修改排序规则如下，仍是从小到大进行排序，但是比较的不是 x 和 y
         * 而是 x + y 和 y + x
         *  1. x + y < y + x 时表示 x < y，x 排在 y 之前可以获得较小值
         *  2. x + y > y + x 时表示 x > y，x 排在 y 之后可以获得较小值
         */
        Arrays.sort(strs, (x, y) -> (x + y).compareTo(y + x));
        
        // 把排序后的字符串数组拼接成结果字符串
        StringBuilder res = new StringBuilder();
        for (String str: strs) {
            res.append(str);
        }
        return res.toString();
    }
}
```

### 3.2 Kotlin

```kotlin
class Solution {
    fun minNumber(nums: IntArray): String {
        // 把整数数组转换为字符串数组
        val strs = arrayOfNulls<String>(nums.size)
        for (i in nums.indices) {
            strs[i] = nums[i].toString()
        }
        /**
         * Arrays.sort默认是对元素进行从小到大的排序
         * 修改排序规则如下，仍是从小到大进行排序，但是比较的不是 x 和 y
         * 而是 x + y 和 y + x
         * 1. x + y < y + x 时表示 x < y，x 排在 y 之前
         * 2. x + y > y + x 时表示 x > y，x 排在 y 之后
         */
        Arrays.sort<String>(strs) { x, y -> (x + y).compareTo(y + x) }

        // 把排序后的字符串数组拼接成结果字符串
        val res = StringBuilder()
        for (str in strs) {
            res.append(str)
        }
        return res.toString()
    }
}
```

### 3.3 复杂度分析

* 时间复杂度 `O(NlogN)` ：其中 N 是结果字符串的长度。使用快排或者内置函数平均时间复杂度为 `O(NlogN)` ，最差时间复杂度为 `O(N^2)` 。
* 空间复杂度 `O(N)` ：字符串占用了 `O(N)` 大小的额外存储空间。

## 4. 解法 - 快排

### 4.1 Java

```java
// 快排
class Solution {
    public String minNumber(int[] nums) {
        // 把数字数组转换为字符串数据，便于比较拼接
        String[] strs = new String[nums.length];
        for(int i = 0; i < nums.length; i++)
            strs[i] = String.valueOf(nums[i]);
        
        // 对字符串数组内的字符进行快速排序
        quickSort(strs, 0, strs.length - 1);

        // 把经过快排后的字符串数组拼接起来即可
        StringBuilder res = new StringBuilder();
        for(String s : strs)
            res.append(s);

        // 返回结果
        return res.toString();
    }

    void quickSort(String[] arr, int left, int right) {
        if(left < right) {
            //得到第一次划分的哨兵位置
            int pivotPos = partition(arr,left,right);
            //左半边继续快速排序
            quickSort(arr,left,pivotPos-1);
            //右半边继续快速排序
            quickSort(arr,pivotPos+1,right);
          }
    }

    // 划分
    int partition(String[] arr, int left, int right) {
        // 哨兵
        String pivotStr = arr[left];
        // 双指针相遇时结束循环
        while (left < right) {
            // 首先移动右指针
            while (left < right && (arr[right] + pivotStr).compareTo(pivotStr + arr[right]) >= 0)
                right--;
            // 此时右指针指向的字符串要比哨兵小，所以放到left位置上
            arr[left] = arr[right];
            // 接着移动左指针
            while (left < right && (arr[left] + pivotStr).compareTo(pivotStr + arr[left]) <= 0)
                left++;
            // 此时左指针指向的字符串要比哨兵大，所以放到right位置上
            arr[right] = arr[left];
        }
        // 结束循环后，把哨兵放到正确的位置，此时左边的都比他小，右边的都比他大
        arr[left] = pivotStr;
        // 返回哨兵位置即可
        return left;
    }
}

```

### 4.2 复杂度分析

* 时间复杂度 `O(NlogN)` ：其中 N 是结果字符串的长度。使用快排或者内置函数平均时间复杂度为 `O(NlogN)` ，最差时间复杂度为 `O(N^2)` 。
* 空间复杂度 `O(N)` ：字符串占用了 `O(N)` 大小的额外存储空间。

## 5. 参考

* [https://leetcode-cn.com/problems/ba-shu-zu-pai-cheng-zui-xiao-de-shu-lcof/](https://leetcode-cn.com/problems/ba-shu-zu-pai-cheng-zui-xiao-de-shu-lcof/)
* [https://leetcode-cn.com/problems/ba-shu-zu-pai-cheng-zui-xiao-de-shu-lcof/solution/mian-shi-ti-45-ba-shu-zu-pai-cheng-zui-xiao-de-s-4/](https://leetcode-cn.com/problems/ba-shu-zu-pai-cheng-zui-xiao-de-shu-lcof/solution/mian-shi-ti-45-ba-shu-zu-pai-cheng-zui-xiao-de-s-4/)

