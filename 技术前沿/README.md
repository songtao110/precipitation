### 1.serverMesh
```
1）微服务下的服务发现和负载均衡的问题
三种服务发现的模式：
模式一：集中式
模式二：客户端嵌入式
模式三：主机独立进程代理，模式三(ServiceMesh)也被形象称为边车(Sidecar)模式
```
![三种模式比较](https://img-blog.csdnimg.cn/20200711235222814.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JhaWNob3VmZWk5MA==,size_16,color_FFFFFF,t_70)

在Service Mesh架构中，给每一个微服务实例部署一个Sidecar Proxy。该Sidecar Proxy负责接管对应服务的入流量和出流量，并将微服务架构中的服务订阅、服务发现、熔断、限流、降级、分布式跟踪等功能从服务中抽离到该Proxy中

![ServiceMesh架构](https://img-blog.csdnimg.cn/20200713105609546.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JhaWNob3VmZWk5MA==,size_16,color_FFFFFF,t_70)
### 2.serverless
