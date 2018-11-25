## 容器数据存储
* [镜像与分层](#镜像与分层)
* [容器与分层](#容器与分层)
* [硬盘容器大小](#硬盘容器大小)
* [copy-on-write(CoW)策略](#copy-on-writecow策略)
---
了解镜像的构建/存储，以及容器对镜像的使用，有助于我们高效运用存储驱动。由此我们可以在应用存储数据时自主选择最佳方案，避免进入一些误区。
借助容器驱动，我们可以在容器的可写层写入数据，当容器实例被删除时相应数据也不会保留，当然读写的速度相对较慢。
如果需要可以使用--mount挂载外部存储，提升性能。

### 镜像与分层
docker镜像由一系列的分层组成。每个分层代表着镜像的dockfile中的一个指令。除了最后一个封层，每个分层都是只读的。
每个分层相较于之前分层，都只是区别性的一组集合。每个分层都是堆叠起来的。当你创建了一个新的镜像，那也就是在底层镜像的基础之上添加了一个新的可写层。
这层我们通常称之为容器层。所有对运行容器的写操作，都会应用在这个轻量的可写层之上。
而存储驱动则会用来负责各个分层之间的通信。由于存储驱动的可选性丰富，因此不同类型也各有千秋。

### 容器与分层
容器和镜像的主要区别就在于顶部可写层。对容器的所有写操作实际都是在可写层存储数据。当容器被删除，可写层也就跟着被删除了，但是底层的镜像文件依然存在，且不会发生变化。
![](https://docs.docker.com/storage/storagedriver/images/sharing-layers.jpg)

因为每个容器都有自己的可写容器层，所有的改变也都存储在容器层，因此多个容器可以共享相同的底层镜像。
> 如果时多个容器需要数据，可以使用docker的volume挂载进容器中。

docker使用存储驱动管理镜像分层和可写容器分层的内容。虽然存储驱动的实现不同，但是它们都采用堆叠镜像分层和copy-on-write (CoW) 策略。

### 硬盘容器大小
查看运行容器的准确大小，可以使用 docker ps -s 命令。
这里会有两个相关参数：
* size - 每个容器的可写层实际占用硬盘亮
* virtual size - 只读镜像分层和实际可写分层合计占用的硬盘量

理想的话，多个来自相同镜像的容器所占用的空间大小是多个容器的可写层容器大小与一个只读镜像层之和。
这还不考虑以下情况：
* 日志
* 外部挂载
* 外部配置
* 外部内存
* 测试检测点

### copy-on-write(CoW)策略
写前拷贝是文件共享拷贝的效率最大化的一个策略。
当容器需要访问一个底层文件时，则直接去访问底层已存在的文件。而当第一次需要去写一个文件的时候，则会将文件拷贝到可写层，然后对这份拷贝进行修改。
这样做，最小化了输入输出和后续分层的大小。

#### 共享轻量化镜像
关于docker history的一点解释
```
$ docker history dbf995fc07ff

IMAGE               CREATED             CREATED BY                                      SIZE                COMMENT
dbf995fc07ff        3 minutes ago       /bin/sh -c #(nop)  CMD ["/bin/sh" "-c" "/a...   0B                  
bd09118bcef6        5 minutes ago       /bin/sh -c #(nop) COPY dir:35a7eb158c1504e...   100B                
31005225a745        3 months ago        /bin/sh -c #(nop)  CMD ["/bin/bash"]            0B                  
<missing>           3 months ago        /bin/sh -c mkdir -p /run/systemd && echo '...   7B                  
<missing>           3 months ago        /bin/sh -c sed -i 's/^#\s*\(deb.*universe\...   2.78kB              
<missing>           3 months ago        /bin/sh -c rm -rf /var/lib/apt/lists/*          0B                  
<missing>           3 months ago        /bin/sh -c set -xe   && echo '#!/bin/sh' >...   745B                
<missing>           3 months ago        /bin/sh -c #(nop) ADD file:eef57983bd66e3a...   103MB 
```
<missing>意味着相应的底层镜像是在其他系统中构建的，本地没有。
  
#### 拷贝使容器更加高效
copy-on-write的执行，不同存储驱动的执行情况不同。
