# precipitation
## 技术沉淀

### 迅速脑补
```
TCP(linux内核协议栈、用户区、内核区、硬件、)
Netty(对外内存、0拷贝)
[DPDK](https://www.cnblogs.com/bakari/p/8404650.html)
高频交易
[gc的语言](https://blog.csdn.net/big_white_py/article/details/107623488)
Go
```
[零拷贝](https://mp.weixin.qq.com/s/tbcQGVXC1B8S7H8BwN9HbQ)
```
mmap
sendfile
java(MappedByteBuffer、map方法、DirectByteBuffer、
FileChannel.transferTo:允许将一个通道交叉连接到另一个通道，而不需要一个中间缓冲区来传递数据； 
注：这里不需要中间缓冲区有两层意思：
第一层不需要用户空间缓冲区来拷贝内核缓冲区，
另外一层两个通道都有自己的内核缓冲区，两个内核缓冲区也可以做到无需拷贝数据)
```
