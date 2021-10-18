# 字节客户端开发面经

{% embed url="https://www.nowcoder.com/discuss/519698" %}

**一面**\
时间：2020.07.16 10:30 时长：48分钟

* 面试官介绍面试流程
* 自我介绍
* 介绍[项目](https://app.gitbook.com/jump/super-jump/word?word=%E9%A1%B9%E7%9B%AE)（面试官不感兴趣，一带而过）
* 四层网络协议说一下
* 应用层有什么协议
* 传输层有什么协议
* 既然你说到TCP和UDP，那么它们两个的区别
* UDP使用的场景，既然UDP既然不安全，可能发生错误为什么还要使用？
* 简单介绍一下堆和栈
* OOM发生的区域，调用方法次数过多，哪部分会报异常（栈，StackOverflow)
* 进程调用[算法](https://app.gitbook.com/jump/super-jump/word?word=%E7%AE%97%E6%B3%95)
* \== 和 equals方法区别
* Object类中有哪些方法
* 介绍final关键字
* 常用的list有哪些
* linkedList和ArrayList的区别
* 你刚才说的CopyOnWriteList，简单的介绍一下
* synchronied加载静态方法和非静态方法的区别（如果创建类的两个对象，分别在两个线程中，调用对应的非静态方法，会相互影响吗？如果只有一个对象，两个线程调用非静态方法，会相互影响吗）
* 什么是死锁？
* 死锁的条件
* 如何避免和预防死锁
* 让你写一个栈，你怎么使用？（使用数组）
*   场景题：

    地上有20枚硬币，一次只能捡一个或两个，两个人轮番减，你怎么能确保赢？如果地上是18枚硬币呢？21枚呢？
*   [算法题](https://app.gitbook.com/jump/super-jump/word?word=%E7%AE%97%E6%B3%95%E9%A2%98)：

    两个有序[链表](https://app.gitbook.com/jump/super-jump/word?word=%E9%93%BE%E8%A1%A8)合并为一个有序[链表](https://app.gitbook.com/jump/super-jump/word?word=%E9%93%BE%E8%A1%A8)？
*   反问环节？

    没啥问的？就问了下[客户端](https://app.gitbook.com/jump/super-jump/word?word=%E5%AE%A2%E6%88%B7%E7%AB%AF)和后端的区别？

**二面**\
时间：2020.07.21 16:00 时长：53分钟

* 自我介绍
* 介绍的[项目](https://app.gitbook.com/jump/super-jump/word?word=%E9%A1%B9%E7%9B%AE)
* 你认为哪个[项目](https://app.gitbook.com/jump/super-jump/word?word=%E9%A1%B9%E7%9B%AE)最重要，它的难点是什么
* 你为什么想转[客户端](https://app.gitbook.com/jump/super-jump/word?word=%E5%AE%A2%E6%88%B7%E7%AB%AF)
* 你怎么跟认真准备学习Android的学生竞争？
* OSI七层模型
* 说说各层都有哪些协议
* TCP和UDP的区别
* 说一说拥塞控制（慢启动、拥塞避免、快重传、快恢复）
* 在浏览器输入网址经历的过程
* DNS解析过程、四次挥手
* 浏览器渲染过程
* 讲讲HashMap，为什么会扩容2倍？（因为2倍Hash冲突会降低很多）
* 处理Hash冲突的方式
* 介绍一下Java的锁
* synchronized的原理
* 讲一讲Java内存模型
* 类加载机制
* 如果头条APP卡了，可能发生的原因有哪些？
*   [算法题](https://app.gitbook.com/jump/super-jump/word?word=%E7%AE%97%E6%B3%95%E9%A2%98)：

    输入数据如：3，32, 321 如何使他们拼接而成的值最小：321323
* 反问
