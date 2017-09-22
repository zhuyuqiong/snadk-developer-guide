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



java2js的Arguments配置示例

@/snsoft90/snsoft\_adk/test/erp/SNS-Invoicing/xjs/build/J2SLibBuild\(invoicing\).Args.txt

iii. 默认规则

1. SN.ConfigPath：指定环境变量，开发环境与单元测试环境可以共用；

2. snconfig目录下的标准文件

   a. System.properties：用于设置启用参数；

   b. WorkSpace.xml：必须含有默认的00帐套；

c. Spring-Configs.xml：用于配置启动后的Spring-Bean参数；

d. TimerTask.xml：定时任务定义文件；

e. ShardingRule.xml：分表分库规则；

