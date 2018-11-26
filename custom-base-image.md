## 自定义基本镜像
gcc环境预装
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
实际操作流程
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
