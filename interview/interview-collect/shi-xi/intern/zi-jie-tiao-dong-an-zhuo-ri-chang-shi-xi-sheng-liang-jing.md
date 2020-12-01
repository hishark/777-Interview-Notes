# 字节跳动安卓日常实习生凉经

{% embed url="https://www.nowcoder.com/discuss/528025" %}

首先不得不说字节捞人效率真滴高，投一天就把我捞起来的，这点表示很nice。下面开始。

一面

1. 讲解一下MVP架构。MVP和MVC的控制层有什么区别？

2. HTTP常用状态码。

3. **除了Json还有哪些数据传输格式。**

4. Json解析的时候是怎么将json解析为对应的类。

5. Java中常见的异常。

6. **热更新**原理。

7. APK文件里面都有些什么。

8. 为什么是DEX文件？

9. Android程序运行时使用的是普通的JVM吗？

10. Flutter dart语言是在什么上运行的。

11. Java怎么实现多线程。

12. Java线程的管理。

13. 线程间切换的方法。线程间通讯。

14. 算法题（1-100建立二叉树，中序遍历输出）



二面

1.算法题：给定单链表，求离终点距离为 k 的节点，要求只扫一次且空间复杂度为O\(1\)？

2.已知一个model类new一个对象，并将该对象作为HashMap的key， value为Hello，修改该对象中某一个属性的值，再去HashMap中get此key，此时的value值是什么？

3.

```text
class A { 
    private int i = 0;

    private void foo() {

        ......

        new Thread(new Runnable() { <a href="/profile/992988" data-card-uid="992988" class="js-nc-card" target="_blank" from-niu="default">@Override public void run() {

                ......

                i = 1;

                ......

            }

        }).start();

        ......

        System.out.print(i);

        ......

    }

}
```

请问这段代码的输出结果是什么？

添加代码，怎么保证输出的结果为1？

4.JVM的**GC机制**。

5.http缓存了解嘛。

面试结束？凉凉

