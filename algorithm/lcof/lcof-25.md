---
title: 25. 合并两个排序的链表
date: '2020-09-16T18:54:51.000Z'
tags:
  - leetcode
  - java
  - kotlin
  - lcof
  - 链表
  - 递归
categories: 算法笔记
---

# 25. 合并两个排序的链表【递归】

## 1. [问题](https://leetcode-cn.com/problems/he-bing-liang-ge-pai-xu-de-lian-biao-lcof)

输入两个递增排序的链表，合并这两个链表并使新链表中的节点仍然是递增排序的。

示例1：

```text
输入：1->2->4, 1->3->4
输出：1->1->2->3->4->4
```

限制：

* 0 &lt;= 链表长度 &lt;= 1000

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
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        if (l1 == null)
            return l2;
        if (l2 == null)
            return l1;
        if (l1.val <= l2.val) {
            l1.next = mergeTwoLists(l1.next, l2);
            return l1;
        } else {
            l2.next = mergeTwoLists(l2.next, l1);
            return l2;
        }
    }
}
```

### 2.2 Kotlin

```kotlin
hellowor/**
 * Example:
 * var li = ListNode(5)
 * var v = li.`val`
 * Definition for singly-linked list.
 * class ListNode(var `val`: Int) {
 *     var next: ListNode? = null
 * }
 */
class Solution {
    fun mergeTwoLists(l1: ListNode?, l2: ListNode?): ListNode? {
        if (l1 == null)
            return l2
        if (l2 == null)
            return l1
        if (l1!!.`val` <= l2!!.`val`) {
            l1!!.next = mergeTwoLists(l1!!.next, l2)
            return l1
        } else {
            l2!!.next = mergeTwoLists(l2!!.next, l1)
            return l2
        }
    }
}ld
```

### 2.3 复杂度分析

* 时间复杂度：`O(n+m)` ，其中 n 和 m 分别为两个链表的长度。因为每次调用递归都会去掉 l1 或者 l2 的头节点（直到至少有一个链表为空），函数 mergeTwoList 至多只会递归调用每个节点一次。因此，时间复杂度取决于合并后的链表长度，即 `O(n+m)`。
* 空间复杂度：`O(n+m)` ，其中 n 和 m 分别为两个链表的长度。递归调用 mergeTwoLists 函数时需要消耗栈空间，**栈空间的大小取决于递归调用的深度**。结束递归调用时 mergeTwoLists 函数最多调用 n+m 次，因此空间复杂度为 `O(n+m)`。

## 3. 参考

* [https://leetcode-cn.com/problems/he-bing-liang-ge-pai-xu-de-lian-biao-lcof](https://leetcode-cn.com/problems/he-bing-liang-ge-pai-xu-de-lian-biao-lcof)
* [https://leetcode-cn.com/problems/merge-two-sorted-lists/solution/he-bing-liang-ge-you-xu-lian-biao-by-leetcode-solu/](https://leetcode-cn.com/problems/merge-two-sorted-lists/solution/he-bing-liang-ge-you-xu-lian-biao-by-leetcode-solu/)

