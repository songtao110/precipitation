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
