0.[redis使用手册](http://redisdoc.com/index.html)

1.[redis事务、lua脚本和管道](https://blog.csdn.net/fangjian1204/article/details/50585080)

2.为啥 Redis 单线程模型也能效率这么高？
```
纯内存操作。
核心是基于非阻塞的 IO 多路复用机制。
C 语言实现，一般来说，C 语言实现的程序“距离”操作系统更近，执行速度相对会更快。
单线程反而避免了多线程的频繁上下文切换问题，预防了多线程可能产生的竞争问题。
```
3.[redis文件时间处理器](http://redisbook.com/preview/event/file_event.html)

**文件处理器4部分**

![文件处理器4部分](http://redisbook.com/_images/graphviz-f0d024ca2782cbbe20e2cd1e52540d92f64b3a37.png)

**IO多路复用程序通过队列实现有序、同步、one-one的向文件事件分配器传送套接字**

![IO多路复用程序通过队列实现有序、同步、one-one的向文件事件分配器传送套接字](http://redisbook.com/_images/graphviz-f4835e5b07c5a6ab04e09dc8d887d62a1854ac94.png)
