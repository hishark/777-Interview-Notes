# LEETCODE 547. 省份数量

## 1. [问题](https://leetcode-cn.com/problems/number-of-provinces/)

有 n 个城市，其中一些彼此相连，另一些没有相连。如果城市 a 与城市 b 直接相连，且城市 b 与城市 c 直接相连，那么城市 a 与城市 c 间接相连。

省份 是一组直接或间接相连的城市，组内不含其他没有相连的城市。

给你一个 `n x n` 的矩阵 isConnected ，其中 `isConnected[i][j] = 1` 表示第 i 个城市和第 j 个城市直接相连，而 `isConnected[i][j] = 0` 表示二者不直接相连。

返回矩阵中 省份 的数量。

示例 1：

![](<../../../.gitbook/assets/image (56).png>)

```
输入：isConnected = [[1,1,0],[1,1,0],[0,0,1]]
输出：2
```

示例 2：

![](<../../../.gitbook/assets/image (57).png>)

```
输入：isConnected = [[1,0,0],[0,1,0],[0,0,1]]
输出：3
```

提示：

* `1 <= n <= 200 `
* `n == isConnected.length`
* `n == isConnected[i].length`
* `isConnected[i][j]` 为 1 或 0 
* `isConnected[i][i] == 1`
* `isConnected[i][j] == isConnected[j][i]`

## 2. 标签

* DFS
* BFS
* 连通分量

## 3. 解法 - DFS

### 3.1 Java

```java
class Solution {
    int cityNum = 0;
    int[][] isConnected;
    boolean[] visited;
    public int findCircleNum(int[][] isConnect) {
        isConnected = isConnect;
        // 城市的数量
        cityNum = isConnected.length;
        // 记录每个城市是否被访问过
        visited = new boolean[cityNum];
        // 省份的数量
        int provinces = 0;
        // 遍历所有的城市
        for (int i = 0; i < cityNum; i++) {
            // 如果当前城市没有访问过
            if (!visited[i]) {
                // 就从当前城市开始深搜，通过矩阵 isConnected 得到与该城市直接相连的城市有哪些
                dfs(i);
                // 把处于同一个连通分量中的所有城市都搜索完了，就得到了一个省份
                provinces++;
            }
        }
        return provinces;
    }

    // 计算和【下标为 i 的城市】直接相连的城市有哪些
    public void dfs(int i) {
        // 对当前城市i，遍历所有城市
        for (int j = 0; j < cityNum; j++) {
            // 如果i和j相连，且j还没有访问过
            if (isConnected[i][j] == 1 && !visited[j]) {
                // 先标记 j 已访问
                visited[j] = true; // 别忘记更新 visited
                // 然后再继续对 j 进行深搜
                dfs(j);
            }
        }
    }
}
```

### 3.2 复杂度分析

* 时间复杂度 `O(n^2)` ：其中 n 是城市的数量，需要遍历矩阵中的每个元素。
* 空间复杂度 `O(n)` ：需要使用数组 visited 记录每个城市是否被访问过，数组长度是 n，递归调用栈的深度不会超过 n。

## 4. 解法 - BFS

### 4.1 Java

```java
class Solution {
    public int findCircleNum(int[][] isConnected) {
        // 城市的数量
        int cityNum = isConnected.length;
        // 标记城市是否已访问
        boolean[] visited = new boolean[cityNum];
        // 省份的数量
        int provinces = 0;
        // 用于BFS的队列
        Queue<Integer> queue = new LinkedList<Integer>();
        // 遍历所有城市
        for (int i = 0; i < cityNum; i++) {
            // 如果当前城市未访问
            if (!visited[i]) { // 这个是大前提，没访问过才有进行下去的必要，别忘了这里
                // 把未访问的城市放入队列
                queue.offer(i);
                // 队列为空时结束循环
                while (!queue.isEmpty()) {
                    // 取出队头元素
                    int j = queue.poll();
                    // 标记为已访问
                    visited[j] = true; // 别忘记标记
                    // 开始对当前城市 j 周围的城市 k 进行遍历
                    for (int k = 0; k < cityNum; k++) {
                        // 找到一个没访问的就加入到队列中
                        if (isConnected[j][k] == 1 && !visited[k]) {
                            queue.offer(k);
                        }
                    }
                }
                // 队列为空时就成功找出了一个省份
                provinces++;
            }
        }
        // 返回即可
        return provinces;
    }
}
```

### 4.2 复杂度分析

* 时间复杂度 `O(n^2)` ：其中 n 是城市的数量，需要遍历矩阵中的每个元素。
* 空间复杂度 `O(n)` ：需要使用数组 visited 记录每个城市是否被访问过，数组长度是 n，使用队列的元素个数不会超过 n 个。

## 5. 参考

* [https://leetcode-cn.com/problems/number-of-provinces/](https://leetcode-cn.com/problems/number-of-provinces/)
* [https://leetcode-cn.com/problems/number-of-provinces/solution/sheng-fen-shu-liang-by-leetcode-solution-eyk0/](https://leetcode-cn.com/problems/number-of-provinces/solution/sheng-fen-shu-liang-by-leetcode-solution-eyk0/)
