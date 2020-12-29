# LCOF 59 - II. 队列的最大值

## 1. [问题](https://leetcode-cn.com/problems/dui-lie-de-zui-da-zhi-lcof/)

请定义一个队列并实现函数 max\_value 得到队列里的最大值，要求函数max\_value、push\_back 和 pop\_front 的均摊时间复杂度都是O\(1\)。

若队列为空，pop\_front 和 max\_value 需要返回 -1

**示例 1：**

```text
输入: 
["MaxQueue","push_back","push_back","max_value","pop_front","max_value"]
[[],[1],[2],[],[],[]]
输出: [null,null,null,2,1,2]
```

**示例 2：**

```text
输入: 
["MaxQueue","pop_front","max_value"]
[[],[],[]]
输出: [null,-1,-1]
```

**限制：**

* `1 <= push_back,pop_front,max_value的总操作数 <= 10000`
* `1 <= value <= 10^5`

## 2. 标签

* 队列
* 设计

## 3. 解法

### 3.1 Java

```java
class MaxQueue {
    // 维护一个单调递减的双端队列（队头永远是最大值）
    Deque<Integer> deque;
    // 使用一个辅助队列来记录所有被插入的值
    Queue<Integer> queue;

    public MaxQueue() {
        deque = new LinkedList<Integer>();
        queue = new LinkedList<Integer>();
    }
    
    // 求最大值
    public int max_value() {
        // 队列为空，返回 -1
        if (deque.isEmpty())
            return -1;
        // 返回队头元素，即双端队列中的最大值
        return deque.peekFirst();
    }
    
    // 插入
    public void push_back(int value) {
        // 当双端队列不为空，且队尾取出的值比 value 小的时候，不停的让队尾元素出队
        // 由于有辅助队列的存在，所以不用担心丢失这些比 value 小的元素
        while(!deque.isEmpty() && deque.peekLast() < value) 
            deque.pollLast();
        
        // 让双端队列中所有比 value 小的元素出队后，就将 value 插入队尾
        // 由此来保持双端队列的单调递减
        deque.offerLast(value);
        // 使用辅助队列来记录所有被插入的值
        queue.offer(value);
    }
   
    // 删除
    public int pop_front() {
        // 如果队列为空，返回 -1
        if (queue.isEmpty())
            return -1;
        
        // 取出辅助队列的队头元素
        int ans = queue.poll();
        // 如果该元素等于双端队列的最大值，也同时取出双端队列中的队头元素
        // 如果该元素不是双端队列中的最大值，可以不用管它
        // 单调递减的双端队列的存在只是为了便于求解最大值
        if (ans == deque.peekFirst())
            deque.pollFirst();

        // 返回删除的元素
        return ans;
    }
}

/**
 * Your MaxQueue object will be instantiated and called as such:
 * MaxQueue obj = new MaxQueue();
 * int param_1 = obj.max_value();
 * obj.push_back(value);
 * int param_3 = obj.pop_front();
 */
```

### 3.2 Kotlin

```kotlin
class MaxQueue {
    // 维护一个单调递减的双端队列（队头永远是最大值）
    var deque: Deque<Int>
    // 使用一个辅助队列来记录所有被插入的值
    var queue: Queue<Int>

    init {
        deque = LinkedList()
        queue = LinkedList()
    }

    // 求最大值
    fun max_value(): Int {
        // 队列为空，返回 -1
        return if (deque.isEmpty()) -1 else deque.peekFirst()
        // 返回队头元素，即双端队列中的最大值
    }

    // 插入
    fun push_back(value: Int) {
        // 当双端队列不为空，且队尾取出的值比 value 小的时候，不停的让队尾元素出队
        // 由于有辅助队列的存在，所以不用担心丢失这些比 value 小的元素
        while (!deque.isEmpty() && deque.peekLast() < value)
            deque.pollLast()

        // 让双端队列中所有比 value 小的元素出队后，就将 value 插入队尾
        // 由此来保持双端队列的单调递减
        deque.offerLast(value)
        // 使用辅助队列来记录所有被插入的值
        queue.offer(value)
    }

    // 删除
    fun pop_front(): Int {
        // 如果队列为空，返回 -1
        if (queue.isEmpty())
            return -1

        // 取出辅助队列的队头元素
        val ans = queue.poll()
        // 如果该元素等于双端队列的最大值，也同时取出双端队列中的队头元素
        // 如果该元素不是双端队列中的最大值，可以不用管它
        // 单调递减的双端队列的存在只是为了便于求解最大值
        if (ans == deque.peekFirst())
            deque.pollFirst()

        // 返回删除的元素
        return ans
    }
}

/**
 * Your MaxQueue object will be instantiated and called as such:
 * var obj = MaxQueue()
 * var param_1 = obj.max_value()
 * obj.push_back(value)
 * var param_3 = obj.pop_front()
 */
```

### 3.3 复杂度分析

* 时间复杂度 `O(1)` ：删除和求最大值显然为 `O(1)`。做一次插入操作最多会有 n 次出队操作，但是由于每个数字只会出队一次，所以将出队的时间均摊到每个插入操作上，时间复杂度也为 `O(1)`。
* 空间复杂度 `O(n)` ：队列占用了 `O(n)` 的额外存储空间。

## 4. 参考

* [https://leetcode-cn.com/problems/dui-lie-de-zui-da-zhi-lcof/](https://leetcode-cn.com/problems/dui-lie-de-zui-da-zhi-lcof/)
* [https://leetcode-cn.com/problems/dui-lie-de-zui-da-zhi-lcof/solution/mian-shi-ti-59-ii-dui-lie-de-zui-da-zhi-by-leetcod/](https://leetcode-cn.com/problems/dui-lie-de-zui-da-zhi-lcof/solution/mian-shi-ti-59-ii-dui-lie-de-zui-da-zhi-by-leetcod/)

