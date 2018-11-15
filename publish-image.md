### 本地登录账号
```
[vagrant@localhost sayhi]$ docker login
Login with your Docker ID to push and pull images from Docker Hub. If you don't have a Docker ID, head over to https://hub.docker.com to create one.
Username: yubiaohyb
Password:
WARNING! Your password will be stored unencrypted in /home/vagrant/.docker/config.json.
Configure a credential helper to remove this warning. See
https://docs.docker.com/engine/reference/commandline/login/#credentials-store

Login Succeeded
```
### 确认镜像名称是否正确使用账号信息

### 发布到docker hub
```
[vagrant@localhost sayhi]$ docker push yubiaohyb/sayhi:latest
The push refers to repository [docker.io/yubiaohyb/sayhi]
de4d5d34729c: Pushed
latest: digest: sha256:cf00b74257e213692c0e2e2b9a0a1c7d119d1ef731309402a75f74bbecb3a90a size: 527
[vagrant@localhost sayhi]$
```
结果如下：
![](https://github.com/yubiaohyb/docker/blob/master/images/publish/CFCBEC92-BAFB-4f74-A978-8105E6621F6E.png)
---
遇到的问题：
```
[vagrant@localhost sayhi]$ docker push yubiaohyb/sayhi
The push refers to repository [docker.io/yubiaohyb/sayhi]
de4d5d34729c: Preparing
denied: requested access to the resource is denied
```
解决：
1-检查镜像命名，重新生成镜像文件；
2-检查是否登陆，重新登陆
