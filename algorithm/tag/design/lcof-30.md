# LCOF 30. 包含min函数的栈

## 1. [问题](https://leetcode-cn.com/problems/bao-han-minhan-shu-de-zhan-lcof/)

定义栈的数据结构，请在该类型中实现一个能够得到栈的最小元素的 min 函数在该栈中，调用 min、push 及 pop 的时间复杂度都是 O(1)。

示例:

```
MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.min();   --> 返回 -3.
minStack.pop();
minStack.top();      --> 返回 0.
minStack.min();   --> 返回 -2.
```

提示：

* 各函数的调用总次数不超过 20000 次

## 2. 解法

### 2.1 Java

```java
class MinStack {
    /**
     * A为主栈，用于存储所有的元素
     * B为辅助栈，用于存储最小数
     */
    Stack<Integer> stackA, stackB;

    // 对两个栈进行初始化
    public MinStack() {
        stackA = new Stack<>();
        stackB = new Stack<>();
    }

    public void push(int x) {
        stackA.push(x);
        // 如果B为空，或者x比B的栈顶元素小，就把x压入B栈
        if (stackB.empty() || x <= stackB.peek())
            stackB.push(x);
    }

    public void pop() {
        // 如果A的栈顶元素和B的栈顶元素（即当前的最小数）一致，那么A和B一起pop
        // 如果不一致，只要pop栈A中的栈顶元素即可，因为最小数此时没有发生改变
        //  注意：这里要用「equals」不能用「==」，仅当整数值处于[-128,127]之间可以使用「==」比较
        if (stackA.pop().equals(stackB.peek()))
            stackB.pop();
    }

    public int top() {
        return stackA.peek();
    }

    public int min() {
        return stackB.peek();
    }
}

/**
 * Your MinStack object will be instantiated and called as such:
 * MinStack obj = new MinStack();
 * obj.push(x);
 * obj.pop();
 * int param_3 = obj.top();
 * int param_4 = obj.min();
 */
```

### 2.2 Kotlin

```kotlin
class MinStack {
    /**
     * A为主栈，用于存储所有的元素
     * B为辅助栈，用于存储最小数
     */
    var stackA: Stack<Int>
    var stackB: Stack<Int>

    // 对两个栈进行初始化
    init {
        stackA = Stack()
        stackB = Stack()
    }

    fun push(x: Int) {
        stackA.push(x)
        // 如果B为空，或者x比B的栈顶元素小，就把x压入B栈
        if (stackB.empty() || x <= stackB.peek())
            stackB.push(x)
    }

    fun pop() {
        // 如果A的栈顶元素和B的栈顶元素（即当前的最小数）一致，那么A和B一起pop
        // 如果不一致，只要pop栈A中的栈顶元素即可，因为最小数此时没有发生改变
        if (stackA.pop() == stackB.peek())
            stackB.pop()
    }

    fun top(): Int {
        return stackA.peek()
    }

    fun min(): Int {
        return stackB.peek()
    }
}

/**
 * Your MinStack object will be instantiated and called as such:
 * var obj = MinStack()
 * obj.push(x)
 * obj.pop()
 * var param_3 = obj.top()
 * var param_4 = obj.min()
 */
```

### 2.3 复杂度分析

* 时间复杂度 `O(1)` ： push(), pop(), top(), min() 四个函数的时间复杂度都属于常数级别。
* 空间复杂度 `O(N)` ：辅助栈 B 最差情况下存储 N 个元素，需要使用 `O(N)` 的额外空间。

## 3. 参考

* [https://leetcode-cn.com/problems/bao-han-minhan-shu-de-zhan-lcof/](https://leetcode-cn.com/problems/bao-han-minhan-shu-de-zhan-lcof/)
* [https://leetcode-cn.com/problems/bao-han-minhan-shu-de-zhan-lcof/solution/mian-shi-ti-30-bao-han-minhan-shu-de-zhan-fu-zhu-z/](https://leetcode-cn.com/problems/bao-han-minhan-shu-de-zhan-lcof/solution/mian-shi-ti-30-bao-han-minhan-shu-de-zhan-fu-zhu-z/)
