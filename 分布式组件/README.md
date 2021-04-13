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

### 2.分布式一致性算法

[分布式一致性算法 Paxos、Raft、Zab的区别与联系](https://www.cnblogs.com/bigband/p/13520586.html)
分布式数据一致性算法（共识算法）

### 强一致性
1.paxos
2.Raft（muti-paxos） 优点是节省同步次数，如果集群中的 Leader 是非常稳定的，那么我们往往不需要准备阶段的工作，这样就能够将 RPC 的数量减少一半
3.ZAB（muti-paxos）

```
说明：ZAB也是对Multi Paxos算法的改进，大部分和raft相同，和raft算法的主要区别：
对于Leader的任期，raft叫做term，而ZAB叫做epoch
在状态复制的过程中，raft的心跳从Leader向Follower发送，而ZAB则相反。
```

### 弱一致性（最终一致性）
4.DNS系统

5.Gossip协议
类似病毒传播的方式，节点之间没有角色区分
