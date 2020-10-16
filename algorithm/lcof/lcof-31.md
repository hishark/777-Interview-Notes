---
title: 31. 栈的压入、弹出序列
date: '2020-10-12T23:16:20.000Z'
tags:
  - leetcode
  - lcof
  - java
  - 栈
  - kotlin
categories: 算法笔记
---

# 31. 栈的压入、弹出序列

## 1. [问题](https://leetcode-cn.com/problems/zhan-de-ya-ru-dan-chu-xu-lie-lcof)

输入两个整数序列，第一个序列表示栈的压入顺序，请判断第二个序列是否为该栈的弹出顺序。假设压入栈的所有数字均不相等。例如，序列 {1,2,3,4,5} 是某栈的压栈序列，序列 {4,5,3,2,1} 是该压栈序列对应的一个弹出序列，但 {4,3,5,1,2} 就不可能是该压栈序列的弹出序列。

示例 1：

```text
输入：pushed = [1,2,3,4,5], popped = [4,5,3,2,1]
输出：true
解释：我们可以按以下顺序执行：
push(1), push(2), push(3), push(4), pop() -> 4,
push(5), pop() -> 5, pop() -> 3, pop() -> 2, pop() -> 1
```

示例 2：

```text
输入：pushed = [1,2,3,4,5], popped = [4,3,5,1,2]
输出：false
解释：1 不能在 2 之前弹出。
```

提示：

1. 0 &lt;= pushed.length == popped.length &lt;= 1000
2. 0 &lt;= pushed\[i\], popped\[i\] &lt; 1000
3. pushed 是 popped 的排列。

## 2. 解法

### 2.1 Java

```java
class Solution {
    public boolean validateStackSequences(int[] pushed, int[] popped) {
        // 题目提示说「pushed 是 popped 的排列」，说明我们不需要考虑两个序列「长度不同」或者「元素不同」的情况
        // 借助一个辅助栈模拟压入和弹出操作
        Stack<Integer> stack = new Stack<>();

        // 工具人i
        int i = 0;

        // 遍历入栈序列
        for (int num: pushed) {
            // 把入栈序列pushed的当前元素放入辅助栈stack
            stack.push(num);
            // 循环判断「stack栈顶元素 == popped序列的当前元素」是否成立
            while(!stack.isEmpty() && stack.peek() == popped[i]) {
                // 如果成立的话，就把该元素弹出辅助栈 stack，这样就完成了一次出入栈模拟操作
                // 发射！
                stack.pop();
                // 每成功模拟一次出入栈操作，才能将 i 自增
                i++;
            }
        }
        // 如果最后辅助栈为空，说明模拟出入栈操作成功。
        // 如果不为空，说明模拟失败。
        return stack.isEmpty();
    }
}
```

### 2.2 Kotlin

```kotlin
class Solution {
    fun validateStackSequences(pushed: IntArray, popped: IntArray): Boolean {
        // 题目提示说「pushed 是 popped 的排列」，说明我们不需要考虑两个序列「长度不同」或者「元素不同」的情况
        // 借助一个辅助栈模拟压入和弹出操作
        val stack = Stack<Int>()

        // 工具人i
        var i = 0

        // 遍历入栈序列
        for (num in pushed) {
            // 把入栈序列pushed的当前元素放入辅助栈stack
            stack.push(num)
            // 循环判断「stack栈顶元素 == popped序列的当前元素」是否成立
            while (!stack.isEmpty() && stack.peek() == popped[i]) {
                // 如果成立的话，就把该元素弹出辅助栈 stack，这样就完成了一次出入栈模拟操作
                // 发射！
                stack.pop()
                // 每成功模拟一次出入栈操作，才能将 i 自增
                i++
            }
        }
        // 如果最后辅助栈为空，说明模拟出入栈操作成功。
        // 如果不为空，说明模拟失败。
        return stack.isEmpty()
    }
}
```

### 2.3 复杂度分析

* 时间复杂度 `O(N)`：N是二叉树的结点数，每个元素最多入栈和出栈一次，所以最多共有 `2N` 次出入栈操作。
* 空间复杂度 `O(N)`：辅助栈最多存储`N`个元素。

## 3. 参考

* [https://leetcode-cn.com/problems/zhan-de-ya-ru-dan-chu-xu-lie-lcof](https://leetcode-cn.com/problems/zhan-de-ya-ru-dan-chu-xu-lie-lcof)
* [https://leetcode-cn.com/problems/zhan-de-ya-ru-dan-chu-xu-lie-lcof/solution/mian-shi-ti-31-zhan-de-ya-ru-dan-chu-xu-lie-mo-n-2/](https://leetcode-cn.com/problems/zhan-de-ya-ru-dan-chu-xu-lie-lcof/solution/mian-shi-ti-31-zhan-de-ya-ru-dan-chu-xu-lie-mo-n-2/)

