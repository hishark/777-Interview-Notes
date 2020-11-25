# lcof-09.-yong-liang-ge-zhan-shi-xian-dui-lie

## [1. 问题](https://leetcode-cn.com/problems/yong-liang-ge-zhan-shi-xian-dui-lie-lcof/)

用两个栈实现一个队列。队列的声明如下，请实现它的两个函数 appendTail 和 deleteHead ，分别完成在队列尾部插入整数和在队列头部删除整数的功能。\(若队列中没有元素，deleteHead 操作返回 -1 \)

示例 1：

> 输入： \["CQueue","appendTail","deleteHead","deleteHead"\] \[\[\],\[3\],\[\],\[\]\] 输出：\[null,null,3,-1\]

示例 2：

> 输入： \["CQueue","deleteHead","appendTail","appendTail","deleteHead","deleteHead"\] \[\[\],\[\],\[5\],\[2\],\[\],\[\]\] 输出：\[null,-1,null,null,5,2\]

提示：

* 1 &lt;= values &lt;= 10000
* 最多会对 appendTail、deleteHead 进行 10000 次调用

## 2. 解法 - 辅助栈

### 2.1 Java

```java
/**
 * Your CQueue object will be instantiated and called as such:
 * CQueue obj = new CQueue();
 * obj.appendTail(value);
 * int param_2 = obj.deleteHead();
 */
class CQueue {
    // 辅助栈
    Stack<Integer> stackIn;
    Stack<Integer> stackOut;

    public CQueue() {
        stackIn = new Stack<Integer>();
        stackOut = new Stack<Integer>();
    }

    public void appendTail(int value) {
        stackIn.push(value);
    }

    public int deleteHead() {
        if(stackIn.empty() && stackOut.empty())
            return -1;

        // out栈不为空，就先pop
        if(!stackOut.empty())
            return stackOut.pop();
        else{
            // 先把in栈的全部pop到out栈中
            while(!stackIn.empty()){
                stackOut.push(stackIn.pop());
            }
            return stackOut.pop();
        }
    }
}
```

## 3. 参考

* [https://leetcode-cn.com/problems/yong-liang-ge-zhan-shi-xian-dui-lie-lcof](https://leetcode-cn.com/problems/yong-liang-ge-zhan-shi-xian-dui-lie-lcof)
* [https://leetcode-cn.com/problems/yong-liang-ge-zhan-shi-xian-dui-lie-lcof/solution/mian-shi-ti-09-yong-liang-ge-zhan-shi-xian-dui-l-3/](https://leetcode-cn.com/problems/yong-liang-ge-zhan-shi-xian-dui-lie-lcof/solution/mian-shi-ti-09-yong-liang-ge-zhan-shi-xian-dui-l-3/)

## 4. 笔记

![](../../../.gitbook/assets/image%20%2825%29.png)

