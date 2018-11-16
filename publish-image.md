## 镜像发布dockerhub
* ### [本地发布](#本地发布-1)
* ### [公共平台Dockerfile发布](#公共平台dockerfile发布-1)
## [镜像发布私有hub](#镜像发布私有hub-1)
### 本地发布
#### 本地登录账号
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
#### 确认镜像名称是否正确使用账号信息

#### 发布到docker hub
```
[vagrant@localhost sayhi]$ docker push yubiaohyb/sayhi:latest
The push refers to repository [docker.io/yubiaohyb/sayhi]
de4d5d34729c: Pushed
latest: digest: sha256:cf00b74257e213692c0e2e2b9a0a1c7d119d1ef731309402a75f74bbecb3a90a size: 527
[vagrant@localhost sayhi]$
```
#### 结果
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

### 公共平台Dockerfile发布

#### github新建repo，提交Dockerfile
![](https://github.com/yubiaohyb/docker/blob/master/images/publish/6167A412-EB28-492f-8CB9-E58B80AA0F46.png)
#### 创建自动构建
![](https://github.com/yubiaohyb/docker/blob/master/images/publish/9F39540F-D70F-4ff6-938D-BD02FDE438E7.png)
#### 关联github或者bitbucket账号
![](https://github.com/yubiaohyb/docker/blob/master/images/publish/1448E9AA-061B-4461-B594-3163CE7E997F.png)
#### 添加关联账号结果
![](https://github.com/yubiaohyb/docker/blob/master/images/publish/F05B1190-349A-487c-A1A5-1BB8192A5DFD.png)
#### 选择自动构建平台
![](https://github.com/yubiaohyb/docker/blob/master/images/publish/C0494121-780D-4fa9-8D18-C30B28D157FA.png)
#### 指定自动创建更新镜像的库
![](https://github.com/yubiaohyb/docker/blob/master/images/publish/7BC271EE-2767-482e-8651-CC9202E648F3.png)
#### 生成结果
![](https://github.com/yubiaohyb/docker/blob/master/images/publish/5331CF43-56C2-40d7-8419-32B504D20F75.png)
> 由于dockerhub是借助消息机制触发添加任务队列，所以相应的镜像发布时间要稍微长一些。

## 镜像发布私有hub
#### 搜索关键字 registry
![](https://github.com/yubiaohyb/docker/blob/master/images/publish/787BE444-1A87-4c49-9E06-47EC8B00E0BC.png)


