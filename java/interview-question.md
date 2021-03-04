# 常见问题

> 要对Java的一些常见问题有所准备，比如GC，面向对象的特征等等。其他语言的话对应准备一些问题就行。

[https://mp.weixin.qq.com/s/st3LORDRXMwADsCWdBH1KQ](https://mp.weixin.qq.com/s/st3LORDRXMwADsCWdBH1KQ)

⬆️ 关于java注释

## 代理模式

Java的三种代理模式：[https://www.cnblogs.com/leeego-123/p/10995975.html](https://www.cnblogs.com/leeego-123/p/10995975.html)

## **JVM**

jvm内存区域，为什么要有jvm // java guide

> [https://zhuanlan.zhihu.com/p/76327745](https://zhuanlan.zhihu.com/p/76327745)
>
> 所以JVM所担任的职责之一，就是当地的翻译员，将位元码文件翻译为当时作业系统看得懂的0101序列。不过这不是最重要的，基本上如果只是要翻译员的话，直译器（Interpreter ）就办得到了。
>
> 　　JVM有个很重要的观念就是：「对于Java程式而言，其实它只认识一种作业系统（或说是一种机器），这个系统叫作JVM，而对于JVM而言，位元码文件就是它的可执行文件！也就是格式为.class的文件。Java代码程序，理想上，并不用理会真正执行于哪个平台之上，它只要知道如何执行于JVM之上就可以了，至于JVM实际上如何与底层平台作沟通，则是JVM自己的事！」这个观念非常的重要，对于以后能够搞清楚所PATH变量与CLASSPATH变量的概念，也有一定的帮助。

jvm 内存

Java内存（分配-&gt;回收）

jvm启动过程? 验证是验证什么

**//**

JVM内存管理相关问题

说说JVM的内存吧，他们都是干啥的？对象怎么创建？

每个区域都会发生怎样的异常啊，谁会发生OOM？

内存分配方式？

堆和栈的区别？

GC？垃圾回收？

class文件生成过程？

Android虚拟机与Java虚拟机之间区别

## **变量**

全局变量和局部变量（分配在什么地方）

静态变量，实例变量，构造函数的初始化顺序。

## **类加载 双亲**

类加载过程

类加载过程，我扯到了invokestatic，面试官问什么时候调用？我答在调用静态方法时调用

讲讲Java中**类的加载过程**

**类加载机制**，**什么时候需要对类进行初始化。**（这个就是在问类初始化的时机

String类如何被加载的【类加载机制】；

String类如何被加载的【类加载机制】；双亲委派模型【常规题】

双亲委派模型【常规题】

//

java对象的加载机制

## **异常 2**

异常体系，可以catch error吗

Java中常见的异常。

//

说一下 JAVA 的异常、泛型、反射。

详细说异常分类

## **热更新原理。**

// 还有安卓的热启动

## **抽象类和接口** 

抽象类与接口的区别

抽象类和接口的区别

Abstract class和interface有什么区别？

多态，有哪些实现

继承多态如何实现

多态

C++和java如何实现多态性，public的父类中子类重写能不能用protected？反过来呢？

如何实现**多态**，**多态的底层实现原理**是什么（方法表）

// 

什么是接口回调？为什么使用接口回调？

## **java容器**

有哪些

说一下Java三种数据集：Map，List，Set，它们分别的特点是什么，它们的优缺点分别是什么

## **HashMap 7**

hashmap底层原理（必考）hash值的计算、为什么要重写equals和hashcode 、插入的时候会发生啥

hashcode 为什么出现、是什么、equals关系

hashmap的扩容机制，为什么要俩倍扩容。

HashMap的源码，扩容的条件。

hashmap 原理 机制 扩容\(他说我扩容说太简单了。。\)

hashmap 扩容，为啥是 2 倍，为啥 size 是 2 的幂次方

Hashmap的具体实现

ArrayList和HashMap了解吗？（面试前恶补过HashMap，这部分说了蛮多的。）

设计一个K-V的数据结构应该考虑哪些问题，如何解决这些问题【说了一下**哈希碰撞，多线程访问，初始容量**等】// 啊 k-v就是key-value就是哈希表，要有应变能力

HashMap原理，get、put的**时间复杂度**

谈谈HashMap\(为什么不适用基础数据类型、添加的时候需要注意什么、添加的key有什么特殊性\)

介绍一下所有的map，以及他们之间的对比，适用场景。

**ConcurrentHashMap**和HashMap**底层实现**

hashmap底层结构 扩容机制 查询机制 hash算法

hashmap的key可以是基本类型吗 如果一定要定义为基本类型怎么做 //⭐️

讲一下**hashCode**\(\)。（这里提到了hashmap的原理）

哈希构造方法、哈希冲突解决方法

//

hashmap的实现原理 get的时间复杂度 如何优化冲突（改变数组长度、再哈希、链表优化为红黑树）

字符串和其他类型的数据做Key如何计算哈希值？（字符串可以使用ASCII码的值求和、或者BKDR等非聚合哈希算法）

concurrentHashmap

HashMap、HashTable、ConcurrentHashMap

HashMap和HastTable，HashMap安全？不安全用什么？hash\(\)？HashTable是怎么实现安全的？

HashMap如何实现、HashMap和HashTable区别、ConcurrentHashMap实现原理。

treeMap的原理和linkeHashMap的原理

## **类型（装箱拆箱**

基本类型和**包裹类型**哪个占用资源多 为什么 //⭐️

## **集合 arraylist等**

说说几种集合的区别 可能是我回答集合的时候顺带把所有的底层实现也都说了，没问我数据结构

`ArrayList`与`LinkedList`区别，**查找的时间复杂度**是多少【底层实现方式不一样】

ArrayList和**LinkedList**的区别。

List如何删除。（为什么用iterator的不用List的删除方法，讲了一下ConcurrentModificationException）

ArrayList&lt;String&gt; 删除空字符串\(""\)对象

sparseArray

// 

ArrayList 底层实现

ArrayList和LinkedList的区别

对ArrayList一个读操作，一个写操作，你用多线程咋实现。死锁你知道不？你怎么解决？

arraylist与vector的区别

介绍一下Arraylist和Linkedlist，说一下它们各自的优缺点是什么，以及它们有什么异同点

## **红黑树**

扯到红黑树特性（就知道什么黑节点层数一样。扯了查找树的特性，试图糊弄）

红黑树。

## **CAS**

CAS介绍，CAS有什么问题，Java是否有解决方法

## **回收 6（Java GC\(Garbage Collection,垃圾收集,垃圾回收\)机制）**

gc算法，收集器，stop the world

Java垃圾回收机制，

如何判断堆中哪些对象需要被回收

Java内存，回收的搜索算法：引用计数和根搜索算法。

gc一整套

JVM的**GC机制**。

gc回收，可达性分析法，

了解JVM吗？讲了JVM的体系结构和GC回收机制。

Java**垃圾回收**的过程

可以作为GCRoot根的对象有哪些【局部变量表中的对象，静态变量，常量，本地方法栈中的对象】

对象判死的两种方法，**gc roots**有哪些

Java的**GC机制**，引用计数和可达性分析算法，finize\(\)方法，四种回收算法，哪些对象可以作为GC ROOTS对象

如何**减少GC**，有哪些高频方\*\*\*经常创建对象（好像是这个意思...） 【这里他问我擅长什么，我说gc（因为关于回收算法和垃圾收集器我记得比较熟），然后他说分代收集算法那些就不用讲了，就一直在问一些我不懂的东西，我真是搬起石头砸自己的脚....】

## **多线程 16**

线程同步问题（为什么需要同步&怎么实现同步）

多核cpu，多线程怎么访问同一个内存

多线程有什么用，怎么处理

多线程相关的几个关键字

volatile关键字作用

讲一下volatile

synchronized修饰代码块，方法，静态代码块的区别

线程安全。我回答了sychronized关键字（关于锁，wait，notify参考我的一篇博客---Java 多线程）。面试官追问是否了解volite关键字，我忘了没回答出来。面试官追问是否了解自旋锁，乐观锁，悲观锁等，我回答了解但是没用过。



lock锁和sy锁 以及使用场景 // 这个我不确定隶属于OS还是java多线程范畴 先放在这 之后找答案再看

Java怎么实现多线程。

Java线程的管理。

线程间切换的方法。线程间通讯。

sync和lock区别，condition干什么

synchronized和lock区别

jvm线程怎么调度的

线程生命周期，我说到中间他就会打断说那这个情况怎么出现呢，java怎么实现的，如何结束线程？提供了什么方法

显式控制各个线程竞争的有哪些对象呢？

线程（线程池的维护/Synchronized/线程进程区别/死锁和如何解决

写一个java多线程

 为什么要使用多线程

Java中Thread与Runnable在线程管理上的区别

实现两个数组利用两个线程交替打印，且固定由第一个开始

工作内存和主内存。（这里是给了一个例子，主线程有一个变量a，子线程里用到了这个变量，问这两处的变量是不是一个东西）

线程安全。

// tencent

给你2个线程，如何产生死锁？为什么会产生死锁？

ThreadLocal

Thread直接继承和使用Runnable

线程的状态 // 2

有没有涉及过多线程编程，Java中线程同步有哪些方法

java如何实现线程的互斥

## 乐观锁

乐观锁和悲观锁，各自的使用场景

乐观锁和悲观锁

手写单例模式\(double-check\)

乐观锁写单例模式

## **synchronized与volatile关键字的作用**

说下Java的synchronized和volatile关键字，可见性，重排序，原子性

线程同步，我又说了sychroized

是否了解Java的atomic，以及好多很底层的东西 （原子性？

**wait\(\)的用法，notifyAll\(\)的用法，notify\(\)唤醒的是哪一个线程。**

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

**//**

讲讲violate，synchronized，静态方法synchronized和普通方法synchronized有什么不同，你在哪些场景用过这些，你考虑应该有哪些场景使用

讲讲default方法

synchronize关键字在字段和方法中使用区别

sychronize关键字修饰同类的两个方法，调用会阻塞吗？

有没有用到synchronized关键词，做什么用的，如果调用一个对象的两个synchronized方\*\*\*不会阻塞

## 多线程场景题

两个用volatile的方法分别对一个为0的常量++5000次，最后结果会是10000吗

如果有一个全局变量，有10000个线程，每个线程对这个元素做+1操作，那么结束后这个变量的值一定是10000吗？如果不是举例说明为什么不是？信号量的机制 // Tuji

线程和进程有什么区别，Java怎么使用线程，线程的新建和销毁的具体过程。

## wait\(\)

wait和sleep的区别？

sleep和wait的区别

## **锁**

锁的底层实现是怎样的

锁原理

 java 的锁怎么实现的？

lock锁和sy锁 以及使用场景

Java synchronized的类锁和对象锁，它们区别，哪些是对象锁，哪些是类锁

Java有哪几种锁

synchronized和可重入锁的区别

countdownLatch

synchronized reetrantlock

reentrantReadWriteLock

说说自旋锁，内部实现。

// tencent

你语言 Java 用的最多是吧？Java 里面有个共享变量，我想保证它的线程安全，比如对它的修改做到线程安全，应该怎么解决？那么加锁可以加什么锁？

volatile 关键字的具体作用是什么？

volatile 可不可以保证线程安全，在什么情况之下，可以保证线程安全？

Java 里面，Object 类有一个 hashCode\(\) 方法和 equals\(\) 方法，可以讲一下它们的区别吗？

什么时候要重写这两个方法？



什么是可重入锁

object.wait\(\) 可重入吗？

什么是公平锁，什么是非公平锁

自己基于原生方法实现一个公平锁

## **AsyncTask的原理。**

## **杂**

优先级翻转

`int`占多少字节【4】`byte`呢【1】，如何判断`byte`的从右数第n位是否为1，写个`if`语句【`((b >> n) & 1) == 1`】

Object有哪些**公有方法**。

//

java 有哪些语法糖

for-each 循环的原理

## **线程池 5**

线程池介绍，任务队列如果满了怎么办；

线程池源码

线程池，线程池参数，从提交任务开始的过程

线程池

线程池/线程池参数

n个线程，应该开多大的线程池

//

怎么创建线程池，类名说一下，线程 池类型

线程池设计的时候需要注意哪些事情？

设计一个线程池

如果只用到少量线程需不需要使用线程池

## **临界区概念**

## **引用 2**

强引用、软引用、弱引用、虚引用，是什么？分别在什么时候用

四大引用

四种引用 **软引用和弱引用的区别 软引用和强引用的区别**

**//**

**软引用是怎么用的，为什么有垃圾回收机制还能发生内存泄漏**

## **序列化 2**

反序列和序列化 为什么要？ 什么情况下要？

序列化和反序列化

{% embed url="https://www.runoob.com/java/java-serialization.html" %}

序列化就是将一个对象转换成字节序列，方便存储和传输。

## **反射 2**

反射 为什么要反射？ 什么时候用？ 缺点？

（反射 反序列化）

java**泛型，反射**

## **关键字 2**

static关键字：c跟java

static、final、finalize、finally？

final关键字

`final`关键字作用【修饰类不可继承，修饰方法不可重写，修饰对象无法重新赋值】

Java里的final有什么用法？

final关键字，final常量存储位置，常量池的好处

讲讲JAVA几个访问权限关键字

如下代码的会执行false吗？A a=new A\(\); System.out.println\(a isInstance of A\) ; **//** [**考察instanceof关键字用法**](https://www.runoob.com/java/method-instanceof.html)\*\*\*\*

## **编译**

java文件的编译方式，谁把源文件编译成.class文件

> 可以讲讲java和c

动态编译、静态编译

[https://www.jianshu.com/p/14c3d36e6ffa](https://www.jianshu.com/p/14c3d36e6ffa)

一个可执行文件的编译过程

[https://www.cnblogs.com/widget90/p/5577728.html](https://www.cnblogs.com/widget90/p/5577728.html)

## **json 2**

除了Json还有哪些数据传输格式。

Json解析的时候是怎么将json解析为对应的类。

## **==和.equals\(\)的区别？**

 // 这个可以说自己碰到的情况\[-128,127\]

重写equals方法\(写不出，面试官一直引导我，最后面试官区去开会去了，让我自己出去查一查，菜\)

讲一下**equals**\(\)。

//

==和equals的区别

## **重写和重载的区别。**

**印象深刻的就java重载能不能重载返回值不同的函数，这块没回答出，然后java重载能不能重载相同的类，但是模板不同的参数。**

## **String场景题**

引用：

String a = new String\(\);

b = a;

a = null;

b 是否= null?

String s=new String\("123"\);建立了几个对象

`String a = new String("abc")`与`String a = "abc"`的区别【前者分配在堆上，后者在常量池中】

String StringBuffer StringBuilder区别？

创建一个字符串对象，这个对象分配在哪里？

String str = “123” + “456”;会创建几个对象。

//

String s = new String\("hello"\)与String s = "hello"的区别

## **内存泄漏问题**

（Java中static引起的内存泄漏问题等）

内部类会有内存泄漏问题吗 内部类为什么能访问外部类的变量，为什么还能访问外部类的私有变量。

讲一下**内存泄漏**

Java可以自动管理内存，为什么会有**OOM**【可达性[算法](https:///jump/super-jump/word?word=%E7%AE%97%E6%B3%95)】

//

内存泄漏问题（Java中static引起的内存泄漏问题等）

内存泄漏？OOM？什么情况会OOM？

## **LRU**

LRU[算法](https:///jump/super-jump/word?word=%E7%AE%97%E6%B3%95)的`get`时间复杂度是多少，为什么【只知道是干什么的但不了解】（不知道属不属于java

LRU\*\*\*

为什么需要**\*? \***是介于哪两个硬件之间的? 简单介绍一下LRU。 然后让我大概写一下模拟LRU的数据结构。

LRU怎么实现

LruCache

LRU怎么实现\(hash+[链表](https:///jump/super-jump/word?word=%E9%93%BE%E8%A1%A8)\)，详细解释步骤、时间复杂度，

## **泛型**

Java中的泛型，类型擦除，如果说Java的泛型是伪泛型，为什么不直接用object代替

[https://blog.csdn.net/wangzhenxing991026/article/details/109785509](https://blog.csdn.net/wangzhenxing991026/article/details/109785509) ⬆️

泛型上界，下界定义/作用

java**泛型，反射**

**Java的泛型擦除问题**

**//**

**泛型概念，extends、super、泛型擦除。**

**反射联想到 Retrofit 动态\*\*\*实现**

**java 泛型方法如何确定类型**

**java 泛型中的?通配符**

## 类型擦除

Java的类型擦除

## **拷贝**

深拷贝/浅拷贝，怎么实现深-浅拷贝 CopyonWrite

讲一下**clone**\(\)，**深拷贝和浅拷贝**的区别。

//

深拷贝 浅拷贝（内存溢出or垃圾回收时有什么区别？）

深拷贝和浅拷贝

父类没有执行深拷贝呢，子类如何让父类深拷贝呢?

## **JMM - Java内存模型**

讲一下jmm

## Java 内存区域

static和final修饰变量的区别，这两种变量存储在什么内存区域？Java的OOM主要发生在什么地方，介绍一下Java的内存区域有哪些？如果加载一个1M的图片，主要存储在什么地方？

Java有几种内存模式，其中变量/方法/类分别储存在哪里，栈内存主要用来存放什么

## **堆栈**

如何在**栈上开辟空间**。

如何在**堆里开辟空间**。

怎么会造成栈溢出，堆溢出。

堆栈的区别

讲讲什么东西会导致一个类被NEW出来的时候对象在堆里面的大小不同

## **内存分配区域**

（Java层面回答？对象引用在堆和栈都有么？函数内部new的对象存放在哪？）

## 数据类型

一个结构体，有一个short类型，一个int，一个char，在32位机器中占用多少存储空间

## static

java静态内部类和非静态内部类的区别：内存分配,创建过程,内存泄漏问题？

Java中内部类和静态内部类的区别

Static 的理解

介绍一下Static这个命名字，以及用它命名的变量和类有什么不同于其他的地方

静态内部类是怎么实现单例的。

解释静态内部类单例的原理。

## 内部类

java 哪些内部类？内部类为什么局部变量用final

## 面向对象

面向对象的3个特性

面向对象的特点，与面向过程的区别

## 和xx的区别/对比

C++和JAVA的区别，java支持多继承吗

JAVA与JS（为什么都喜欢问这个？）

有C/C++/Java/Swift，询问你觉得这些语言有什么区别，优缺点，适用场景

指针了解吗？

java和C里new的区别

new 和 malloc的区别

Kotlin 与 Java 比较

## IDE

平时用啥IDE？知道项目run之前干什么吗？

> 说了个编译和检查错误，但是面试官似乎还想让我说点东西，知识盲区.....后来跟同学交流了一下，应该是预编译、编译、汇编、链接。

## 注解

注解介绍下？



