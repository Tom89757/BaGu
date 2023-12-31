# Spring Cloud Alibaba 组件 Nacos 问题

## 1、主流的服务注册中心产品？（美团）

|                  | **Nacos**                  | **Eureka**  | **Consul**        | **CoreDNS** | **Zookeeper** |
| ---------------- | -------------------------- | ----------- | ----------------- | ----------- | ------------- |
| 一致性协议       | CP+AP                      | AP          | CP                | —           | CP            |
| 健康检查         | TCP/HTTP/MYSQL/Client Beat | Client Beat | TCP/HTTP/gRPC/Cmd | —           | Keep Alive    |
| 负载均衡策略     | 权重/ metadata/Selector    | Ribbon      | Fabio             | RoundRobin  | —             |
| 雪崩保护         | 有                         | 有          | 无                | 无          | 无            |
| 自动注销实例     | 支持                       | 支持        | 不支持            | 不支持      | 支持          |
| 访问协议         | HTTP/DNS                   | HTTP        | HTTP/DNS          | DNS         | TCP           |
| 监听支持         | 支持                       | 支持        | 支持              | 不支持      | 支持          |
| 多数据中心       | 支持                       | 支持        | 支持              | 不支持      | 不支持        |
| 跨注册中心同步   | 支持                       | 不支持      | 支持              | 不支持      | 不支持        |
| SpringCloud 集成 | 支持                       | 支持        | 支持              | 不支持      | 支持          |
| Dubbo 集成       | 支持                       | 不支持      | 不支持            | 不支持      | 支持          |
| K8S 集成         | 支持                       | 不支持      | 支持              | 支持        | 不支持        |

## 2、nacos 工作原理？（华为）（滴滴）

1. **服务注册原理：**在`nacos`的服务端，有一个用来**管理微服务实例的容器**，注册中心将微服务的实例交由`ServiceHolder`处理，`ServiceHolder`为微服务提供空间并将它的所有实例挂在该空间下。服务注册完成后提供者将于注册中心维护心跳机制，心跳机制可以保证注册中心可以及时的剔除失效的实例。

2. **服务发现原理：**服务完成注册之后，消费者可以向注册中心订阅某个服务，并提交一个监视器，当注册中心的服务发生变更时监听器会收到通知，然后消费者可以更新本地的服务实例列表，以保证所有的服务均可用。

3. **nacos 的负载均衡：**`Nacos` 的客户端在获取到服务的完整实例列表后，会在客户端进行负载均衡算法来获取一个可用的实例，模式使用的是随机获取的方式。

## 3、dubbo 的注册中心原理？（百度）

0、服务容器负责启动，加载，运行服务提供者。
1、服务提供者在启动时，向注册中心注册自己提供的服务。
2、服务消费者在启动时，向注册中心订阅自己所需的服务。
3、注册中心返回服务提供者地址列表给消费者，如果有变更，注册中心将基于长连接推送变更数据给消费者。
4、服务消费者，从提供者地址列表中，**基于软负载均衡算法**，选一台提供者进行调用，如果调用失败，再选另一台调用。

5、服务消费者和提供者，在内存中累计调用次数和调用时间，定时每分钟发送一次统计数据到监控中心。

# Spring Cloud Alibaba 组件 seata 问题

## 1、什么是分布式事务？（shopee）（平安科技）（有赞）

是指事务的参与方位于不同的分布式系统的节点上。

## 2、分布式事务的基础理论？（shopee）

- CAP 理论：是设计分布式系统的基础理论依据。强一致性、可用性、分区容错性。

  BASE 理论，是 Basically Available(基本可用)、Soft state(软状态)和 Eventually consistent (最终一致性)三个短语的缩写。是对 CAP 中 AP 的一个扩展。

  - 基本可用：
  - 软状态：相对于原子性而言，要求**多个节点的数据副本都是一致**的，这是一种“硬状态”。软状态指的是：允许系统中的数据存在中间状态，并认为该状态不影响系统的整体可用性，即允许系统在多个不同节点的数据副本存在数据延时。
  - 最终一致性：

## 3、分布式事务协议？（shopee）（美团）

**两阶段提交协议 2PC：**

两阶段提交协议中，存在一个节点作为**协调者**，其他参与事务的节点作为**参与者**。

**第一阶段（准备阶段）：**

