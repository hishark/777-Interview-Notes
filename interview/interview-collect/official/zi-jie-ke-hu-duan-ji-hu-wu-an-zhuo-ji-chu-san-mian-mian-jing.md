# 字节客户端几乎无安卓基础三面面经

{% embed url="https://www.nowcoder.com/discuss/450449" %}

背景：985渣硕，无安卓[项目](/jump/super-jump/word?word=%E9%A1%B9%E7%9B%AE)，只会Java，安卓基础约等于没有（只是自学了《第一行代码》前几章）  
 内推投了[客户端](/jump/super-jump/word?word=%E5%AE%A2%E6%88%B7%E7%AB%AF)，简历评估等了挺久才进面试的，但是一进了面试之后流程就跟火箭一样快![](https://uploadfiles.nowcoder.com/images/20191018/468200_1571394935765_09DD8C2662B96CE14928333F055C5580)  
 

## 一面 46min

1.  简单介绍[项目](/jump/super-jump/word?word=%E9%A1%B9%E7%9B%AE)
2.  了解哪些数据结构
3.  了解哪些[排序](/jump/super-jump/word?word=%E6%8E%92%E5%BA%8F)[算法](/jump/super-jump/word?word=%E7%AE%97%E6%B3%95)
4.  手撕代码：堆[排序](/jump/super-jump/word?word=%E6%8E%92%E5%BA%8F)
5.  Java集合类：a\)LinkedList与ArrayList；b\)HashMap扩容 ConcurrentHashMap
6.  TCP与UDP，区别及运用场景
7.  http是用的TCP还是UDP
8.  http与https的区别
9.  JVM内存模型（Static方法在哪个区）
10.  Activity生命周期，Activity启动模式，Handler[源码](/jump/super-jump/word?word=%E6%BA%90%E7%A0%81)
11.  代码题：[旋转数组](/jump/super-jump/word?word=%E6%97%8B%E8%BD%AC%E6%95%B0%E7%BB%84)

 （一面面试官很nice，答的时候卡壳还会给引导，问的问题、撕的代码都不难）  
 下午面完当天晚上就接到约二面的通知了 

## 二面 55min（部分问题有重叠的不再列出）

1.  final、finally、finalize的区别
2.  抽象类的成员变量与成员方法的继承
3.  socket是否了解，简单聊聊
4.  经典问题：在浏览器输入网址敲回车后经历了什么（这题我感觉我至少说了10分钟\[捂脸\]） a\)三次握手；b\)https的加密流程；c\)对称加密与非对称加密原理（RSA、AES）

> 是面试官配合配合不停追问才能说那么久的，以这个问题为引子开始，包括：  
> 1. dns，http；  
> 2. 二者用的tcp还是udp  
> 3. http报文格式；  
> 4. https加密过程;  
> 5. ca证书  
> 6.12306为什么要安装根证书；  
> 7. 非对称加密rsa的原理;  
> 8.还了解什么加密方式。  
> 这一连串问题我全部归于这一个初始问题中了

1.  数据库有哪几种隔离机制
2.  union与union all的区别
3.  MySQL的索引怎么实现的
4.  B+树查找的时间复杂度，数据结构讲一下
5.  设计模式：a\) 手撕DCL单例；b\) 还了解什么设计模式（讲了观察者模式、策略模式）
6.  JVM的垃圾回收机制，GC Roots有哪些，说说了解的垃圾回收器
7.  View的事件分发机制
8.  代码题：两数相加（[链表](/jump/super-jump/word?word=%E9%93%BE%E8%A1%A8)，要求原地实现，空间复杂度O\(1\)，这个犯蠢撕了好久结果还是靠强行打印发现的问题）

  
 面完后二面面试官希望直接进行三面，可惜似乎三面面试官在开会，所以另约在了两天后 

## 三面 70min （部分问题有重叠的不再列出）

1.  线程与进程
2.  死锁条件，如何排查、解决
3.  虚拟内存、分页机制，讲一讲LRU
4.  创建对象的方式有哪几种（new 反射 clone 序列化）
5.  序列化与反序列化
6.  反射中的class.forname\(\)与class.getclass\(\)二者有什么区别
7.  String.equals\(\)，StringBuffer
8.  类加载的过程讲一下
9.  Java锁的种类
10.  volatile关键字的作用、原理
11.  handler.post\(Runable\(\)\)，聊一聊这个
12.  ANR，OOM了解吗？
13.  代码题：a\) 螺旋遍历矩阵；b\)（变种）原地旋转图像
14.  聊人生聊理想聊爱好

  
 三场面试的面试体验都非常好，面试官感觉年龄都很接近，面试的过程也很会引导。安卓方面我如实说只学习过《第一行代码》，所以安卓方面基本只是问了一些简单的问题，主要还是考察简历中你写的会的东西。  
 经验和教训： 面试开头的自我介绍最好能够简单说明自己强项，好引导面试官多考你擅长的领域；当然简历也务必需要好好整理，至少让面试官有针对性地进行考察。

