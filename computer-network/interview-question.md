---
description: 以下是从面经里扒拉出来的面试题
---

# 常见问题

## OSI 和 TCP/IP 网络模型

\_\_[_计算机网络体系结构_](basic/cn-summary.md#ji-suan-ji-wang-luo-ti-xi-jie-gou)\_\_

![](https://img-blog.csdnimg.cn/20190802001835308.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1lhbnNreTU4Njg1,size_16,color_FFFFFF,t_70)

## 路由器和交换机位于哪一层

[_网络层 - 路由器_](basic/cn-network-layer.md#lu-you-qi-de-jie-gou)\_\_

\_\_[_链路层 - 交换机_](basic/cn-link-layer.md#jiao-huan-ji)\_\_

* 路由器：网络层
  * 网络层负责为分组交换网上的不同主机提供通信服务。在发送数据时，网络层把运输层产生的报文段或用户数据报封装成分组或包\(packet\)进行传送。
  * 因特网主要的网络层协议是无连接的网际协议IP \(InternetProtocol\)和许多种路由选择协议，因此因特网的网络层也叫做网际层或IP层。在本书中，网络层、网际层和IP层都是同义语。
  * 综上，路由选择协议是在路由器中使用的，所以路由器应该是位于网络层的。
* 交换机：链路层
  * 1990年问世的交换式集线器\(switching hub\)，可明显地提高以太网的性能。交换式集线器常称为以太网交换机\(switch\)或**第二层**交换机，表明这种交换机工作在数据链路层。“交换机”并无准确的定义和明确的概念，而现在的很多交换机已混杂了网桥和路由器的功能。

## **计算机网络每层对应的协议**

这个要看不同的体系结构，已知是有三个网络体系结构：

* OSI的七层协议体系结构。理论也较完整，但它既复杂又不实用。
* TCP/IP四层体系结构。它现在已经得到了非常广泛的应用。TCP/IP是一个四层的体系结构。不过从实质上讲，TCP/IP只有最上面的三层，因为最下面的网络接口层基本上和一般的通信链路在功能上没有多大差别，对于计算机网络来说，这一层并没有什么特别新的具体内容。
* 五层协议体系结构。在学习计算机网络的原理时往往采取**折中**的办法，即综合OSI和TCP/IP的优点，采用一种只有五层协议的体系结构，这样既简洁又能将概念阐述清楚。

对应的协议如下图：

![](https://img-blog.csdnimg.cn/20190802001835308.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1lhbnNreTU4Njg1,size_16,color_FFFFFF,t_70)

## TCP连接的三次握手，四次挥手

\_\_[_TCP 的三次握手_](basic/cn-transport-layer.md#tcp-de-san-ci-wo-shou)\_\_

> 类似问题：
>
> * 3次握手、4次挥手、为什么不4次、5次
> * 三次握手，没有第三次会有什么影响
> * TCP三次握手原理及细节，谈及为什么不能两次握手的原因
> * TCP挥手 第三次不挥手会怎么样

## TCP 属于哪一层

传输层。

## TCP 与 UDP 协议的区别

\_\_[_TCP 与 UDP 的区别_](basic/cn-transport-layer.md#udp-he-tcp-de-te-dian)\_\_

## 浏览器渲染页面完成后会保持 TCP 连接吗

根据请求头中的 Connection 判断，若为`keep-alive`则保持连接。

## TCP 连接和释放中的状态有哪些，以及如果日志中出现某些状态码过多如何处理

## TCP 的拥塞控制、慢开始

## TCP为什么是可靠的。注意拥塞机制涉及的算法（慢开始，拥塞避难，快重传，快恢复）

## 为什么需要快重传和快恢复，什么场景下使用

## TCP服务端能否无限等待

## TCP四次挥手过程

## 滑动窗口的实现机制以及如何作用流量控制

## UDP 主要有哪些应用

## UDP如何实现可靠传输

## 即时视频用什么协议

## 网络较差用什么协议

## IP TCP 传输的都是什么数据

## DNS

## 客户端发送完最后一个 ACK 后会进入什么状态

## HTTP 的**八种方法**，有没有用过

## HTTP 如何实现断点续传的

## HTTPS SSL 加密等

## SSL 的运行原理，如何确保安全传输

## 对称加密和非对称加密

## 知道哪些加密算法

## 私钥的发送方式

## CA证书怎么生成，怎么保证安全，加密过程，对称加密怎么保证安全

## HTTP 和 HTTPS 区别

> 类似问题：
>
> * HTTP和HTTPS原理，区别，各自的优势
> * HTTP2和HTTPS关系

## HTTP1.0和HTTP2.0的区别

## HTTP 报文发送的全过程，

## HTTP 3xx系列的状态码

## HTTPS是如何加密的，详细说下加密算法

## HTTPS 的加解密过程

> 类似问题：
>
> * HTTPS 的加密过程，为什么要这么做？
> * HTTPS 加密的解释

## 对称/非对称加密

## HTTP 常用状态码

## 状态码 200、404、500

## HTTP 头

## IP 头都有啥内容

## HTTP 报文首部的User-Agent字段

## HTTP的**报文格式**

## HTTP 缓存

## 抓包工具用过吗，为什么抓包可以抓取HTTPS的所有数据

## 抓包的原理

## 在浏览器中输入网址回车后发生了什么

> 类似问题：
>
> * 访问一个页面发生了什么
> * 网页中输入一个网址会发生啥
> * 浏览器输入网址之后的具体操作
> * 在浏览器中输入一个网站点击回车会发生什么
> * 你在访问一个网站的时候，发生了什么，涉及到什么协议，讲传输层里的。

## 分析一个 URL 各字段的含义

## DNS 域名解析的过程

> 类似问题：
>
> * DNS解析过程，如果服务器ip地址改变了，客户端怎么知道呢
> * DNS域名解析过程，接收到DNS查询结果之后还做了什么？

## DNS缓存存在哪？有效期多少？可以设置吗？

## HTTP 是用什么实现的？

HTTP协议定义了浏览器（即万维网客户进程）怎样向万维网服务器请求万维网文档，以及服务器怎样把文档传送给浏览器。从层次的角度看，HTTP是面向事务的\(transaction-oriented\)\[插图\]应用层协议，它是万维网上能够可靠地交换文件（包括文本、声音、图像等各种多媒体文件）的重要基础。

## GET 请求和 POST 请求的区别

\_\_[_GET 和 POST_](basic/cn-application-layer/http.md#jiu-get-he-post-bi-jiao)\_\_

## GET POST请求，除了这两个还有啥

> 类似问题：
>
> * 知道其他请求方式吗，比如Put，Delete，Head。

\_\_[_HTTP方法_](basic/cn-application-layer/http.md#er-http-fang-fa)\_\_

## Socket 创建流程

## 谈谈对 T**oken** 的理解

## cookie 和 session 有了解吗

## 网络协议有了解吗

## 跨域问题如何解决

[什么是跨域？](https://juejin.cn/post/6844904100035821575#heading-67)

## 什么是子网掩码，它的作用是什么

