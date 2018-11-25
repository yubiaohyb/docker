### 缺点
* 无法容器间共享数据
* 仅限于linux系统可用

### -tmpfs与--mount的选择
起初，-tmpfs用于独立容器，--mount用于swarm服务。
Docker 17.06开始，可以使用也鼓励使用--mount，因为语义明显充足易于理解。
最大的不同点就是-tmpfs不支持配置选项。
