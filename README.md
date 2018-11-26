### 学习地址
[入门](https://docs.docker.com/get-started/)

### 学习路径
* [安装docker](https://github.com/yubiaohyb/docker/blob/master/install-docker.md)
* [网络配置](https://github.com/yubiaohyb/docker/blob/master/configure-network.md)
* [应用数据管理](https://github.com/yubiaohyb/docker/blob/master/manage-app-data.md)

---
docker运行实例镜像
```
[vagrant@localhost ~]$ sudo docker run hello-world
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
d1725b59e92d: Pull complete
Digest: sha256:0add3ace90ecb4adbf7777e9aacf18357296e799f81cabc9fde470971e499788
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/
```

docker运行实例镜像
```
[vagrant@localhost ~]$ sudo docker run -it ubuntu bash
Unable to find image 'ubuntu:latest' locally
latest: Pulling from library/ubuntu
473ede7ed136: Pull complete
c46b5fa4d940: Pull complete
93ae3df89c92: Pull complete
6b1eed27cade: Pull complete
Digest: sha256:29934af957c53004d7fb6340139880d23fb1952505a15d69a03af0d1418878cb
Status: Downloaded newer image for ubuntu:latest
root@e92bbf2bf6e9:/# ls
bin  boot  dev  etc  home  lib  lib64  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
root@e92bbf2bf6e9:/#
root@e92bbf2bf6e9:/#
root@e92bbf2bf6e9:/# getcpuinfo
bash: getcpuinfo: command not found
root@e92bbf2bf6e9:/# getsysinfo
bash: getsysinfo: command not found
root@e92bbf2bf6e9:/# uname -a
Linux e92bbf2bf6e9 3.10.0-862.14.4.el7.x86_64 #1 SMP Wed Sep 26 15:12:11 UTC 2018 x86_64 x86_64 x86_64 GNU/Linux
root@e92bbf2bf6e9:/# lsb_release -a
bash: lsb_release: command not found
root@e92bbf2bf6e9:/# cat /etc/issue
Ubuntu 18.04.1 LTS \n \l

root@e92bbf2bf6e9:/#
```
docker的卸载
```
1/卸载程序包
sudo yum remove docker-ce
2/删除相关文件
sudo rm -rf /var/lib/docker
```
```
[vagrant@localhost ~]$ docker-machine version
-bash: docker-machine: command not found
```
解决办法<br>
https://github.com/docker/machine/releases<br>
```
curl -L https://github.com/docker/machine/releases/download/v0.16.0/docker-machine-`uname -s`-`uname -m` >/tmp/docker-machine &&
    chmod +x /tmp/docker-machine &&
    sudo cp /tmp/docker-machine /usr/local/bin/docker-machine

[vagrant@localhost ~]$ docker-machine -v
docker-machine version 0.16.0, build 702c267f
[vagrant@localhost ~]$
```
查看服务器上所有镜像
```
[vagrant@localhost ~]$ sudo docker image ls

REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
hello-world         latest              4ab4c602aa5e        2 months ago        1.84kB
```
docker获取镜像的三种方式：
1-通过dockerfile构建；
2-通过registry拉取：
```
[vagrant@localhost ~]$ sudo docker pull ubuntu:14.04
14.04: Pulling from library/ubuntu
027274c8e111: Pull complete
d3f9339a1359: Pull complete
872f75707cf4: Pull complete
dd5eed9f50d5: Pull complete
Digest: sha256:e6e808ab8c62f1d9181817aea804ae4ba0897b8bd3661d36dbc329b5851b5637
Status: Downloaded newer image for ubuntu:14.04
[vagrant@localhost ~]$
```
添加用户到docker分组下
```
[vagrant@localhost ~]$ docker image ls

Got permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Get http://%2Fvar%2Frun%2Fdocker.sock/v1.39/images/json: dial unix /var/run/docker.sock: connect: permission denied
[vagrant@localhost ~]$
[vagrant@localhost ~]$
[vagrant@localhost ~]$ docker image ls
Got permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Get http://%2Fvar%2Frun%2Fdocker.sock/v1.39/images/json: dial unix /var/run/docker.sock: connect: permission denied
[vagrant@localhost ~]$ sudo groupadd docker
groupadd: group 'docker' already exists
[vagrant@localhost ~]$ sudo gpasswd -a vagrant docker
Adding user vagrant to group docker
[vagrant@localhost ~]$ docker image ls
Got permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Get http://%2Fvar%2Frun%2Fdocker.sock/v1.39/images/json: dial unix /var/run/docker.sock: connect: permission denied
[vagrant@localhost ~]$
[vagrant@localhost ~]$ sudo service docker restart
Redirecting to /bin/systemctl restart docker.service
[vagrant@localhost ~]$ docker image ls
Got permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Get http://%2Fvar%2Frun%2Fdocker.sock/v1.39/images/json: dial unix /var/run/docker.sock: connect: permission denied
[vagrant@localhost ~]$ exit
```
自定义基本镜像
```
[vagrant@localhost sayhi]$ cat sayhi.c
#include<stdio.h>
int main(){
        printf("Hi!\n");
}
[vagrant@localhost sayhi]$
[vagrant@localhost sayhi]$ gcc -static sayhi.c -o sayhi
[vagrant@localhost sayhi]$ ls
sayhi  sayhi.c
[vagrant@localhost sayhi]$ ./sayhi
Hi!
[vagrant@localhost sayhi]$ cat Dockerfile
FROM scratch
ADD sayhi /
CMD ["/sayhi"]
[vagrant@localhost sayhi]$
[vagrant@localhost sayhi]$ docker build -t yubiaohyb/sayhi .
Sending build context to Docker daemon  864.8kB
Step 1/3 : FROM scratch
 --->
Step 2/3 : ADD sayhi /
 ---> 1a380afb9d12
Step 3/3 : CMD ["/sayhi"]
 ---> Running in 8a31a66738e4
Removing intermediate container 8a31a66738e4
 ---> 2b84f6b4e970
Successfully built 2b84f6b4e970
Successfully tagged yubiaohyb/sayhi:latest
[vagrant@localhost sayhi]$ docker image ls

REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
yubiaohyb/sayhi     latest              2b84f6b4e970        3 minutes ago       861kB
ubuntu              14.04               f216cfb59484        3 weeks ago         188MB
hello-world         latest              4ab4c602aa5e        2 months ago        1.84kB
[vagrant@localhost sayhi]$ docker run yubiaohyb/sayhi
Hi!
[vagrant@localhost sayhi]$ ls -lh
total 852K
-rw-rw-r--. 1 vagrant vagrant   40 Nov 14 11:27 Dockerfile
-rwxrwxr-x. 1 vagrant vagrant 841K Nov 14 11:25 sayhi
-rw-rw-r--. 1 vagrant vagrant   50 Nov 14 11:08 sayhi.c
[vagrant@localhost sayhi]$ docker history 2b84f6b4e970
IMAGE               CREATED             CREATED BY                                      SIZE                COMMENT
2b84f6b4e970        12 minutes ago      /bin/sh -c #(nop)  CMD ["/sayhi"]               0B
1a380afb9d12        12 minutes ago      /bin/sh -c #(nop) ADD file:ed2d8976b0c808c2b…   861kB
[vagrant@localhost sayhi]$
[vagrant@localhost sayhi]$ docker run yubiaohyb/sayhi
Hi!
[vagrant@localhost sayhi]$
```
gcc环境安装
```
yum groupinstall "Development Tools"
yum install -y glibc-static
```
查看yum已安装列表
```
[vagrant@localhost sayhi]$ yum list installed | grep gcc
gcc.x86_64                           4.8.5-28.el7_5.1          @updates
gcc-c++.x86_64                       4.8.5-28.el7_5.1          @updates
gcc-gfortran.x86_64                  4.8.5-28.el7_5.1          @updates
libgcc.x86_64                        4.8.5-28.el7_5.1          @koji-override-1
[vagrant@localhost sayhi]$
```
查看容器
```
[vagrant@localhost sayhi]$ docker container ls
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
[vagrant@localhost sayhi]$ docker container  ls -a
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS                      PORTS               NAMES
de1b83225feb        yubiaohyb/sayhi     "/sayhi"            18 minutes ago      Exited (4) 18 minutes ago                       affectionate_archimedes
9cd71337bed6        hello-world         "/hello"            2 hours ago         Exited (0) 2 hours ago                          relaxed_blackburn
[vagrant@localhost sayhi]$
```
交互式运行容器
```
[vagrant@localhost sayhi]$ docker run ubuntu
[vagrant@localhost sayhi]$ docker container ls
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
[vagrant@localhost sayhi]$ docker run -it ubuntu
root@788d2b733964:/# pwd
/
root@788d2b733964:/# ls
bin  boot  dev  etc  home  lib  lib64  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
root@788d2b733964:/#
root@788d2b733964:/#
root@788d2b733964:/#
root@788d2b733964:/# touch test.txt
root@788d2b733964:/# cat test.txt
root@788d2b733964:/# exist
bash: exist: command not found
root@788d2b733964:/# exit
exit
[vagrant@localhost sayhi]$ docker container ls
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
[vagrant@localhost sayhi]$
```
