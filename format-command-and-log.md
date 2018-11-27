### 格式化命令与日志输出
docker使用go模板操作某些命令或log驱动的输出格式。<br>
下面例子中都使用了docker inspect来操作模板输出，实际上docker提供了许多操作元素的功能集合，其他许多命令也都支持--format的使用。<br>
将参数列表使用指定符号连接起来生成一个字符串
```
docker inspect --format '{{join .Args " , "}}' container
```
将字符全部转小写
```
docker inspect --format "{{lower .Name}}" container
```
将字符串使用指定符号分割为字符串列表
```
docker inspect --format '{{split .Image ":"}}'
```
将字符串的第一个字母大写
```
docker inspect --format "{{title .Name}}" container
```
将字符串转为全部大写
```
docker inspect --format "{{upper .Name}}" container
```
换行打印
```
docker inspect --format='{{range .NetworkSettings.Networks}}{{println .IPAddress}}{{end}}' container
```
