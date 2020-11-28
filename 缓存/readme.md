0.[redis使用手册](http://redisdoc.com/index.html)

1.[redis事务、lua脚本和管道](https://blog.csdn.net/fangjian1204/article/details/50585080)

2.为啥 Redis 单线程模型也能效率这么高？
```
纯内存操作。
核心是基于非阻塞的 IO 多路复用机制。
C 语言实现，一般来说，C 语言实现的程序“距离”操作系统更近，执行速度相对会更快。
单线程反而避免了多线程的频繁上下文切换问题，预防了多线程可能产生的竞争问题。
```
