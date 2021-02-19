# question draft

## **Handler**

Handler机制，Looper.loop会不会阻塞线程，为什么？

handler机制 looper，message，handler，queue

handler内存泄漏，内存泄漏的引用链是啥？（looper—&gt;messagequeue-&gt;message-&gt;handler,所以如果队

列为空就不会泄露）

handle作用

Handler的原理。Looper，MessageQueue，Message。面试官追问在一个Handler中给另一个Handler发送消息

主线程的looper.loop\(\)是谁在调用

Handler的原理（Handler、Looper、MessageQueue等）

Handler机制\(**延时消息机制、handler泄漏原理**\)

异步消息处理流程，如果发送一个延时消息，messagequeue里面怎么个顺序，messagequeue是个什么数据结构

handler 如何切换线程\(handler聊了挺久\)

handler **如何回调**

handler注意事项\(**预防内存泄漏**\)

handler封装使用\(handlerThread IntentService\)

Handler和Looper（单个Looper和多个Handler）

Handler内存泄漏

Handler原理。 （讲完后，问了一下**取出message之后怎么知道要给哪个handler分发**）

HandlerThread原理。

Looper。（大致就是想让回答 **Android是依靠事件驱动的，通过Looper.loop\(\)不断进行消息循环之类的**）

扯到了对象池（Message类维护，每个message有next指针）

> 四大组件，生命周期函数，view的绘制流程，事件分发机制。

## **内存泄漏**

怎么解决内存泄漏（声明static，弱引用包裹）

有没有接触过安卓，怎么看内存占用情况

内存溢出和内存泄漏，提到了bitmap

什么时候会发生**内存泄漏**

内存泄漏的可能原因

内存泄漏，以及使用过哪些工具

AS里面有哪些**常用的工具**，第三方的也行。我竟然不知道，。。

什么情况会导致**内存抖动**，举个例子

## **View**

View的绘制过程（OnMeasure、OnLayout、OnDraw）

view绘制流程

如何去绘制一个view

设计一个自定义View,View中包含图片和文字，并且只能继承View

子View如何让父view不拦截触摸事件，requestDisAllowIntercept啥的。

Android里布局用过哪些？怎么自定义View? View的绘制大概是个怎么样的流程？

**WebView**机制

## **Binder 进程间通信**

Binder机制以及原理（binder驱动、共享内存等）

进程间通信的方式，安卓中有哪些方式，**为什么是基于Binder的，不用传统的操作系统进程间通信方式呢**

binder机制 2

## **多线程**

线程有没有了解过？线程安全呢？ Android里有接触过动画吗？怎么实现的？

安卓多线程 3

Android中多线程使用方式。面试官追问如何停止一个线程。

有没有写过安卓的多线程

安卓的 线程通信 和进程通信 机制

进程通信底层

线程和进程以及Android中的对应关系

Android的线程同步机制和进程通信机制

一个app如何管理线程

怎么创建线程池，类名说一下，线程 池类型

## **进程**

讲讲Android进程。前台进程、后台进程……这块不大会

一个app可以开启多个进程嘛，怎么做呢，每个进程都是在独立的虚拟机上嘛

项目中定时为什么用AlarmManager，不用postDelayed

项目中后台网络请求为什么用service不用线程

## **Eventbus**

eventbus 2

eventbus实现

框架源码（没看过，不会），

eventbus有哪些缺点，什么类可以作为event，为什么不用广播

## **广播**

广播的种类，注册的方式，以及不同注册方式的生命周期。

局部广播和全局广播的区别分别用什么实现的。

## **通信方式**

activity和service的通信方式

## **注解**

运行时注解和编译时注解区别（没注意过，回头看看）

## **Dex**

dex 3

dex了解吗？我答只知道65535，了解类的编译过程吗，不了解；知道源文件编译成什么吗？class文件；为什

么要有dex？在dex做了优化；哪些优化？不了解

为什么是DEX文件？

## **杂**

dalvik和hotspot虚拟机了解吗

怎么学安卓

学习Android多长时间了，平时是怎么学的，**你认为比起其他人，你有哪些优点**。看过哪些Android方面的书，讲一讲，未来的职业规划

## **框架**

有没有用过什么框架

谈谈读过哪些开源的**安卓库源码**

看过哪些Android源码

