* 默认桥校验
  * 启动配置
  * 连通性测试
  * 验证结果
* 自建桥校验
  * 启动配置
  * 连通性测试
  * 验证结果

### 默认桥校验
#### 启动配置
容器1启动：
```
[vagrant@localhost ~]$ docker run -it --name=test1 yubiaohyb/centos-vim /bin/bash
```
容器2启动：
```
[vagrant@localhost ~]$ docker run -it --name=test2 yubiaohyb/centos-vim /bin/bash
```
#### 连通性测试
宿主查看默认桥信息：
```
[vagrant@localhost ~]$ docker network ls
NETWORK ID          NAME                DRIVER              SCOPE
b5aa03158677        bridge              bridge              local
98674bbeb131        host                host                local
945c0b1351b7        none                null                local
[vagrant@localhost ~]$ docker network inspect b5aa03158677
[
    {
        "Name": "bridge",
        "Id": "b5aa03158677332c81f1a44c8899a8305001331a29c319a102dff9ff01dba770",
        "Created": "2018-11-20T05:18:59.710306423Z",
        "Scope": "local",
        "Driver": "bridge",
        "EnableIPv6": false,
        "IPAM": {
            "Driver": "default",
            "Options": null,
            "Config": [
                {
                    "Subnet": "172.17.0.0/16",
                    "Gateway": "172.17.0.1"
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
            "181630c69783ddae8b65a23106499c1233a080c97c5464088c31f9ed4c978b65": {
                "Name": "test1",
                "EndpointID": "bcb187537aeffb84d3ad7c435c35c266da5de1b70b338623e3681d2732ee86f2",
                "MacAddress": "02:42:ac:11:00:02",
                "IPv4Address": "172.17.0.2/16",
                "IPv6Address": ""
            },
            "85bea04d4faae893e157c6b2b614c2faef75ade6a530f5e7f136909c0949e1a2": {
                "Name": "test2",
                "EndpointID": "2259d5a9679f3ee9e7a9aa86b2d985c4395ab5149a28bc667ab09790dacaefe8",
                "MacAddress": "02:42:ac:11:00:03",
                "IPv4Address": "172.17.0.3/16",
                "IPv6Address": ""
            }
        },
        "Options": {
            "com.docker.network.bridge.default_bridge": "true",
            "com.docker.network.bridge.enable_icc": "true",
            "com.docker.network.bridge.enable_ip_masquerade": "true",
            "com.docker.network.bridge.host_binding_ipv4": "0.0.0.0",
            "com.docker.network.bridge.name": "docker0",
            "com.docker.network.driver.mtu": "1500"
        },
        "Labels": {}
    }
]
```
宿主：
```
[vagrant@localhost ~]$ ping 172.17.0.2
PING 172.17.0.2 (172.17.0.2) 56(84) bytes of data.
64 bytes from 172.17.0.2: icmp_seq=1 ttl=64 time=0.111 ms
64 bytes from 172.17.0.2: icmp_seq=2 ttl=64 time=0.097 ms

--- 172.17.0.2 ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1000ms
rtt min/avg/max/mdev = 0.097/0.104/0.111/0.007 ms
[vagrant@localhost ~]$ ping 172.17.0.3
PING 172.17.0.3 (172.17.0.3) 56(84) bytes of data.
64 bytes from 172.17.0.3: icmp_seq=1 ttl=64 time=0.158 ms
64 bytes from 172.17.0.3: icmp_seq=2 ttl=64 time=0.086 ms
64 bytes from 172.17.0.3: icmp_seq=3 ttl=64 time=0.095 ms

--- 172.17.0.3 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2001ms
rtt min/avg/max/mdev = 0.086/0.113/0.158/0.032 ms
[vagrant@localhost ~]$
```
容器1：
```
[root@181630c69783 /]# ping 172.17.0.1
PING 172.17.0.1 (172.17.0.1) 56(84) bytes of data.
64 bytes from 172.17.0.1: icmp_seq=1 ttl=64 time=0.174 ms
64 bytes from 172.17.0.1: icmp_seq=2 ttl=64 time=0.106 ms
64 bytes from 172.17.0.1: icmp_seq=3 ttl=64 time=0.099 ms
^C
--- 172.17.0.1 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2000ms
rtt min/avg/max/mdev = 0.099/0.126/0.174/0.035 ms
[root@181630c69783 /]# ping 172.17.0.2
PING 172.17.0.2 (172.17.0.2) 56(84) bytes of data.
64 bytes from 172.17.0.2: icmp_seq=1 ttl=64 time=0.073 ms
64 bytes from 172.17.0.2: icmp_seq=2 ttl=64 time=0.081 ms
64 bytes from 172.17.0.2: icmp_seq=3 ttl=64 time=0.072 ms
64 bytes from 172.17.0.2: icmp_seq=4 ttl=64 time=0.080 ms
^C
--- 172.17.0.2 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3003ms
rtt min/avg/max/mdev = 0.072/0.076/0.081/0.009 ms
[root@181630c69783 /]#
```
容器2：
```
[root@85bea04d4faa /]# ping 172.17.0.2
PING 172.17.0.2 (172.17.0.2) 56(84) bytes of data.
64 bytes from 172.17.0.2: icmp_seq=1 ttl=64 time=0.180 ms
64 bytes from 172.17.0.2: icmp_seq=2 ttl=64 time=0.125 ms
64 bytes from 172.17.0.2: icmp_seq=3 ttl=64 time=0.126 ms
...
^C
--- 172.17.0.2 ping statistics ---
16 packets transmitted, 16 received, 0% packet loss, time 15017ms
rtt min/avg/max/mdev = 0.117/0.127/0.180/0.017 ms
```
#### 验证结果
容器2：
```
[root@85bea04d4faa /]# ping test1
ping: test1: Name or service not known
[root@85bea04d4faa /]#
```
