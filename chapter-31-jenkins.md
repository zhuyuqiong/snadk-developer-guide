# Chapter 31. Jenkins

The leading open source automation server, Jenkins provides hundreds of plugins to support building, deploying and automating any project.

[Jenkins](https://jenkins.io/) 是一款开源自动化部署平台，可用于自动化打包、部署项目。丰富的插件可以应对不同的语言、不同的服务环境。

新版底层可使用传统方式部署，也可以使用Jenkins部署。

## 安装

### Windows

官网下载jenkins.war包，下载地址如下：

```
https://jenkins.io/download/
```

环境变量中需要配置`JENKINS_HOME`，这个目录会初始化为Jenkins的工作空间。

Jenkins支持多种部署方案：

* 使用中间件如Tomcat部署。
* Java -jar 直接部署：

  ```
  java -jar jenkins.war --httpPort=8080
  ```

  > 注意：经过测试可以部署的Tomcat至少为8.0或以上版本，jdk为1.8。其他版本待验证。

### Linux

？？

## 初始化

部署成功后使用如下地址访问平台：

```
http://127.0.0.1::8080/jenkins
```

首次进入后会先初始化环境安装插件，使用默认配置就可以，使用过程中如果使用额外插件在按需下载。

![](/assets/jinkins-initial.png)

插件安装完成之后，需要创建第一个用户。创建完成后就可以使用Jenkins了。

![](/assets/jenkins-fisrt-user.png)

## 配置

本步骤可以不用配置，如果当前环境没有安装对应的工具，Jenkins都可以自动帮你完成工具的安装。

### 配置maven、jdk、git

Jenkins系统设置菜单位于：`系统管理-Global Tool Configuraion`

这里需要依次安装/配置Maven、JDK、Git工具。

### 系统设置

这里主要设置远程服务器SSH相关配置

#### Publish over SSH配置（可多个）

找到Publish over SSH，配置远程服务连接（注意此配置不是必须的，例如发布到同一服务器的Docker中时）

配置说明：

```java
说明：这个插件可以通过ssh连接其他Linux机器
官方说明：Publish Over SSH
安装步骤：
系统管理→管理插件→可选插件→Artifact Uploaders→Publish Over SSH
 系统设置（所有的高级全部展开）
公共配置：
Passphrase：密码（key的密码，如果你设置了）
Path to key：key文件（私钥）的路径
Key：将私钥复制到这个框中
Disable exec：禁止运行命令
私有配置：
SSH Server Name：标识的名字（随便你取什么）
Hostname：需要连接ssh的主机名或ip地址（建议ip）
Username：用户名
Remote Directory：远程目录
Use password authentication, or use a different key：可以替换公共配置（选中展开的就是公共配置的东西，这样做扩展性很好）
私有配置的高级设置：
Port：端口（默认22）
Timeout (ms)：超时时间（毫秒）默认即可
Disable exec：禁止运行命令
Test Configuration：测试连接
```

## 新建自动部署任务

点击新建菜单后，录入任务名称、选择自由风格软件项目、点击OK。

新建完成后进入任务配置界面。任务配置界面主要完成源码配置、Maven打包配置、自动部署三项。



