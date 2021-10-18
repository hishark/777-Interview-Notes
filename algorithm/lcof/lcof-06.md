# 06. 从尾到头打印链表【栈/递归】

## 1. [问题](https://leetcode-cn.com/problems/cong-wei-dao-tou-da-yin-lian-biao-lcof/)

输入一个链表的头节点，从尾到头反过来返回每个节点的值（用数组返回）。

示例 1：

```
输入：head = [1,3,2]
输出：[2,3,1]
```

限制：

* 0 <= 链表长度 <= 10000

## 2. 解法1 - 栈

### 2.1 Java

```java
class Solution {
    public int[] reversePrint(ListNode head) {
        // 此题为典型的先进后出，可以使用栈来实现
        Stack<Integer> stack = new Stack<Integer>();
        // 链表长度
        int len = 0;
        // 把链表中的所有结点推入栈中
        while (head!=null) {
             stack.push(head.val);
             head = head.next;
             len++;
        }
        // 结果数组
        int[] res = new int[len];
        int i = 0;

        // 从栈顶开始取出所有结点即可
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
class Solution {
    fun reversePrint(head: ListNode?): IntArray {
        var head = head
        // 此题为典型的先进后出，可以使用栈来实现
        val stack = Stack<Int>()
        // 链表长度
        var len = 0
        // 把链表中的所有结点推入栈中
        while (head != null) {
            stack.push(head!!.`val`)
            head = head!!.next
            len++
        }
        // 结果数组
        val res = IntArray(len)
        var i = 0

        // 从栈顶开始取出所有结点即可
        while (!stack.empty()) {
            res[i++] = stack.pop()
        }

        return res
    }
}
```

### 2.3 复杂度分析

* 时间复杂度 `O(N)` ：入栈 + 出栈。
* 空间复杂度 `O(N)` ：辅助栈和结果数组。

## 3. 解法2 - 递归

### 3.1 Java

```java
class Solution {
    // 工具人 tmp 用于存储所有结点（从尾部到头部）
    ArrayList<Integer> tmp = new ArrayList<Integer>();

    public int[] reversePrint(ListNode head) {
        // 递归的从尾到头添加结点值到tmp
        recursion(head);
        
        // 结果数组
        int[] res = new int[tmp.size()];
        
        // 从 tmp 中取出所有结点的值即可
        for (int i=0;i<res.length;i++) {
            res[i] = tmp.get(i);
        }
        return res;
    }

    // 递归的从尾到头添加结点值到tmp
    // 每访问一个节点的时候，先递归添加它后面的结点，再添加它本身
    public void recursion(ListNode head) {
        // 结点为空，返回
        if(head == null)
            return;
        // 先递归添加之后的结点
        recursion(head.next);
        // 最后再把自己加进去
        tmp.add(head.val);
    }
}
```

### 3.2 Kotlin

> Error: Exception in thread "main" java.lang.IllegalStateException: param\_1 must not be null

```kotlin
class Solution {
    // 工具人 tmp 用于存储所有结点（从尾部到头部）
    var tmp = ArrayList<Int>()

    fun reversePrint(head: ListNode): IntArray = head?.let {
        // 递归的从尾到头添加结点值到tmp
        recursion(head)
        
        // 结果数组
        val res = IntArray(tmp.size)
        
        // 从 tmp 中取出所有结点的值即可
        for (i in res.indices) {
            res[i] = tmp[i]
        }
        return res
    } ?: intArrayOf()

    // 递归的从尾到头添加结点值到tmp
    // 每访问一个节点的时候，先递归添加它后面的结点，再添加它本身
    fun recursion(head: ListNode?) {
        // 结点为空，返回
        if (head == null)
            return
        // 先递归添加之后的结点
        recursion(head!!.next)
        // 最后再把自己加进去
        tmp.add(head!!.`val`)
    }
}
```

### 3.3 复杂度分析

* 时间复杂度 `O(N)` ：遍历链表，递归 N 次。
* 空间复杂度 `O(N)` ：系统递归需要 O(N) 的栈空间。

## 4. 参考

* [https://leetcode-cn.com/problems/cong-wei-dao-tou-da-yin-lian-biao-lcof/](https://leetcode-cn.com/problems/cong-wei-dao-tou-da-yin-lian-biao-lcof/)
* [《剑指Offer（第2版）》](https://book.douban.com/subject/27008702/)

## 5. 笔记

![](https://777blog.oss-cn-shanghai.aliyuncs.com/leetcode/lcof-06.jpg)
