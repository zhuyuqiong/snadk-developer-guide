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

## 应用

部署成功后使用如下地址访问平台：

```
http://127.0.0.1::8080/jenkins
```





