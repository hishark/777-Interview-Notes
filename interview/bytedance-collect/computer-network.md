# 计算机网络

## OSI 和 TCP/IP 网络模型

[https://blog.csdn.net/kavensu/article/details/8020400](https://blog.csdn.net/kavensu/article/details/8020400)

![](https://cs-notes-1256109796.cos.ap-guangzhou.myqcloud.com/0fa6c237-a909-4e2a-a771-2c5485cd8ce0.png)

![](https://img-blog.csdnimg.cn/20190802001835308.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1lhbnNreTU4Njg1,size_16,color_FFFFFF,t_70)

## 路由器和交换机位于哪一层

* 路由器：应该是网络层
  * 网络层负责为分组交换网上的不同主机提供通信服务。在发送数据时，网络层把运输层产生的报文段或用户数据报封装成分组或包\(packet\)进行传送。
  * 因特网主要的网络层协议是无连接的网际协议IP \(InternetProtocol\)和许多种路由选择协议，因此因特网的网络层也叫做网际层或IP层。在本书中，网络层、网际层和IP层都是同义语。
  * 综上，路由选择协议是在路由器中使用的，所以路由器应该是位于网络层的。我觉得被问问题的时候也可以这样子回答。不要直接简单的回答一句「路由器位于网络层」
* 交换机：应该是数据链路层
  * 1990年问世的交换式集线器\(switching hub\)，可明显地提高以太网的性能。交换式集线器常称为以太网交换机\(switch\)或**第二层**交换机，表明这种交换机工作在数据链路层。“交换机”并无准确的定义和明确的概念，而现在的很多交换机已混杂了网桥和路由器的功能。

## **计算机网络每一层分别对应什么协议**

这个要看不同的体系结构，已知是有三个网络体系结构：

* OSI的七层协议体系结构。理论也较完整，但它既复杂又不实用。
* TCP/IP四层体系结构。它现在已经得到了非常广泛的应用。TCP/IP是一个四层的体系结构。不过从实质上讲，TCP/IP只有最上面的三层，因为最下面的网络接口层基本上和一般的通信链路在功能上没有多大差别，对于计算机网络来说，这一层并没有什么特别新的具体内容。
* 五层协议体系结构。在学习计算机网络的原理时往往采取**折中**的办法，即综合OSI和TCP/IP的优点，采用一种只有五层协议的体系结构，这样既简洁又能将概念阐述清楚。

对应的协议如下图：

![](https://img-blog.csdnimg.cn/20190802001835308.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1lhbnNreTU4Njg1,size_16,color_FFFFFF,t_70)

这里可以稍微总结一下这些协议对应的中文名称：

* HTTP
  * **H**yper**T**ext **T**ransfer **P**rotocol 超文本传输协议
* TFTP 简单文件传送协议（为什么不叫Simple File呢！）
  * TCP/IP协议族中还有一个简单文件传送协议TFTP \(Trivial File Transfer Protocol\)，它是一个很小且易于实现的文件传送协议。
* FTP 文件传送协议
  * 文件传送协议FTP \(File Transfer Protocol\) \[RFC 959\]是因特网上使用得最广泛的文件传送协议。FTP提供交互式的访问，允许客户指明文件的类型与格式（如指明是否使用ASCII码），并允许文件具有存取权限（如访问文件的用户必须经过授权，并输入有效的口令）。FTP屏蔽了各计算机系统的细节，因而适合于在异构网络中任意计算机之间传送文件。RFC959很早就成为了因特网的正式标准。
* NFS
  * 属于文件共享协议的有网络文件系统NFS\(Network File System\) \[COME06\]。网络文件系统NFS最初是在UNIX操作系统环境下实现文件和目录的共享。NFS可使本地计算机共享远程的资源，就像这些资源在本地一样。由于NFS原先是美国SUN公司在TCP/IP网络上创建的，因此目前NFS主要应用在TCP/IP网络上。然而现在NFS也可在OS/2,MS-Windows, NetWare等操作系统上运行。NFS还没有成为因特网的正式标准，现在的版本4（NFSv4）是2000年底发表的\[RFC 3010\]，目前还只是建议标准。限于篇幅，本书不讨论NFS的详细工作过程。
* WAIS
  * 教材都搜不到，不用管。
* SMTP 简单邮件传送协议
  * 1982年ARPANET的电子邮件标准问世：简单邮件传送协议SMTP \(Simple Mail Transfer Protocol\) \[RFC 821\]和因特网文本报文格式\[RFC 822\]。电子邮件很快就成为最受广大网民欢迎的因特网应用。
* Telnet 远程终端协议
  * TELNET是一个简单的远程终端协议\[RFC 854\]，它也是因特网的正式标准。用户用TELNET就可在其所在地通过TCP连接注册（即登录）到远地的另一个主机上（使用主机名或IP地址）。TELNET能将用户的击键传到远地主机，同时也能将远地主机的输出通过TCP连接返回到用户屏幕。这种服务是透明的，因为用户感觉到好像键盘和显示器是直接连在远地主机上。因此，TELNET又称为终端仿真协议。
* SNMP 简单网络管理协议
  * 简单网络管理协议SNMP \(Simple Network ManagementProtocol\)中的管理程序和代理程序按客户-服务器方式工作。管理程序运行SNMP客户程序，而代理程序运行SNMP服务器程序。
* DNS 域名系统
  * 域名系统DNS \(Domain Name System\)是因特网使用的命名系统，用来把便于人们使用的机器名字转换为IP地址。域名系统其实就是名字系统。为什么不叫“名字”而叫“域名”呢？这是因为在这种因特网的命名系统中使用了许多的“域”\(domain\)，因此就出现了“域名”这个名词。
* TCP
  * 传输控制协议TCP \(Transmission Control Protocol\)——提供面向连接的、可靠的数据传输服务，其数据传输的单位是报文段\(segment\)。
* UDP
  * 用户数据报协议 UDP \(User Datagram Protocol\)——提供无连接的、尽最大努力\(best-effort\)的数据传输服务（不保证数据传输的可靠性），其数据传输的单位是用户数据报。
* IP 网际协议IP
  * Internet Protocol 互联网协议
  * 网际协议IP是TCP/IP体系中两个最主要的协议之一，也是最重要的因特网标准协议之一。与IP协议配套使用的还有三个协议：ARP，ICMP，IGMP。本来还有一个协议叫做逆地址解析协议RARP \(ReverseAddress Resolution Protocol\)，是和ARP协议配合使用的。但现在已被淘汰不使用了。
  * IP是Internet Protocol（网际互连协议）的缩写，是[TCP/IP](https://baike.baidu.com/item/TCP%2FIP/214077)体系中的网络层协议。设计IP的目的是提高网络的可扩展性：一是解决[互联网](https://baike.baidu.com/item/%E4%BA%92%E8%81%94%E7%BD%91/199186)问题，实现大规模、[异构网络](https://baike.baidu.com/item/%E5%BC%82%E6%9E%84%E7%BD%91%E7%BB%9C/1306810)的互联互通；二是分割顶层网络应用和底层网络技术之间的耦合关系，以利于两者的独立发展。根据[端到端](https://baike.baidu.com/item/%E7%AB%AF%E5%88%B0%E7%AB%AF/8851783)的设计原则，IP只为主机提供一种无连接、不可靠的、尽力而为的数据包传输服务。
* ICMP
  * 网际控制报文协议ICMP \(Internet Control MessageProtocol\)
* IGMP
  * 网际组管理协议IGMP \(Internet Group ManagementProtocol\)
* ARP
  * 地址解析协议ARP \(Address Resolution Protocol\)
* RARP
  * 本来还有一个协议叫做逆地址解析协议RARP \(ReverseAddress Resolution Protocol\)，是和ARP协议配合使用的。但现在已被淘汰不使用了。
  * [https://www.codenong.com/p11923567/](https://www.codenong.com/p11923567/)
  * RARP已经被淘汰了，原因有两个：首先，RARP利用了数据链路层的广播服务，这也就表示**每个网络上都必须存在一台RARP服务器**。第二，RARP**只能提供计算机的IP地址**，但如今的计算机需要前面提到的所有四种信息——（每个连接到TCP/IP互联网的计算机都必须知道自己的**IP地址**、一个路由器的IP地址、一个名字服务器的IP地址以及自己的子网掩码这四种信息）
* AKP
  * 教材都搜不到，不用管。
* UUCP
  * 同上
* SLIP
  * 同上
* PPP 点对点协议PPP \(Point-to-Point Protocol\)
  * 在通信线路质量较差的年代，在数据链路层使用可靠传输协议曾经是一种好办法。因此，能实现可靠传输的高级数据链路控制HDLC \(High-level Data Link Control\)就成为当时比较流行的数据链路层协议。但现在HDLC已很少使用了。对于点对点的链路，简单得多的点对点协议PPP \(Point-to-PointProtocol\)则是目前使用得最广泛的数据链路层协议。
  * 我们知道，因特网用户通常都要连接到某个ISP才能接入到因特网。PPP协议就是用户计算机和ISP进行通信时所使用的数据链路层协议。
* IEEE
  * **电气电子工程师学会**（英语：**I**nstitute of **E**lectrical and **E**lectronics **E**ngineers，简称为**IEEE**，英文读作“i triple e”\[ai trɪpl i:\]）是一个建立于1963年1月1日的国际性电子技术与电子工程师协会，亦是世界上最大的专业技术组织之一，拥有来自175个国家的42万会员。
  * 2019年5月29日，网络上曝光的邮件显示，由于美国政府将华为列入“实体清单”，IEEE向旗下刊物的主编提出这样的要求：**禁止来自华为的同僚担任审稿人或编辑**\[2\]\[3\]。 IEEE随后在其中文官网上发表中英文声明，承认发布禁令\[4\]。

    此事在学术圈引起轩然大波，接连有北大、清华的两名学者宣布退出IEEE编委\[5\]\[6\]。中国计算机学会发表声明，暂时中止与IEEE旗下通信学会ComSoc的交流与合作，不建议CCF会员向任何ComSoc主办的会议和刊物投稿，建议CCF会员不参加ComSoc主办的刊物和会议的审稿和其他学术评价活动\[7\]。有评论认为这代表全球最大技术学术机构向政治弯腰，IEEE是在滥用它作为平台的先发优势，透支自己的国际信誉。早前IEEE就曾因禁运的原因，禁止伊朗学者担任会议的大会主席或者财务官；还曾禁止古巴、伊朗、利比亚和苏丹学者向IEEE任何出版物发表文章\[8\]。6月2日，中国科协所属十大学会发表声明，指出 “敦促IEEE清醒认识事件对全球科学共同体所造成的危害”\[9\]。

    2019年6月3日，IEEE官网发布中英文声明，确认解除对华为的禁令。

