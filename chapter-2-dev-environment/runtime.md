## 运行环境

目前的工程支持两种方式启动：

1. Tomcat启动
2. SpringBoot方式启动。（建议开发使用）

### Tomcat

Tomcat要求版本为Tomcat8+。

### SpringBoot

使用SpringBoot启动可以省去web.xml配置，使用Java Code进行Servlet注册。且启动过程中都可调试源码，启动过程更加透明。建议开发人员使用此方式作为日常开发的启动方式。

在服务部署上，目前平台采用Service服务组件和UI控制分层的方案，因此在启动工程中需要有两个启动项：

1. boot-ui

2. boot-server

boot-ui Run/Debug 配置

```
Name: Boot-UI
Main Class: snsoftboot.BootLaunch
Project: boot-run-ui
VM options: -DSN.ID=SN-HostUI
```

其中，`SN.ID`为服务器ID，用于dubbo的Service注册group参数。

在ui启动工程中，还有个类`snsoftboot.BootConfig`值得我们关注，这个类使用Spring `@Configuration`注解，用于向Spring 的web上下文注入平台应用所依赖的Servlet。

boot-service Run/Debug 配置

```
Name: Boot-Service
Main Class: snsoftboot.BootLaunch
Project: boot-run-service
VM options: -DSN.ID=SN-HostService
            -Ddubbo.protocol.port=20881
```

其中，`dubbo.protocol.port`为dubbo服务使用端口，dubbo默认会使用20880端口，而当我们启动多个dubbo服务时，需要为每个服务都指定不同的端口。

### Java2js

java2js Run/Debug 配置

```
Name: java2js
Main Class: snsoftx.j2stools.LibBuild
Project: snadk-java2js
Program arguments:
    #@/snsoft90/snsoft_adk/snadk-mq/xjs/build/J2SLibBuild(mq).Args.txt
    #@/snsoft90/snsoft_adk/snadk-cli/snadk-xjs/build/J2SLibBuild.Args.txt
    @/snsoft90/snsoft_adk/snadk-cmc/xjs/build/J2SLibBuild(cmc).Args.txt
    #@/snsoft90/snsoft_adk/snadk-help/xjs/build/J2SLibBuild(help).Args.txt
    @/snsoft90/snsoft_adk/snadk-ui/snadk-ui/theme-src/BuildJs.txt
```

java2js中的Arguments文件配置示例：

方式一：只使用路径描述编译目标

```
-path /snsoft90/snsoft_adk/snadk-cmc/xjs/src/main/java=>/snsoft90/snsoft_adk/snadk-cmc/cmc-ui/web/xjslib
```

方式二：支持宏替换方式

```
#define SNADKSRC_ROOT ${BASEDIR}/../../..

-classpath ${BASEDIR}/../target/classes

-path ${BASEDIR}/../src/main/java=>${SNADKSRC_ROOT}/snadk-ui/snadk-ui/web/xjslib
```

```
#BASEDIR 为当前txt文件所在目录
@see snsoftx.j2stools.LibBuild#parseArgSet中代码逻辑
```

注意：IntelliJ Idea中，启动配置无法显式地配置classpath，需要在VM options中手工指定：

```
-Xbootclasspath/a:D:\snsoft90\snsoft_adk\snadk-cmc\xjs\target\classes;D:\snsoft90\snsoft_adk\snadk-cli\snadk-xjs\target\classes
```

### Webstart-cli

新平台中，我们强烈建议开发/运维人员在Web环境下工作，支持大家使用浏览器进行配置设置，鼓励使用第三方工具促进开发/运维效率，作为一种Java官方已不建议使用的技术方案，我们同样不建议使用webstart方式。同时在发布项目时，webstart相关工程可能不会发布支持。

webstart-cli Run/Debug 配置

```
Name: webstart
Main Class: snsoft.cli.app.TApplication
Project: snadk-cli-app
VM options: 
    -Xmx1024m
    -DServerURL=http://127.0.0.1:1010/n10
    -ea
    -Dsn.test=true
```

### 默认规则

环境变量中配置参数：

```
#指定平台配置文件所在文件夹
SN.ConfigPath： D:\snsoft90\snconfig
```

#### SN.ConfigPath目录下的标准文件

* System.properties：用于设置启用参数
* WorkSpace.xml：必须含有默认的00帐套
* Spring-Configs.xml：用于配置启动后的Spring-Bean参数
* TimerTask.xml：定时任务定义文件
* ShardingRule.xml：分表分库规则



