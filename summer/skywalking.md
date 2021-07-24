### 关于skywalking的学习

* service mesh 是微服务时代的TCP协议

##### 整体架构

![](/home/jingzhe/IT/src/github.com/royal-dargon/typora/summer/0081Kckwly1gkl533fk5xj31pc0s8h04.jpg)

* 整个架构分为上下左右四个部分
  * 上部分 **Agent** ：负责从应用中，收集链路信息，发送给 SkyWalking OAP 服务器。目前支持 SkyWalking、Zikpin、Jaeger 等提供的 Tracing 数据信息。而我们目前采用的是，SkyWalking Agent 收集 SkyWalking Tracing 数据，传递给服务器。
  * 下部分 **SkyWalking OAP** ：负责接收 Agent 发送的 Tracing 数据信息，然后进行分析(Analysis Core) ，存储到外部存储器( Storage )，最终提供查询( Query )功能。
  * 右部分 **Storage** ：Tracing 数据存储。目前支持 ES、MySQL、Sharding Sphere、TiDB、H2 多种存储器。而我们目前采用的是 ES ，主要考虑是 SkyWalking 开发团队自己的生产环境采用 ES 为主。
  * 左部分 **SkyWalking UI** ：负责提供控台，查看链路等等。

