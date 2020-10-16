---
title: 24. 反转链表
date: '2020-09-15T11:01:09.000Z'
tags:
  - leetcode
  - java
  - kotlin
  - lcof
  - 链表
  - 双指针
categories: 算法笔记
---

# 24. 反转链表

## 1. [问题](https://leetcode-cn.com/problems/fan-zhuan-lian-biao-lcof)

定义一个函数，输入一个链表的头节点，反转该链表并输出反转后链表的头节点。

示例:

```text
输入: 1->2->3->4->5->NULL
输出: 5->4->3->2->1->NULL
```

限制：

* 0 &lt;= 节点个数 &lt;= 5000

## 2. 解法 - 递归

### 2.1 Java

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode reverseList(ListNode head) {
        // 递归终止条件
        if (head == null || head.next == null) 
            return head;

        /**
         * 假设链表为1->2->3->4->5
         * 最后一层递归返回的cur就是最后一个节点5
         */
        ListNode cur = reverseList(head.next);
        // 此时的head是4，下面这个操作就是让5指向4，完成一次反转
        head.next.next = head;
        // 4的next本来是5，现在置为空，防止产生循环
        head.next = null;
        // 返回cur即可
        return cur;
    }
}
```

### 2.2 Kotlin

```kotlin
/**
 * Definition for singly-linked list.
 * public class ListNode {
 * int val;
 * ListNode next;
 * ListNode(int x) { val = x; }
 * }
 */
class Solution {
    fun reverseList(head: ListNode?): ListNode? {
        // 递归终止条件
        if (head == null || head!!.next == null)
            return head

        /**
         * 假设链表为1->2->3->4->5
         * 最后一层递归返回的cur就是最后一个节点5
         */
        val cur = reverseList(head!!.next)
        // 此时的head是4，下面这个操作就是让5指向4，完成一次反转
        head!!.next.next = head
        // 4的next本来是5，现在置为空，防止产生循环
        head!!.next = null
        // 返回cur即可
        return cur
    }
}
```

### 2.3 复杂度分析

* 时间复杂度：O\(n\)，n是链表的长度。
* 空间复杂度：O\(n\)，由于使用递归，将会使用隐式栈空间，递归深度可能会达到 n 层。

## 3. 解法 - 双指针迭代

### 3.1 Java

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode reverseList(ListNode head) {
        // 指向cur的前一个结点
        ListNode pre = null;
        // cur最先指向head
        ListNode cur = head;
        // tmp工具人用来保存cur的下一个结点
        ListNode tmp = null;

        // cur遍历整个链表，当cur指向空，遍历就结束了
        while (cur != null) {
            tmp = cur.next;
            cur.next = pre;
            pre = cur;
            cur = tmp;
        }

        // 别写成cur了，退出上面的循环之后cur就为空了
        return pre;
    }
}
```

### 3.2 Kotlin

```kotlin
/**
 * Definition for singly-linked list.
 * public class ListNode {
 * int val;
 * ListNode next;
 * ListNode(int x) { val = x; }
 * }
 */
class Solution {
    fun reverseList(head: ListNode): ListNode? {
        // 指向cur的前一个结点
        var pre: ListNode? = null
        // cur最先指向head
        var cur: ListNode? = head
        // tmp工具人用来保存cur的下一个结点
        var tmp: ListNode? = null

        // cur遍历整个链表，当cur指向空，遍历就结束了
        while (cur != null) {
            tmp = cur!!.next
            cur!!.next = pre
            pre = cur
            cur = tmp
        }

        // 别写成cur了，退出上面的循环之后cur就为空了
        return pre
    }
}
// 测试样例为[]时报错 Exception in thread "main" java.lang.IllegalStateException: param_1 must not be null 应该是kotlin不允许参数为空
```

### 3.3 复杂度分析

* 时间复杂度：O\(n\)，n是链表的长度。
* 空间复杂度：O\(1\)。

## 4. 参考

* [https://leetcode-cn.com/problems/fan-zhuan-lian-biao-lcof](https://leetcode-cn.com/problems/fan-zhuan-lian-biao-lcof)
* [https://leetcode-cn.com/problems/fan-zhuan-lian-biao-lcof/solution/dong-hua-yan-shi-duo-chong-jie-fa-206-fan-zhuan-li/](https://leetcode-cn.com/problems/fan-zhuan-lian-biao-lcof/solution/dong-hua-yan-shi-duo-chong-jie-fa-206-fan-zhuan-li/)
* [https://leetcode-cn.com/problems/reverse-linked-list/solution/fan-zhuan-lian-biao-by-leetcode/](https://leetcode-cn.com/problems/reverse-linked-list/solution/fan-zhuan-lian-biao-by-leetcode/)

