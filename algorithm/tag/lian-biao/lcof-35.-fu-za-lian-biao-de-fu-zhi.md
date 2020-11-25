# LCOF 35. 复杂链表的复制

## 1. [问题](https://leetcode-cn.com/problems/fu-za-lian-biao-de-fu-zhi-lcof/)

请实现 `copyRandomList` 函数，复制一个复杂链表。在复杂链表中，每个节点除了有一个 `next` 指针指向下一个节点，还有一个 `random` 指针指向链表中的任意节点或者 `null`。

示例 1：

![](../../../.gitbook/assets/image%20%281%29.png)

```text
输入：head = [[7,null],[13,0],[11,4],[10,2],[1,0]]
输出：[[7,null],[13,0],[11,4],[10,2],[1,0]]
```

示例2：

![](../../../.gitbook/assets/image%20%282%29.png)

```text
输入：head = [[1,1],[2,1]]
输出：[[1,1],[2,1]]
```

示例3：

![](../../../.gitbook/assets/image%20%283%29.png)

```text
输入：head = [[3,null],[3,0],[3,null]]
输出：[[3,null],[3,0],[3,null]]
```

示例4：

```text
输入：head = []
输出：[]
解释：给定的链表为空（空指针），因此返回 null。
```

提示：

* `-10000 <= Node.val <= 10000`
* `Node.random` 为空（null）或指向链表中的节点。
* 节点数目不超过 1000 。

## 2. 标签

* 链表
* 哈希表

## 3. 解法

### 3.1 Java

```java
/*
// Definition for a Node.
class Node {
    int val;
    Node next;
    Node random;

    public Node(int val) {
        this.val = val;
        this.next = null;
        this.random = null;
    }
}
*/
class Solution {
    public Node copyRandomList(Node head) {
        // 利用哈希表进行链表复制
        HashMap<Node, Node> map = new HashMap<>();

        // 使用工具人 cur 指向头结点 head，用于做复制操作
        Node cur = head;

        // 第一步，先复制所有结点的值
        while (cur != null) {
            map.put(cur, new Node(cur.val));
            cur = cur.next;
        }

        // 第二步，复制所有结点 next 和 random 的指向
        // 将 cur 重新指向头结点
        cur = head;

        while (cur != null) {
            map.get(cur).next = map.get(cur.next);
            map.get(cur).random = map.get(cur.random);
            cur = cur.next;
        }

        // 此时已经全部串起来了，返回 head 即可
        return map.get(head);
    }
}
```

### 3.2 复杂度分析

* 时间复杂度 `O(N)` ：N 是链表中结点的个数，需要对所有结点进行遍历。
* 空间复杂度 `O(N)` ：使用了一个哈希表。

## 5. 参考

* [https://leetcode-cn.com/problems/fu-za-lian-biao-de-fu-zhi-lcof/](https://leetcode-cn.com/problems/fu-za-lian-biao-de-fu-zhi-lcof/)
* [https://leetcode-cn.com/problems/fu-za-lian-biao-de-fu-zhi-lcof/solution/tong-guo-hashmaplai-shi-xian-by-try-62/](https://leetcode-cn.com/problems/fu-za-lian-biao-de-fu-zhi-lcof/solution/tong-guo-hashmaplai-shi-xian-by-try-62/)

