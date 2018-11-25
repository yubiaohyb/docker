## tmpfs的使用
* [缺点](#缺点)
* [--tmpfs与--mount的选择](#--tmpfs与--mount的选择)
* [--tmpfs与--mount的行为区别](#--tmpfs与--mount的行为区别)
* [tmpfs的使用](#tmpfs的使用)
* [设置tmpfs可选项](#设置tmpfs可选项)
---
### 缺点
* 无法容器间共享数据
* 仅限于linux系统可用

### --tmpfs与--mount的选择
起初，-tmpfs用于独立容器，--mount用于swarm服务。
Docker 17.06开始，可以使用也鼓励使用--mount，因为语义明显充足易于理解。
最大的不同点就是-tmpfs不支持配置选项。
* --tmpfs - 仅限于独立容器使用，且不可指定配置选项
* --mount
  由多个键值对组成，中间用逗号分隔，键的顺序没有特定要求。
  * type可以是volume/bind/tmpfs。这里自然是volume。
  * destination指定挂载位置。键可以使用destination/target或dst。
  * 可以指定tmpfs-type和tmpfs-mode可选项属性。
  
### --tmpfs与--mount的行为区别
--tmpfs不支持可选属性的配置。
--tmpfs不能用于swarm服务。

### tmpfs的使用
--tmpfs
```
huangyubiaodeMacBook-Pro:share-demo huangyubiao$ docker run -d --name demo --rm -p 80:8080 -tmpfs /test  yubiaohyb/share-demo:latest
invalid argument "pfs" for "-m, --memory" flag: invalid size: 'pfs'
See 'docker run --help'.
huangyubiaodeMacBook-Pro:share-demo huangyubiao$ docker run -d --name demo --rm -p 80:8080 --tmpfs /test  yubiaohyb/share-demo:latest
1aa715663c1bc98ef2253f80941a6daa993050ae273ccf14ec66e436bb5a3e7e
```
--mount
```
$ docker run -d \
  -it \
  --name tmptest \
  --mount type=tmpfs,destination=/app \
  nginx:latest
```
查看
```
huangyubiaodeMacBook-Pro:share-demo huangyubiao$ docker inspect demo
...
  "Tmpfs": {
      "/test": ""
  },
...
huangyubiaodeMacBook-Pro:share-demo huangyubiao$ docker exec -it demo /bin/bash
root@1aa715663c1b:/# ls
bin  boot  dev  etc  home  lib  lib64  log  media  mnt  opt  proc  root  run  sbin  share-demo.jar  srv  sys  test  tmp  usr  var
root@1aa715663c1b:/# 
```
删除
```
$ docker container stop tmptest
$ docker container rm tmptest
```

### 设置tmpfs可选项
tmpfs支持两个配置可选项，但仅限于 --mount 使用。
* tmpfs-size - 设置tmpfs挂载的字节大小。默认没有限制。
* tmpfs-mode - 设置tmpfs读写属性。默认值为1777或全局可写。
```
docker run -d \
  -it \
  --name tmptest \
  --mount type=tmpfs,destination=/app,tmpfs-mode=1770 \
  nginx:latest
```


