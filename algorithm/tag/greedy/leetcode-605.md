# LEETCODE 605. 种花问题

## 1. [问题](https://leetcode-cn.com/problems/can-place-flowers/)

假设你有一个很长的花坛，一部分地块种植了花，另一部分却没有。可是，花卉不能种植在相邻的地块上，它们会争夺水源，两者都会死去。

给定一个花坛（表示为一个数组包含0和1，其中0表示没种植花，1表示种植了花），和一个数 n 。能否在不打破种植规则的情况下种入 n 朵花？能则返回True，不能则返回False。

**示例 1:**

```text
输入: flowerbed = [1,0,0,0,1], n = 1
输出: True
```

**示例 2:**

```text
输入: flowerbed = [1,0,0,0,1], n = 2
输出: False
```

**注意:**

1. 数组内已种好的花不会违反种植规则。
2. 输入的数组长度范围为 \[1, 20000\]。
3. **n** 是非负整数，且不会超过输入数组的大小。

## 2. 标签

* 贪心

## 3. 解法 - 贪心

### 3.1 Java

```java
public class Solution {
    public boolean canPlaceFlowers(int[] flowerbed, int n) {
        // 可以种花的数目
        int count = 0;
        // 从左到右扫描数组
        for (int i=0;i<flowerbed.length;i++) {
            // 如果数组中有一个 0，并且这个 0 的左右两侧都是 0，那么就可以在这个位置种花
            // 对于头尾只需要考虑一侧是否是 0 即可
            // 官方题解这个判断条件写的太优秀了OTZ
            if (flowerbed[i] == 0 && (i == 0 || flowerbed[i - 1] == 0) && (i == flowerbed.length - 1 || flowerbed[i + 1] == 0)) {
                flowerbed[i] = 1;
                count++;
            }
        }
        // 最后比较一下大小即可，只要 count 大于等于 n 都说明可以种下 n 朵花
        return count >= n;
    }
}
```

### 3.2 复杂度分析

* 时间复杂度 `O(N)` ：其中 N 是数组的长度。
* 空间复杂度 `O(1)` ：仅使用常数大小的空间。

## 4. 参考

* [https://leetcode-cn.com/problems/can-place-flowers/](https://leetcode-cn.com/problems/can-place-flowers/)
* [https://leetcode-cn.com/problems/can-place-flowers/solution/chong-hua-wen-ti-by-leetcode/](https://leetcode-cn.com/problems/can-place-flowers/solution/chong-hua-wen-ti-by-leetcode/)

