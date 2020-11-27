# 字节提前批-客户端Android一面面经

{% embed url="https://www.nowcoder.com/discuss/450867" %}

*  Activity生命周期，onSaveInstanceState\(\)方法何时执行；
*  HandlerThread讲一下

 可以参考IntentService[源码](/jump/super-jump/word?word=%E6%BA%90%E7%A0%81)，我的博客： [https://blog.csdn.net/SPACESTUDIO/article/details/107302229](https://blog.csdn.net/SPACESTUDIO/article/details/107302229)  
  


*  SharedPreference的commit\(\)和apply\(\)区别，apply\(\)何时写磁盘，平时用哪个；

 apply\(\)的注解：The framework makes sure in-flight disk writes from apply\(\) complete before switching states。state应该是指Activity的，也就是说活动生命周期变化之前会写磁盘  
  


*  ANR，系统是怎样判断的；
*  访问控制符；如何在外部执行一个类的private方法；
*  内部类与静态内部类区别；
*  sleep与wait区别，sleep如何打断；
*  GC；
*  wait实现生产者消费者问题，如何做到同步；
*  synchronized与lock区别；
*  写一个线程安全的单例模式；volatile关键字作用；
*  编程：判断两个[链表](/jump/super-jump/word?word=%E9%93%BE%E8%A1%A8)是否相交并返回交点；
*  TCP如何保证可靠；
*  B树介绍下；B+树的区别。

 就是这些了，通过面试也了解了很多，求好运

