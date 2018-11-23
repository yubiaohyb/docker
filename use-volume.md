### volume相较于bind mount的优点
* 备份/迁移简单
* 可以使用docker的命令或api接口直接管理
* Linux和Windows容器均可使用
* 允许远程存储/数据加密以及添加其他功能特性
* 允许容器预填充空volume

volume使用rprivate绑定传播，且对于volume来说传播绑定是不可配置的。

### -v与--mount的选择
起初，-v or --volume用于独立容器，--mount用于swarm服务。
Docker 17.06开始，可以使用也鼓励使用--mount，因为语义明显充足易于理解。
最大的不同点就是-v可以结合所有的选项属性一起使用，而--mount会将它们分开。
> 初学者建议使用--mount

如果需要指定volume驱动选项，则必须使用--mount。
* -v or --volume
  由三个字段组成，中间以 ： 分隔。字段顺序必须正确，可读性较差
  * 命名了的volumes第一个字段是volume的名称，且必须在宿主机上唯一；对于匿名volume则可以忽略。
  * 第二个字段是文件或目录在容器中挂载的位置
  * 第三个字段是可选的，是一个逗号分隔可选属性清单，稍后会作说明

* --mount
  由多个键值对组成，中间用逗号分隔，键的顺序没有特定要求。
  * type可以是volume/bind/tmpfs。这里自然是volume。
  * source是volume的名称，匿名时可以忽略。键可以使用source或src。
  * destination指定挂载位置。键可以使用destination/target或dst。
  * readonly如果出现，则bind mount只可读。
  * volume-opt可以指定多次，由键值对组成。
  
##### 外部CSV解析器值转义
如果volume驱动接收一个逗号分隔的清单作为可选属性，则可以使用单引号包围挂载参数，双引号包围这个清单属性
```
     --mount 'type=volume,src=<VOLUME-NAME>,dst=<CONTAINER-PATH>,volume-driver=local,volume-opt=type=nfs,volume-opt=device=<nfs-server>:<nfs-path>,"volume-opt=o=addr=<nfs-address>,vers=4,soft,timeo=180,bg,tcp,rw"'

```
#### -v 与 --mount的行为区别
相较于bind mount，-v和--mount可以使用所有的可选属性。
service使用volume时，只能使用--mount。

### volumes的创建管理
创建
```
$ docker volume create my-vol
```
罗列
```
$ docker volume ls

local               my-vol
```
查看
```
$ docker volume inspect my-vol
[
    {
        "Driver": "local",
        "Labels": {},
        "Mountpoint": "/var/lib/docker/volumes/my-vol/_data",
        "Name": "my-vol",
        "Options": {},
        "Scope": "local"
    }
]
```
移除
```
$ docker volume rm my-vol
```

### 使用volume启动容器
--mount
```
$ docker run -d \
  --name devtest \
  --mount source=myvol2,target=/app \
  nginx:latest
```
-v
```
$ docker run -d \
  --name devtest \
  -v myvol2:/app \
  nginx:latest
```
使用docker inspect devtest检查容器是否成功挂载
```
"Mounts": [
    {
        "Type": "volume",
        "Name": "myvol2",
        "Source": "/var/lib/docker/volumes/myvol2/_data",
        "Destination": "/app",
        "Driver": "local",
        "Mode": "",
        "RW": true,
        "Propagation": ""
    }
],
```
volume移除的正确顺序
```
$ docker container stop devtest

$ docker container rm devtest

$ docker volume rm myvol2
```
### 使用volume启动service
```
$ docker service create -d \
  --replicas=4 \
  --name devtest-service \
  --mount source=myvol2,target=/app \
  nginx:latest
```
docker service ps devtest-service检查服务运行
```
ID                  NAME                IMAGE               NODE                DESIRED STATE       CURRENT STATE            ERROR               PORTS
4d7oz1j85wwn        devtest-service.1   nginx:latest        moby                Running             Running 14 seconds ago
```
移除服务
```
$ docker service rm devtest-service
```
#### service语法区别
只能使用--mount

### 使用只读volume
-- mount
```
$ docker run -d \
  --name=nginxtest \
  --mount source=nginx-vol,destination=/usr/share/nginx/html,readonly \
  nginx:latest
```
-v
```
$ docker run -d \
  --name=nginxtest \
  -v nginx-vol:/usr/share/nginx/html:ro \
  nginx:latest
```
docker inspect nginxtest查看效果
```
"Mounts": [
    {
        "Type": "volume",
        "Name": "nginx-vol",
        "Source": "/var/lib/docker/volumes/nginx-vol/_data",
        "Destination": "/usr/share/nginx/html",
        "Driver": "local",
        "Mode": "",
        "RW": false,
        "Propagation": ""
    }
],
```
### 数据多机共享
* 应用程序逻辑处理
* 使用volume将底层数据访问抽象出来

### 使用volume驱动
创建volume时可以指定驱动类型，以vieux/sshfs为例：
插件预装
```
$ docker plugin install --grant-all-permissions vieux/sshfs
```
直接创建
```
$ docker volume create --driver vieux/sshfs \
  -o sshcmd=test@node2:/home/test \
  -o password=testpassword \
  sshvolume
```
启动容器创建
```
$ docker run -d \
  --name sshfs-container \
  --volume-driver vieux/sshfs \
  --mount src=sshvolume,target=/app,volume-opt=sshcmd=test@node2:/home/test,volume-opt=password=testpassword \
  nginx:latest
```
如果驱动需要传递附加属性，则必须使用--mount。

### 备份、重载或迁移volume数据
volume适用于数据的备份、重载和迁移，因此可以启动一个新的容器使用 --volumes-from 挂载相应的volume。


### 移除volume
容器删除后，volume数据仍然存在于宿主系统当中。
volume大概分为两种类型：
* 命名volume
* 匿名volume

对于匿名volume，在使用volume启动容器时通过添加 --rm 参数，docker引擎会将容器实例连同匿名volume一起删除。
```
[vagrant@localhost ~]$ docker run -d --name demo --rm -v /testdir -v namedvolume:/namedir yubiaohyb/share-demo
```
删除所有闲置volume
```
[vagrant@localhost ~]$ docker volume ls
DRIVER              VOLUME NAME
local               namedvolume
[vagrant@localhost ~]$ docker volume prune
WARNING! This will remove all local volumes not used by at least one container.
Are you sure you want to continue? [y/N] y
Deleted Volumes:
namedvolume

Total reclaimed space: 0B
[vagrant@localhost ~]$ docker volume ls
DRIVER              VOLUME NAME
[vagrant@localhost ~]$
```


