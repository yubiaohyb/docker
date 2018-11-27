### 配置所有对象
#### 自定义元数据
Label提供了配置docker对象元数据的一种机制。docker对象包括：
* Images
* Containers
* Local daemons
* Volumes
* Networks
* Swarm nodes
* Swarm services

使用Label组织镜像/记录认证信息/备注容器/网络/挂载之间的关系等等。
##### Label键值对
成对存在。一个对象可以有多个Label，但key必须唯一，否则新的值会覆盖老的值。
###### 键格式推荐
键的组成可以是字母/数字/./-
* 第三方工具的编辑者应该在标签上添加倒序域名前缀（com.example.some-label）。
* 不要使用未经授权的域名
* com.docker.* , io.docker.* 以及org.dockerproject.* 由docker项目内部使用
* 开始或结尾均为单词，使用限制于小写字母。不允许出现连续的 . 或 -
* . 用来分隔字段。label中没有命名空间的key应该yong'y

#### 移除闲置对象
#### 格式化命令/日志输出
### 配置守护进程

### 配置容器
