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
#### 开启容器外部请求转发
默认连接默认桥网络的容器的请求无法被转发的外面，需要另外配置<br>
1 - 配置内核允许IP转发
```
$ sysctl net.ipv4.conf.all.forwarding=1
```
2 - 重置路由表转发策略
```
$ sudo iptables -P FORWARD ACCEPT
```
由于命令是临时性的，所以最好加入到启动脚本当中去。

#### 默认桥的使用
由于默认桥被认为有缺陷，所以不推荐使用。

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
