docker的网络子系统采用了插件化设计，使用驱动可以进行设置。默认提供了几款驱动，以提供核心的的网络功能。
另外，在docker ee中借助UCP提供了两个特性：
* HTTP routing mesh - 允许多个服务共享ip和端口，结合主机名和端口进行路由
* Session stickiness - HTTP设置头信息，维持会话状态

#### 默认驱动分类
type|desc
---|---
bridge|默认网络驱动，常用于需要通信的独立容器。
host|移除独立容器与docker宿主机之间的网络隔离，直接使用宿主机网络。
overlay|连接多个docker守护进程，方便swarm服务通信。也可用于swarm与独立容器或两个不同docker守护进程的独立容器之间。避免了进行操作系统级的路由。
macvlan|为容器分配mac地址，使之虚拟为网络上的一台物理设置。docker守护进程会根据mac地址进行路由。是解决历史程序直连网络的最佳选择，优于host。
none|关闭容器所有网络，通常配合自定义驱动使用。swarm服务无法使用此选项。
Network plugins|安装使用第三方网络插件，这些插件可以从docker store或第三方渠道获取。

#### 网络驱动总结
* bridge适用于一台宿主机上的多台容器相互通信
* host适用于宿主机和容器网络不需要隔离，而其他的方面又需要隔离的情况
* overlay适用于不同宿主机上的容器通信或者swarm服务中协调运行的多个应用
* macvlan适用于VM设置迁移或者需要像直连网络的物理设备的场景
* Network pluginsk可以实现docker与特定的网络栈集成

#### 具体配置
* [配置桥接网络](https://github.com/yubiaohyb/docker/blob/master/configure-bridge.md)
* [配置overlay网络](https://github.com/yubiaohyb/docker/blob/master/configure-overlay.md)
* 配置host网络
* 配置MACvlan网络
* 关闭容器网络
* 网络指南
* 守护进程和容器配置
* 历史遗留


