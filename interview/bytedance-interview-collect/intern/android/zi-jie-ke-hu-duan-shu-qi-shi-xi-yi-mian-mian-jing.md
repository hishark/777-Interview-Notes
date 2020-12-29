# 字节客户端暑期实习一面面经

{% embed url="https://www.nowcoder.com/discuss/415087" %}

*  java容器有哪些
*  hashmap底层原理（必考）
  *  hash值的计算（不知道为啥我说高16和低16位异或面试官有点犹疑的亚子。。）
  *  为什么要重写equals和hashcode （我说提高比较的效率）
  *  插入的时候会发生啥（直接插值，链表，红黑树，忘记说扩容了不过也没问）
*  扯到红黑树特性（就知道什么黑节点层数一样。扯了查找树的特性，试图糊弄）
*  网页中输入一个网址会发生啥\(DNS，http，tcp，ip。。。）
*  DNS流程是怎样的（迭代和递归询问，忘说先查本地缓存了，没细究）
*  TCP三次握手四次挥手，为什么，和UDP的区别
*  handler机制
  *  looper，message，handler，queue
  *  handler内存泄漏，内存泄漏的引用链是啥？（looper—&gt;messagequeue-&gt;message-&gt;handler,所以如果队列为空就不会泄露）
  *  扯到了对象池（Message类维护，每个message有next指针）
  *  怎么解决内存泄漏（声明static，弱引用包裹）
*  Recyclerview缓存机制
  *  四级缓存
    *  attachedScrap：还在页面的viewholder
    *  changedScrap：与view分离的viewholder
    *  cacheView：刚移出屏幕的缓存，可直接复用
    *  ViewCacheExtension：自己定义
    *  RecycledViewPool：超出cachedView的viewHold，数据被清空要重新设置
*  fragment生命周期
  *  大概说了跟activity对应的流程，（方法名饶了我吧）
  *  说了怎么替换fragment，怎么用fragmentmanager
  *  fragment结束的时候回调什么？（母鸡）
*  binder机制（跳过）
*  算法题：找树中有没有和为特定值的路径，返回boolean，看错条件被提醒两次。。（人傻了当时）

