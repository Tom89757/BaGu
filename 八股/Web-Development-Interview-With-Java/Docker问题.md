# Docker 问题

## 1、是什么？（美团）（滴滴）

Docker 是一个容器化平台，它以容器的形式将您的应用程序及其所有依赖项打包在一起，以确保您的应用程序在任何环境中无缝运行。

## 2、docker 与虚拟机的区别？（网易）（滴滴）

1. docker 不需要像 VM 一样去模拟计算机硬件环境，
2. 与 VM 相比，docker 中的**镜像只保留核心功能**，如 Linux 镜像在 docker 中仅仅有 170M。
3. 主机上的**所有容器共享主机的调度程序**，从而节省了额外资源的需求。

## 3、docker 原理？（美团）（百度）

Docker 分客户端和服务端概念，Docker 服务端有一个**守护线程**以及多个工作线程概念（类似于 nginx）。Docker 客户端与 Docker 守护进程通信，**Docker 守护进程负责构建，运行和分发 Docker 容器。**工作线程负责从仓库拉取镜像。

![](docker.png)

## 4、docker 镜像是什么？（美团）（百度）

Docker 镜像是 Docker 容器的源代码，Docker 镜像用于创建容器。使用 build 命令创建镜像。

## 5、docker 容器是什么?（美团）（百度）

Docker 容器包括应用程序及其所有依赖项，作为操作系统的独立进程运行。

## 6、docker 常用命令?

1. docker pull 从仓库中拉取镜像
2. docker push 将镜像推送到远程仓库
3. docker rm 删除容器
4. docker rmi 删除镜像
5. docker images 列出所有的镜像
6. docker ps 列出所有的容器
7. docker run 运行一个容器
