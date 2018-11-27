## 配置启动docker
### 守护进程的启动
* 系统工具
```
$ sudo systemctl start docker.service
```
* 手动
```
$ dockerd

INFO[0000] +job init_networkdriver()
INFO[0000] +job serveapi(unix:///var/run/docker.sock)
INFO[0000] Listening for HTTP on unix (/var/run/docker.sock)
```

### 守护进程的配置
* json配置文件方式，也是推荐的方式
* dockerd启动携带标记参数
```
dockerd --debug \
  --tls=true \
  --tlscert=/var/docker/server.pem \
  --tlskey=/var/docker/serverkey.pem \
  --host tcp://192.168.59.3:2376
```

### 守护进程的目录
* 默认： /var/lib/docker
* 可以使用 data-root 另外指定

### 排错
[查看](https://docs.docker.com/config/daemon/#troubleshoot-the-daemon)
