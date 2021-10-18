# LCOF 18. 删除链表的节点

## 1. [问题](https://leetcode-cn.com/problems/shan-chu-lian-biao-de-jie-dian-lcof)

给定单向链表的头指针和一个要删除的节点的值，定义一个函数删除该节点。

返回删除后的链表的头节点。

注意：此题对比原题有改动

示例 1:

```
输入: head = [4,5,1,9], val = 5
输出: [4,1,9]
解释: 给定你链表中值为 5 的第二个节点，那么在调用了你的函数之后，该链表应变为 4 -> 1 -> 9.
```

示例 2:

```
输入: head = [4,5,1,9], val = 1
输出: [4,5,9]
解释: 给定你链表中值为 1 的第三个节点，那么在调用了你的函数之后，该链表应变为 4 -> 5 -> 9.
```

说明：

* 题目保证链表中节点的值互不相同
* 若使用 C 或 C++ 语言，你不需要 free 或 delete 被删除的节点

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
    public ListNode deleteNode(ListNode head, int val) {
        // 如果要删除头结点，直接返回next即可
        if (head.val == val) 
            return head.next;

        // 当前结点cur，从head开始遍历
        ListNode cur = head;
        // cur的上一个结点
        ListNode pre = null;

        // 当前结点值不等于要删除的结点值，就一直往下一个节点移动
        while(cur.val != val) {
            pre = cur;
            cur = cur.next;
        }

        // 退出循环的时候，cur就是要删除的结点，把pre的next指向cur的next就好啦 
        pre.next = cur.next;
        // 返回头结点
        return head;
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
internal class Solution {
    fun deleteNode(head: ListNode, `val`: Int): ListNode {
        // 如果要删除头结点，直接返回next即可
        if (head.`val` === `val`)
            return head.next

        // 当前结点cur，从head开始遍历
        var cur = head
        // cur的上一个结点
        var pre: ListNode? = null

        // 当前结点值不等于要删除的结点值，就一直往下一个节点移动
        while (cur.`val` !== `val`) {
            pre = cur
            cur = cur.next
        }

        // 退出循环的时候，cur就是要删除的结点，把pre的next指向cur的next就好啦 
        pre!!.next = cur.next
        // 返回头结点
        return head
    }
}
```

## 3. 参考

* [https://leetcode-cn.com/problems/shan-chu-lian-biao-de-jie-dian-lcof](https://leetcode-cn.com/problems/shan-chu-lian-biao-de-jie-dian-lcof)
