# LEETCODE 461. 汉明距离

## 1. [问题](https://leetcode-cn.com/problems/hamming-distance/)

两个整数之间的汉明距离指的是这两个数字对应二进制位不同的位置的数目。

给出两个整数 x 和 y，计算它们之间的汉明距离。

注意： 0 ≤ x, y < 231.

示例:

```
输入: x = 1, y = 4

输出: 2

解释:
1   (0 0 0 1)
4   (0 1 0 0)
       ↑   ↑

上面的箭头指出了对应二进制位不同的位置。
```

## 2. 标签

* 位运算

## 3. 解法 - 位运算

### 3.1 Java

```java
class Solution {
    public int hammingDistance(int x, int y) {
        // 异或值
        int xor = x ^ y;
        // 汉明距离
        int distance = 0;
        // 如果异或值为0，那么两个数字完全一致，不需要再计算
        while (xor != 0) {
            // 逐位判断异或值的每一位
            // 如果是1，说明原来两个数字的对应二进制位不同
            if (xor % 2 == 1)
                distance += 1;
            // 每判断完一位就右移一位
            xor = xor >> 1;
        }
        // 返回即可
        return distance;
    }
}
```

### 3.2 复杂度分析

* 时间复杂度 `O(1)` 
* 空间复杂度 `O(1)` 

## 4. 参考

* [https://leetcode-cn.com/problems/hamming-distance/](https://leetcode-cn.com/problems/hamming-distance/)
* [https://leetcode-cn.com/problems/hamming-distance/solution/yi-ming-ju-chi-by-leetcode/](https://leetcode-cn.com/problems/hamming-distance/solution/yi-ming-ju-chi-by-leetcode/)
