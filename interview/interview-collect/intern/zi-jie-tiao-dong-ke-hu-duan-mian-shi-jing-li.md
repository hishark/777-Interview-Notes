# 字节跳动客户端面试经历

{% embed url="https://www.nowcoder.com/discuss/427064" %}

**2020-4-24  投递简历**

 **2020-4-26  hr约1面**

 **2020-5-13  1面  43min**

 **自我介绍**

 [**项目**](/jump/super-jump/word?word=%E9%A1%B9%E7%9B%AE)**介绍**

 **Java相关**

 1、线程池介绍，任务队列如果满了怎么办；

 参考：[https://www.cnblogs.com/dolphin0520/p/3932921.html](https://www.cnblogs.com/dolphin0520/p/3932921.html)

 2、**CAS介绍**，CAS有什么问题，Java是否有解决方法；

 参考：[https://www.cnblogs.com/qjjazry/p/6581568.html](https://www.cnblogs.com/qjjazry/p/6581568.html)

 3、**HashMap**介绍，equals和hashCode函数；

 参考：[https://blog.csdn.net/woshimaxiao1/article/details/83661464](https://blog.csdn.net/woshimaxiao1/article/details/83661464)

 4、**final**关键字，final常量存储位置，**常量池**的好处；

 参考：[https://www.cnblogs.com/dolphin0520/p/3736238.html](https://www.cnblogs.com/dolphin0520/p/3736238.html)

 [https://www.jianshu.com/p/c7f47de2ee80](https://www.jianshu.com/p/c7f47de2ee80)

 **网络相关**

 1、**HTTPS**介绍；

 参考：[https://www.jianshu.com/p/14cd2c9d2cd2](https://www.jianshu.com/p/14cd2c9d2cd2)

 2、**TCP**三次握手和四次挥手；

 参考：[https://yuanrengu.com/2020/77eef79f.html](https://yuanrengu.com/2020/77eef79f.html)

 [**算法题**](/jump/super-jump/word?word=%E7%AE%97%E6%B3%95%E9%A2%98)

 **合并两个有序**[**链表**](/jump/super-jump/word?word=%E9%93%BE%E8%A1%A8)；面试官让我先写函数，然后在主函数中测试运行。 Leetcode：[https://leetcode-cn.com/problems/merge-two-sorted-lists/](https://leetcode-cn.com/problems/merge-two-sorted-lists/)  


 **2020-5-13** **1面结束后2小时，hr约2面，因2面面试官当天有事，所以约了下周二。**

 **2020-5-19  2面  60min**

 [**项目**](/jump/super-jump/word?word=%E9%A1%B9%E7%9B%AE)**介绍**

 主要做了什么，**是否还有可以优化的地方**。

 [**算法题**](/jump/super-jump/word?word=%E7%AE%97%E6%B3%95%E9%A2%98)

 **三个线程，线程1打印a，线程2打印b，线程3打印c，要求循环打印abc10次。** 参考： [https://blog.csdn.net/xiaokang123456kao/article/details/77331878?utm\_medium=distribute.pc\_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-2.nonecase&depth\_1-utm\_source=distribute.pc\_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-2.nonecase](https://blog.csdn.net/xiaokang123456kao/article/details/77331878?utm_medium=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-2.nonecase&depth_1-utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-2.nonecase)

 **Java相关**

 **volatile**关键字作用。 参考： [https://blog.csdn.net/u012723673/article/details/80682208?depth\_1-utm\_source=distribute.pc\_relevant.none-task&utm\_source=distribute.pc\_relevant.none-tas](https://blog.csdn.net/u012723673/article/details/80682208?depth_1-utm_source=distribute.pc_relevant.none-task&utm_source=distribute.pc_relevant.none-task) **2020-5-1** **9** **2面结束后** **4** **小时，hr约** **3** **面。**

 **2020-5-20** **3面 60min**

 [**算法题**](/jump/super-jump/word?word=%E7%AE%97%E6%B3%95%E9%A2%98)

 计算从一棵多叉树（节点取值不相同）的根节点走N步，能走到节点x的概率，任何一个走过的节点不能走第二次（即不能往回走），如果没路可以走可以原地走，如果有路可走，但是步数没用完需要接着走。

 例：

 1

 2            3            4

 5   6       7         8     9

 N = 2

 x = 6

 result = 1/6（第1步，从节点1走到节点2的概率为1/3；第2步，从节点2走到节点6的概率为1/2）

 class Node {

 int val;

 List&lt;Node&gt; subNodes;

 }

 float func\(Node root, int N, int x\){

 }

 个人思路：层次遍历，累积每层的数目，注意考虑结束条件。时间复杂度O\(n\)。

 **自我介绍**

 **场景题**

 **1、如何实现牛客网的在线编程。**

 个人理解：[客户端](/jump/super-jump/word?word=%E5%AE%A2%E6%88%B7%E7%AB%AF)通过HTTP的POST请求把代码传给服务端，服务端在编译运行之后把结果反馈给[客户端](/jump/super-jump/word?word=%E5%AE%A2%E6%88%B7%E7%AB%AF)。

 **2、在上述过程中，如果有多个服务器，如何平衡任务量。**

 个人理解：将服务器分成主服务器和辅服务器两种，主服务器负责接收[客户端](/jump/super-jump/word?word=%E5%AE%A2%E6%88%B7%E7%AB%AF)请求，并根据负载情况，将任务分派给相应的辅服务器编译运行，最后主服务器把结果反馈给[客户端](/jump/super-jump/word?word=%E5%AE%A2%E6%88%B7%E7%AB%AF)。

 **3、在上述过程中，如果主服务器的请求量过大，如何解决。**

 个人理解：设置多个主服务器，根据请求所在地域划分主服务器的处理范围，比如按照省份划分。

 **4、在上述过程中，如何实现不同地域的**[**客户端**](/jump/super-jump/word?word=%E5%AE%A2%E6%88%B7%E7%AB%AF)**输入同一个URL后访问不同的主服务器。**

 个人理解：在域名解析阶段，DNS服务器根据请求所在地域返回相应服务器的ip地址。

 **5、如果服务器在执行一个任务时，出现了异常，比如陷入死循环，一直占用CPU资源，那么如何监测出来。**

 个人理解：服务器启动一个监测进程，每隔一段时间监测一下其它进程的运行情况。但如何区分死循环还是程序在处理一个耗时任务，我不清楚。

 注：以上的个人理解不一定正确。

 [**项目**](/jump/super-jump/word?word=%E9%A1%B9%E7%9B%AE)**介绍**

 **Java相关**

 如何判断堆中哪些对象需要被**回收**。 参考：[https://www.cnblogs.com/czwbig/p/11127159.html](https://www.cnblogs.com/czwbig/p/11127159.html)

 **2020-5-22 HR面  20min**

 **2020-5-25 录用通知**

 **总结：**

 人生第一次实习面试，面试体验不错，感谢字节给予的面试机会。

 **各位牛客同仁发的**[**面经**](/jump/super-jump/word?word=%E9%9D%A2%E7%BB%8F)**还是挺有用的，有了这些面试问题，再结合搜索到的博客，认真学习、思考和总结。**

 感谢牛客同仁和博客博主的无私分享，南无阿弥陀佛。

