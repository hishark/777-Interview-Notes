# 字节跳动安卓客户端面经（安卓开发零经验）

作者：Aengus\
链接：[https://www.nowcoder.com/discuss/393929](https://www.nowcoder.com/discuss/393929)\
来源：牛客网\
\


字节实习生招聘开始的还是挺早的，一直很喜欢字节的名称与logo，而且一直对网上所传的“技术氛围”心有所往。但是听说字节的面试很难，所以在字节官微发布实习生招聘的推文后，最开始很没有底气，于是就准备了几天，把简历完善了一下，最后硬着头皮把简历发给了招聘推文下留的一个邮箱（事实上并不建议一开始就把简历投给自己喜欢的企业，毕竟第一次面试没有经验被挂的话还是挺伤心的）。

我自己是大三的数学系学生，平时涉及的东西挺多（图像处理、Flutter、后端），所以总感觉自己学的太杂而不精，自己的意愿是[客户端](https://app.gitbook.com/jump/super-jump/word?word=%E5%AE%A2%E6%88%B7%E7%AB%AF)或后端（偏后端多一些，感觉发展潜力更大），不过后端接触的比较晚，所以了解的并不深。发送邮件后很快就收到的回复，过了两天字节HR就打来电话约面试时间，还是挺快的，岗位是安卓[客户端](https://app.gitbook.com/jump/super-jump/word?word=%E5%AE%A2%E6%88%B7%E7%AB%AF)开发。官网的岗位说明上接受Android开发零基础，所以面试时没有问与Android相关的东西。

### 字节一面

* 自我介绍；
* Flutter热更新（这是因为[项目](https://app.gitbook.com/jump/super-jump/word?word=%E9%A1%B9%E7%9B%AE)经历中有一个Flutter软件）【Dart语言特性，采用JIT方式实现】
* `String a = new String("abc")`与`String a = "abc"`的区别【前者分配在堆上，后者在常量池中】
* `ArrayList`与`LinkedList`区别，**查找的时间复杂度**是多少【底层实现方式不一样】
* String类如何被加载的【类加载机制】；双亲委派模型【常规题】
* `final`关键字作用【修饰类不可继承，修饰方法不可重写，修饰对象无法重新赋值】
* 计算机网络七层/五层协议；TCP属于哪一层【传输层】，TCP与UDP协议区别
* [算法](https://app.gitbook.com/jump/super-jump/word?word=%E7%AE%97%E6%B3%95)：单[链表](https://app.gitbook.com/jump/super-jump/word?word=%E9%93%BE%E8%A1%A8)的逆序、[算法](https://app.gitbook.com/jump/super-jump/word?word=%E7%AE%97%E6%B3%95)的时间复杂度与空间复杂度

### 字节二面

* [项目](https://app.gitbook.com/jump/super-jump/word?word=%E9%A1%B9%E7%9B%AE)（如何实现的某个功能；知道哪些加密[算法](https://app.gitbook.com/jump/super-jump/word?word=%E7%AE%97%E6%B3%95)）
* Java可以自动管理内存，为什么会有**OOM**【可达性[算法](https://app.gitbook.com/jump/super-jump/word?word=%E7%AE%97%E6%B3%95)】
* 可以作为GCRoot根的对象有哪些【局部变量表中的对象，静态变量，常量，本地方法栈中的对象】
* 设计一个K-V的数据结构应该考虑哪些问题，如何解决这些问题【说了一下**哈希碰撞，多线程访问，初始容量**等】
* 在浏览器中输入一个网站点击**回车**会发生什么【常规题】
* 浏览器渲染页面完成后会保持TCP连接吗【根据Connection请求头，若为[`keep`](https://app.gitbook.com/jump/super-jump/word?word=keep)`-alive`则保持】
* TCP四次挥手过程【常规题】；[客户端](https://app.gitbook.com/jump/super-jump/word?word=%E5%AE%A2%E6%88%B7%E7%AB%AF)发送完最后一个ACK后会进入什么状态【`time_wait`后进入`CLOSED`状态】
* [算法](https://app.gitbook.com/jump/super-jump/word?word=%E7%AE%97%E6%B3%95)1：给定一个数组，**将奇数排在左边，偶数排在右边**【利用快排的思想很快就可以做出来】
* [算法](https://app.gitbook.com/jump/super-jump/word?word=%E7%AE%97%E6%B3%95)2：给定一个三角形，找出自顶向下的**最小路径和**。每一步只能移动到下一行中相邻的结点上。 例如，给定三角形： \[ \[2], \[3,4], \[6,5,7], \[4,1,8,3] ] 自顶向下的最小路径和为 11（即，2 + 3 + 5 + 1 = 11）【遍历路径求和】

### 字节三面

* 前两面感觉怎么样
* `synchronized`与`volatile`关键字的作用
* 给定代码，会输出`i`等于什么；如何令`i`输出为1【用`static`与`volatile`修饰，主线程调用`sleep()`】；如何保证`i`一定输出为1，写一下代码【用`wait()`与`notifyAll()`？】；`Runnable`的`run()`方法中使用`this`指的是什么，`Runnable`还是`Thread`【`Runnable`的匿名内部类】

```java
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

* `int`占多少字节【4】`byte`呢【1】，如何判断`byte`的从右数第n位是否为1，写个`if`语句【`((b >> n) & 1) == 1`】
* [算法](https://app.gitbook.com/jump/super-jump/word?word=%E7%AE%97%E6%B3%95)1：给定一个`byte`返回倒序排列后的`byte`，如输入`10110000`返回`00001101`【面试官提醒可以用移位保存每个位置的值然后再倒序】
* LRU[算法](https://app.gitbook.com/jump/super-jump/word?word=%E7%AE%97%E6%B3%95)的`get`时间复杂度是多少，为什么【只知道是干什么的但不了解】
* 4个CPU，16个数，每个CPU每次只能比较一次两个数的大小，只能返回`true`或`false`，互相之间不能通信，一轮以时间片为单位，需要几轮能够找出最大的数（4个CPU与4个数，可以一轮就找到最大的数吗）
* [算法](https://app.gitbook.com/jump/super-jump/word?word=%E7%AE%97%E6%B3%95)2：两个数字非常大的`String`，对其求和，如`"999","2"->"1001"`【转为`char[]`倒序相加，注意进位】
* 你从专业课中**最大的收获**是什么
* 还有什么想问的吗

字节的面试体验还是挺好的，面试官态度挺不错，人生的第一次面试没有留下不好的回忆。前两面面试自我感觉还可以，第三面直接给整懵了，问的太细了，一个点一直往深里问，有很多之前都没注意的地方，所以面试完心态都崩了。

许愿能过🙏
