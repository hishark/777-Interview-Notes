---
title: 2. 两数相加
date: 2020-06-11 14:33:37
tags:
- 链表
- 数学
- leetcode
- java
- kotlin
categories: 算法笔记
notshow: true
---
# 2. 两数相加
## [1. 问题](https://leetcode-cn.com/problems/add-two-numbers/)
给出两个 非空 的链表用来表示两个非负的整数。其中，它们各自的位数是按照 逆序 的方式存储的，并且它们的每个节点只能存储 一位 数字。

如果，我们将这两个数相加起来，则会返回一个新的链表来表示它们的和。

您可以假设除了数字 0 之外，这两个数都不会以 0 开头。

示例：

>输入：(2 -> 4 -> 3) + (5 -> 6 -> 4)
输出：7 -> 0 -> 8
原因：342 + 465 = 807
<!--more-->
## 2. 解法
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
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        // 初始化
        // 结果链表的头节点
        ListNode head = new ListNode(0); //值任意，反正没有任何意义
        // 当前节点，用于向结果链表插入节点，初始化时指向head
        ListNode cur = head;
        // 进位，初始值为0
        int carry = 0;

        // 当且仅当l1和l2都为空时，才终止遍历链表
        // 也就是说只要有一方不为空，就会一直遍历下去
        while (l1!=null || l2!=null) {
            // 先判断一下l1和l2之间是否有指针为空
            // 如果有为空的，就给它补上0，用于相加
            // 不为空就直接取到节点的值
            int x1 = l1 == null ? 0 : l1.val;
            int x2 = l2 == null ? 0 : l2.val;

            // 两数之和
            int sum = x1 + x2 + carry;

            // 更新进位的值
            carry = sum / 10;
            // 求余数，用于插入结果链表
            sum = sum % 10;
            cur.next = new ListNode(sum);

            // 移动cur
            cur = cur.next;

            // 移动l1和l2
            // 记得要判空，走到这里可能已经有一个指针为空了
            if(l1!=null)
                l1 = l1.next;
            if(l2!=null)
                l2 = l2.next;
        }

        // 结束循环后，判断carry是否为1，若为1就添加到结果链表的最后
        if (carry == 1) {
            cur.next = new ListNode(carry);
        }
        
        // 返回结果链表
        return head.next;
    }
}
```
### 2.2 Kotlin
```kotlin
/**
 * Example:
 * var li = ListNode(5)
 * var v = li.`val`
 * Definition for singly-linked list.
 * class ListNode(var `val`: Int) {
 *     var next: ListNode? = null
 * }
 */
class Solution {
    fun addTwoNumbers(ll1: ListNode?, ll2: ListNode?): ListNode? {
        // 初始化
        // 结果链表的头节点
        var head = ListNode(0); //值任意，反正没有任何意义
        // 当前节点，用于向结果链表插入节点，初始化时指向head
        var cur = head;
        // 进位，初始值为0
        var carry = 0;

        // 当且仅当l1和l2都为空时，才终止遍历链表
        // 也就是说只要有一方不为空，就会一直遍历下去
        var l1 = ll1
        var l2 = ll2
        while (l1!=null || l2!=null) {
            // 先判断一下l1和l2之间是否有指针为空
            // 如果有为空的，就给它补上0，用于相加
            // 不为空就直接取到节点的值
            var x1 = if(l1 == null) 0 else l1.`val`
            var x2 = if(l2 == null) 0 else l2.`val`

            // 两数之和
            var sum = x1 + x2 + carry;

            // 更新进位的值
            carry = sum / 10;
            // 求余数，用于插入结果链表
            sum = sum % 10;
            cur.next = ListNode(sum);

            // 移动cur
            cur = cur.next;

            // 移动l1和l2
            // 记得要判空，走到这里可能已经有一个指针为空了
            if(l1!=null)
                l1 = l1.next;
            if(l2!=null)
                l2 = l2.next;
        }

        // 结束循环后，判断carry是否为1，若为1就添加到结果链表的最后
        if (carry == 1) {
            cur.next = ListNode(carry);
        }
        
        // 返回结果链表
        return head.next;
    }
}
```
## 3. 参考
- [力扣：2. 两数相加](https://leetcode-cn.com/problems/add-two-numbers)
- [灵魂画手：画解算法：2. 两数相加](https://leetcode-cn.com/problems/add-two-numbers/solution/hua-jie-suan-fa-2-liang-shu-xiang-jia-by-guanpengc/)
## 4. 学习草稿
![](https://777blog.oss-cn-shanghai.aliyuncs.com/blog%20pic/IMG_4168.JPG)