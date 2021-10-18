# LEETCODE 1014. 最佳观光组合

## [1. 问题](https://leetcode-cn.com/problems/best-sightseeing-pair/)

给定正整数数组 A，A\[i] 表示第 i 个观光景点的评分，并且两个景点 i 和 j 之间的距离为 j - i。

一对景点（i < j）组成的观光组合的得分为（A\[i] + A\[j] + i - j）：景点的评分之和减去它们两者之间的距离。

返回一对观光景点能取得的最高分。

示例：

> 输入：\[8,1,5,2,6] 输出：11 解释：i = 0, j = 2, A\[i] + A\[j] + i - j = 8 + 5 + 0 - 2 = 11

提示：

* 2 <= A.length <= 50000
* 1 <= A\[i] <= 1000

## 2. 解法

### 2.1 Java

```java
class Solution {
    public int maxScoreSightseeingPair(int[] A) {
        int res = 0;
        int preMax = A[0] + 0; //preMax = A[i] + i;
        for (int j=1;j<A.length;j++) {
            // res = A[i] + A[j] + i - j
            // res = A[i] + i + A[j] - j
            // res = preMax + (A[j] - j)
            res = Math.max(res, preMax + (A[j] - j));//不断更新最大结果
            // 更新j前面最大的A[i] + i
            preMax = Math.max(preMax, A[j] + j); //这个就是题中的A[i]+i
        }
        return res;
    }
}
```

### 2.2 Kotlin

```java
import kotlin.math.max
class Solution {
    fun maxScoreSightseeingPair(A: IntArray): Int {
        var res = 0
        var preMax = A[0] + 0 //preMax = A[i] + i
        for (j in 1..A.size-1) {
            // res = A[i] + A[j] + i - j
            // res = A[i] + i + A[j] - j
            // res = preMax + (A[j] - j)
            res = max(res, preMax + (A[j] - j))//不断更新最大结果
            // 更新j前面最大的A[i] + i
            preMax = max(preMax, A[j] + j) //这个就是题中的A[i]+i
        }
        return res
    }
}
```

## 3. 参考

* [https://leetcode-cn.com/problems/best-sightseeing-pair/](https://leetcode-cn.com/problems/best-sightseeing-pair/)
* [https://leetcode-cn.com/problems/best-sightseeing-pair/solution/zui-jia-guan-guang-zu-he-by-leetcode-solution/](https://leetcode-cn.com/problems/best-sightseeing-pair/solution/zui-jia-guan-guang-zu-he-by-leetcode-solution/)

## 4. 草稿

![](https://777blog.oss-cn-shanghai.aliyuncs.com/blog%20pic/leetcode1014.jpeg)
