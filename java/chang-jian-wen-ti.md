# 常见问题

## **线程安全**

保证线程安全可从多线程三特性出发：

**原子性（Atomicity）**：单个或多个操作是要么全部执行，要么都不执行

* Lock：保证同时只有一个线程能拿到锁，并执行申请锁和释放锁的代码
* synchronized：对线程加独占锁，被它修饰的类/方法/变量只允许一个线程访问

原子性就是说一个操作不可以被中途cpu暂停然后调度**，**即不能被中断，要不就执行完，要不就不执行。如果一个操作是原子性的，那么在多线程环境下，就不会出现变量被修改等奇怪的问题。

**可见性（Visibility）**：当一个线程修改了共享变量的值，其他线程能够立即得知这个修改

* volatile：保证新值能立即同步到主内存，且每次使用前立即从主内存刷新；
* synchronized：在释放锁之前会将工作内存新值更新到主存中

**有序性（Ordering）**：程序代码按照指令顺序执行

* volatile： 本身就包含了禁止指令重排序的语义
* synchronized：保证一个变量在同一个时刻只允许一条线程对其进行lock操作，使得持有同一个锁的两个同步块只能串行地进入

## synchronized 和 volatile 的区别

> 技术点：线程安全

synchronized能保证操作的原子性，而[volatile不可以](https://blog.csdn.net/shenmegui_32/article/details/70153821)，假设线程A和线程B同时读取到变量a值，A修改a后将值更新到主内存，同时B也修改a值会覆盖A的修改操作。

synchronized可修饰变量、方法和类，而volatile只能修饰变量 synchronized可能会造成线程阻塞\(因为synchronized会加锁——我自己的理解\)，而volatile不会造成线程的阻塞。

## volatile的可见性具体是如何实现的

* [volatile实现可见性的原理](https://blog.csdn.net/hxcaifly/article/details/88093099)
* [volatile原理看这一篇就够了](https://zhuanlan.zhihu.com/p/77085695)

