docker的网络子系统采用了插件化设计，使用驱动可以进行设置。默认提供了几款驱动，以提供核心的的网络功能。
另外，在docker ee中借助UCP提供了两个特性：
* HTTP routing mesh - 允许多个服务共享ip和端口，结合主机名和端口进行路由
* Session stickiness - HTTP设置头信息，维持会话状态

#### 默认驱动分类
type|desc
---|---
[bridge](https://github.com/yubiaohyb/docker/blob/master/bridge-verify.md)|默认网络驱动，常用于需要通信的独立容器。
host|移除独立容器与docker宿主机之间的网络隔离，直接使用宿主机网络。
overlay|连接多个docker守护进程，方便swarm服务通信。也可用于swarm与独立容器或两个不同docker守护进程的独立容器之间。避免了进行操作系统级的路由。
macvlan|为容器分配mac地址，使之虚拟为网络上的一台物理设置。docker守护进程会根据mac地址进行路由。是解决历史程序直连网络的最佳选择，优于host。
none|关闭容器所有网络，通常配合自定义驱动使用。swarm服务无法使用此选项。
Network plugins|安装使用第三方网络插件，这些插件可以从docker store或第三方渠道获取。

#### bridge网络的使用
从网络的角度来看，bridge是一台链路层设备，负责网络帧的转发。<br>
从docker的角度来看，bridge则像一条本地通信规则，自动告知系统，哪些docker可以相互通信，哪些则不可以。<br>
bridge网络适用于本地docker，如果涉及跨机通信，则需要进行系统级配置或使用overlay。<br>
启动docker守护进程，默认会自动创建bridge。当然也可选择自定义bridge,相应的优先级也要高于默认创建的。

#### 用户自定义bridge和默认bridge的区别
* 可以得到更好的隔离和协调的效果
* 提供了容器间的自动DNS解析（使用name）
* 容器间可以在运行时选择连接或断开
* 更加能够满足不同应用组的网络需求
* 唯一特殊：默认bridge可以共享一些环境变量（但是也是有其他的替代方案的）

#### 自建桥生命周期
创建
```
$ docker network create my-net
```
删除
```
$ docker network rm my-net
```
连接
```
$ docker create --name my-nginx \
  --network my-net \
  --publish 8080:80 \
  nginx:latest
```
```
$ docker network connect my-net my-nginx
```
断连
```
$ docker network disconnect my-net my-nginx
```
#### IPv6的使用
##### 启用ipv6
目前只支持运行在linux系统上的docker守护进程<br>
编辑/etc/docker/daemon.json
```
{
  "ipv6": true
}
```
重载配置文件
```
$ systemctl reload docker
```
