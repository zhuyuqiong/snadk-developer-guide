## 2.5 MySQL

本地MySQL【ftp/software软件安装包/数据库/MySQL/mysql-5.7.17.msi】；

在指定的ftp目录下找到上述安装包安装mysql，注意记住root用户的用户名密码，安装完毕后使用Command Line Client或者其他可视化工具（navicat等）新建数据库：

输入root用户密码，使用create database n10test; 命令创建数据库（n10test）。

使用show databases;查看创建的数据库；

如果选用本地数据库开发测试需要修改账套文件里的数据源配置，本地测试账套改成自己本地数据源。

