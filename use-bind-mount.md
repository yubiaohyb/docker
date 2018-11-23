bind mount在docker的早期版本中就已存在，docker宿主机并不要求文件或目录一定存在，不存在的话，会去主动创建。
bind mount的性能非常好，但它们依赖于主机的文件系统具有可用的特定目录结构。
如果是开发新的docker应用推荐使用命名了的volume，这样可以使用docker CLI命令进行管理。

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
  * 第三个字段是可选的，是一个逗号分隔可选属性清单，稍后会作说明(ro, consistent, delegated, cached, z, and Z)

* --mount
  由多个键值对组成，中间用逗号分隔，键的顺序没有特定要求。
  * type可以是volume/bind/tmpfs。这里自然是volume。
  * source是volume的名称，匿名时可以忽略。键可以使用source或src。
  * destination指定挂载位置。键可以使用destination/target或dst。
  * readonly如果出现，则bind mount只可读。
  * volume-opt可以指定多次，由键值对组成。
  * bind-propagation设置绑定传播行为。值可以为rprivate, private, rshared, shared, rslave, slave
  * consistency设置值可以为consistent, delegated, or cached。仅适用于mac平台。
  * --mount不支持使用 z 或 Z 属性改变selinux标签
  
  ### -v与--mount的行为区别
  使用-v or --volume挂载文件或目录时，没有的话则直接在容器中创建，且创建的只会是目录；
  使用--mount挂载一个不存在的目录或文件时，则会报错。
  ```
  [vagrant@localhost /]$ docker run -d --name demo --rm  -v type=bind,source=/aa,target=/bb yubiaohyb/share-demo
ed2a6b84d22d81b1acceddcbcd969d16a5a032091ca1edcefb9af860cec9234b
[vagrant@localhost /]$ ls
bin   dev  home  lib64       media  opt   root  sbin  swapfile  tmp  vagrant
boot  etc  lib   lost+found  mnt    proc  run   srv   sys       usr  var
[vagrant@localhost /]$ docker exec -it demo /bin/bash
root@ed2a6b84d22d:/# pwd
/
root@ed2a6b84d22d:/# ls
app.jar  boot  etc   lib    log    mnt  proc  run   srv  tmp                usr
bin      dev   home  lib64  media  opt  root  sbin  sys  type=bind,source=  var
root@ed2a6b84d22d:/type=bind,source=/aa,target=/bb# exit
exit
[vagrant@localhost /]$ docker stop demo
demo
[vagrant@localhost /]$ ls
bin   dev  home  lib64       media  opt   root  sbin  swapfile  tmp  vagrant
boot  etc  lib   lost+found  mnt    proc  run   srv   sys       usr  var
  ```
  ```
  [vagrant@localhost /]$ docker run -d --name demo --rm  --mount type=bind,source=/aa,target=/bb yubiaohyb/share-demo
docker: Error response from daemon: invalid mount config for type "bind": bind source path does not exist: /aa.
See 'docker run --help'.
  ```
  
  
