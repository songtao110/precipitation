1.[看完这篇JVM垃圾回收，和面试官扯皮没问题了](https://mp.weixin.qq.com/s/GekJhJBo2WY7girWV7GhBQ)

2.[Java垃圾回收CMS、G1、ZGC](https://www.cnblogs.com/zeussbook/p/12726824.html)

3.[Java中9种常见的CMS GC问题分析与解决](https://mp.weixin.qq.com/s/RFwXYdzeRkTG5uaebVoLQw)

4.[CMS GC 新生代默认是多大](https://blog.csdn.net/a479898045/article/details/96074734)

5.[CMS](https://blog.csdn.net/u010013573/article/details/88782757)

6.划分内存的方法：
```
1).指针碰撞
2).空闲列表
解决并发问题：
CAS、本地线程分配缓冲TLAB -XX:+/-UseTLAB、-XX:TLABSize 
```
7.对象信息

**Java 对象头**

GC分代信息，锁信息，哈希码，指向Class类元信息的指针
Hotspot 虚拟机的对象头主要包括两部分数据：Mark Word（标记字段）、Klass Pointer（类型指针）
    - Klass Point 是是对象指向它的类元数据的指针，虚拟机通过这个指针来确定这个对象是哪个类的实例
    - Mark Word 用于存储对象自身的运行时数据，如哈希码（HashCode）、GC 分代年龄、锁状态标志、线程持有的锁、偏向线程 ID、偏向时间戳等等。Java 对象头一般占有两个机器码（在 32 位虚拟机中，1 个机器码等于 4 字节，也就是 32 bits）。但是如果对象是数组类型，则需要三个机器码，因为 JVM 虚拟机可以通过 Java 对象的元数据信息确定 Java 对象的大小，无法从数组的元数据来确认数组的大小，所以用一块来记录数组长度。

**Java 对象实例数据**

实例数据部分是对象真正存储的有效信息
    
**Java 对象对齐填充**   

虚拟机规范要求对象大小必须是8字节的整数倍

![对象头信息](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/d71b6b702af4479f8e0185ba70b67fa5~tplv-k3u1fbpfcp-watermark.image)

8.[JVM小册子](https://juejin.cn/post/6930605141280325639)
