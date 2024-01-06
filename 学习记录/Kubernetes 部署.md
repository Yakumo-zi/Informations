# Kubernetes 部署

Kubernetes是一个开源的容器编排平台，简称K8s。

## K8s基本概念

* Pod：实例，一个Pod里面可以跑很多个容器
* Service：逻辑上的服务，可以认为是业务上某个服务的直接映射
* Deployment：管理Pod的东西

Pod和Service的关系：

如果一个Web应用部署了三个实例，那么一个Web Service对应了三个Pod。

## 使用K8s部署Web服务器

