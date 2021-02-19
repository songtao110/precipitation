### 1.serverMesh
```
1）微服务下的服务发现和负载均衡的问题
三种服务发现的模式：
模式一：集中式
模式二：客户端嵌入式
模式三：主机独立进程代理，模式三(ServiceMesh)也被形象称为边车(Sidecar)模式
```
![三种模式比较](https://img-blog.csdnimg.cn/20200711235222814.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JhaWNob3VmZWk5MA==,size_16,color_FFFFFF,t_70)
```
2) 在Service Mesh架构中，给每一个微服务实例部署一个Sidecar Proxy。该Sidecar Proxy负责接管对应服务的入流量和出流量，并将微服务架构中的服务订阅、服务发现、熔断、限流、降级、分布式跟踪等功能从服务中抽离到该Proxy中
```

![ServiceMesh架构](https://img-blog.csdnimg.cn/20200713105609546.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2JhaWNob3VmZWk5MA==,size_16,color_FFFFFF,t_70)
```
IstioIstio是ServiceMesh的产品化落地
```
### 2.serverless
```
无服务器架构
对于开发者来说，Serverless架构可以将其服务器端应用程序分解成多个执行不同任务的函数，整个应用分为几个独立、松散耦合的组件，这些组件可以在任何规模上运行
FaaS
PaaS：传统的部署机器、运维服务
Baas:入Auth0和Amazon Cognito公用的登录组件

适用场景：
移动端基于事件处理的后端事件功能，如：括物联网，移动应用，基于网络的应用程序和聊天机器人

不适用的场景：
执行时间超过5秒的
有状态，在本地存储数据的
长链接，ws等
后台任务，有大数据执行的
依赖多进程通信的
大文件上传的
自定义环境的
```
