# Chapter 2. 开发环境

## 基础环境要求

SNADK使用[maven](http://maven.apache.org/)作为构建工具，Eclipse作为开发工具，[Git](https://git-scm.com/)作为版本控制工具。相关工具知识可前往对应官方网站了解补充。

* Java 使用jdk1.8作为开发版本，低版本jdk与依赖中部分jar包不兼容。
* Maven 3.0或以上版本
* Git
* \*MySQL
* \*Redis
* \*Zookeeper
* \*ActiveMQ

> 注：\*号标记的为可选安装。

## 代码签出

底层源文件目录：`D:\snsoft90`

创建上述目录，通过以下地址可以签出SNADK最新源码：

```
git clone snsoftadk:snsoft_adk.git
```

## 分支

我们使用 `master` 作为主干版本的开发，使用分支作为维护版本。

可以通过？？来查看所有版本的标签。

