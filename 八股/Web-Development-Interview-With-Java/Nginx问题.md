# Nginx 问题

## 1、常用配置参数？

```java
worker_processes number | auto;  // 设置工作线程数，是Nginx服务器实现并发处理服务的关键所在。
```

```tsx
worker_connections number; // 设置最大连接数
```

```Java
keepalive_timeout timeout [header_timeout]; // 配置连接超时时间
```

## 2、nginx 进程模型？（shopee）

![](nginx.png)

Nginx 是**多进程**的，启动时会先启动一个 Master 进程，然后由 Master 进程启动 子 Worker 工作进程，Master 主要作**配置读取**，**维护 Worker 进程启动-销毁**等，Worker 进程对请求进行处理，**Worker 进程之间通过共享内存进行通信**，启动 Nginx 时，默认设置 Worker 进程数为 CPU 的核心数。、

## 3、nginx 负载均衡？（美团）（滴滴）（平安科技）

round robin (轮询)
random (随机)
weight (权重)
// fair (按响应时长，三方插件)
url_hash (url 的 hash 值)
ip_hash (ip 的 hash 值)
least_conn (最少连接数)
