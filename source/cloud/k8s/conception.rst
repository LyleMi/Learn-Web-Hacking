k8s概念
========================================
Kubernetes 在希腊语意为“舵手”或“驾驶员”，和 Docker 对应，常简称为K8s。Kubernetes 由 Google 的 Borg 演化而来，是用于自动部署、扩展和管理容器的开源系统。

组成
----------------------------------------
Kubernetes 由控制面 (Master) 与数据面 (Worker Node) 组成。
Master 的核心组件：

- API Server
- Controller-Mananger
- Scheduler
- etcd

Worker Node 则由以下节点组成：

- Kubelet
- Kube-Proxy
- 容器运行时

核心设计
----------------------------------------

Pod
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Pod 是 Kubernetes 的基本调度单元，一个 Pod 一般包含一个或多个容器。
Kubernetes 中的每个 Pod 都被分配一个集群内唯一的IP地址，使得应用程序可以使用同一端口。
Pod 可以定义一个卷，例如本地磁盘目录或网络磁盘，并将其暴露在pod中的一个容器之中。
Pod 可以通过 Kubernetes API 手动管理，也可以委托给控制器来实现自动管理。

Service
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Service是为一组具有相同功能的容器应用提供一个统一的入口地址，本质是一组协同工作的Pod。
