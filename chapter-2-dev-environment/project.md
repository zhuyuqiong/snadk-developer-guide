## 2.2 工程

### 工程的标准结构

1. \(api+impl\)：根据需要可以合并。
2. \(ui+xjs\)：根据需要可以没有。

### 工作空间

### 导入Maven工程

Maven工程下仅存在pom.xml文件和src目录。

### 生成工程

4、本地MySQL【ftp/software软件安装包/数据库/MySQL/mysql-5.7.17.msi】；

在指定的ftp目录下找到上述安装包安装mysql，注意记住root用户的用户名密码，安装完毕后使用Command Line Client或者其他可视化工具（navicat等）新建数据库：

输入root用户密码，使用create database n10test; 命令创建数据库（n10test）。

使用show databases;查看创建的数据库；

如果选用本地数据库开发测试需要修改账套文件里的数据源配置，本地测试账套改成自己本地数据源。

