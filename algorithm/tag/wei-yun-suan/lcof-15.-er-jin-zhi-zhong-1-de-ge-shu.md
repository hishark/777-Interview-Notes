# LCOF 15. 二进制中1的个数

## 1. [问题](https://leetcode-cn.com/problems/er-jin-zhi-zhong-1de-ge-shu-lcof/)

请实现一个函数，输入一个整数，输出该数二进制表示中 1 的个数。例如，把 9 表示成二进制是 1001，有 2 位是 1。因此，如果输入 9，则该函数输出 2。

示例 1：

```text
输入：00000000000000000000000000001011
输出：3
解释：输入的二进制串 00000000000000000000000000001011 中，共有三位为 '1'。
```

示例 2：

```text
输入：00000000000000000000000010000000
输出：1
解释：输入的二进制串 00000000000000000000000010000000 中，共有一位为 '1'。
```

示例 3：

```text
输入：11111111111111111111111111111101
输出：31
解释：输入的二进制串 11111111111111111111111111111101 中，共有 31 位为 '1'。
```

## 2. 解法 - 逐位判断

### 2.1 Java

```java
public class Solution {
    public int hammingWeight(int n) {
        /**
         * 根据位运算的定义：
         *  1. 如果n&1=0，那么n二进制的最右位是0
         *  2. 如果n&1=1，那么n二进制的最右位是1
         */

        // n二进制中1的个数
        int num = 0;

        /**
         * 本题中n为无符号数，所以右移时使用无符号右移
         * 无符号右移：不管符号位，右移时往最左边补0即可
         */
        while(n != 0) {
            // 如果n的最右边是1，那么n&1=1，所以1的个数就加一
            // 如果n的最右边是0，那么n&1=0，所以1个个数不变
            num += n & 1;

            // 每次判断完最右位数字就将n右移一位
            n >>>= 1;            
        }

        return num;
    }
}
```

## 3. 解法 - 使用n&\(n−1\)

### 3.1 Java

```java
public class Solution {
    // you need to treat n as an unsigned value
    public int hammingWeight(int n) {
        // 利用 n&(n−1)
        // n       = 100100100000
        // n-1     = 100100011111
        // n&(n-1) = 100100000000
        // 所以n和n-1的&操作会消去n最右边的1
        // 只要算出n变为0总共做了几次&操作即可求解1的个数
        int num = 0;
        while (n != 0) {
            n = n & (n - 1);
            num++;
        }
        return num;
    }
}
```

### 3.2 复杂度分析

时间复杂度：O\(M\)

* n&\(n−1\)操作只有【减法】和【与】运算，占用O\(1\)；设M为二进制数字n中1的个数，那么需要循环M次（每次消去一个1），所以是O\(M\)。

空间复杂度：O\(1\)

* 变量ans占用常数空间。

## 4. 参考

* [https://leetcode-cn.com/problems/er-jin-zhi-zhong-1de-ge-shu-lcof/](https://leetcode-cn.com/problems/er-jin-zhi-zhong-1de-ge-shu-lcof/)
* [https://leetcode-cn.com/problems/er-jin-zhi-zhong-1de-ge-shu-lcof/solution/mian-shi-ti-15-er-jin-zhi-zhong-1de-ge-shu-wei-yun/](https://leetcode-cn.com/problems/er-jin-zhi-zhong-1de-ge-shu-lcof/solution/mian-shi-ti-15-er-jin-zhi-zhong-1de-ge-shu-wei-yun/)

