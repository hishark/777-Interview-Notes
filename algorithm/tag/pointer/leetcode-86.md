# LEETCODE 86. 分隔链表



## 1. [问题](https://leetcode-cn.com/problems/partition-list/)

给你一个链表和一个特定值 x ，请你对链表进行分隔，使得所有小于 x 的节点都出现在大于或等于 x 的节点之前。

你应当保留两个分区中每个节点的初始相对位置。

示例：

```text
输入：head = 1->4->3->2->5->2, x = 3
输出：1->2->2->4->3->5
```

## 2. 标签

* 链表
* 双指针

## 3. 解法 - 双指针

### 3.1 Java

```java
class Solution {
    public ListNode partition(ListNode head, int x) {
        // 双指针
        // left 链表储存小于 x 的结点
        ListNode left = new ListNode(0);
        // left 会不停地移动，由于后面还需要用到所以使用 leftTmp 记下初始位置
        ListNode leftTmp = left;
        // right 链表储存大于等于 x 的结点
        ListNode right = new ListNode(0);
        // right 会不停地移动，由于后面还需要用到所以使用 rightTmp 记下初始位置
        ListNode rightTmp = right;
        // 遍历链表
        while (head != null) {
            // 小于 x 的结点全部放到 left 链表中
            if (head.val < x) {
                left.next = head;
                left = left.next;
            } else {
                // 大于等于 x 的结点全部放到 right 链表中
                right.next = head;
                right = right.next;
            }
            // head 移向下一个结点
            head = head.next;
        }
        // 把两个链表串起来即可
        right.next = null;
        left.next = rightTmp.next;
        return leftTmp.next;
    }
}
```

### 3.2 复杂度分析

* 时间复杂度 `O(n)` ：其中 n 是原链表的长度。对该链表进行了一次遍历。
* 空间复杂度 `O(1)` ：未开辟新的空间。

## 4. 参考

* [https://leetcode-cn.com/problems/partition-list/](https://leetcode-cn.com/problems/partition-list/)
* [https://leetcode-cn.com/problems/partition-list/solution/fen-ge-lian-biao-by-leetcode-solution-7ade/](https://leetcode-cn.com/problems/partition-list/solution/fen-ge-lian-biao-by-leetcode-solution-7ade/)

