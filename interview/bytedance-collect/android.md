# Android

Handler机制，Looper.loop会不会阻塞线程，为什么？

框架源码（没看过，不会），**eventbus**有哪些缺点，什么类可以作为event，为什么不用广播

**dex**了解吗？我答只知道65535，了解类的编译过程吗，不了解；知道源文件编译成什么吗？class文件；为什么要有dex？在dex做了优化；哪些优化？不了解

dalvik和hotspot虚拟机了解吗

我做的是音乐播放器，所以面试官问音乐播放在哪里实现，activity还是**service**，用thread可以吗？为什么？

handler机制 looper，message，handler，queue

handler内存泄漏，内存泄漏的引用链是啥？（looper—&gt;messagequeue-&gt;message-&gt;handler,所以如果队列为空就不会泄露）

 扯到了对象池（Message类维护，每个message有next指针）

怎么解决内存泄漏（声明static，弱引用包裹）

Recyclerview缓存机制

fragment生命周期

binder机制（跳过）

## 碎碎念

感觉安卓会问到的问题来来回回就这么多的样子

我感觉针对简历上的项目可能会问一些想不到的点

到时候简历上项目千万别给自己挖坑啊- -



handler 不同场景

application

anr

onSaveInstanceState

dex

flutter dart

\*eventbus



