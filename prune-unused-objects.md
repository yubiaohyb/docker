### 删除镜像
删除没有打tag的闲置镜像
```
$ docker image prune

WARNING! This will remove all dangling images.
Are you sure you want to continue? [y/N] y
```
删除所有闲置镜像
```
$ docker image prune -a

WARNING! This will remove all images without at least one container associated to them.
Are you sure you want to continue? [y/N] y
```
使用 -f 或 --force 可以绕过提示。

使用 --filter 可以对过滤要删除的镜像。
```
$ docker image prune -a --filter "until=24h"
```

### 删除容器
手动删除容器
```
$ docker container prune

WARNING! This will remove all stopped containers.
Are you sure you want to continue? [y/N] y
```
使用 -f 或 --force 可以绕过提示。
使用 --filter 可以对过滤要删除的容器。
```
$ docker container prune --filter "until=24h"
```
### 删除挂载
```
$ docker volume prune

WARNING! This will remove all volumes not used by at least one container.
Are you sure you want to continue? [y/N] y
```
使用 -f 或 --force 可以绕过提示。
使用 --filter 可以对过滤要删除的容器。
```
$ docker volume prune --filter "label!=keep"
```
### 删除网络
```
$ docker network prune

WARNING! This will remove all networks not used by at least one container.
Are you sure you want to continue? [y/N] y
```
使用 -f 或 --force 可以绕过提示。
使用 --filter 可以对过滤要删除的容器。
```
$ docker network prune --filter "until=24h"
```
### 删除一切
```
$ docker system prune

WARNING! This will remove:
        - all stopped containers
        - all networks not used by at least one container
        - all dangling images
        - all build cache
Are you sure you want to continue? [y/N] y
```
使用 -f 或 --force 可以绕过提示。

