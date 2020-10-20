1.[重复消费、顺序消费、分布式事务](https://mp.weixin.qq.com/s/OKon95MRUqDc9IwtEqPSjQ)

幂等、hash取余到相同的分区、rocketmq事务消息
```
MessageQueueSelector，此接口RocketMQ提供了三种实现SelectMessageQueueByRandoom，SelectMessageQueueByHash，SelectMessageQueueByMachineRoom，
可由调用方自行根据业务实现。指定将消息发送到对应的队列中去
```
