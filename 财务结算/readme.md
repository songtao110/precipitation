## 1.高并发下怎么做余额扣减？
```
》悲观锁：行锁，select * from xxx where for update
》乐观锁：CAS
》业务层面多账户：提高并行度
》记录持久化，实时余额内存化，或者redis化，异步化汇总

```
