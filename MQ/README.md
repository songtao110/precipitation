1.[重复消费、顺序消费、分布式事务](https://mp.weixin.qq.com/s/OKon95MRUqDc9IwtEqPSjQ)

幂等、hash取余到相同的分区、rocketmq事务消息
```
MessageQueueSelector，此接口RocketMQ提供了三种实现SelectMessageQueueByRandoom，SelectMessageQueueByHash，SelectMessageQueueByMachineRoom，
可由调用方自行根据业务实现。指定将消息发送到对应的队列中去

1).先发送预提交消息，根据消息唯一key幂等（Producer.checkLocalTransaction）
2).处理业务逻辑
3).根据业务处理成功或者失败，发送提交或者回滚通知（ack）
```
2.[kafka中生产者是如何把消息投递到哪个分区的？消费者又是怎么选择分区的？](https://mp.weixin.qq.com/s/vAzyODtGbvZfv0iXV4Ij1Q)
```
生成者分区策略
如果在发消息的时候指定了分区，则消息投递到指定的分区
如果没有指定分区，但是消息的key不为空，则基于key的哈希值来选择一个分区
如果既没有指定分区，且消息的key也是空，则用轮询的方式选择一个分区

消费者分区策略
rang(范围)
roundrobin(轮询)
一个分区只能分配个给同组的一个消费者消费
```
3.kafka为什么那么快？
```
1.写入数据
顺序读写：在顺序读写的情况下，某些优化场景磁盘的读写速度可以和内存持平
而且Linux对于磁盘的读写优化也比较多，包括read-ahead和write-behind，磁盘缓存

不是要java堆而使用磁盘的好处：
磁盘顺序读写速度超过内存随机读写
JVM的GC效率低，内存占用大。使用磁盘可以避免这一问题
系统冷启动后，磁盘缓存依然可用

2.Memory Mapped Files
即便是顺序写入硬盘，硬盘的访问速度还是不可能追上内存。所以Kafka的数据并 不是实时的写入硬盘 ，它充分利用了现代操作系统 分页存储 来利用内存提高I/O效率。
Memory Mapped Files(后面简称mmap)也被翻译成 内存映射文件 ，在64位操作系统中一般可以表示20G的数据文件，它的工作原理是直接利用操作系统的Page来实现文件到物理内存的直接映射。完成映射之后你对物理内存的操作会被同步到硬盘上（操作系统在适当的时候）。

通过mmap，进程像读写硬盘一样读写内存（当然是虚拟机内存），也不必关心内存的大小有虚拟内存为我们兜底。

使用这种方式可以获取很大的I/O提升， 省去了用户空间到内核空间 复制的开销（调用文件的read会把数据先放到内核空间的内存中，然后再复制到用户空间的内存中。）也有一个很明显的缺陷——不可靠， 写到mmap中的数据并没有被真正的写到硬盘，操作系统会在程序主动调用flush的时候才把数据真正的写到硬盘。 Kafka提供了一个参数——producer.type来控制是不是主动flush，如果Kafka写入到mmap之后就立即flush然后再返回Producer叫 同步 (sync)；写入mmap之后立即返回Producer不调用flush叫 异步 (async)。

3.基于sendfile实现Zero Copy

4.批量压缩

小结：
partition 并行处理
顺序写磁盘，充分利用磁盘特性
利用了现代操作系统分页存储 Page Cache 来利用内存提高 I/O 效率
采用了零拷贝技术
Producer 生产的数据持久化到 broker，采用 mmap 文件映射，实现顺序的快速写入
Customer 从 broker 读取数据，采用 sendfile，将磁盘文件读到 OS 内核缓冲区后，转到 NIO buffer进行网络发送，减少 CPU 消耗
```
4.[我用kafka两年踩过的一些非比寻常的坑](https://mp.weixin.qq.com/s?__biz=MzkxMjE5NTY4MQ==&mid=2247484317&idx=1&sn=3e53094cdabfab9c40ec42106c8b763e&chksm=c111ea93f6666385d5b7df02d6ed82965d791803d8c8832e66fb0dfdc3b5aa32889bd13c7e65&mpshare=1&scene=24&srcid=0421haTaVBrtxtMtMBCNayqM&sharer_sharetime=1618968559641&sharer_shareid=b781b4c59f55ee8f91f5e266479b254f&exportkey=Aa9EVyOmHQf1rFCajqxlNIs%3D&pass_ticket=FrHlmTp2yk2o8dyk5WkyzuKGZL%2FUdU%2BnDWf%2B5RWtIjpQGlYBxiRzdTt7riT2C1Ms&wx_header=0#rd)

```
1.顺序问题，按照一定业务规则到一个分区，保证顺序，下游保证消费的失败重试。
2.消息积压，消息体不易过大，分区规则注意热点问题
3.大批量消息积压，增加partition数量，增加消费能力，数据库表过大，处理耗时严重，影响TPS
4.重复消费，不使用分布式锁，可以使用 mysql的INSERT INTO ...ON DUPLICATE KEY UPDATE
5.注意数据库主从延迟的问题
```
5.下一代消息中间件
[pulsar](http://pulsar.apache.org/docs/zh-CN/next/standalone-docker/)
