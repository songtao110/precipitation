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
7.对象头信息

![对象头信息](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/d71b6b702af4479f8e0185ba70b67fa5~tplv-k3u1fbpfcp-watermark.image)

8.[JVM小册子](https://juejin.cn/post/6930605141280325639)
