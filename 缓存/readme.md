## 0.[redis使用手册](http://redisdoc.com/index.html)

## 1.[redis事务、lua脚本和管道](https://blog.csdn.net/fangjian1204/article/details/50585080)

## 2.为啥 Redis 单线程模型也能效率这么高？
```
纯内存操作。
核心是基于非阻塞的 IO 多路复用机制。
C 语言实现，一般来说，C 语言实现的程序“距离”操作系统更近，执行速度相对会更快。
单线程反而避免了多线程的频繁上下文切换问题，预防了多线程可能产生的竞争问题。
```
## 3.[redis文件事件](http://redisbook.com/preview/event/file_event.html)

**3.1文件处理器4部分**

![文件处理器4部分](http://redisbook.com/_images/graphviz-f0d024ca2782cbbe20e2cd1e52540d92f64b3a37.png)

**3.2IO多路复用程序通过队列实现有序、同步、one-one的向文件事件分配器传送套接字**

![IO多路复用程序通过队列实现有序、同步、one-one的向文件事件分配器传送套接字](http://redisbook.com/_images/graphviz-f4835e5b07c5a6ab04e09dc8d887d62a1854ac94.png)

**3.3IO多路复用程序**

![IO多路复用程序](http://redisbook.com/_images/graphviz-840bfb6ea3cc590829fecd9b9062002d59dbf673.png)

**3.4事件类型**
| 事件类型 | 客户端对套接字的操作 |
| --- | --- |
| ae.h/AE_READABLE | write、close、connectread |
| ae.h/AE_WRITABLE | read |

如果一个套接字又可读又可写的话， 那么服务器将先读套接字， 后写套接字

**3.5文件事件处理器**
```
连接应答处理器、命令请求处理器、命令回复处理器、特别为复制功能编写的复制处理器

连接应答处理器创建客户端套接字之后，将客户端套接字的 AE_READABLE 事件与命令请求处理器进行关联， 使得客户端可以向主服务器发送命令请求。
在客户端连接服务器的整个过程中， 服务器都会一直为客户端套接字的 AE_READABLE 事件关联命令请求处理器。
当命令回复发送完毕之后， 服务器就会解除命令回复处理器与客户端套接字的 AE_WRITABLE 事件之间的关联。
```
![客户端与 Redis 的一次通信过程](https://doocs.gitee.io/advanced-java/docs/high-concurrency/images/redis-single-thread-model.png)

## redis设计与实现
[redis设计与实现](http://redisbook.com/)

[源码阅读指引](https://github.com/huangz1990/redis-3.0-annotated)

[《Redis 设计与实现》图片集](http://1e-gallery.redisbook.com/)

[从应用到底层 36张图带你进入Redis世界](https://juejin.cn/post/6906680666214105102?utm_source=gold_browser_extension)

[redis命令参考](http://redisdoc.com/index.html)

## redis分布式锁的问题
[解决Redis分布式锁业务代码超时导致锁失效问题](https://copyfuture.com/blogs-details/20200319225649988yl21w5wqv89z2fj)

## 4.数据编码结构
![Redis基本数据类型](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/3e11f892646f4f58ab9b6f5d558863cf~tplv-k3u1fbpfcp-watermark.image)

## 5.redis使用技巧
```
1.redis cluster架构下怎么让相关的数据落到同一节点上？
在key最加{hash tag} 。Redis在计算槽编号的时候只会获取{}之间的字符进行槽编号计算。如：set a{aqs}a 1、set a{aqs}b 2
2.命令统计工具INFO commandstats
比如命令执行了多少次，执行命令所耗费的毫秒数(每个命令的总时间和平均时间)
3.如果你的数据很重要，请使用 Try/Except
5.
```
## 6.redis客户端
[剖析更高级的Redis客户端Lettuce](https://mp.weixin.qq.com/s?__biz=MzI3MTEwODc5Ng==&mid=2650860743&idx=1&sn=91742ee5f6d4b4173613d12196de9d84&chksm=f1329314c6451a025a6327b7a9f868a8cdba08af6258ebbde2ef0b0cf732103621a921be0c39&scene=21#wechat_redirect)
