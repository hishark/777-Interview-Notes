# lcof-06.-cong-wei-dao-tou-da-yin-lian-biao

## 1. [问题](https://leetcode-cn.com/problems/cong-wei-dao-tou-da-yin-lian-biao-lcof/)

输入一个链表的头节点，从尾到头反过来返回每个节点的值（用数组返回）。

示例 1：

```text
输入：head = [1,3,2]
输出：[2,3,1]
```

限制：

* 0 &lt;= 链表长度 &lt;= 10000

## 2. 解法1 - 栈

### 2.1 Java

```java
class Solution {
    public int[] reversePrint(ListNode head) {
        Stack<Integer> stack = new Stack<Integer>();
        int len = 0;
        while (head!=null) {
             stack.push(head.val);
             head = head.next;
             len++;
        }
        int[] res = new int[len];
        int i = 0;

        while (!stack.empty()) {
            res[i] = stack.pop();
            i++;
        }

        return res;
    }
}
```

### 2.2 Kotlin

```kotlin
// 栈
class Solution {
    fun reversePrint(head: ListNode?): IntArray {
        var head = head
        val stack = Stack<Int>()
        var len = 0
        while (head != null) {
            stack.push(head!!.`val`)
            head = head!!.next
            len++
        }
        val res = IntArray(len)
        var i = 0

        while (!stack.empty()) {
            res[i++] = stack.pop()
        }

        return res
    }
}
```

## 3. 解法2 - 递归

### 3.1 Java

```java
// 递归
class Solution {
    ArrayList<Integer> tmp = new ArrayList<Integer>();

    public int[] reversePrint(ListNode head) {
        recursion(head);
        int[] res = new int[tmp.size()];
        for (int i=0;i<res.length;i++) {
            res[i] = tmp.get(i);
        }
        return res;
    }

    // 递归的从尾到头添加结点值到tmp
    // 每访问一个节点的时候，先递归添加它后面的结点，再添加它本身
    public void recursion(ListNode head) {
        if(head == null)
            return;
        recursion(head.next);
        tmp.add(head.val);
    }
}
```

## 4. 参考

* [https://leetcode-cn.com/problems/cong-wei-dao-tou-da-yin-lian-biao-lcof/](https://leetcode-cn.com/problems/cong-wei-dao-tou-da-yin-lian-biao-lcof/)
* [《剑指Offer（第2版）》](https://book.douban.com/subject/27008702/)

## 5. 笔记

![](../../../.gitbook/assets/image%20%2822%29.png)

