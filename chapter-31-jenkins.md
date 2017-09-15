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
```

系统设置（所有的高级全部展开）

```bash
公共配置：
Passphrase：密码（key的密码，如果你设置了）
Path to key：key文件（私钥）的路径
Key：将私钥复制到这个框中
Disable exec：禁止运行命令
```

```bash
私有配置：
SSH Server Name：标识的名字（随便你取什么）
Hostname：需要连接ssh的主机名或ip地址（建议ip）
Username：用户名
Remote Directory：远程目录
Use password authentication, or use a different key：可以替换公共配置（选中展开的就是公共配置的东西，这样做扩展性很好）
```

```bash
私有配置的高级设置：
Port：端口（默认22）
Timeout (ms)：超时时间（毫秒）默认即可
Disable exec：禁止运行命令
Test Configuration：测试连接
```

## 新建自动部署任务

点击新建菜单后，录入任务名称、选择自由风格软件项目、点击OK。

新建完成后进入任务配置界面。任务配置界面主要完成源码配置、Maven打包配置、自动部署三项。

### 配置源码

![](/assets/jenkins-git.png)

配置仓库地址，然后点击ADD按钮添加ssh秘钥，输入名称。

![](/assets/jenkins-git-ssh.png)

点击ADD添加完成后选择刚刚创建的秘钥，选择需要拉取的分支。

![](/assets/jenkins-master.png)

### 配置maven打包项

配置构建选项，选择 Invoke top-level Maven targets

配置maven打包命令Goals：

```bash
clean install -Dmaven.test.skip=true
```

选择高级设置，配置打包使用的pom.xml文件，其他选择默认即可。

Jenkins会自动clone源码到工作空间中，此时选择的文件都是基于工作空间的相对路径。

### 配置自动部署

#### 基于远程SSH方式

点击构建后操作，选择Send build artifacts over SSH ，填写配置说明如下：

```bash
SSH  Server Name：选个一个你在系统设置里配置的配置的名字
```

```bash
Transfer Set Source files：需要上传的文件（注意：相对于工作区的路径。看后面的配置可以填写多个，默认用,分隔）
注意：这个是相对于Jenkins服务的工作区而言的相对路径，例如：我自己的Jenkins的主目录设置为 /apps/Jenkins_home（Jenkins服务器）
我创建的该工程的工作区的目录绝对路径是 /apps/Jenkins_home/jobs/gulu-admin_test/workspace（Jenkins服务器） 
那我Source files中的 target/*.war 的绝对路径就是 /apps/Jenkins_home/jobs/gulu-admin_test/workspace/target/*.war
```

```bash
Remove prefix：移除目录（只能指定Transfer Set Source files中的目录）
注：如果该处不填，则构建后的war包相对于远程目录Remote directory的相对路径为 target/*.war (实际上*为maven构建的war包名称)
如果此处填了，比如我填了target，那么构建后的war包相对于远程目录Remote directory的相对路径为 *.war (实际上*为maven构建的war包名称)
```

```bash
Remote directory：远程目录（根据你的需求填写吧，因为我这儿是测试,所以偷懒没有填写。默认会继承系统配置）
说明：如果不填写，则将Jenkins服务器打的war包拷贝到远程默认的Remote directory目录
（系统设置中的Remote directory，如我途中设置的为 /apps 目录）
如果填写，比如我填写的为jenkins_war，则将Jenkins服务器打的war包拷贝到远程的Remote directory目录下的jenkins_war 目录下，
即该路径是相对于系统配置的远程Remote directory目录的相对路径
```

```bash
Exec command：把你要执行的命令写在里面
```

以下是Exec command的一个例子：

```bash
sudo cp /tmp/run-ui-war.4.0.0-SNAPSHOT.war /opt/run-ui.war
docker rm -f snadk-ui
docker rmi snadk-ui:latest
cd /opt
docker build -f Dockerfile-ui -t snadk-ui:latest .
docker run --name snadk-ui -p 1010:1010 -v /snconfig:/opt/snconfig -d snadk-ui:latest
```

#### 本地部署

注意此种配置适用于Docker和jenkins在同一台服务器。

点击构建操作，选择下列选项（根据具体的操作系统选择脚本执行选项）

* Execute Windows batch command
* Execute shell

填入脚本例子：

```bash
docker rm -f snadk-ui
docker rmi snadk-ui:latest
docker build -f Dockerfile-ui -t snadk-ui:latest .
docker run --name snadk-ui -p 1010:1010 -v D:/snsoft90/snconfig:/opt/snconfig -d snadk-ui:latest
```

## 执行任务

回到首页，点击任务视图右侧的构建图标按钮即可进行自动打包部署。

可以点击任务进去任务详情，点击左侧的console控制台进入查看打包日志，追踪打包出现的问题进行调试。

接下来就是整个打包部署过程中出现的错误调试过程了。

