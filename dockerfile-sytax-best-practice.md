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
