# LCOF 25. 合并两个排序的链表

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

* 时间复杂度：O\(n+m\)其中 n 和 m 分别为两个链表的长度。
* 空间复杂度：O\(n+m\)其中 n 和 m 分别为两个链表的长度。

## 3. 参考

* [https://leetcode-cn.com/problems/he-bing-liang-ge-pai-xu-de-lian-biao-lcof](https://leetcode-cn.com/problems/he-bing-liang-ge-pai-xu-de-lian-biao-lcof)
* [https://leetcode-cn.com/problems/merge-two-sorted-lists/solution/he-bing-liang-ge-you-xu-lian-biao-by-leetcode-solu/](https://leetcode-cn.com/problems/merge-two-sorted-lists/solution/he-bing-liang-ge-you-xu-lian-biao-by-leetcode-solu/)

