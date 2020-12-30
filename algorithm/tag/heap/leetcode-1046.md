# LEETCODE 1046. 最后一块石头的重量

## 1. [问题](https://leetcode-cn.com/problems/last-stone-weight/)

有一堆石头，每块石头的重量都是正整数。

每一回合，从中选出两块最重的石头，然后将它们一起粉碎。假设石头的重量分别为 x 和 y，且 x &lt;= y。那么粉碎的可能结果如下：

* 如果 x == y，那么两块石头都会被完全粉碎； 
* 如果 x != y，那么重量为 x 的石头将会完全粉碎，而重量为 y 的石头新重量为 y-x。 

最后，最多只会剩下一块石头。返回此石头的重量。如果没有石头剩下，就返回 0。

**示例：**

```text
输入：[2,7,4,1,8,1]
输出：1
解释：
先选出 7 和 8，得到 1，所以数组转换为 [2,4,1,1,1]，
再选出 2 和 4，得到 2，所以数组转换为 [2,1,1,1]，
接着是 2 和 1，得到 1，所以数组转换为 [1,1,1]，
最后选出 1 和 1，得到 0，最终数组转换为 [1]，这就是最后剩下那块石头的重量。
```

**提示：**

1. `1 <= stones.length <= 30`
2. `1 <= stones[i] <= 1000`

## 2. 标签

* 贪心
* 堆

## 3. 解法 - 堆

### 3.1 Java

```java
class Solution {
    public int lastStoneWeight(int[] stones) {
        // PriorityQueue 默认为小顶堆，所以需要重写 Comparator，变成大顶堆
        PriorityQueue<Integer> queue = new PriorityQueue<Integer>((x, y) -> y - x);
        // 把所有石头塞进大顶堆里
        for (int stone : stones) {
            queue.offer(stone);
        }
        // 堆里小于等于1个石头时，停止循环
        while (queue.size() > 1) {
            // 取出堆顶石头，也就是最重的石头
            int stone1 = queue.poll();
            // 取出堆顶石头，也就是次重的石头
            int stone2 = queue.poll();
            // 如果二者不相等，把差值再放回堆里
            // 如果二者相等，都扔出去
            if (stone1 > stone2) {
                queue.offer(stone1 - stone2);
            }
        }
        // 此时判断堆是否为空即可
        return queue.isEmpty() ? 0 : queue.poll();
    }
}
```

### 3.2 复杂度分析

* 时间复杂度 `O(nlogn)` ：其中 n 是石头数量。每次从队列中取出元素需要花费 `O(logn)` 的时间，最多共需要粉碎 n 次石头。
* 空间复杂度 `O(n)` ：使用了一个 `PriorityQueue` 存放所有石头。

## 4. 参考

* [https://leetcode-cn.com/problems/last-stone-weight](https://leetcode-cn.com/problems/last-stone-weight)
* [https://leetcode-cn.com/problems/last-stone-weight/solution/zui-hou-yi-kuai-shi-tou-de-zhong-liang-b-xgsx/](https://leetcode-cn.com/problems/last-stone-weight/solution/zui-hou-yi-kuai-shi-tou-de-zhong-liang-b-xgsx/)

