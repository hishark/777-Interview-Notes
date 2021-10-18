# BAT集齐！Java/安卓暑期实习面经汇总

作者：Goldfische\
链接：[https://www.nowcoder.com/discuss/414219](https://www.nowcoder.com/discuss/414219)\
来源：牛客网\
\
本人情况：大三本科生，去年暑假因为学校课程开始接触安卓，前后一共写过三个小[项目](https://app.gitbook.com/jump/super-jump/word?word=%E9%A1%B9%E7%9B%AE)。参与过一点实验室的[项目](https://app.gitbook.com/jump/super-jump/word?word=%E9%A1%B9%E7%9B%AE)开发，在其中负责一些小模块的实现。 在准备实习以及接受面试的过程中，牛友的[面经](https://app.gitbook.com/jump/super-jump/word?word=%E9%9D%A2%E7%BB%8F)对我的帮助非常大，在这里主要从一定要看和面试问题来分享一下。 **本贴持续更新\~** 需要注意的是，[字节跳动](https://app.gitbook.com/jump/super-jump/word?word=%E5%AD%97%E8%8A%82%E8%B7%B3%E5%8A%A8)是如果一面过了可能连着二面，二面过了连着三面这样，所以要提前准备齐全。或者直接和联系你的hr联系说接下来有事，调整时间。



作者：Goldfische\
链接：[https://www.nowcoder.com/discuss/414219](https://www.nowcoder.com/discuss/414219)\
来源：牛客网\
\


## 一定要准备

###  简历

 一份好的简历是十分重要的。其实我的[项目](https://app.gitbook.com/jump/super-jump/word?word=%E9%A1%B9%E7%9B%AE)经历并没有很丰富，99%也都是课程作业。但我建议大家写简历的时候 **不要概述的罗列自己大学期间所有的**[**项目**](https://app.gitbook.com/jump/super-jump/word?word=%E9%A1%B9%E7%9B%AE)**列表**，挑选部分你觉得十分出彩的进行重点描述，在简历上可以 **用分论点的方式讲述你在这个**[**项目**](https://app.gitbook.com/jump/super-jump/word?word=%E9%A1%B9%E7%9B%AE)**中使用了什么方法实现了什么功能**。 我是使用超级简历的大学生互联网春招简历模板编辑的，大概就是分教育经历/实习经历/科研经历基本技能几块，其实在简历上也就列出了3[项目](https://app.gitbook.com/jump/super-jump/word?word=%E9%A1%B9%E7%9B%AE)1研究经历。 另外在面试前一定要再 **挖挖看自己的**[**项目**](https://app.gitbook.com/jump/super-jump/word?word=%E9%A1%B9%E7%9B%AE) ，这个部分当时我是怎么什么实现的，现在有没有更好的方法对他进行改善，要表达出你对自己做完的[项目](https://app.gitbook.com/jump/super-jump/word?word=%E9%A1%B9%E7%9B%AE)并不是做完扔掉，你是把他当孩子一样一直继续努力去改善他。

###  知识点

 这里主要总结不管哪里一定会问到的知识点 

1\. 线程（线程池的维护/Synchronized/线程进程区别/死锁和如何解决 

2\. Hashmap的具体实现 

3\. TCP/UDP的区别/HTTP相关知识点/浏览器输入网址之后的具体操作



作者：Goldfische\
链接：[https://www.nowcoder.com/discuss/414219](https://www.nowcoder.com/discuss/414219)\
来源：牛客网\
\


## 字节

###  一面

 1\. 自我介绍 2. [项目](https://app.gitbook.com/jump/super-jump/word?word=%E9%A1%B9%E7%9B%AE)介绍 3. final关键字 4. activity之间的切换/返回 5. 线程池 6. 死锁 7. 线程通信 8. 同步 9. http头 10. 笔试

//笔试1： // 写一个java多线程

//笔试2： char\[] www.people.com.cn char\[] www.elpoep.moc.nc //在原数组上操作，不使用 String 的类方法，不创建额外的空间（数组、堆、栈、对列等）

###  二面

 1\. 自我介绍 2. [项目](https://app.gitbook.com/jump/super-jump/word?word=%E9%A1%B9%E7%9B%AE)介绍 3. 如果多图片进行压缩：bitmap 4. 如何正常显示图片 5. hashmap 6. 四大组件 7. contextprovider 8. android中多种数据存储类型的应用场景 9. 笔试

//笔试： // 你有一个函数random7可以等概率随机产生1\~7中的一个值 // 现在用这个random7去实现一个random10.

###  三面

 1\. 自我介绍 2. [项目](https://app.gitbook.com/jump/super-jump/word?word=%E9%A1%B9%E7%9B%AE)介绍 3. [项目](https://app.gitbook.com/jump/super-jump/word?word=%E9%A1%B9%E7%9B%AE)中提到的纯自主实现的拍摄/实时预览是怎么实现的 4. 如果做登录界面，如何保证账号密码的安全性 5. GET/POST区别 6. 其他的HTTP请求 7. 线程池/线程池参数 8. 为什么要使用多线程 9. n个线程，应该开多大的线程池 10. 笔试

笔试： struct treeNode{ treeNode left, right; int val; }; //实现是否为AVL树的判断 bool isBalance(treeNode root){ }

##  反问总结

 1\. 觉得之前的面试过程中有哪些不足 2. 部门主要业务内容 3. 阅读[源码](https://app.gitbook.com/jump/super-jump/word?word=%E6%BA%90%E7%A0%81)的技巧\
 整体感觉下来，一定要有一个好的简历，在面试过程中其实感觉我的准备并没有很充分，完全是靠简历被捞。对自己不了解的问题，可以先表明自己不了解/没有尝试过，但可能可以猜测或者用自己一些课外知识尝试解答一下。 

另外这里分享一点面试技巧/感悟：

字节的笔试鼓励你和面试官进行沟通，你可以把你的思路和面试官进行分享，明确题目的意思和输入输出。 遇到不会的笔试题，可以尝试和面试官聊聊想法，分享一下你现在的一些想法和思路，面试官一般也会提示你。 

另外还有一点，阿里的现场笔试一般都是压力笔试，虽然说会给你指定时间，但是你可以一直一直写下去，直到你觉得你写完为止，不要主动放弃或者中途叫停。 希望这些面试经验对牛友们有帮助，大家都能找到心仪的offer\~
