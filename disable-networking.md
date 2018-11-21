### 关闭容器网络
完全关闭容器网络可以在创建容器时携带参数 --network none 
```
$ docker run --rm -dit \
  --network none \
  --name no-net-alpine \
  alpine:latest \
  ash
```
#### 检验
使用 ip a 会发现 eth0 没有创建
```
$ docker exec no-net-alpine ip link show

1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN qlen 1
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
2: tunl0@NONE: <NOARP> mtu 1480 qdisc noop state DOWN qlen 1
    link/ipip 0.0.0.0 brd 0.0.0.0
3: ip6tnl0@NONE: <NOARP> mtu 1452 qdisc noop state DOWN qlen 1
    link/tunnel6 00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00 brd 00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00
```
也可以查看路由表，此时没有路由信息输出
```
$ docker exec no-net-alpine ip route
```
创建容器携带参数 --rm，容器退出后会自动删除容器实例
