# LCOF 46. 把数字翻译成字符串

## [1. 问题](https://leetcode-cn.com/problems/ba-shu-zi-fan-yi-cheng-zi-fu-chuan-lcof/)

给定一个数字，我们按照如下规则把它翻译为字符串：0 翻译成 “a” ，1 翻译成 “b”，……，11 翻译成 “l”，……，25 翻译成 “z”。一个数字可能有多个翻译。请编程实现一个函数，用来计算一个数字有多少种不同的翻译方法。

示例 1:

> 输入: 12258 输出: 5 解释: 12258有5种不同的翻译，分别是"bccfi", "bwfi", "bczi", "mcfi"和"mzi"

提示：

*  $$0 \leq num < 2^{31}$$ 

## 2. 解法 - 动态规划

### 2.1 Java

```java
    class Solution {
    public int translateNum(int num) {
        // 使用一个字符串将整个数字存下来
        String str = String.valueOf(num);
        int n = str.length();

        // 状态数组
        // dp[i]表示以第i个数字结尾的数字的翻译方案的数量
        int[] dp = new int[n+1];

        // 边界值
        dp[1] = 1; //只有一个数字时，翻译方案显然为1
        dp[0] = 1; //若前两个数字可以合并翻译，那么dp[2]=dp[0]+dp[1], 由于dp[1]=1所以dp[0]=0  

        // 遍历字符串
        for (int i=2;i<=n;i++) {
            // 取出第i-1个数字和第i个数字
            // substring: [i, j) 左闭右开
            // dp数组中，数字的下标是从1开始的
            // 但是字符串的下标是从0开始的，所以这里应该是(i-2, i)
            String curNum = str.substring(i-2, i); 

            // 计算dp[i]，如果第i-1和第i个数字可以合并翻译就：
            if(curNum.compareTo("10")>=0 && curNum.compareTo("25")<=0) {
                dp[i] = dp[i-1] + dp[i-2];
            } else {//如果第i-1和第i个数字不可以合并翻译就：
                dp[i] = dp[i-1];
            }
        }

        return dp[n];
    }
}
```

### 2.2 Kotlin

```kotlin
class Solution {
    fun translateNum(num: Int): Int {
        // 使用一个字符串将整个数字存下来
        var str = num.toString()
        var n = str.length

        // 状态数组
        // dp[i]表示以第i个数字结尾的数字的翻译方案的数量
        var dp = IntArray(n+1)

        // 边界值
        dp[1] = 1 //只有一个数字时，翻译方案显然为1
        dp[0] = 1 //若前两个数字可以合并翻译，那么dp[2]=dp[0]+dp[1], 由于dp[1]=1所以dp[0]=0  

        // 遍历字符串
        for (i in 2..n) {
            // 取出第i-1个数字和第i个数字
            // substring: [i, j) 左闭右开
            // dp数组中，数字的下标是从1开始的
            // 但是字符串的下标是从0开始的，所以这里应该是(i-2, i)
            var curNum = str.substring(i-2, i)

            // 计算dp[i]，如果第i-1和第i个数字可以合并翻译就：
            dp[i] = if(curNum.compareTo("10")>=0 && curNum.compareTo("25")<=0) {
                dp[i-1] + dp[i-2]
            } else {//如果第i-1和第i个数字不可以合并翻译就：
                dp[i-1]
            }
        }

        return dp[n]
    }
}
```

## 3. 参考

* [《剑指 Offer（第 2 版）》：面试题46. 把数字翻译成字符串](https://leetcode-cn.com/problems/ba-shu-zi-fan-yi-cheng-zi-fu-chuan-lcof)
* [Krahets：面试题46. 把数字翻译成字符串（动态规划，清晰图解）](https://leetcode-cn.com/problems/ba-shu-zi-fan-yi-cheng-zi-fu-chuan-lcof/solution/mian-shi-ti-46-ba-shu-zi-fan-yi-cheng-zi-fu-chua-6/)

## 4. 学习草稿

![](../../../.gitbook/assets/image%20%2827%29.png)

