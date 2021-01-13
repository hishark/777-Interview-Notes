---
description: 全是从面经里扒拉出来的面试题
---

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

## volatile的可见性具体是如何实现的

* [volatile实现可见性的原理](https://blog.csdn.net/hxcaifly/article/details/88093099)
* [volatile原理看这一篇就够了](https://zhuanlan.zhihu.com/p/77085695)

## gc算法，收集器

## jvm内存区域，为什么要有jvm

## jvm 内存

## jvm启动过程? 验证是验证什么

## JVM内存管理相关问题

## 抽象类与接口的区别

## Object有哪些**公有方法**

## 全局变量和局部变量

（分配在什么地方）

## 静态变量，实例变量，构造函数的初始化顺序

## 类加载过程

扯到了invokestatic，面试官问什么时候调用？答在调用静态方法时调用

## 讲讲Java中**类的加载过程**

## 类加载机制，什么时候需要对类进行初始化

## String类如何被加载的

【类加载机制】

## 双亲委派模型

## 异常体系，可以catch error吗

## Java中常见的异常。

## 热更新原理

## 多态，有哪些实现

## 继承多态如何实现

## java容器有哪些

## HashMap

> HashMap 问题超多

hashmap底层原理（必考）hash值的计算、为什么要重写equals和hashcode 、插入的时候会发生啥

hashcode 为什么出现、是什么、equals关系

hashmap的扩容机制，为什么要俩倍扩容。

HashMap的源码，扩容的条件。

hashmap 原理 机制 扩容

hashmap 扩容，为啥是 2 倍，为啥 size 是 2 的幂次方

Hashmap的具体实现

HashMap原理，get、put的时间复杂度

谈谈HashMap\(为什么不适用基础数据类型、添加的时候需要注意什么、添加的key有什么特殊性\)

介绍一下所有的map，以及他们之间的对比，适用场景。

ConcurrentHashMap和HashMap底层实现

hashmap底层结构 扩容机制 查询机制 hash算法

hashmap的key可以是基本类型吗 如果一定要定义为基本类型怎么做 //⭐️

讲一下hashCode\(\)。（这里提到了hashmap的原理）

哈希构造方法、哈希冲突解决方法

## ArrayList和HashMap了解吗？

## 设计一个K-V的数据结构应该考虑哪些问题，如何解决这些问题

【说了一下哈希碰撞，多线程访问，初始容量等】

## 基本类型和**包裹类型**哪个占用资源多 为什么

## 说说几种集合的区别

## ArrayList和**LinkedList**的区别

查找的时间复杂度是多少【底层实现方式不一样】

## List 如何删除

（为什么用iterator的不用List的删除方法，讲了一下ConcurrentModificationException）

## ArrayList&lt;String&gt; 删除空字符串\(""\)对象

## SparseArray

## 红黑树

扯到红黑树特性（就知道什么黑节点层数一样。扯了查找树的特性，试图糊弄）

## 线程池介绍，任务队列如果满了怎么办

CAS介绍，CAS有什么问题，Java是否有解决方法

final关键字，final常量存储位置，常量池的好处

## GC

（Java GC\(Garbage Collection,垃圾收集,垃圾回收\)机制）

Java垃圾回收机制，

如何判断堆中哪些对象需要被回收

Java内存，回收的搜索算法：引用计数和根搜索算法。

gc一整套

JVM的GC机制

gc回收，可达性分析法

了解JVM吗？讲了JVM的体系结构和GC回收机制。

Java垃圾回收的过程

可以作为GCRoot根的对象有哪些【局部变量表中的对象，静态变量，常量，本地方法栈中的对象】

对象判死的两种方法，gc roots有哪些

Java的GC机制，引用计数和可达性分析算法，finize\(\)方法，四种回收算法，哪些对象可以作为GC ROOTS对象

如何减少GC，有哪些高频方法经常创建对象

## 多线程有什么用，怎么处理

## 多线程相关的几个关键字

## volatile关键字作用

## synchronized修饰代码块，方法，静态代码块的区别

## 线程安全

我回答了sychronized关键字（关于锁，wait，notify）。面试官追问是否了解volite关键字，我忘了没回答出来。面试官追问是否了解自旋锁，乐观锁，悲观锁等，我回答了解但是没用过。

## 乐观锁和悲观锁，各自的使用场景

## lock锁和sy锁 以及使用场景

## Java怎么实现多线程

## Java线程的管理

## 线程间切换的方法

## 线程间通讯

## synchronized和lock区别，使用场景

## jvm线程怎么调度的

线程生命周期，我说到中间他就会打断说那这个情况怎么出现呢，java怎么实现的，如何结束线程？提供了什么方法

## 显式控制各个线程竞争的有哪些对象呢？

## 线程池的维护

## 线程进程区别

## 死锁和如何解决

## 写一个java多线程

##  为什么要使用多线程

## Java中Thread与Runnable在线程管理上的区别

## 实现两个数组利用两个线程交替打印，且固定由第一个开始

## 工作内存和主内存

（这里是给了一个例子，主线程有一个变量a，子线程里用到了这个变量，问这两处的变量是不是一个东西）

## 线程安全

## `synchronized`与`volatile`关键字的作用

说下Java的synchronized和volatile关键字，可见性，重排序，原子性

## **wait\(\)的用法，notifyAll\(\)的用法，notify\(\)唤醒的是哪一个线程**。

## 案例分析

给定代码，会输出`i`等于什么；如何令`i`输出为1【用`static`与`volatile`修饰，主线程调用`sleep()`】；如何保证`i`一定输出为1，写一下代码【用`wait()`与`notifyAll()`？】；`Runnable`的`run()`方法中使用`this`指的是什么，`Runnable`还是`Thread`【`Runnable`的匿名内部类】

```text
class A {
    private int i = 0;
    public static void main(String[] args) {
        new Thread(new Runnable() {
            @Override
            public void run() {
                i = 1;
            }
        }).start();
        System.out.println(i);
    }
}
```

## 锁原理

## 说说自旋锁，内部实现

## java 的锁怎么实现的 

## synchronized的类锁和对象锁

它们区别，哪些是对象锁，哪些是类锁

## Java有哪几种锁

## synchronized和可重入锁（reetrantlock）的区别

## countdownLatch

## reentrantReadWriteLock 

可重入读写锁

## AsyncTask的原理

## 优先级翻转

## 基本类型字节长度

`int`占多少字节【4】`byte`呢【1】，

## 如何判断`byte`的从右数第n位是否为1

写个`if`语句【`((b >> n) & 1) == 1`】

## 线程池

## 线程池，线程池参数，从提交任务开始的过程

## n个线程，应该开多大的线程池

## 怎么创建线程池，类名说一下

## 临界区概念

## 四大引用

强引用、软引用、弱引用、虚引用，是什么？分别在什么时候用

四种引用 软引用和弱引用的区别 软引用和强引用的区别

## 序列化

## 反序列化和序列化 为什么要？ 什么情况下要？

## 反射

反射 为什么要反射？ 什么时候用？ 缺点？

（反射 反序列化）

java泛型，反射

## static关键字

## static、final、finalize、finally

## `final`关键字作用

【修饰类不可继承，修饰方法不可重写，修饰对象无法重新赋值】

## Java里的final有什么用法

动态编译、静态编译

## 多核 CPU，多线程怎么访问同一个内存

## 是否了解Java的atomic

## 除了Json还有哪些数据传输格式

## Json解析的时候是怎么将json解析为对应的类

## ==和.equals\(\)的区别 

\[-128,127\]

## 重写equals方法

## 讲一下**equals**\(\)

## 重写和重载的区别

## 引用

String a = new String\(\);

b = a;

a = null;

b 是否= null?

## String s=new String\("123"\);建立了几个对象

## `String a = new String("abc")`与`String a = "abc"`的区别

【前者分配在堆上，后者在常量池中】

## String StringBuffer StringBuilder区别？

## 内存泄漏问题

## 内部类会有内存泄漏问题吗 

## 内部类为什么能访问外部类的变量，为什么还能访问外部类的私有变量

## 讲一下**内存泄漏**

## Java可以自动管理内存，为什么会有**OOM**



## LRU

LRU[算法](https:///jump/super-jump/word?word=%E7%AE%97%E6%B3%95)的`get`时间复杂度是多少，为什么

简单介绍一下LRU。 然后让我大概写一下模拟LRU的数据结构。

LRU怎么实现

LruCache

LRU怎么实现\(hash+[链表](https:///jump/super-jump/word?word=%E9%93%BE%E8%A1%A8)\)，详细解释步骤、时间复杂度

## 多态

C++和java如何实现多态性，public的父类中子类重写能不能用protected？反过来呢？

## 如何实现**多态**，**多态的底层实现原理**是什么

## Java中的泛型，类型擦除

## 如果说Java的泛型是伪泛型，为什么不直接用object代替

## 泛型上界，下界定义/作用

## java**泛型，反射**

## 深拷贝/浅拷贝，怎么实现深-浅拷贝

## 讲一下**clone**\(\)，**深拷贝和浅拷贝**的区别

## 讲一下 jmm

## 如何在**栈上开辟空间**

## 如何在**堆里开辟空间**

## 怎么会造成栈溢出，堆溢出

## 线程同步问题

（为什么需要同步&怎么实现同步）

## 内存分配区域

（Java层面回答？对象引用在堆和栈都有么？函数内部new的对象存放在哪？）

## 面向对象的基本概念

## **面向对象的特性是什么**

## 堆和栈的区别

## 怎么解决内存泄漏

（声明static，弱引用包裹）