熟悉使用什么框架？（回答AFN，SDWebImage和[百度](https:///jump/super-jump/word?word=百度)地图SDK，让我选择一种技术解释，本来选择的是AFN，不过在一面的时候说过，让我重新换一个，选择了SDW，解释了大概原理）；

**retrofit**

**retrofit**源码

**retrofit**如何跨线程

**rxjava**

RxJava的通信机制

## **Glide相关**

说下Glide的使用

除了Glide还用过哪些图片加载框架，毕加索用过吗

## **okhttp**

okHttp的缓存策略，你觉得**okHttp**有哪些特别的优势\(讲了_\*_源码\)

okhttp怎么实现的

## **Activity 生命周期** 

安卓生命周期

Activity生命周期

有其他活动加入时生命周期变化

若ActivityB变透明状态 ActivityA的周期变化

activity生命周期，启动模式

activity之间的切换/返回

Activity生命周期有哪些？你是如何获取当前的生命状态？哪些情况下会执行onStop（）方法？

Activity生命周期简单介绍？出题：从Activity a返回到Activity b经历了哪些阶段？（我的回答是a先onPause-&gt;onStop-&gt;onDestroy，然后b再onStart-&gt;onResume，面试官纠正其实先让b可见并且可操作再让a onStop-&gt;onDestroy，还解释了为什么要这么做）

Activity的创建流程与原理（OnStart、OnCreate、OnResume等）

然后开始问安卓有关的问题 讲一下Activity的生命周期 两个Activity A与B，A切到B，然后按返回键，B再切回A，请问两个Activity都经历了生命周期的哪几步

Activity的创建原理，谈及**ActivityManagerService**偏Framework层的理解

activity生命周期，**息屏或者按Home键的流程**

## 启动模式

Activity的四种**启动模式**，区别

回答中提到了Activity的启动模式，接着问了Activity的启动模式是哪些？

项目中询问一个 A Activity 跳到一个 B Activity中，生命周期的走动，点击Back返回呢。如果一个 A Activity是透明的呢？如果 B Activity是一个Dialog呢？面试官追问横竖屏切换生命周期走动，以及是否了解onConfigurationChanged。

## Android静态库和动态库的区别

## **Fragment**

fragment生命周期

fragment生命周期

使用addView达到弹出框的效果，但是耗时长。后来了解Fragment，使用Fragment代替addView。面试官追问你能分析为什么这么慢吗，我就说了Android的Activity-&gt;PhoneWindow-&gt;DecorView-&gt;ContentView-&gt;WindowManager-&gt;RootViewImpl的绘制流程。面试官继续追问ANR出现的类型，原因以及排查的方式。面试官继续追问Fragment和Activity的区别以及Fragment的优点。

## **Service**

服务的启动方式，生命周期

如何保证service不被杀死

谈谈WindowManagerService的工作机制和原理

## **四大组件**

Andriod四大组件？每一个是干什么的（除了Activity之外其实都不是很了解，，我就重点说了Activity）

安卓都学过啥？四大组件是什么？

常用控件

Android中你常用哪些控件

## **IDE 调试 工具**

过渡绘制的查看工具有哪些

一般我们调试的时候，会用到断点，**断点在底层是怎么实现的**，为什么还可以看到一些变量的值。

IDE如何判断代码哪一行报错\(瞎编，不会，就说了说函数栈之类的糊弄过去了\)

## **大小端**

这问题应该不属于安卓吧

{% embed url="https://zhuanlan.zhihu.com/p/144718837" %}

## **布局**

四大布局\(主要帧布局\)

线性布局组件能否覆盖

用过约束布局吗，它的特点和原理，比起相对布局的优势

**约束layout**和线性layout有什么区别和优势

自定义布局 怎么把一个布局定义为圆形 比如qq头像

**recyclerview  listview**

// 这俩要问肯定一起问的

Recyclerview缓存机制

recyclerview缓存

itemdecoration

recyclerview怎么实现动画（不会，只会用属性动画）

**recyclerView**的复用机制

listview的item复用和recyclerview的区别

**Listview的复用机制**，Listview和Recyclerview的区别。

**抖音无限上滑**怎么实现 // 肯定是在这个下面引申问出来的

我简历里有个安卓，他首先问了下中间肯定用到了ListView，问一下这个怎么用。（Adapter）

为什么要用Adapter （我先回答buffer，然后他问还有么，我想了想说感觉用Adapter更**oop**一些，问他是不是想听到这个答案，他说是...）

OOP Object Oriented Programming 面向对象编程

## **动画**

// 不知道

补间动画，属性动画（没看源码说的一点）

## **架构问题**

讲解一下MVP架构。MVP和MVC的控制层有什么区别

Mvc，mvp，mvvm的区别（不会，答了下mvc的modle，view，controller，说了下关系，其他不知道，追问modle和view交互过程中，controller起什么作用，我说起中间件的作用，防止两个直接交互）

设计模式有了解吗？MVC？MVVM？详细讲一下MVC？MVC数据流通的关系？为什么实际上可以做到V直接到M但一般实际情况中却不去使用呢？

## **APK**

APK文件里面都有些什么。

## **Java**

Android程序运行时使用的是普通的JVM吗

## **Flutter**

Flutter dart语言是在什么上运行的。

## **图片 Bitmap**

如果多图片进行压缩：bitmap

如何正常显示图片

了解bitmap的解析吗

内存溢出和内存泄漏，提到了bitmap

然后问下载一个图片的时候直接下载了一个5g的图片，不压缩一定会产生**OOM**问题，那么怎么去获取这个图片的长宽呢，或者说这个图片的大小在你没下载之前如何得到。不会。

加载图片需要注意什么，怎么缩放图片，**三级缓存**啥的

想要在一个图片右上角**实现一个圆角**怎么实现

## **contentprovider**

// 这个不知道 看一下概念

介绍项目用到了**contentprovider**,然后问ContentProvider的生命周期，**application,activity，service,contentprovider他们的context有什么区别。**

## **数据存储**

android中多种数据存储类型的应用场景

如果做登录界面，如何保证账号密码的安全性

ShareReference的用法和**原理**

## **事件分发**

事件分发机制，滑动冲突处理

事件分发

**事件分发机制**。（ 讲完后问 如果注册了onTouchListener会发生什么）

## **屏幕适配**

\(**dp、px怎么转换，屏幕真实DPI**...\)

手机端应该和电脑端应用的注意事项和区别。（机型适配）

## **开发者选项 实践**

连接手机的时候**开发者选项里面那些开关都有什么，用过哪些**

## **序列化 Serializable Parcelable**

**Parcelable和Serializable**是什么，做什么用，**谁更高效**

parcelable serializable

## **新特性**

安卓10有什么新的特性。

也问了一些**安卓的新特性**。

## **场景题目**

实现登录功能的实现流程；

一个按钮，手抖了连续点了两次，会跳转两次页面，怎么让这种情况不发生。

一个商品页一个商详页，点击商详页的一个关注按钮，希望回到商品页也能够显示关注的状态，怎么做

音乐播放场景

我做的是音乐播放器，所以面试官问音乐播放在哪里实现，activity还是service，用thread可以吗？为什么？

