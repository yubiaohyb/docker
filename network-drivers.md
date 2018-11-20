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
错误配置
```
[vagrant@localhost ~]$ sudo  systemctl reload docker
[vagrant@localhost ~]$ docker ls


docker: 'ls' is not a docker command.
See 'docker --help'
[vagrant@localhost ~]$
[vagrant@localhost ~]$
[vagrant@localhost ~]$ docker images
REPOSITORY             TAG                 IMAGE ID            CREATED             SIZE
yubiaohyb/centos-vim   latest              061720069b26        4 hours ago         355MB
yubiaohyb/sayhi        latest              b5f206fc59be        4 days ago          861kB
[vagrant@localhost ~]$ docker network ls
NETWORK ID          NAME                DRIVER              SCOPE
b5aa03158677        bridge              bridge              local
98674bbeb131        host                host                local
945c0b1351b7        none                null                local
[vagrant@localhost ~]$ docker ps
CONTAINER ID        IMAGE                  COMMAND             CREATED             STATUS              PORTS               NAMES
72f3cc63e3af        yubiaohyb/centos-vim   "/bin/bash"         About an hour ago   Up About an hour                        test2
736b639eb825        yubiaohyb/centos-vim   "/bin/bash"         About an hour ago   Up About an hour                        test1
[vagrant@localhost ~]$ docker network create myBridge
3143457bc95120e845a779393939661eea42a9526ba6b65695b7bd9dce323b71
[vagrant@localhost ~]$ docker network ls
NETWORK ID          NAME                DRIVER              SCOPE
b5aa03158677        bridge              bridge              local
98674bbeb131        host                host                local
3143457bc951        myBridge            bridge              local
945c0b1351b7        none                null                local
[vagrant@localhost ~]$ docker network inspect myBridge
[
    {
        "Name": "myBridge",
        "Id": "3143457bc95120e845a779393939661eea42a9526ba6b65695b7bd9dce323b71",
        "Created": "2018-11-20T07:01:15.346627148Z",
        "Scope": "local",
        "Driver": "bridge",
        "EnableIPv6": false,
        "IPAM": {
            "Driver": "default",
            "Options": {},
            "Config": [
                {
                    "Subnet": "172.19.0.0/16",
                    "Gateway": "172.19.0.1"
                }
            ]
        },
        "Internal": false,
        "Attachable": false,
        "Ingress": false,
        "ConfigFrom": {
            "Network": ""
        },
        "ConfigOnly": false,
        "Containers": {},
        "Options": {},
        "Labels": {}
    }
]
[vagrant@localhost ~]$ docker network connect  myBridge test1
[vagrant@localhost ~]$ docker network connect  myBridge test2
[vagrant@localhost ~]$ docker network inspect myBridge
[
    {
        "Name": "myBridge",
        "Id": "3143457bc95120e845a779393939661eea42a9526ba6b65695b7bd9dce323b71",
        "Created": "2018-11-20T07:01:15.346627148Z",
        "Scope": "local",
        "Driver": "bridge",
        "EnableIPv6": false,
        "IPAM": {
            "Driver": "default",
            "Options": {},
            "Config": [
                {
                    "Subnet": "172.19.0.0/16",
                    "Gateway": "172.19.0.1"
                }
            ]
        },
        "Internal": false,
        "Attachable": false,
        "Ingress": false,
        "ConfigFrom": {
            "Network": ""
        },
        "ConfigOnly": false,
        "Containers": {
            "72f3cc63e3af9cc948ef419be52b44e9328c6df2d161b7e3e571c0d2af214a41": {
                "Name": "test2",
                "EndpointID": "c49333fd4adad1dd7ca63b752e76cd40d2e386ef2862b2a7c3f78438872f08c8",
                "MacAddress": "02:42:ac:13:00:03",
                "IPv4Address": "172.19.0.3/16",
                "IPv6Address": ""
            },
            "736b639eb8257af24e2139f64f797c7d523160414a0ab7e5ffffe51a2202b919": {
                "Name": "test1",
                "EndpointID": "528fdede3499646b74870b1862d138809b30e7890beaaf903ab9459712894726",
                "MacAddress": "02:42:ac:13:00:02",
                "IPv4Address": "172.19.0.2/16",
                "IPv6Address": ""
            }
        },
        "Options": {},
        "Labels": {}
    }
]
[vagrant@localhost ~]$
```
正确配置
```
[vagrant@localhost ~]$ docker network disconnect myBridge test1
[vagrant@localhost ~]$ docker network disconnect myBridge test2
[vagrant@localhost ~]$ docker network rm myBridge
myBridge
[vagrant@localhost ~]$ docker network create --ipv6 myBridge
Error response from daemon: could not find an available, non-overlapping IPv6 address pool among the defaults to assign
to the network
[vagrant@localhost ~]$ docker network create --ipv6 myBridge --help

Usage:  docker network create [OPTIONS] NETWORK

Create a network

Options:
      --attachable           Enable manual container attachment
      --aux-address map      Auxiliary IPv4 or IPv6 addresses used by Network driver (default map[])
      --config-from string   The network from which copying the configuration
      --config-only          Create a configuration only network
  -d, --driver string        Driver to manage the Network (default "bridge")
      --gateway strings      IPv4 or IPv6 Gateway for the master subnet
      --ingress              Create swarm routing-mesh network
      --internal             Restrict external access to the network
      --ip-range strings     Allocate container ip from a sub-range
      --ipam-driver string   IP Address Management Driver (default "default")
      --ipam-opt map         Set IPAM driver specific options (default map[])
      --ipv6                 Enable IPv6 networking
      --label list           Set metadata on a network
  -o, --opt map              Set driver specific options (default map[])
      --scope string         Control the network's scope
      --subnet strings       Subnet in CIDR format that represents a network segment
[vagrant@localhost ~]$ sudo vi /etc/docker/daemon.json
[vagrant@localhost ~]$ sudo systemctl reload docker
{
        "ipv6": true,
        "fixed-cidr-v6": "2001:db8:1::/64"
}
[vagrant@localhost ~]$ docker network create --ipv6 myBridge
Error response from daemon: could not find an available, non-overlapping IPv6 address pool among the defaults to assign to the network
[vagrant@localhost ~]$
```
待解决。。。
