1.[ThoughtWorks洞见](https://insights.thoughtworks.cn/tag/domain-driven-design/)

2.理解领域驱动设计中的聚合
  
  1).聚合的定义
  ```
    将实体和值对象划分为聚合并围绕着聚合定义边界。选择一个实体作为每个聚合的根，并仅允许外部对象持有对聚合根的引用。
    作为一个整体来定义聚合的属性和不变量，并把其执行责任赋予聚合根或指定的框架机制
  ```
  
  2).聚合划分的原则
  ```
    a.生命周期一致性
    b.问题域一致性
    c.场景一致性
    d.聚合内的元素尽可能少
  ```
   3).在实现层面看
  ```
    从实现角度，资源库、工厂的粒度应该和聚合的粒度一致，代码结构和部署结构也可以和聚合对齐。实现和领域模型保持一致，
    这也是领域驱动设计作为正确的 OO 的目标和价值所在。
  ```