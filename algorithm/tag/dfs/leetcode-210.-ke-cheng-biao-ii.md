# \*LEETCODE 210. 课程表 II

## 1. [问题](https://leetcode-cn.com/problems/course-schedule-ii/)

现在你总共有 n 门课需要选，记为 0 到 n-1。

在选修某些课程之前需要一些先修课程。 例如，想要学习课程 0 ，你需要先完成课程 1 ，我们用一个匹配来表示他们: \[0,1\]

给定课程总量以及它们的先决条件，返回你为了学完所有课程所安排的学习顺序。

可能会有多个正确的顺序，你只要返回一种就可以了。如果不可能完成所有课程，返回一个空数组。

示例 1:

```text
输入: 2, [[1,0]] 
输出: [0,1]
解释: 总共有 2 门课程。要学习课程 1，你需要先完成课程 0。因此，正确的课程顺序为 [0,1] 。
```

示例 2:

```text
输入: 4, [[1,0],[2,0],[3,1],[3,2]]
输出: [0,1,2,3] or [0,2,1,3]
解释: 总共有 4 门课程。要学习课程 3，你应该先完成课程 1 和课程 2。并且课程 1 和课程 2 都应该排在课程 0 之后。
     因此，一个正确的课程顺序是 [0,1,2,3] 。另一个正确的排序是 [0,2,1,3] 。
```

说明:

* 输入的先决条件是由边缘列表表示的图形，而不是邻接矩阵。详情请参见[图的表示法](http://blog.csdn.net/woaidapaopao/article/details/51732947)。 
* 你可以假定输入的先决条件中没有重复的边。 

提示:

* 这个问题相当于查找一个循环是否存在于有向图中。如果存在循环，则不存在拓扑排序，因此不可能选取所有课程进行学习。 
* [通过 DFS 进行拓扑排序](https://www.coursera.org/specializations/algorithms) - 一个关于Coursera的精彩视频教程（21分钟），介绍拓扑排序的基本概念。 
* 拓扑排序也可以通过 BFS 完成。

## 2. 标签

* DFS
* BFS
* 图
* 拓扑排序

## 3. 解法 - DFS

### 3.1 Java

```java
class Solution {
    // 存储有向图
    List<List<Integer>> edges;
    // 标记每个节点的状态：0=未搜索，1=搜索中，2=已完成
    int[] visited;
    // 用数组来模拟栈，下标 n-1 为栈底，0 为栈顶
    int[] stack;
    // 判断有向图中是否有环
    // 初始状态：无环
    boolean existCycle = false;
    // 栈下标
    int index;

    // 找到拓扑排序
    public int[] findOrder(int numCourses, int[][] prerequisites) {
        // 初始化
        edges = new ArrayList<List<Integer>>();
        for (int i = 0; i < numCourses; ++i) {
            edges.add(new ArrayList<Integer>());
        }
        // 初始化
        visited = new int[numCourses];

        // 栈中存储的即为拓扑排序
        stack = new int[numCourses];

        // 栈下标
        index = numCourses - 1;

        // 遍历所有的匹配
        for (int[] info : prerequisites) {
            // 根据匹配构建出有向图
            // info[1] 指向 info[0]
            edges.get(info[1]).add(info[0]);
        }

        // 遍历所有节点，每次挑选一个「未搜索」的节点，开始进行深度优先搜索
        for (int i = 0; i < numCourses && !existCycle; i++) {
            // 
            if (visited[i] == 0) {
                dfs(i);
            }
        }

        // 如果存在环，返回空
        if (existCycle) {
            return new int[0];
        }

        // 如果不存在环，那么就存在拓扑排序
        return stack;
    }

    // 深度优先搜索
    public void dfs(int u) {
        // 首先将节点标记为「搜索中」
        visited[u] = 1;

        // 根据有向图 edges 遍历当前节点的相邻节点
        for (int v: edges.get(u)) {
            // 如果相邻节点「未搜索」那么就对相邻节点进行搜索
            if (visited[v] == 0) {
                dfs(v);
                // 一旦发现有环，就立刻停止遍历
                if (existCycle)
                    return;
            }
            // 如果相邻节点处于「搜索中」说明找到了环
            // u 在搜索相邻结点，所以 u 指向 v
            // 如果 v 也处于搜索中，说明 v 也在搜索相邻结点，所以 v 指向 u
            // 从而构成环
            else if (visited[v] == 1) {
                existCycle = true;
                return;
            }
        }
        // 当 u 的所有相邻结点都为「已完成」时，将 u 放入栈中，并标记为「已完成」
        visited[u] = 2;
        // 将节点入栈，组成拓扑排序
        stack[index--] = u;
    }
}
```

### 3.2 复杂度分析

* 时间复杂度 `O(n+m)` ：其中 n 为课程数，m 为先修课程的要求数。O\(n+m\) 即对图进行深度优先搜索的时间复杂度。
* 空间复杂度 `O(n+m)` ：

## 4. 解法 - BFS

### 4.1 Java

```java

```

### 4.2 复杂度分析

* 时间复杂度 `O()` ：
* 空间复杂度 `O()` ：

## 5. 参考

* [https://leetcode-cn.com/problems/course-schedule-ii/](https://leetcode-cn.com/problems/course-schedule-ii/)
* [https://leetcode-cn.com/problems/course-schedule-ii/solution/ke-cheng-biao-ii-by-leetcode-solution/](https://leetcode-cn.com/problems/course-schedule-ii/solution/ke-cheng-biao-ii-by-leetcode-solution/)

