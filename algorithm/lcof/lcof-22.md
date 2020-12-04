---
title: 22. 链表中倒数第k个节点
date: '2020-09-15T10:34:29.000Z'
tags:
  - 双指针
  - 链表
  - leetcode
  - java
  - kotlin
  - lcof
categories: 算法笔记
---

# 22. 链表中倒数第k个节点

## 1. [问题](https://leetcode-cn.com/problems/lian-biao-zhong-dao-shu-di-kge-jie-dian-lcof/)

输入一个链表，输出该链表中倒数第k个节点。为了符合大多数人的习惯，本题从1开始计数，即链表的尾节点是倒数第1个节点。例如，一个链表有6个节点，从头节点开始，它们的值依次是1、2、3、4、5、6。这个链表的倒数第3个节点是值为4的节点。

示例：

```text
给定一个链表: 1->2->3->4->5, 和 k = 2.
返回链表 4->5.
```

## 2. 解法 - 双指针

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
    public ListNode getKthFromEnd(ListNode head, int k) {
        // 双指针
        ListNode pre = head;
        ListNode aft = head;

        // 先将pre移动到第k个结点的位置
        for(int i=0;i<k;i++) {
            pre = pre.next;
        }

        // 然后同时移动两个指针pre和aft，直到pre为空，此时aft指向的就是倒数第k个结点
        while (pre != null) {
            pre = pre.next;
            aft = aft.next;
        }

        // 返回aft即可
        return aft;
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
    fun getKthFromEnd(head: ListNode, k: Int): ListNode {
        // 双指针
        var pre: ListNode? = head
        var aft = head

        // 先将pre移动到第k个结点的位置
        for (i in 0 until k) {
            pre = pre!!.next
        }

        // 然后同时移动两个指针pre和aft，直到pre为空，此时aft指向的就是倒数第k个结点
        while (pre != null) {
            pre = pre!!.next
            aft = aft.next
        }

        // 返回aft即可
        return aft
    }
}
```

### 2.3 复杂度分析

* 时间复杂度 `O(N)`：N是链表的结点数量。总体来看，pre走了N步，aft走了N-k步。
* 空间复杂度 `O(1)`：双指针pre和aft使用了常数大小的额外空间。

## 3. 参考

* [https://leetcode-cn.com/problems/lian-biao-zhong-dao-shu-di-kge-jie-dian-lcof/](https://leetcode-cn.com/problems/lian-biao-zhong-dao-shu-di-kge-jie-dian-lcof/)
* [https://leetcode-cn.com/problems/lian-biao-zhong-dao-shu-di-kge-jie-dian-lcof/solution/mian-shi-ti-22-lian-biao-zhong-dao-shu-di-kge-j-11/](https://leetcode-cn.com/problems/lian-biao-zhong-dao-shu-di-kge-jie-dian-lcof/solution/mian-shi-ti-22-lian-biao-zhong-dao-shu-di-kge-j-11/)

