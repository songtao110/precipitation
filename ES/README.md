## 1.ES性能优化

[理解Elasticsearch和面试总结](https://mp.weixin.qq.com/s?__biz=MzAwNjQwNzU2NQ==&mid=2650345870&idx=1&sn=a266d67f1b34db3e0aa4cba8f375bc56&chksm=8300656cb477ec7a4735c3ec47712bb20794335abc1b9fd1d00e5a142361747145e5518ec8bf&scene=132#wechat_redirect)

1).理解filesystem cache
需要控制索引字段的数量，只存储用来搜索的那些字段，其他全量的数据可能放在Hbase或者MySQL里

2).数据预热，必要的时候需要提供专门的缓存预热子系统

3).冷热分离，冷数据 和 热数据单独分开索引

4).优化分页
```
  不允许深度分页（from+size）（默认深度分页性能很差）
  类似于 app 里的推荐商品不断下拉出来一页一页的（scroll api），不支持跳页
  
  scroll 会一次性给你生成所有数据的一个快照，然后每次滑动向后翻页就是通过游标 scroll_id 移动，获取下一页下一页这样子，
  性能会比上面说的那种分页性能要高很多很多，基本上都是毫秒级的。
  缺点是：不支持实时请求，会占用大量的资源（特别是排序的请求）。
  
  search_after 的方式（>= 5.0），支持实时数据，search_after 适用于深度分页+ 排序，不支持跳页。
  其实和目前 moa 内存中使用rbtree 分页的原理
```

## 2.原理
[Elasticsearch基本概念和索引原理](https://juejin.cn/post/6897815686802833416?utm_source=gold_browser_extension)

![写索引流程](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/693731cfa5234a4fa88a73ca69ee17ab~tplv-k3u1fbpfcp-zoom-1.image)