- 协调者询问所有参与者是否可以执行提交操作，并等待参与者节点的响应。
- 参与者执行各自的本地事务操作，并将操作写入 undo 日志。
- 若参与者事务执行成功，返回给协调者同意信号，否则返回终止信息。

**第二阶段（提交阶段）：**

**当协调者节点从所有参与者节点获得的相应消息都为"同意"时**

- 协调者向所有参与者发出 commit 请求。
- 参与者节点完成事务提交操作并释放整个事务期间占用的资源。
- 参与者向协调者返回完成信息。协调者接收到所有参与者返回的完成信息后完成事务。

**若任一参与者节点在第一阶段返回的响应消息为"中止"。**

- 协调者节点向所有参与者节点发出"回滚操作(rollback)"的请求。
- 参与者节点利用之前写入的 Undo 信息执行回滚，并释放在整个事务期间内占用的资源。
- 参与者节点向协调者节点发送"回滚完成"消息。
- 协调者节点受到所有参与者节点反馈的"回滚完成"消息后，取消事务。

**三阶段提交协议 3PC：**

与两阶段提交不同的是，三阶段提交有两个改动点。

- 引入超时机制。同时在协调者和参与者中都引入超时机制。
- 在第一阶段和第二阶段中插入一个准备阶段。保证了在最后提交阶段之前各参与节点的状态是一致的。

也就是说，除了引入超时机制之外，3PC 把 2PC 的准备阶段再次一分为二，这样三阶段提交就有`CanCommit`、`PreCommit`、`DoCommit`三个阶段。

## 3.1、2PC 的缺点？

## 4、分布式事务的解决方案？（shopee）（美团）

**1. XA：**该协议采用两阶段提交（2PC），即整个事务控制过程经历了两个阶段。

1. 第一阶段：所有分支的操作都准备好了，由 TM 告知每个分支准备提交，此时，作为全局事物中的每个 RM 记录着在稳定存储中的动作（也就是说记录着准备好的这个动作）。
2. 第二阶段：TM 会告诉 RM 是提交或回滚，如果所有分支表明准备好能够提交时，RM 会被告知提交，如果任何一个 RM 表明没有准备好或者不能提交，则进行全部回滚。

**2. TCC（try-confirm-cancel）：**

try 阶段：尝试执行，完成所有的业务检查，预留完成业务所必须的资源。

confirm 阶段：当 TCC 事务管理器决定 commit 全局事务时，就会逐个执行**Try**操作指定的**Confirm**操作，将**Try**未完成的事项最终完成。不作任何业务检查，只使用 Try 阶段预留的业务资源。

cancel 阶段：**Cancel** 是对**Try**操作的一个回撤。当 TCC 事务管理器决定 rollback 全局事务时，就会逐个执行**Try**操作指定的**Cancel**操作，将**Try**操作已完成的事项全部撤回。

**3. MQ 事务：**

![](MQ事务.jpg)

1. 在系统 A 处理任务 A 前，首先向消息中间件发送一条消息
2. 消息中间件收到后将该条消息持久化，但并不投递。此时下游系统 B 仍然不知道该条消息的存在。
3. 消息中间件持久化成功后，便向系统 A 返回一个确认应答；
4. 系统 A 收到确认应答后，则可以开始处理任务 A；
5. 任务 A 处理完成后，向消息中间件发送 Commit 请求。该请求发送完成后，对系统 A 而言，该事务的处理过程就结束了，此时它可以处理别的任务了。 但 commit 消息可能会在传输途中丢失，从而消息中间件并不会向系统 B 投递这条消息，从而系统就会出现不一致性。这个问题由消息中间件的事务回查机制完成。
6. 消息中间件收到 Commit 指令后，便向系统 B 投递该消息，从而触发任务 B 的执行；
7. 当任务 B 执行完成后，系统 B 向消息中间件返回一个确认应答，告诉消息中间件该消息已经成功消费，此时，这个分布式事务完成。

## 5、Seata 是什么？（滴滴）（华为）（shopee）

`Seata`提供**一站式的分布式事务解决方案**。可以提供**AT**（默认使用，基于 2PC 两阶段模式）、 TCC、 SAGA 、XA 事务模式。

`Seata`的 3 + 1 个概念：

- **TC：事务协调器**，负责维护分布式事务的运行状态。负责协调并驱动全局事务的提交或者回滚。
- **TM： 事务管理器**，是一个分布式的发起者和终结者。最终发起全局提交或回滚决议。
- **RM：资源管理器**，负责本地事务的运行。负责分支注册，状态汇报，接收事务协调器的指令，驱动本地事务的提交和回滚。
- **Transaction ID**：全局事务的唯一 ID ， XID。

