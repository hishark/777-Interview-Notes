# Interview 2

[字节跳动的校招面试精髓（提前批免笔试）](https://www.nowcoder.com/discuss/373163?type=post&order=time&pos=&page=2&channel=1009&source_id=search_post)

作者：神迹难觅  
链接：[https://www.nowcoder.com/discuss/373163?type=post&order=time&pos=&page=2&channel=1009&source\_id=search\_post](https://www.nowcoder.com/discuss/373163?type=post&order=time&pos=&page=2&channel=1009&source_id=search_post)  
来源：牛客网

[字节跳动](https://github.com/hishark/777-Interview-Notes/tree/ef739eabf33b61414b4af8a4ed176c4cd57067e6/jump/super-jump/word?word=字节跳动/README.md)面试具有一定的特点，下面谈一些自己的了解以及自己的经验（不多谈面试题） 1. 必考[算法](https://github.com/hishark/777-Interview-Notes/tree/ef739eabf33b61414b4af8a4ed176c4cd57067e6/jump/super-jump/word?word=算法/README.md)一般每一面各有一个[算法](https://github.com/hishark/777-Interview-Notes/tree/ef739eabf33b61414b4af8a4ed176c4cd57067e6/jump/super-jump/word?word=算法/README.md)作为压轴（根据岗位等情况）。对于[leetcode](https://github.com/hishark/777-Interview-Notes/tree/ef739eabf33b61414b4af8a4ed176c4cd57067e6/jump/super-jump/word?word=leetcode/README.md)的hot前100，[剑指offer](https://github.com/hishark/777-Interview-Notes/tree/ef739eabf33b61414b4af8a4ed176c4cd57067e6/jump/super-jump/word?word=剑指offer/README.md)的67道题，自然必须要会的。其他的就多多益善。而且[算法](https://github.com/hishark/777-Interview-Notes/tree/ef739eabf33b61414b4af8a4ed176c4cd57067e6/jump/super-jump/word?word=算法/README.md)也不只是可以写出来就ok了，最好能更进一步。 针对有的[算法](https://github.com/hishark/777-Interview-Notes/tree/ef739eabf33b61414b4af8a4ed176c4cd57067e6/jump/super-jump/word?word=算法/README.md)可以快速写出多种解决方法，并能很好的针对 时间空间复杂度作出对比。代码中变量，函数命名也要注意明确，多注意[算法](https://github.com/hishark/777-Interview-Notes/tree/ef739eabf33b61414b4af8a4ed176c4cd57067e6/jump/super-jump/word?word=算法/README.md)的边界问题。当然想做到这些肯定都需要不懈的努力。

1. 面试常问一些网络、操作系统的基本问题，常见的包括但不限于以下方面
2. tcp连接的三次握手，四次挥手。
3. 网络的拥塞控制的基本四种[算法](https://github.com/hishark/777-Interview-Notes/tree/ef739eabf33b61414b4af8a4ed176c4cd57067e6/jump/super-jump/word?word=算法/README.md) 慢开始，拥塞避免，快重传，快恢复。
4. tcp连接和释放中的状态有哪些，以及如果日志中出现某些状态码过多如何处理。
5. http连接中状态码有哪些，如果出现某些错误的状态码，分析出是什么情况吗？
6. 线程和进程的区别，java，go，python的线程模型的区别。
7. java的常见问题（如果做过java开发）。
8. linux的常见操作。
9. 业务开发中使用的git命令。
10. http2.0和http1.1的区别，http2.0的原理。

    这里其实就是基础，包括在大学里学习到的基础理论知识和在实习岗位中所获得的实践知识。

11. [项目](https://github.com/hishark/777-Interview-Notes/tree/ef739eabf33b61414b4af8a4ed176c4cd57067e6/jump/super-jump/word?word=项目/README.md)的提问，在准备阶段，一定要在自己的[项目](https://github.com/hishark/777-Interview-Notes/tree/ef739eabf33b61414b4af8a4ed176c4cd57067e6/jump/super-jump/word?word=项目/README.md)中要注意5点，业务背景和意义、业务难度、业务优化、业务达到的效果、业务未来的发展
12. 业务背景和意义，这点大家经常忽略，其实这点在面试中也是很重要的一项，你要清楚你的业务为什么要做，做了能带来什么收益（最好能够量化）。
13. 业务难度，很多校招生都会在这里提到这点，但不足的是没有简述清楚业务的难度具体体现在哪些地方，（比如说如果你说是业务中逻辑复杂，那就描述清楚，自己的业务为什么逻辑复杂。拿国际化的业务举例，比如国际化业务中会有几百个国家，业务在每个国家都有很多不同的细节要求，怎么做才能在后期的迭代中更易于维护，更易于扩展，这就是难点），最后谈谈使用哪些方法应对出现的这些难点。
14. 业务优化，[项目](https://github.com/hishark/777-Interview-Notes/tree/ef739eabf33b61414b4af8a4ed176c4cd57067e6/jump/super-jump/word?word=项目/README.md)开发可能会经历很多次迭代，业务也可能会发展迅速，最终都可能暴露出很多问题，而这些问题你在后续开发中使用什么方法优化解决的，优化前和优化后的比较（最好具有量化标准，无论是qps还是错误率等）。
15. 业务达到的效果，这个很多校招同学经常忽略，或者从没有了解过。这点也是面试官所经常 care 的点，业务开发人员要有主人公的精神，不仅完成好[项目](https://github.com/hishark/777-Interview-Notes/tree/ef739eabf33b61414b4af8a4ed176c4cd57067e6/jump/super-jump/word?word=项目/README.md)的开发，还要有推动产品发展的想法和行动。
16. 业务未来的发展，这个是可选项和业务达到的效果类似，如果写可以加上当前业务与竞品的对比（优缺点的对比，功能的对比），以及未来需要做什么。
    1. 中间件，中间件是大佬们平时喜欢钻研的一部分，因为中间件在很多业务中都会使用到的，了解中间件的学习收益比了解其他业务的收益要高很多，对以后换工作有很大的帮助，并且大多中间件都在团队中经过了长期打磨，无论是架构 、业务处理的技巧、语言特性的使用都是非常值得我们去学习的。如果想作为一个合格的 bytedancer，除了了解中间件的原理以外，我们必须还要做到能够举一反三。要考虑某些技巧，抽象的思维是否如何能够在自己的[项目](https://github.com/hishark/777-Interview-Notes/tree/ef739eabf33b61414b4af8a4ed176c4cd57067e6/jump/super-jump/word?word=项目/README.md)中有所使用， 从而提高[项目](https://github.com/hishark/777-Interview-Notes/tree/ef739eabf33b61414b4af8a4ed176c4cd57067e6/jump/super-jump/word?word=项目/README.md)的性能、可扩展性等。 
17. 自己的技术文档，大多数做技术的同学都会写写博客，会在简历中贴出自己的博客，但是有的同学的博客质量很差，包括但不限于以下问题，
18. 技术原理的不准确，甚至错误的描述。
19. 内容结构和文章排版的混乱。
20. 文档中还会包含很多错别字。

    一个人所做的文章也能体现出这个人对待工作和技术的态度，所以在写文章时要时刻保证严谨的态度，自己的文章尽量做到排版工整，内容丰富，这样无论是别人看还是自己看都会很愉悦，并且会带来更新的欲望。

21. 智力题，这部分需要准备一些常见智力题的回答。
22. 场景设计题，这部分不要急于回答，可以思考更全面的时候在在作出回答。为了更好的回答这类问题，需要在完成自己的业务开发任务外，还要主动参与到更多的[项目](https://github.com/hishark/777-Interview-Notes/tree/ef739eabf33b61414b4af8a4ed176c4cd57067e6/jump/super-jump/word?word=项目/README.md)流程中（包括技术评审，review，开发），对自己不owner的[项目](https://github.com/hishark/777-Interview-Notes/tree/ef739eabf33b61414b4af8a4ed176c4cd57067e6/jump/super-jump/word?word=项目/README.md)也要有所了解。 同时也多和同事或者同学讨论技术方案，这种交流碰撞往往会让你的思维更加活跃。在了解过很多业务场景的时候并总结出自己的解决方案后，你再面对场景设计题便会得心应手。 如果以上的都可以做的很好，我相信你的评分必然在3.5及以上。

