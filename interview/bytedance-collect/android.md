# Android

**Handler**

Handler机制，Looper.loop会不会阻塞线程，为什么？

handler机制 looper，message，handler，queue

handler内存泄漏，内存泄漏的引用链是啥？（looper—&gt;messagequeue-&gt;message-&gt;handler,所以如果队列为空就不会泄露）

handle作用

Handler的原理。Looper，MessageQueue，Message。面试官追问在一个Handler中给另一个Handler发送消息



扯到了对象池（Message类维护，每个message有next指针）

怎么解决内存泄漏（声明static，弱引用包裹）

有没有接触过安卓，怎么看内存占用情况

框架源码（没看过，不会），**eventbus**有哪些缺点，什么类可以作为event，为什么不用广播

**dex**了解吗？我答只知道65535，了解类的编译过程吗，不了解；知道源文件编译成什么吗？class文件；为什么要有dex？在dex做了优化；哪些优化？不了解

dalvik和hotspot虚拟机了解吗

我做的是音乐播放器，所以面试官问音乐播放在哪里实现，activity还是**service**，用thread可以吗？为什么？

Recyclerview缓存机制

fragment生命周期

binder机制 2 

怎么学安卓



**安卓多线程 2**

Android中多线程使用方式。面试官追问如何停止一个线程。

有没有写过安卓的多线程



有没有用过什么框架

安卓生命周期

项目中询问一个 A Activity 跳到一个 B Activity中，生命周期的走动，点击Back返回呢。如果一个 A Activity是透明的呢？如果 B Activity是一个Dialog呢？面试官追问横竖屏切换生命周期走动，以及是否了解onConfigurationChanged。

Android静态库和动态库的区别

使用addView达到弹出框的效果，但是耗时长。后来了解Fragment，使用Fragment代替addView。面试官追问你能分析为什么这么慢吗，我就说了Android的Activity-&gt;PhoneWindow-&gt;DecorView-&gt;ContentView-&gt;WindowManager-&gt;RootViewImpl的绘制流程。面试官继续追问ANR出现的类型，原因以及排查的方式。面试官继续追问Fragment和Activity的区别以及Fragment的优点。

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



