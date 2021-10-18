# 字节三面问题整理

[https://github.com/Sophia-fez/SE-IOS-Notes/blob/master/%E8%AE%A1%E7%BD%91%20OS/%E5%AD%97%E8%8A%82%E4%B8%80%E9%9D%A2%E4%BA%8C%E9%9D%A2%E9%97%AE%E9%A2%98%E6%95%B4%E7%90%86.md](https://github.com/Sophia-fez/SE-IOS-Notes/blob/master/%E8%AE%A1%E7%BD%91%20OS/%E5%AD%97%E8%8A%82%E4%B8%80%E9%9D%A2%E4%BA%8C%E9%9D%A2%E9%97%AE%E9%A2%98%E6%95%B4%E7%90%86.md)

面的时候这些问题都答的不太好……之后查了下，稍微清楚一点点，也不是很能查得到说的清楚的资料\_(:з」∠)\_

一面二面是一个下午面完的，都是技术面，三面是一面二面面完后再约的，三面更偏HR面

### 在浏览器输入一个网址接下来会发生的事情

详情见 “牛客IOS面经整理”

大概是有DNS解析、HTTPS整套流程（TCP链接，SSL链接，对称加密、非对称加密、CA证书链）等

### 栈和堆的区别

详情见 “牛客IOS面经整理”

### 分页、分段、段页式

详情见 “牛客IOS面经整理”

### 设计模式及demo相关问题

详情见 “牛客IOS面经整理”

### 复制黏贴怎么实现的

**问：比如一个应用复制了另一个应用怎么拿到的，复制的内容太大了怎么办，如何分辨是image还是text？**

操作系统中会有一块地方，称作剪贴板（clipboard），专门用来处理复制粘贴。

不同系统的细节可能会不同，但大致上是这样的：

* 复制文本时，会把所复制的文本克隆一份到剪贴板里面。粘贴文本时，再将剪贴板里的文本克隆到所粘贴应用程序之中；
*
  * 复制文本时会保留其样式（比如在 Office 软件中复制，也会存储字体、字号等等信息，复制到剪贴板的实质上是一种「标记语言」）。但粘贴时若应用程序（比如记事本）不支持这些样式，则会去掉样式；
  * 复制图片、混合富文本时，也是同样先克隆到剪贴板里。
* 复制文件时，系统只会把文件的**路径**复制到剪贴板，等到粘贴时再**分情况处理**：
*
  * 同一分区下，粘贴（或剪切）文件，都不会真正在存储设备里直接克隆、挪动，而是更改此文件的路径（path）属性。当然这与不同文件系统的具体实现有关；
*
  *
    * （这也就是为什么，「复制 → 删除复制源文件 → 粘贴」这个操作会在大部分系统中失效了）
*
  * 不同分区下，粘贴（或剪切）文件，会重新开辟空间，然后克隆文件；
  * 涉及到与其他设备（即插即用设备等）之间的复制粘贴则更加复杂，实现各有不同。
* 还要考虑的情况，就是涉及虚拟机、远程主机的复制粘贴机制。虚拟机软件、远程主机软件都会有一个「介于两系统之间的」剪贴板，「连接起」这两个系统的各自剪贴板，并做一些编码格式转换的工作。
*
  * 关于虚拟机复制粘贴，更具体的细节可以看这里：[Is it possible to copy paste between Mac OS and its virtual machine?](https://link.zhihu.com/?target=http%3A//apple.stackexchange.com/questions/48756/is-it-possible-to-copy-paste-between-mac-os-and-its-virtual-machine) 各软件实现有异。

按照我自己想的和面试时候回答的，如果复制的是文件本身，那都是01串，在比特层面，不同后缀的文件是在某一块区域有区别的，CTF比赛里就是通过这种方式把隐藏的图片啊、文本啊提取出来的

然后复制的图片/文件太大了的话，复制的是路劲是地址，然后粘贴时候看情况处理，如上面所说的可能是重新开辟新空间然后克隆文件，网络图片那复制的只有地址

### 一个可执行文件的编译过程

这个问题本应该会的，本科汇编课还研究过，但是长久没有复习都忘记了，直接的java文件是javac这个命令编译，C++是gcc这个当时都没想起来，我只记得那个命令是什么cc

### 如何将一个长URL转换为一个短URL

[如何将一个长URL转换为一个短URL](https://blog.csdn.net/xlgen157387/article/details/80026452)

[HTTP重定向](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Redirections)

URL 重定向，也称为 URL 转发，是一种当实际资源，如单个页面、表单或者整个 Web 应用被迁移到新的 URL 下的时候，保持（原有）链接可用的技术。HTTP 协议提供了一种特殊形式的响应—— HTTP 重定向（HTTP redirects）来执行此类操作。

HTTP重定向：服务器无法处理浏览器发送过来的请求（request），服务器告诉浏览器跳转到可以处理请求的url上。（浏览器会自动访问该URL地址，以至于用户无法分辨是否重定向了。） 重定向的返回码3XX说明。Location响应首部包含了内容的新地址或是优选地址的URL。

状态码 301：在请求的URL已被移除时使用。响应的Location首部中应该包含资源现在所处的URL。 302：与301状态码类似，但是，客户端应该使用Location首部给出的URL来零食定位资源，将来的请求仍然使用老的URL。

官方的比较简洁的说明：

301 redirect: 301 代表永久性转移(Permanently Moved) 302 redirect: 302 代表暂时性转移(Temporarily Moved ) 尽量使用301跳转！301和302状态码都表示重定向，就是说浏览器在拿到服务器返回的这个状态码后会自动跳转到一个新的URL地址，这个地址可以从响应的Location首部中获取（用户看到的效果就是他输入的地址A瞬间变成了另一个地址B）——这是它们的共同点。他们的不同在于。301表示旧地址A的资源已经被永久地移除了（这个资源不可访问了），搜索引擎在抓取新内容的同时也将旧的网址交换为重定向之后的网址；302表示旧地址A的资源还在（仍然可以访问），这个重定向只是临时地从旧地址A跳转到地址B，搜索引擎会抓取新的内容而保存旧的网址。

### 两个线程同时访问i++ 10000次操作，多线程并发问题

多线程访问最后的结果不确定，可能是各加一次，也可能只加一次

### image框架 Kingfisher

[特征](https://www.jianshu.com/p/e025cec4197a)

* 异步下载和缓存图片
* 基于`networking`的`URLSession`, 提供基础的图片处理器和过滤器
* 内存和磁盘的多层缓存
* 可撤销组件，可根据需要分开地使用下载器和缓存系统
* 必要时可从缓存中读取并展示图片
* 扩展`UIImageView`、`NSImage`、`UIButton`来直接设置一个`URL`图片
* 设置图片时，内置过渡动画
* 支持扩展图片处理和图片格式

[Kingfisher获取图片](https://www.jianshu.com/p/cc8a2900fe4d)

Kingfisher从`url`下载图片，将图片存储在内存缓存和磁盘缓存，然后将它展示在`imageView`上。当使用同样的代码后（url不变），就会直接从内存中获取之前缓存的图片并立即显示出来。

### 算法题

以下不一定是完整代码，因为有些调试没有进行到最后，做的也不是很完美，三次都各出现了点小状况，惭愧。算法题只有一个main函数，不是核心代码模式哦，三条感觉都是easy里偏难，medium里偏简单的题目，不过输出、调试比较坑，害，被leetcode惯坏了。

#### 一面 [445. 两数相加 II](https://leetcode-cn.com/problems/add-two-numbers-ii/)

给定两个非空链表来代表两个非负整数。数字最高位位于链表开始位置。它们的每个节点只存储单个数字。将这两数相加会返回一个新的链表。

```
import java.util.*;
public class Main {
    public static void main(String[] args) {
        //Scanner in = new Scanner(System.in);
        //int a = in.nextInt();
        //System.out.println(a);
        System.out.println("Hello World!");
        
        
        
        reverse(l1);
        reverse(l2);
        reverse(add(l1, l2));
    }
    
    public static ListNode add(ListNode l1, ListNode l2) {
        ListNode dummpy = new ListNode(0);
        ListNode cur = dummpy;
        int carry = 0
        while(l1 != null || l2 != null) {
            int n1 = l1 == null ? 0 : l1.val;
            int n2 = l2 == null ? 0 : l2.val;
            int sum = n1 + n2 + carry;
            carry = sum / 10;
            cur.next = new ListNode(sum % 10);
            cur = cur.next;
        }
        if(carry != 0) cur.next = new ListNode(carry);
        return dummpy.next;
    }
    
    public static ListNode reverse(ListNode head) {
        ListNode pre = null;
        ListNode cur = head;
        while(cur != null) {
            ListNode temp = cur.next;
            cur.next = pre;
            pre = cur;
            cur = temp;
        }
        return pre;
    }
}
```

#### 二面

找出一个数组中的所有K数。

* K数定义：前面的数都比它小，后面的数都比它大。
* 举例：1 3 2 4 7 5 9 其中K数有：1 4 9

思路一看就是快排，暂时不知道leetcode上哪题，印象里没见过

```
import java.util.*;
public class Main {
    public static int index = 0;
    public static void main(String[] args) {
        //Scanner in = new Scanner(System.in);
        //int a = in.nextInt();
        //System.out.println(a);
        System.out.println("Hello World!");
        
        int[] nums = {1, 3, 2, 4, 7, 5, 9};
        int[] ans = isK(nums);
        for(int i = 0; i < index; i++)
            System.out.print(ans[i] + " ");
        }
    }
    
    public static int[] isK(int[] nums) {
        //ArrayList<Integer> ans = new ArrayList<>();
        
        int len = nums.length;
        if(len == 0) return new int[]{};
        int[] ans = new int[len];
        
        for(int i = 0; i < len; i++) {
            swap(nums, 0, i);
            if(position(nums, 0, len - 1) == i) {
                ans[index++] = nums[i];
            }
            swap(nums, 0, i);
        }
        return ans;
    }
    
    public static void swap(int nums[], int i, int j) {
        int temp = nums[i];
        nums[i] = nums[j];
        nums[j] = temp;
    }
    
    //一次划分
    public static int position(int[] nums, int left, int right) {
        int pos = nums[left]; // 基准
        while(left < right) {
            while(nums[right] > pos) {
                right--;
            }
            if(left < right){
                nums[left] = nums[right];
                left++;
            }
            while(nums[left] <= pos) {
                left++;
            }
            if(left < right){
                nums[right] = nums[left];
                right--;
            }
        }
        return left;
    }
}
```

#### 三面 [剑指 Offer 67. 把字符串转换成整数](https://github.com/Sophia-fez/SE-IOS-Notes/blob/master/%E8%AE%A1%E7%BD%91%20OS)

判断一个字符串是否是10进制32位正整数

```
import java.util.*;
public class Main {
    public static void main(String[] args) {
        //Scanner in = new Scanner(System.in);
        //int a = in.nextInt();
        //System.out.println(a);
        System.out.println("Hello World!");
        System.out.println(Integer.MAX_VALUE);
        String str = "+12649901";
        int ans = judge(str);
        System.out.println(ans);
    }
    public static int judge(String str) {
        int len = str.length();
        if(len == 0) return -1;
        
        char[] c = str.toCharArray();
        int i = 0;
        
        // 找第一个不是空格且不是+的字符
        while(i < len && c[i] == ' ') {
            i++;
        }
        
        if(i < len && c[i] == '+') {
            i++;
        }
        
        while(i < len && c[i] == '0') {
            i++;
        }
        
        if(i == len) return -1;
        
        int num = 0;
        int max = Integer.MAX_VALUE / 10;
        
        if(c[i] < '0' && c[i] > '9') {
            return -1;
        } else {
            while(i < len) {
                if(c[i] >= '0' && c[i] <= '9') {
                    int temp = (int)(c[i] - '0');
                    // 处理越界
                    if(max < num || (max == num && temp > 7)) {
                        return -1;
                    }
                    num = num * 10 + temp;
                } else {
                    return -1;
                }
                i++;
            }
        }
        return num;
    }
}
```
