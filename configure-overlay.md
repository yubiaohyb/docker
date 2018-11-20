overlay驱动在多个docker宿主机之间创建了一个分布式网络，它处于各个宿主机私有网络的顶层。通过此驱动可以实现包括swarm服务在内的容器间进行安全通信。
整个过程是透明的。<br>
初始化swarm或者添加docker宿主机到已有swarm中，相应的宿主机上会创建2个网络：
* 一个是叫ingress的overlay网络，用于控制处理swarm服务相关的数据交换。创建swarm服务，未指定自定义overlay网络时，默认使用此网络。
* 一个是叫docker_gwbridge的bridge网络，用于连接swarm中docker宿主机。

尽管swarm服务容器群和单个容器都可以添加到overlay网络。但是两者在默认行为和相关配置上有所区别。

#### 通用配置
##### 创建overlay网络
前提：
* 防火墙配置
  * TCP端口2377用于集群管理
  * TCP和UDP端口7946用于节点通信
  * UDP端口4789用于overlay网络数据交换

* 创建overlay网络前，需要使用docker swarm init将docker宿主机初始化为swarm管理器或者使用docker swarm join加入已存在的swarm<br>（两者默认都会创建默认的ingress overlay网络，哪怕你用不到，也得这么做）

创建
```
$ docker network create -d overlay my-overlay
```
追加--attachable允许与其他dockers宿主机上的容器进行通信
```
$ docker network create -d overlay --attachable my-attachable-overlay
```
#### 加密overlay网络包
