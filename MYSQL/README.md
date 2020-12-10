1.[MySQL实战45讲 笔记](https://jiankunking.com/45-lectures-on-mysql-in-practice-notes.html)

2.[数据库分库分表](https://juejin.im/post/6892916124141551629?utm_source=gold_browser_extension)

3.[为什么是B+tree](https://juejin.im/post/6893291359675875336)

4.[三歪连MVCC和事务隔离级别的关系都不知道](https://mp.weixin.qq.com/s/0-YEqTMd0OaIhW99WqavgQ)

5.[MySQL 是怎么死锁的?](https://mp.weixin.qq.com/s/wwe07uJ0N1Hk6ZQyGsCkHA)

6.[MySQL相关工具](https://juejin.cn/post/6899306849686781959?utm_source=gold_browser_extension)

## 日志&MVCC
### binlog
是数据库server层面基于sql语句层面记录的日志，数据库改变事件，包括事件发生的时间、开始位置、结束位置等信息。

### redolog（重做日志）
mysql 有一个基本的技术理念，那就是 WAL，即  Write-Ahead Logging，先写日志，再写磁盘可即redolog。
redolog占用固定大小的磁盘空间，循环顺序写，基于磁盘块的方式写入，和binlog两阶段提交的方式配合写入。
写入redulog，并标记prepare>写入binlog>提交事务commit
redolog基于事务粒度的记录，保证数据库的原子性

### undolog（回滚日志）
undolog记录的是逻辑日志，insert操作那日志就记录delete，update操作就记录相反的update，因此保证数据库的一致性。
mvcc的实现原理

### MVCC
在数据库的每一行中，添加额外的三个字段：
- DB_TRX_ID — 记录插入或更新该行的最后一个事务的事务 ID
- DB_ROLL_PTR — 指向改行对应的 undolog 的指针
- DB_ROW_ID — 单调递增的行 ID，他就是 AUTO_INCREMENT 的主键 ID
![MVCC](https://mmbiz.qpic.cn/mmbiz_jpg/VtlKaFJha2V0GUGShWFd8W5MZrfkvQ1D11qkTqib4FdpfGomm0DflSvmF5xL1WnsTdtwJLEWo2aLqs1x3vH46qQ/640?wx_fmt=jpeg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

[MVCC实现原理](https://mp.weixin.qq.com/s/rKYpQp4JPZL2q5p41f6V6Q)

#### 快照度
当前事务的事务ID和该条记录的DB_TRX_ID比较，如果小于或者早于该条记录的DB_TRX_ID，就说明当前事务开启后提交的，需要拿着DB_ROLL_PTR到undolog日志中读取数据。
#### 当前度
- insert
- update
- select … lock in share mode
- select … for update

**可重复读解决不可重复读与幻读问题的原理**

那么，可重复读的隔离级别是否解决了不可重复读与幻读问题呢？
上面我们提到，对于正常的 select 查询 innodb 实际上进行的是快照读，即通过判断读取到的行的 DB_TRX_ID 与 DB_ROLL_PTR 字段指向的 undo log 回溯到事务开启前或当前事务最后一次更新的数据版本，从而在这样的场景下避免了可重复读与幻读的问题。
针对已存在的数据，insert 和 update 操作虽然是进行当前读，但 insert 与 update 操作后，该行的最新修改事务 ID 为当前事务 ID，因此读到的值仍然是当前事务所修改的数据，不会产生不可重复读的问题。
**但如果当前事务更新到了其他事务新插入并提交了的数据，这就会造成该行数据的 DB_TRX_ID 被更新为当前事务 ID，此后即便进行快照读，依然会查出该行数据，产生幻读**（其他事务插入或删除但未提交该行数据的情况下会锁定该行，造成当前事务对该行的更新操作被阻塞，所以这种情况不会产生幻读问题，有关事务间的锁，不在本篇文章的讨论范围内，接下来的文章我们会进一步讨论）

## 主从同步
### 主从同步出现的原因是：
从库拷贝主库binlog日志并且串行化执行，在高并发场景下，从库的数据是有延迟的，主库宕机器，还没有同步binlog日志到从库有可能丢失数据。
### 解决方案
**半同步复制**
用来解决主库数据丢失问题

**并行复制**
用来解决主从同步延时问题（数据库级别的并行，所以要分库）

**强制走主库**
解决


