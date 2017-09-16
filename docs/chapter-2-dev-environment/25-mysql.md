## 2.5 MySQL

SNADK 4.x版本中，约定所有开发配置都基于文件定义。这样可以减轻对数据库的依赖，使得每个开发使用独立数据库，甚至非关系型数据库成为可能。因此推荐每个开发都在本地安装私有数据库，方便个人调试。

MySQL获取途径：

```java
ftp/software软件安装包/数据库/MySQL/mysql-5.7.17.msi
```

或者[mysql.com](https://www.mysql.com/)

安装MySQL过程中，注意记住root用户的用户名密码。

安装完毕后使用Command Line Client或者其他可视化工具（[Navicat](https://www.navicat.com/en/products/navicat-for-mysql)等）新建数据库：

* 输入root用户密码，使用`create database n10test;`命令创建数据库（`n10test`）。
* 使用`show databases;`查看创建的数据库；
* 如果选用本地数据库开发测试，需要修改账套文件里的数据源配置，将本地测试账套改成自己本地数据源。