TM 是一个分布式事务的发起者和终结者，TC 负责维护分布式事务的运行状态，而 RM 则负责本地事务的运行。

## 6、Seata 工作流程？

1. TM 向 TC 申请开启一个全局事务，全局事务创建成功并生成一个全局唯一的 XID
2. XID 在微服务的调用链路中传播
3. RM 向 TC 注册分支事务，将其纳入 XID 对应的全局事务管辖
4. TM 向 TC 发起针对 XID 的全局提交或者回滚决议
5. TC 调度 XID 下管辖的全部分支事务完成提交或者回滚请求

## 7、怎么用？

1. 对于每个微服务对应的数据库都需要添加一张回滚日志表。用于自动的回滚一些数据。

2. 下载`seata-server`软件包，`github.com/seata/seata/releases`

3. 导入依赖 `spring-cloud-starter-alibaba-seata`

4. 启动 `seata-server`

5. 所有想要使用到分布式事务的微服务使用`seata DatasourceProxy`代理自己的数据源

6. `@GlobaTransactional` 开启全局事务。（只需要给分布式事务入口标上该注解即可），对于远程调用的方法不需要标。

7. 启动各个微服务即可。

# Spring Cloud Alibaba 组件 sentinel 问题

由于 Netflix 的`hystrix`停止更新，所以改用 spring cloud Alibaba 的 sentinel 组件实现系统的**限流、熔断、降级。**

## 1、 sentinel 是什么？

随着**微服务**的流行，**服务和服务之间的稳定性变得越来越重要**。Sentinel 是面向**分布式服务**架构的**轻量级高可用流量控制**产品，由阿里中间件团队开源。主要以流量为切入点，从**流量限制、服务熔断降级、**系统负载保护等多个维度来帮助您保护服务的稳定性。

## 2、sentinel 原理？

sentinel 项目分为 7 个主要部分，其中最主要的 就是 sentinel-core 模块。限流、熔断、降级、系统保护等都在这里实现。

## 2、什么是流量控制？

流量控制在网络传输中是一个常用的概念，**它用于调整网络包的发送数据**。然而，从系统稳定性角度考虑，在处理请求的速度上，也有非常多的讲究。任意时间到来的请求往往是随机不可控的，而系统的处理能力是有限的。我们需要根据系统的处理能力对流量进行控制。Sentinel 作为一个调配器，可以根据需要把随机的请求调整成合适的形状。

## 3、限流、熔断、降级分别是什么？

**限流：**对于打入集群的请求流量在入口处进行控制，使服务能够承担不超过自己能力的流量压 力。

**熔断：**A 服务调用 B 服务，由于各种各样的原因导致请求时间过长。这样的情况次数过多就应该考虑将 B 服务直接断路。凡是调用 B 服务直接返回错误数据。

**降级：**由于服务器的压力较大而对一些服务进行有针对的降级，从而保证核心业务的正常运行。

## 4、服务端接口有哪些保护方案？

## 5、服务降级有哪几种策略？

## 7、sentinel 对比 hystrix？（美团）

| 对比内容       | Sentinel                                       | Hystrix                       |
| -------------- | ---------------------------------------------- | ----------------------------- |
| 隔离策略       | 信号量隔离                                     | 线程池隔离/信号量隔离         |
| 熔断降级策略   | 基于响应时间或失败比率                         | 基于失败比率                  |
| 实时指标实现   | 滑动窗口                                       | 滑动窗口（基于 RxJava）       |
| 规则配置       | 支持多种数据源                                 | 支持多种数据源                |
| 扩展性         | 多个扩展点                                     | 插件的形式                    |
| 基于注解的支持 | 支持                                           | 支持                          |
| 限流           | 基于 QPS，支持基于调用关系的限流               | 不支持                        |
| 流量整形       | 支持慢启动、匀速器模式                         | 不支持                        |
| 系统负载保护   | 支持                                           | 不支持                        |
| 控制台         | 开箱即用，可配置规则、查看秒级监控、机器发现等 | 不完善                        |
| 常见框架的适配 | Servlet、Spring Cloud、Dubbo、gRPC 等          | Servlet、Spring Cloud Netflix |

#
