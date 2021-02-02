# LEETCODE 888. 公平的糖果棒交换

## 1. [问题](https://leetcode-cn.com/problems/fair-candy-swap/)

爱丽丝和鲍勃有不同大小的糖果棒：A\[i\] 是爱丽丝拥有的第 i 根糖果棒的大小，B\[j\] 是鲍勃拥有的第 j 根糖果棒的大小。

因为他们是朋友，所以他们想交换一根糖果棒，这样交换后，他们都有相同的糖果总量。（一个人拥有的糖果总量是他们拥有的糖果棒大小的总和。）

返回一个整数数组 ans，其中 ans\[0\] 是爱丽丝必须交换的糖果棒的大小，ans\[1\] 是 Bob 必须交换的糖果棒的大小。

如果有多个答案，你可以返回其中任何一个。保证答案存在。

示例 1：

```text
输入：A = [1,1], B = [2,2]
输出：[1,2]
```

示例 2：

```text
输入：A = [1,2], B = [2,3]
输出：[1,2]
```

示例 3：

```text
输入：A = [2], B = [1,3]
输出：[2,3]
```

示例 4：

```text
输入：A = [1,2,5], B = [2,4]
输出：[5,4]
```

提示：

* 1 &lt;= A.length &lt;= 10000 
* 1 &lt;= B.length &lt;= 10000 
* 1 &lt;= A\[i\] &lt;= 100000 
* 1 &lt;= B\[i\] &lt;= 100000 
* 保证爱丽丝与鲍勃的糖果总量不同。 
* 答案肯定存在。

## 2. 标签

* 数组
* 哈希表

## 3. 解法 - 哈希表

### 3.1 Java

```java
class Solution {
    public int[] fairCandySwap(int[] A, int[] B) {
        // 数组 A 中数字的总和
        int sumA = Arrays.stream(A).sum();
        // 数组 B 中数字的总和
        int sumB = Arrays.stream(B).sum();
        
        // 对一个可行解(x,y)，他们的差值应该为 delta。（公式推导见 ref）
        int delta = (sumA - sumB) / 2;
        // 为了快速查询 A 中是否存在某个数字，先把数字全部存入哈希表
        // 然后再遍历 B，在哈希表中查询是否有差值为 delta 的数字
        Set<Integer> set = new HashSet<Integer>();

        // 遍历 A，存入哈希表
        // set 会自动去重
        for (int num : A) {
            set.add(num);
        }

        // 一个可行解
        int[] ans = new int[2];

        // 遍历 B 中的数字 y，查找哈希表中是否存在一个数字 x 与 y 差值为 delta
        for (int y : B) {
            // 先将 y 加上差值 delta，假设一个 x
            int x = y + delta;
            // 再判断哈希表里是否存在
            if (set.contains(x)) {
                // 若存在，找到一个可行解，886
                ans[0] = x;
                ans[1] = y;
                break;
            }
        }
        return ans;
    }
}
```

### 3.2 复杂度分析

* 时间复杂度 `O(n+m)` ：其中 n 是序列 A 的长度，m 是序列 B 的长度。
* 空间复杂度 `O(n)` ：需要建立一个和序列 A 等长的哈希表。

## 4. 参考

* [https://leetcode-cn.com/problems/fair-candy-swap/](https://leetcode-cn.com/problems/fair-candy-swap/)
* [https://leetcode-cn.com/problems/fair-candy-swap/solution/gong-ping-de-tang-guo-jiao-huan-by-leetc-tlam/](https://leetcode-cn.com/problems/fair-candy-swap/solution/gong-ping-de-tang-guo-jiao-huan-by-leetc-tlam/)

