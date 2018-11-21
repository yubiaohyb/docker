#### 宿主机存储方式
* volumes
* bind mounts
* tmpfs

#### 三者区别
![](https://docs.docker.com/storage/images/types-of-mounts.png)

* volumes - 存储在宿主机文件系统中一块由docker管理的区域（/var/lib/docker/volumes/），docker之外的进程不能变动。是最佳的存储方式。
* bind mounts - 存储在宿主机文件系统中的任意位置，可能会被其他进程操作。
* tmpfs - 存储于宿主机内存当中。

#### 载具类型的更多细节
volumes - 由docker创建并管理。可以通过ocker volume create命令或者在docker创建容器或服务时创建。volumes可以同时被多个容器加载，也可以没有容器加载。
但除非手动删除，否则会一直存在。使用命令 docker volume prune 进行删除。
挂载volume时，可能有名称，也可能是匿名的，如果匿名的话，docker会给它一个随机的名称方便管理。
volumes也可以使用volume驱动支持远程主机或云提供商。

bind mounts - 是docker的早期产出。相较于volumes，功能有限。使用时可以将宿主机当中的文件或文件夹挂载到容器当中。挂载的是一个宿主机绝对路径。
如果不存在，会自动创建。使用此命令应该给路径一个别名，方便管理运维。

>可以直接访问宿主机文件，所以存在一定的安全隐患
