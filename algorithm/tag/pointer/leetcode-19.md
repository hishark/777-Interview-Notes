# LEETCODE 19. 删除链表的倒数第N个节点

## 1. [问题](https://leetcode-cn.com/problems/remove-nth-node-from-end-of-list/)

给定一个链表，删除链表的倒数第 _n _个节点，并且返回链表的头结点。

**示例：**

```
给定一个链表: 1->2->3->4->5, 和 n = 2.
当删除了倒数第二个节点后，链表变为 1->2->3->5.
```

**说明：**

给定的 _n_ 保证是有效的。

**进阶：**

你能尝试使用一趟扫描实现吗？

## 2. 标签

* 链表
* 双指针

## 3. 解法 - 双指针

> 快慢指针

### 3.1 Java

```java
class Solution {
    public ListNode removeNthFromEnd(ListNode head, int n) {
        // 在 head 前面添加一个空的头结点
        ListNode preHead = new ListNode(0, head);
        // 快慢指针
        ListNode fast = head;
        ListNode slow = preHead;
        // 快指针先单独移动 n 步
        for (int i = 0; i < n; ++i) {
            fast = fast.next;
        }
        // 然后快慢指针一起移动，直到快指针指向空
        while (fast != null) {
            fast = fast.next;
            slow = slow.next;
        }
        // 此时慢指针的下一个结点就是要删去的结点
        // 调整 next 的指向即可删去下一个结点
        slow.next = slow.next.next;
        // 返回链表
        return preHead.next;
    }
}
```

### 3.2 复杂度分析

* 时间复杂度 `O()` ：其中  n  是链表的长度。
* 空间复杂度 `O(1)` ：原地算法，未占用额外的存储空间。

## 4. 参考

* [https://leetcode-cn.com/problems/remove-nth-node-from-end-of-list/](https://leetcode-cn.com/problems/remove-nth-node-from-end-of-list/)
* [https://leetcode-cn.com/problems/remove-nth-node-from-end-of-list/solution/shan-chu-lian-biao-de-dao-shu-di-nge-jie-dian-b-61/](https://leetcode-cn.com/problems/remove-nth-node-from-end-of-list/solution/shan-chu-lian-biao-de-dao-shu-di-nge-jie-dian-b-61/)
