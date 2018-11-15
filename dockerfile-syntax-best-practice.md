[Dockerfile reference](https://docs.docker.com/engine/reference/builder/)

### 制作base image
```
FROM scratch
FROM centos
FROM ubuntu:14.04
```
> 尽量使用官方image作为base image

### 提供元数据
```
LABEL version="1.0"
```
> metadata不可少

### 运行脚本
```
RUN yum update && yum install -y vim\
    python-dev
```
> 为避免无用分层，可以使用 && 合并多条命令；为了美观，可以使用 \ 对较长的RUN命令进行换行

### 设置工作目录
```
WORKDIR /test # 进入根目录下test子目录，如果没有则创建
WORKDIR demo  # 进入当前目录下demo子目录
```
> 使用WORKDIR，不要使用RUN cd；尽量使用绝对路径

### 复制拷贝
```
ADD hello /
ADD a.txt a/
ADD b.tar.gz /test

COPY a.txt /
```
