# 常见问题

## 参考

* [Android 面试题集](https://www.yuque.com/docs/share/73271436-56d3-4c63-9311-ae499378198a)
* [LRH1993/android\_interview](https://github.com/LRH1993/android_interview#android) ⭐️

## APP/APK

[https://www.jianshu.com/p/c8ccf7ffa79e](https://www.jianshu.com/p/c8ccf7ffa79e)

一个APP完整的打包流程

讲讲APP的启动流程

讲讲APP的安装流程

apk里面有几部分

android编译流程，资源什么时候开始编译的

apk编译，apk安装过程

androidManifest文件的作用，proguard什么用途

Android 编译过程介绍一下，反编译呢

知道apk怎么缩减体积吗

答：应该用插件化去处理 但自己没有实践过。真正用到的可能是将图片压缩、用svg图代替png、启动代码混淆等。

## **Handler**

\*\*\*\*[**https://github.com/LRH1993/android\_interview/blob/master/android/basis/message-mechanism.md**](https://github.com/LRH1993/android_interview/blob/master/android/basis/message-mechanism.md)\*\*\*\*

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

//

handler原理；能否让message被push到非主线程的线程里？（提示looper\)

谈谈对Handler、Looper的理解，他们俩的数量关系

还有就是Handler实现，这个比较简单，但是问了个MessageQueue的具体实现，有点忘了，以前看过源码，不过后面温习了下，还包括postDelay实现。

这个就是安卓面试必问的问题，基本上把源码看下都能说出来，然后是个生产者消费者模型



如下代码的打印顺序，为什么要这样打印？

```java
public void onCreate(Bundle savedInstance){
Log.i(TAG,"a");
handler.post(()->{
   Log.i(TAG,"b"); 
})
Log.i(TAG,"c"); 
}
```



多个handler绑定了一个looper,如何区分哪个handler对应哪个message呢?





## **内存泄漏**

\*\*\*\*[**https://github.com/LRH1993/android\_interview/blob/master/android/advance/memory-leak.md**](https://github.com/LRH1993/android_interview/blob/master/android/advance/memory-leak.md)\*\*\*\*

怎么解决内存泄漏（声明static，弱引用包裹） // 避免干嘛干嘛

有没有接触过安卓，怎么看内存占用情况

内存溢出和内存泄漏，提到了bitmap

什么时候会发生**内存泄漏**

内存泄漏的可能原因

内存泄漏，以及使用过哪些工具

AS里面有哪些**常用的工具**，第三方的也行。我竟然不知道，。。

什么情况会导致**内存抖动**，举个例子

如果让你写APP你会在哪里去检测内存泄漏的问题

// 

asynctask内存泄漏

内存泄漏，什么时候会无法正确回收？举例

有关注内存泄漏问题吗

答：内存泄漏有关注，比如使用ContentResolver查询数据后，光标对象Cursor要进行close\(\)回收；Bitmap在加载完成后要记得回收等。（顺带提到了Bitmap容易造成的OOM问题，并提出解决方案。）

## **View**

\*\*\*\*[**https://github.com/LRH1993/android\_interview/blob/master/android/basis/custom\_view.md**](https://github.com/LRH1993/android_interview/blob/master/android/basis/custom_view.md)\*\*\*\*

View的绘制过程（OnMeasure、OnLayout、OnDraw）

view绘制流程

如何去绘制一个view

子View如何让父view不拦截触摸事件，requestDisAllowIntercept啥的。

Android里布局用过哪些？怎么自定义View? View的绘制大概是个怎么样的流程？

讲讲ViewRootImpl，Dialog有ViewRootImpl，还有什么UI视图也有ViewRootImpl，讲讲View完整的绘制流程

//

View显示过程？

Android的Button是View吗



## 自定义View

自定义view怎么画圆。

设计一个自定义View,View中包含图片和文字，并且只能继承View

## WebView

谈谈webview的原理和通信机制

**WebView**机制

## SurfaceView

用过SurfaceView吗？（脑抽了忘了视频播放用的这个 // us

SurfaceView与View区别？SurfaceView原理？

## **Binder 进程间通信**

binder 机制：

[https://github.com/LRH1993/android\_interview/blob/master/android/advance/binder.md](https://github.com/LRH1993/android_interview/blob/master/android/advance/binder.md)

[https://www.yuque.com/docs/share/73271436-56d3-4c63-9311-ae499378198a\#ccf2414e](https://www.yuque.com/docs/share/73271436-56d3-4c63-9311-ae499378198a#ccf2414e) （为什么用Binder）

进程间通信：

[https://github.com/LRH1993/android\_interview/blob/master/android/basis/ipc.md](https://github.com/LRH1993/android_interview/blob/master/android/basis/ipc.md)

Binder机制以及原理（binder驱动、共享内存等）

进程间通信的方式，安卓中有哪些方式，**为什么是基于Binder的，不用传统的操作系统进程间通信方式呢 // 还有AIDL**

binder机制 2

讲讲几种IPC方式的优劣，以及Binder的原理

Binder机制以及原理（binder驱动、共享内存等）

//

对Android进程间通信有了解吗，有哪些方式（AIDL那些）

AIDL了解么？

IPC方式？谁最快？

// 内存拷贝：[https://juejin.cn/post/6844904113046568973](https://juejin.cn/post/6844904113046568973)

## **多线程**

> 问到多线程直接答 Java 的就行吧，细问再说。

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

\*\*\*\*[**https://github.com/LRH1993/android\_interview/blob/master/android/basis/process-priority.md**](https://github.com/LRH1993/android_interview/blob/master/android/basis/process-priority.md)\*\*\*\*

讲讲Android进程。前台进程、后台进程……这块不大会

一个app可以开启多个进程嘛，怎么做呢，每个进程都是在独立的虚拟机上嘛

项目中定时为什么用AlarmManager，不用postDelayed

项目中后台网络请求为什么用service不用线程

多进程：[https://github.com/BlackZhangJX/Android-Notes/blob/master/Docs/Android%E7%9F%A5%E8%AF%86%E7%82%B9%E6%B1%87%E6%80%BB.md\#%E5%A4%9A%E8%BF%9B%E7%A8%8B](https://github.com/BlackZhangJX/Android-Notes/blob/master/Docs/Android%E7%9F%A5%E8%AF%86%E7%82%B9%E6%B1%87%E6%80%BB.md#%E5%A4%9A%E8%BF%9B%E7%A8%8B)

//

Android多进程（不知道他具体想问什么，回答了IPC他冷笑），

怎么理解多进程

APP中多进程有什么用？

Activity进程的优先级。

## Application

application和activity的onCreat哪个先调用

## **Eventbus**

// 问我干脆说我没用过哈哈哈哈我确实没用过OTZ

\*\*\*\*[**https://github.com/LRH1993/android\_interview/blob/master/android/open-source-framework/EventBus.md**](https://github.com/LRH1993/android_interview/blob/master/android/open-source-framework/EventBus.md)\*\*\*\*

eventbus 2

eventbus实现

框架源码（没看过，不会），

eventbus有哪些缺点，什么类可以作为event，为什么不用广播

## **广播**

\*\*\*\*[**https://github.com/LRH1993/android\_interview/blob/master/android/basis/broadcastreceiver.md**](https://github.com/LRH1993/android_interview/blob/master/android/basis/broadcastreceiver.md)\*\*\*\*

广播的种类，注册的方式，以及不同注册方式的生命周期。

局部（本地）广播和全局广播的区别分别用什么实现的。

//

广播的收发过程，如何做一个有序广播

Broadcast有几种注册方式

## **通信方式**

\*\*\*\*[**https://www.jianshu.com/p/6040dfa83594**](https://www.jianshu.com/p/6040dfa83594)\*\*\*\*

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

SurfaceFlinger SurfaceFlinger了解吗

有没有解决过性能优化相关的问题

Protocol Buffer了解么

热更新原理（当时没复习好 这个答得不好）

安卓和js的交互方式，那种更好，安全性比较

主要是百度那边手百安卓和js交互比较多，所以就讲了下安卓和js的交互方式，比较了下几种方法

app 如何判断在后台？

说一下什么是热修复和热修复的原理 // 热更新、热修复、热启动都看看

## **框架源码**

有没有用过什么框架

谈谈读过哪些开源的**安卓库源码**

看过哪些Android源码

熟悉使用什么框架？（回答AFN，SDWebImage和[百度](https:///jump/super-jump/word?word=百度)地图SDK，让我选择一种技术解释，本来选择的是AFN，不过在一面的时候说过，让我重新换一个，选择了SDW，解释了大概原理）；

**retrofit**

**retrofit**源码

**retrofit**如何跨线程

**rxjava**

RxJava的通信机制

// 

你看过android源码吗，说一下你最近看过的源码吧

 项目里好像用到了视频开发 是VideoView吗

答：一开始用的VideoView，后来觉得其无论是播放的响应还是读取的速度都不太理想，改用了七牛的框架（然后简单介绍了一下这个框架）。

平时怎么学习的 有阅读源码的经验吗

答：看书看博客。有。（大致分析了一下Handler的源码和属性动画的启动源码）

那你还有看过一些网络框架吗

答：项目里用到的是Retrofit+Rxjava+MVP的经典架构模式，所以有看过Retrofit的创建源码。（又从源码层面讲了一下流程。）



## **Glide相关**

{% embed url="https://blog.csdn.net/so1993/article/details/106489951" %}

{% embed url="https://blog.csdn.net/xwh\_1230/article/details/100006311" %}

{% embed url="https://juejin.cn/post/6844904002551808013" %}

{% embed url="https://juejin.cn/post/6844903986412126216" caption="⭐️" %}

说下Glide的使用

除了Glide还用过哪些图片加载框架，毕加索用过吗

// 生命周期感知

Glide框架的分析

因为这块我看过源码，然后讲下了这个框架的俩个亮点 1虚拟碎片监视生命周期 2 缓存机制，然后就讲到lru算法,然后就扯到操作系统这块内存算法。

用到了图片加载框架G，有没有了解过\*\*\*的F图片加载框架?

## **okhttp**

{% embed url="https://github.com/LRH1993/android\_interview/blob/master/android/open-source-framework/okhttp.md" %}

{% embed url="https://juejin.cn/post/6844904087788453896" %}

{% embed url="https://cloud.tencent.com/developer/article/1601358" caption="这个最后提到了设计模式" %}

{% embed url="https://juejin.cn/post/6844904077726334984" caption="这一系列不错，还有其他的源码比如Glide" %}

okHttp的缓存策略，你觉得**okHttp**有哪些特别的优势\(讲了_\*_源码\)

okhttp怎么实现的

//

OkHttp了解不？

OkHttp使用需要注意什么？

OKHTTP 对HTTP与HTTPs之间的区别

让我说一个常见框架原理，我说了OKHttp实现原理，我只说了具体是如何实现同步和异步发送，线程池相关的设计，又问我底层如何发包的，这个没看哈哈。当时应该跟他说AsynTask实现原理才对。

okHttp源码解析

因为我项目网络框架就用过okHttp,然后大三上学期看过这块源码分析，就给面试官讲了下主体流程，然后说了下框架的最重要的拦截器的作用是，讲了下责任链模式。

其实okhttp那些都是应用层，特别简单等等，了解过别的http 请求框架吗?

## WindowManagerService

windowManagerService了解吗

谈谈WindowManagerService的工作机制和原理

讲一讲Activity、View、Window

## Activity

在哪注册Activity

Activity的创建原理，谈及ActivityManagerService偏Framework层的理解

谈谈Activity的原理，生命周期（面试官希望我答出Native层的原理，虽然我读过安卓源码的书籍，但当时一紧张就答得不太全面

Android Framework层有了解吗，比方说Activity的 onCreated方法执行前，都做了哪些工作

一个APP 怎么退出所有Activity？

接上问如果有第三方SDK，怎么退出？

Activity在AndroidManifest.xml文件中有哪些标志位？

按关机键息屏，属于哪个情况

Activity从打开状态到到运行状态经历了哪几个方法

activity 被挡住了之后，要经过哪些生命周期?为什么经过onStart方法呢？

activtiy 如何被实例化的

activity是通过反射被初始化的吗？初始化的类加载器是哪个呢？

## **Activity 生命周期** 

\*\*\*\*[**https://github.com/LRH1993/android\_interview/blob/master/android/basis/activity.md**](https://github.com/LRH1993/android_interview/blob/master/android/basis/activity.md)\*\*\*\*

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

**//**

\*\*\*\*

## 启动模式

[https://github.com/LRH1993/android\_interview/blob/master/android/basis/activity.md](https://github.com/LRH1993/android_interview/blob/master/android/basis/activity.md)

Activity的四种**启动模式**，区别

回答中提到了Activity的启动模式，接着问了Activity的启动模式是哪些？

项目中询问一个 A Activity 跳到一个 B Activity中，生命周期的走动，点击Back返回呢。如果一个 A Activity是透明的呢？如果 B Activity是一个Dialog呢？面试官追问横竖屏切换生命周期走动，以及是否了解onConfigurationChanged。

//

singleTop和singleTask分别的使用场景

Activity的启动模式，应用场景，然后举了很多微信的场景，让我去选择用那种启动模式，说下理由。

## Android静态库和动态库的区别

{% embed url="https://juejin.cn/post/6844903814118670344" %}

**静态库**：在编译的时候加载生成目标文件，在运行时不用加载**库**，在运行时对**库**没有依赖性。 

**动态库**：在目标文件运行时加载，手动加载，且对**库**有依赖性。

## **Fragment**

\*\*\*\*[**https://github.com/LRH1993/android\_interview/blob/master/android/basis/Fragment.md**](https://github.com/LRH1993/android_interview/blob/master/android/basis/Fragment.md)\*\*\*\*

fragment生命周期

fragment生命周期

使用addView达到弹出框的效果，但是耗时长。后来了解Fragment，使用Fragment代替addView。面试官追问你能分析为什么这么慢吗，我就说了Android的Activity-&gt;PhoneWindow-&gt;DecorView-&gt;ContentView-&gt;WindowManager-&gt;RootViewImpl的绘制流程。面试官继续追问ANR出现的类型，原因以及排查的方式。面试官继续追问Fragment和Activity的区别以及Fragment的优点。

**//** 

主界面UI的fragment设计的优势，安卓系统对于多个fragment的管理了解吗



## **Service**

\*\*\*\*[**https://github.com/LRH1993/android\_interview/blob/master/android/basis/service.md**](https://github.com/LRH1993/android_interview/blob/master/android/basis/service.md)\*\*\*\*

服务的启动方式，生命周期

如何保证service不被杀死

谈谈WindowManagerService的工作机制和原理

//

前台服务与后台服务区别？

service两种启动模式，区别**；两种启动模式，如果我在退出Activity的时候没有退出service会怎么样**

## 组件之间的关系

Activity与Fragment的关系，如何创建一个Fragment

Activity和Service的关系

Activity、View、Surface、SurfaceView之间的联系？

View和Activity之间的关系

## **四大组件**

> Activity, Service, Broadcast, ContentProvider

[这个目录的前四个](https://github.com/LRH1993/android_interview/blob/master/android/basis.md#%E4%BA%8C%E7%9B%AE%E5%BD%95)

Andriod四大组件？每一个是干什么的（除了Activity之外其实都不是很了解，，我就重点说了Activity）

安卓都学过啥？四大组件是什么？

常用控件

Android中你常用哪些控件

## **IDE 调试 工具**

过渡绘制的查看工具有哪些

一般我们调试的时候，会用到断点，**断点在底层是怎么实现的**，为什么还可以看到一些变量的值。

IDE如何判断代码哪一行报错\(瞎编，不会，就说了说函数栈之类的糊弄过去了\)

## **大小端**

这问题应该不属于安卓范畴内吧，放在这懒得挪啦。

{% embed url="https://zhuanlan.zhihu.com/p/144718837" %}

字节序

C的字节对齐，大小端对齐

## **布局**

\*\*\*\*[**https://github.com/Omooo/Android-Notes/blob/master/blogs/Android/RecyclerView.md**](https://github.com/Omooo/Android-Notes/blob/master/blogs/Android/RecyclerView.md)\*\*\*\*

四大布局\(主要帧布局\)

// 六大布局 ：LineartLayout 、FrameLayout 、TableLayout 、 RelativeLayout 、 AbsoluteLayout 、 GridLayout ；

线性布局组件能否覆盖

用过约束布局吗，它的特点和原理，比起相对布局的优势

{% embed url="https://hishark777.com/post/constraint-layout/" %}

{% embed url="https://developer.android.com/training/constraint-layout?hl=zh-cn" %}

**约束layout**和线性layout有什么区别和优势

自定义布局 怎么把一个布局定义为圆形 比如qq头像

//

Android布局优化，为什么多层嵌套下，相对布局不如线性布局，原理是什么，可以结合view绘制说说吗

介绍一下六大布局，线性布局和相对布局哪个效率更高

## ListView RecyclerView

**recyclerview  listview** // 这俩要问肯定一起问的

{% embed url="https://www.jianshu.com/p/4f9591291365" %}

Recyclerview缓存机制

recyclerview缓存

Recyclerview itemdecoration

recyclerview怎么实现动画（不会，只会用属性动画）

**recyclerView**的复用机制

{% embed url="https://www.jianshu.com/p/0a72276c537f" %}

listview的item复用和recyclerview的区别

**Listview的复用机制**，Listview和Recyclerview的区别。

**抖音无限上滑**怎么实现 // 肯定是在这个下面引申问出来的

我简历里有个安卓，他首先问了下中间肯定用到了ListView，问一下这个怎么用。（Adapter）

为什么要用Adapter （我先回答buffer，然后他问还有么，我想了想说感觉用Adapter更**oop**一些，问他是不是想听到这个答案，他说是...）

OOP Object Oriented Programming 面向对象编程

// 

recyclerview item太多会内存泄漏吗

ListView和RecyclerView的区别，如何用ListView实现RecyclerView等同的效果



RecyvleView的源码

我一开始没听清楚面试官的问题，我给人家讲下下ListView和RecyvleView的区别，然后面试官让我讲了下RecyvleView的源码，然后这块我真没看这块源码，自己就讲了下在recyclerview中持有一个adapter的观察者，然后在setAdapter之后会注册这个被观察者，然后会去requestLayout,去请求重绘布局。

## ListView

ListView源代码有看过吗？没看过。

想一下ListView应该是怎么实现的？链表？

ListView滑动页面如何实现页面的复用？队列？后来经过面试官的引导，有了思路。一开始往下滑，为了不影响用户体验，下面的数据，需要先预加载，这样往下滑的时候，就可以快速地显示内容。如果往下滑了之后，又想要往上滑，采用移出页面的内容，就把相应的数据销毁掉，等需要再显示的时候重新加载，比较费时；可以在一开始往下滑的时候，移出页面的内容，将相应的UI数据（不是实际的内容数据，这个一直在存储空间中）压到一个栈里面，等要往回滑的时候，再出栈，恢复数据，这样就比较快。因此在做滑动页面的操作的时候，需要上下预留出一定量的项的数据，超过这个量，再把这些数据释放掉，具体需要留多少，一个是跟页面能显示多少有关，可以通过大量测试，看看多少比较合适。还跟用户的使用习惯有关，动态调节，可以引入机器学习的方法。

listView怎么去优化，（假如数据量很多怎么让它显示得更流畅，假如每条数据里面还包含图片，怎么加载更流畅）

ListView的优化

这个我就讲了下ViewHolder缓存机制，然后顺便讲了下listView的源码，和重复利用机制

## **动画**

\*\*\*\*[**https://github.com/LRH1993/android\_interview/blob/master/android/basis/animator.md**](https://github.com/LRH1993/android_interview/blob/master/android/basis/animator.md)\*\*\*\*

// 不知道

补间动画，属性动画（没看源码说的一点）

## **架构问题**

讲解一下MVP架构。MVP和MVC的控制层有什么区别

Mvc，mvp，mvvm的区别（不会，答了下mvc的modle，view，controller，说了下关系，其他不知道，追问modle和view交互过程中，controller起什么作用，我说起中间件的作用，防止两个直接交互）

设计模式有了解吗？MVC？MVVM？详细讲一下MVC？MVC数据流通的关系？为什么实际上可以做到V直接到M但一般实际情况中却不去使用呢？

// MVP设计模式？对比来看MVC有什么坏处？

## **APK**

APK文件里面都有些什么。

## **Java**

Android程序运行时使用的是普通的JVM吗

## **Flutter**

**// 没用过886**

Flutter dart语言是在什么上运行的。

//

让你设计一个跨平台的框架，你怎么设计（这里我谈了flutter的架构）。

## **图片 Bitmap**

\*\*\*\*[**https://github.com/LRH1993/android\_interview/blob/master/android/basis/bitmap.md**](https://github.com/LRH1993/android_interview/blob/master/android/basis/bitmap.md)\*\*\*\*

如果多图片进行压缩：bitmap

如何正常显示图片

了解bitmap的解析吗

内存溢出和内存泄漏，提到了bitmap

然后问下载一个图片的时候直接下载了一个5g的图片，不压缩一定会产生**OOM**问题，那么怎么去获取这个图片的长宽呢，或者说这个图片的大小在你没下载之前如何得到。不会。

加载图片需要注意什么，怎么缩放图片，**三级缓存**啥的

想要在一个图片右上角**实现一个圆角**怎么实现

//

项目里有图片资源吧，怎么引入图库的资源

如何计算bitmap的大小，行，我再问问压缩算法（因为他是搞音视频开发的）

有一个很大很大的图片加载到内存上，不能降低清晰度和压缩图片你怎么解决？（提示我局部显示？我没懂）//压缩把？

## **contentprovider**

[https://github.com/LRH1993/android\_interview/blob/master/android/basis/ContentProvider.md](https://github.com/LRH1993/android_interview/blob/master/android/basis/ContentProvider.md)

介绍项目用到了**contentprovider**,然后问ContentProvider的生命周期，**application,activity，service,contentprovider他们的context有什么区别。**

## **数据存储**

![](../.gitbook/assets/image%20%2864%29.png)

android中多种数据存储类型的应用场景

如果做登录界面，如何保证账号密码的安全性

ShareReference的用法和**原理**

**//**

数据存储有学过吗？数据库和文件保存有什么区别？

讲讲本地持久化储存的方法

除了数据库，有没有了解其他存储数据的方式

ShareReference的用法和原理

## **事件分发**

\*\*\*\*[**https://github.com/LRH1993/android\_interview/blob/master/android/basis/Event-Dispatch.md**](https://github.com/LRH1993/android_interview/blob/master/android/basis/Event-Dispatch.md)\*\*\*\*

事件分发机制，滑动冲突处理

事件分发

**事件分发机制**。（ 讲完后问 如果注册了onTouchListener会发生什么）

讲讲事件分发机制和多点触控

//

触摸event的具体过程

## **屏幕适配**

\*\*\*\*[**https://mp.weixin.qq.com/s/d9QCoBP6kV9VSWvVldVVwA**](https://mp.weixin.qq.com/s/d9QCoBP6kV9VSWvVldVVwA)\*\*\*\*

\(**dp、px怎么转换，屏幕真实DPI**...\)

手机端应该和电脑端应用的注意事项和区别。（机型适配）

//

在平板电脑上和手机上设计app有什么不同

看到你简历写了分辨率适配，分辨率适配有哪些方案？（我答了头条那套）// 就是上面这个链接

Android中dp、px、sp有什么区别，用在哪

如何适配不同厂商的手机，然后设计模式，brara又说了一大堆，最后还说到jenkins自动部署上面去了 // jenkins可以搞一下

## **开发者选项 实践**

**// 看一下pixel 2xl**

连接手机的时候**开发者选项里面那些开关都有什么，用过哪些**

## **序列化 Serializable Parcelable**

**Parcelable和Serializable**是什么，做什么用，**谁更高效**

parcelable serializable

{% embed url="https://lrh1993.gitbooks.io/android\_interview\_guide/content/android/advance/serializable.html" %}

//

安卓的序列化内部实现原理？反射了解吗？

其它的问了个Intent.putString\(Object\) 行不行，就是不进行序列化，然后直接传递对象，嗯，就进程内可以，内存空间相同，跨进程不行。

## **新特性**

安卓10有什么新的特性。

也问了一些**安卓的新特性**。

## **项目/场景题**

实现登录功能的实现流程；

一个按钮，手抖了连续点了两次，会跳转两次页面，怎么让这种情况不发生。

一个商品页一个商详页，点击商详页的一个关注按钮，希望回到商品页也能够显示关注的状态，怎么做

音乐播放场景

我做的是音乐播放器，所以面试官问音乐播放在哪里实现，activity还是service，用thread可以吗？为什么？

// 

上线一款apk，如何瘦身（Tencent）

有接触过登录自动化吗

项目怎么做的，问了一下业务功能

抖音点赞动画怎么实现

登陆一般是如何实现 **// 项目里也有，重点梳理一下**

怎么让图片占的空间变小

图片过大怎么处理

如果做一个看图软件，应该如何设计

USB模块的数据怎么传输的？超声数据怎么转化成绘图数据？ **// 重点梳理一下**

数据按照什么协议传输的？项目中是怎么保证数据的安全性的？如果要和远端进行网络通信怎么实现数据加密？

做过的项目里的app是怎么用地图的

项目什么地方用到数据的持久化，说一下。

如何防止微信不被系统杀死？

设计一个图片浏览框架，（线程池，lru缓存，brabra的说了一堆）。

一个商场里有一个电影院，你会把厕所建设在哪里，说一下你的理由？

说一下你觉得你的项目里觉得最有印象的一个

答：我觉得是XXX项目。（然后剖析了一下里面用的框架 并且谈到了使用Glide而不用Picasso的理由 然后又从其源码层面跟面试官分析了一波。）

在百度实习的经历，然后问我手百的框架，写的需求

讲了下百度手百的框架，自己当时负责的需求，如何写的，遇到问题咋处理的

设计一个云相册：

要设计那些部分？

从用户的角度出发，怎么保证相册的安全性？

作为一个云相册，它的展示体验其实是很重要的，你觉得你应该做哪些事情保证云相册查看过程过程中，用户有比较好的体验？

整个过程就是问还有吗、能具体点吗、还有吗。我就一直在作补充。

一个1000个人的qq群里，有人发消息其他人有小概率收不到消息，用户向你反馈这个问题你怎么解决

## ANR

ANR，有遇到过ANR吗，如何规避ANR

ANR一般会在什么情况出现，分别有什么事件导致ANR

项目中遇到过什么软件崩溃或异常？

在实习和项目中遇到过ANR吗？怎么解决的（ADB扒日志）

anr是什么？如果主线程一定要执行耗时逻辑，如何保证不发生ANR

## OOM

OOM一般怎么优化，内存泄漏会导致OOM嘛，BITMAP加载导致内存泄漏一般怎么优化，假如优化后还是会出现OOM怎么防止APP崩溃

OOM需要处理吗

讲讲内存溢出，什么时候会出现内存溢出，怎么解决

## AMS

AMS你的理解是什么，AMS是在另外一个线程的嘛，AMS在APP里面起什么作用，一个APP从点击启动到VIEW绘制完成是一个怎么样的过程

## Context

context你的理解他起到一个什么样的作用，生命周期和Context有关系嘛

## 断点续传

## AsyncTask

AsyncTask



AsyncTask源码分析，每个方法在哪个线程执行的？





## Native层

Java层和native层的数据如何传递？如果Java层传递了引用给native层，在native层进行了修改后会不会影响Java层的对象？如果要做到既能修改又能不影响Java层的对象，要怎么做？（我回答深拷贝）所有的数据类型都可以深拷贝吗？

native层的多线程会不会涉及到多个线程访问？怎么避免的？Java的多线程了解吗？

## Canva

OpenGL和Canvas的优缺点？canvas底层也是c++，为啥OpenGL更快？图层叠加会涉及到过度绘制，你怎么理解？项目中用什么控制canvas刷新频率？这样做有什么不好的地方吗？

## Kotlin

有了解过安卓近两年的新东西吗？现在都不用Java用kotlin，你怎么看kotlin？

## 网络编程

会不会网络编程

{% embed url="https://www.runoob.com/w3cnote/android-tutorial-http.html" %}



**有自己写过网络编程吗 比如TCP/UDP类似这种的编程**

 答：无。然后扯到了https。（面试官：能说一下https和http的区别吗 https如何实现加密的呢）=&gt; 继续这个话题答 然后说了一下https的非对称加密以及加密过程的五次握手。

## 内存机制

android的内存机制，也可以说下windows或linux的内存机制

## 自定义控件

自定义控件有哪些步骤？

## 蓝牙

BlueboothAdapter

## 性能分析

平时有用到一些安卓的分析工具吗 比如一些性能分析之类的

答：知道Memory Monitor的内存分析工具；还有 HierarchyView这种布局分析工具。

开发中的优化，有哪些地方会存在界面卡顿，怎么解决

## 跨域问题

