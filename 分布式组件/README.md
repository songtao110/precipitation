## 1.分布式链路追踪系统（APM（Application Performance Management））
### 1.1 理论基础 APM理论模型
Google Dapper论文
### 1.2 对标产品
[Skywalking](https://mp.weixin.qq.com/s/A9gmNsmuSdrMw8GqgbKa3A)

[Skywalking源码](https://zhuanlan.zhihu.com/p/110933177)

[zipkin、pinpoint](https://www.jianshu.com/p/4fa81b661f55)

### 1.3 javaAgent相关技术
[javaagent使用指南](https://www.cnblogs.com/rickiyang/p/11368932.html)

## 2.分布式监控系统
### 2.1 prometheus
```
主要可以和Kubernetes、Grafana集成
TSDB(时序数据库)
```
### 2.2 Zabbix、Open-Falcon
[Zabbix、Open-Falcon](https://www.sohu.com/a/342733264_198222)

## 3.分布式一致性算法

[分布式一致性算法 Paxos、Raft、Zab的区别与联系](https://www.cnblogs.com/bigband/p/13520586.html)
分布式数据一致性算法（共识算法）

### 3.1强一致性
1.paxos
2.Raft（muti-paxos） 优点是节省同步次数，如果集群中的 Leader 是非常稳定的，那么我们往往不需要准备阶段的工作，这样就能够将 RPC 的数量减少一半
```
Raft故障选举：如果跟随者节点不能及时收到领导角色的消息，那么跟随者就会变为竞选者，给其他节点发送选举投票通知，有过半票数则称为领导者。
Raft日志复制：
所有的写请求都交给领导者，将请求操作写入日志，标记该状态为未提交状态。
为了提交该日志，领导者就会将日志以心跳形式发送给其他跟随者，只要满足过半的跟随者可以写入该数据，则直接通知其他节点同步该数据，这个过程称为日志复制。
```
4.ZAB（muti-paxos）

```
说明：ZAB也是对Multi Paxos算法的改进，大部分和raft相同，和raft算法的主要区别：
对于Leader的任期，raft叫做term，而ZAB叫做epoch
在状态复制的过程中，raft的心跳从Leader向Follower发送，而ZAB则相反。
```

### 3.2弱一致性（最终一致性）
4.DNS系统

5.Gossip协议
类似病毒传播的方式，节点之间没有角色区分


## 4.分布式事务解决方案

### 4.1 [XA协议](https://blog.csdn.net/BruceLiu_code/article/details/114922914)
2PC 
```
缺点：它是一个强一致性的同步阻塞协议，事务执⾏过程中需要将所需资源全部锁定，也就是俗称的 刚性事务。
```
3PC
```
2PC 中只有协调者有超时机制，3PC 在协调者和参与者中都引入了超时机制，协调者出现故障后，参与者就不会一直阻塞。
虽然 3PC 用超时机制，解决了协调者故障后参与者的阻塞问题，但与此同时却多了一次网络通信，性能上反而变得更差，也不太推荐。
```

### 4.2 TCC
```
所谓的 TCC 编程模式，也是两阶段提交的一个变种，不同的是 TCC 为在业务层编写代码实现的两阶段提交。TCC 分别指 Try、Confirm、Cancel ，一个业务操作要对应的写这三个方法。
以下单扣库存为例，Try 阶段去占库存，Confirm 阶段则实际扣库存，如果库存扣减失败 Cancel 阶段进行回滚，释放库存。
TCC 不存在资源阻塞的问题，因为每个方法都直接进行事务的提交，一旦出现异常通过则 Cancel 来进行回滚补偿，这也就是常说的补偿性事务。
原本一个方法，现在却需要三个方法来支持，可以看到 TCC 对业务的侵入性很强，而且这种模式并不能很好地被复用，会导致开发量激增。还要考虑到网络波动等原因，为保证请求一定送达都会有重试机制，
所以考虑到接口的幂等性。
```

### 4.3 消息事务
```
消息事务其实就是基于消息中间件的两阶段提交，将本地事务和发消息放在同一个事务里，保证本地操作和发送消息同时成功。
```

### 4.4 Saga
```
Saga的核心就是补偿，一阶段就是服务的正常顺序调用（数据库事务正常提交），如果都执行成功，则第二阶段则什么都不做；
但如果其中有执行发生异常，则依次调用其补偿服务（一般多逆序调用未已执行服务的反交易）来保证整个交易的一致性。应用实施成本一般比较低
向后恢复：逆向补偿回滚成功的子事务，最终达到回滚的一致性
向前恢复：正向补偿重试失败的子事务，最终达到成功提交的一致性
```

### 4.5 Seata

[Seate](http://seata.io/zh-cn/docs/overview/what-is-seata.html)
