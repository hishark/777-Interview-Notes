# 字节跳动面经|iOS开发|大三暑期实习（已收offer）

作者：牛客151369345号\
链接：[https://www.nowcoder.com/discuss/420264](https://www.nowcoder.com/discuss/420264)\
来源：牛客网\
\


本人某985大三学生，没有开发类的[项目](https://app.gitbook.com/jump/super-jump/word?word=%E9%A1%B9%E7%9B%AE)经历，在实验室和导师干过一点科研，大三找暑期实习，4.1号投了字节的后端开发，又被转岗到iOS开发（然而其实从没用过苹果）

 准备面试期间受到好多大佬的指点，现收到offer，也写个[面经](https://app.gitbook.com/jump/super-jump/word?word=%E9%9D%A2%E7%BB%8F)还愿，希望能对大家有所帮助

####  一面（4.15）

1.  自我介绍
2.  [项目](https://app.gitbook.com/jump/super-jump/word?word=%E9%A1%B9%E7%9B%AE)细节，这个[项目](https://app.gitbook.com/jump/super-jump/word?word=%E9%A1%B9%E7%9B%AE)中你解决的印象最深刻的问题是什么。
3.  C++的虚函数虚表
4.  如果很多的客户和服务器连接，会建立几个TCP连接
5.  TCP的慢启动机制
6.  new和malloc的区别，你觉得new会调用malloc吗
7.  内联函数的机制，有什么优缺点
8.  C++在调用函数时编译器会怎么做？
9.  内存分页的机制，如果发生了颠簸（有的也叫抖动），会有什么体现
10.  C++内存堆和栈的区别
11.  [算法题](https://app.gitbook.com/jump/super-jump/word?word=%E7%AE%97%E6%B3%95%E9%A2%98)：（面试官问我想做个[动态规划](https://app.gitbook.com/jump/super-jump/word?word=%E5%8A%A8%E6%80%81%E8%A7%84%E5%88%92)，贪心还是搜索，我选了[动态规划](https://app.gitbook.com/jump/super-jump/word?word=%E5%8A%A8%E6%80%81%E8%A7%84%E5%88%92)）

     一套卷子，这个卷子有n个多项选择题，每个选择题有A、B、C、D四个选项。每道多项选择题的答案有15种

     要求: 按顺序做下来，做完每一题的时候，目前正确答案中A出现的次数和C出现的次数差距不超过1，B出现的次数和D出现的次数差距不超过2.

     举个例子：有两个选择题，那么第一题答案为AC，第二题答案为A，这是满足要求的，因为做完第一题的时候A出现了1次C出现了1次，做完第二题的时候A出现了2次，C出现了1次。

     如果第一题答案是AD，第二题答案是A，那么做完第一题的时候A出现了1次，D出现了1次，符合要求。做完第二题的时候A出现了2次，C出现了0次，D出现了1次，A和C差距为2，则不符合要求。

     如果有n个多项选择题，那么一共有多少种试卷答案是符合牛牛的要求的。

     另:我朋友面了字节[算法](https://app.gitbook.com/jump/super-jump/word?word=%E7%AE%97%E6%B3%95)岗，他遇到的[算法题](https://app.gitbook.com/jump/super-jump/word?word=%E7%AE%97%E6%B3%95%E9%A2%98)是：[数组中只出现一次的数字](https://app.gitbook.com/jump/super-jump/word?word=%E6%95%B0%E7%BB%84%E4%B8%AD%E5%8F%AA%E5%87%BA%E7%8E%B0%E4%B8%80%E6%AC%A1%E7%9A%84%E6%95%B0%E5%AD%97)（[leetcode](https://app.gitbook.com/jump/super-jump/word?word=leetcode)136）和[买卖股票的最佳时机](https://app.gitbook.com/jump/super-jump/word?word=%E4%B9%B0%E5%8D%96%E8%82%A1%E7%A5%A8%E7%9A%84%E6%9C%80%E4%BD%B3%E6%97%B6%E6%9C%BA)（Leetcode121，Leetcode188）
12.  你有什么想问我的

####  二面（4.21）

1.  自我介绍
2.  [项目](https://app.gitbook.com/jump/super-jump/word?word=%E9%A1%B9%E7%9B%AE)细节
3.  说一下TCP的拥塞控制机制
4.  TCP的稳定性体现在哪？四次挥手最后为什么要等待2MSL时间才断开？
5.  说一下C++和python的区别，它们各有什么特点
6.  说一下C++的内存分区，了解bss段吗
7.  malloc函数调用时要说明分配的内存大小，但是free的时候不需要，这是为什么
8.  vector和list有什么区别？各有什么优缺点？
9.  用过智能指针吗？
10.  如果有一个全局变量，有10000个线程，每个线程对这个元素做+1操作，那么结束后这个变量的值一定是10000吗？如果不是举例说明为什么不是？信号量的机制
11.  问了一个Linux指令，原谅我忘记是什么了，当时说的不了解
12.  char \*p="123445"和char p\[]="123445"这两条指令有什么区别
13.  extern "c"这条指令的功能是什么
14.  [算法题](https://app.gitbook.com/jump/super-jump/word?word=%E7%AE%97%E6%B3%95%E9%A2%98)：一颗[二叉树](https://app.gitbook.com/jump/super-jump/word?word=%E4%BA%8C%E5%8F%89%E6%A0%91)，每条从根节点到叶子节点的路径可以看作一个整数，例如1->2->3就是123，求出所有这种路径对应的整数和
15.  [算法题](https://app.gitbook.com/jump/super-jump/word?word=%E7%AE%97%E6%B3%95%E9%A2%98)：最大子序列和（Leetcode53）

####  三面（4.23）

1.  自我介绍
2.  [项目](https://app.gitbook.com/jump/super-jump/word?word=%E9%A1%B9%E7%9B%AE)细节
3.  上次面试的第9，13会了没有（二面时没答出来，还好后来查了）
4.  C和C++在编译时的区别
5.  new一个对象和直接声明一个对象有什么区别
6.  C++除了堆栈还有什么内存区域
7.  对于一个图形用户界面，当你点击一个组件(比如按钮)，系统怎么快速找到要调用的程序？（这道题面试官给了提示：一般几个组件类是包含在同一父类里的，所以可以先确定大范围，再逐步缩小范围）
8.  一个多路搜索树，每个节点有m个子节点，树高度为n，查找的时间复杂度。
9.  你了解你面试的部门是干啥的吗
10.  [职业规划](https://app.gitbook.com/jump/super-jump/word?word=%E8%81%8C%E4%B8%9A%E8%A7%84%E5%88%92)是啥，毕业了有什么打算
11.  你不在北京上学，实习能来北京吗
12.  你有什么问我的吗

####  4.28接到HR电话，了解基本情况，说offer正在审批。4.29 正式收到offer

####  一些关于面试的个人建议

1.  字节的面试好像比较看重[算法题](https://app.gitbook.com/jump/super-jump/word?word=%E7%AE%97%E6%B3%95%E9%A2%98)，我在第二面的时候面试官问的一些基础知识并没有答出来，但[算法题](https://app.gitbook.com/jump/super-jump/word?word=%E7%AE%97%E6%B3%95%E9%A2%98)写的还可以。感觉如果在面试中能给出最优时空的算\*\*\*很加分。建议面试前把Leetcode top100，[剑指offer](https://app.gitbook.com/jump/super-jump/word?word=%E5%89%91%E6%8C%87offer)，以及[动态规划](https://app.gitbook.com/jump/super-jump/word?word=%E5%8A%A8%E6%80%81%E8%A7%84%E5%88%92)的几个常见题型尽量刷一刷，如果没时间写程序可以大致看一下解法，有个印象。
2.  每次面试后不会的问题一定要查明，例如我三面的面试官就问了二面时不会的题目
3.  基础知识要尽量做到知其然也知其所以然，比如B+树的叶子节点为什么要串成[链表](https://app.gitbook.com/jump/super-jump/word?word=%E9%93%BE%E8%A1%A8)，TCP四次挥手为什么最后要等两个MSL才释放
4.  如果面试官提出的问题不是很熟悉，可以把自己熟悉的部分先说一下，多多少少可以起到补救的作用.
5.  简历中的[项目](https://app.gitbook.com/jump/super-jump/word?word=%E9%A1%B9%E7%9B%AE)一定要熟悉，尤其是里面提到的数字（比如准确率达到90%），一定要明确是如何计算的，切忌造假
6.  切忌说自己精通某种语言（大佬除外），如果你对某种语言有自信，可以在开始的自我介绍时说自己比较熟悉某种语言
7.  最后面试官问你有什么想问我吗，可以问您对我有什么评价，如果回答基础好过的可能性会比较大，如果回答要加强基础，很可能是挂了

 最后祝大家都能收到想要的offer
