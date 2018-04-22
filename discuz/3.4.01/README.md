# discuz:3.4.01

利用 `php 7.x` 部署 `discuz` 论坛程序

# 注意事项

1. `discuz` 默认使用 `mysqli` 扩展访问 `Mysql`。该扩展并没有包含在php7.x中，所以一定要自行编译该扩展。（具体实现参考Dockerfile）

2. Mysql 5.7安装之后，无法远程访问，需要根据根据方式进行设置：

```bash
# 利用 docker exec -it <container id> mysql 进行mysql命令行
docker exec -it <container id> mysql
# 设置权限
use mysql;
GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY '<有授权的账户的密码>' WITH GRANT OPTION;

# 刷新权限 or 重启容器
flush privileges;
```

3. 编译php扩展的方法

```bash
# 先解压源代码，并进入到ext目录
xz -d xxx.tar.xz
tar -xf xxx.tar

# 进行ext中，特定的扩展目录
cd xxx/ext/mysqli

# 执行phpize命令（一般是全局命令）
phpize 

# 配置构建
./configure -with-php-config=/usr/local/bin/php-config

# 执行构建
make
make test # 该步骤可省略
make install
```
