# 40. 最小的k个数\#TODO

## 1. [问题](https://leetcode-cn.com/problems/zui-xiao-de-kge-shu-lcof/)

输入整数数组 `arr` ，找出其中最小的 `k` 个数。例如，输入4、5、1、6、2、7、3、8这8个数字，则最小的4个数字是1、2、3、4。

示例1：

```text
输入：arr = [3,2,1], k = 2
输出：[1,2] 或者 [2,1]
```

示例2：

```text
输入：arr = [0,1,2,1], k = 1
输出：[0]
```

限制：

* `0 <= k <= arr.length <= 10000`
* `0 <= arr[i] <= 10000`

## 2. 标签

* 堆
* 分治

### 3. 解法

### 3.1 Java

```java
// 会挨打，别这么做，我就先随便一提交OTZ
class Solution {
    public int[] getLeastNumbers(int[] arr, int k) {
        Arrays.sort(arr);
        int[] res = new int[k];
        for (int i=0;i<k;i++) {
            res[i] = arr[i];
        }
        return res;
    }
}
```

### 3.2 Kotlin

```kotlin

```

### 3.3 复杂度分析

* 时间复杂度 `O()` ：
* 空间复杂度 `O()` ：

## 4. 参考

* 1
* 2

