# LEETCODE 338. 比特位计数

## [1. 问题](https://leetcode-cn.com/problems/counting-bits/)

给定一个非负整数 num。对于 0 ≤ i ≤ num 范围中的每个数字 i ，计算其二进制数中的 1 的数目并将它们作为数组返回。

示例 1:

> 输入: 2 输出: \[0,1,1] 

示例 2:

> 输入: 5 输出: \[0,1,1,2,1,2]

进阶:

* 给出时间复杂度为O(n\*sizeof(integer))的解答非常容易。但你可以在线性时间O(n)内用一趟扫描做到吗？
* 要求算法的空间复杂度为O(n)。
* 你能进一步完善解法吗？要求在C++或任何其他语言中不使用任何内置函数（如 C++ 中的 \__builtin_popcount）来执行此操作。

## 2. 解法-位运算

### Java

```java
class Solution {
    public int[] countBits(int num) {
        int[] ans = new int[num+1];
        ans[0] = 0;

        for (int i=1;i<=num;i++) {
            ans[i] = count(i);
        }
        return ans;
    }

    public int count(int n) {
        int cnt = 0;
        while (n!=0) {
            n = n & (n-1);
            cnt++;
        }
        return cnt;
    }
}
```

## 3. 参考

* [https://leetcode-cn.com/problems/counting-bits/](https://leetcode-cn.com/problems/counting-bits/)
* [https://leetcode-cn.com/problems/counting-bits/solution/bi-te-wei-ji-shu-by-leetcode/](https://leetcode-cn.com/problems/counting-bits/solution/bi-te-wei-ji-shu-by-leetcode/)

## 4. 笔记

![](https://777blog.oss-cn-shanghai.aliyuncs.com/blog%20pic/leetcode338.JPEG)
