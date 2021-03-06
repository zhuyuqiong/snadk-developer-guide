# SNConfig

本章节简要介绍snconfig文件夹下个文件内容，主要目的在于让开发人员对应系统各种配置文件有一个整体了解，而每个文件中的定义方式、使用说明另有文档介绍。

## System.properties

用于设置启动用参数。

示例：

```
SN-MQ.Comm.Name=SN-MQ
SN-MQ.Comm.Client=SN-MQ
#logback.configurationFile=D:/snsoft90/snconfig/logback.xml
#log4j.configuration=file:/E:/adkdoc/configs/log4j/log4j-dev.xml
logging.config=D:/snsoft90/snconfig/logback.xml
dubbo.application.logger=slf4j
﻿
#Zookeeper=========================================================
snsoft.zk=true
snsoft.zk.connectString=172.18.3.186:2181
snsoft.zk.sessionTimeout=2181
#snsoft.zk.watcherClass=
dubbo.registryAddress=172.18.3.186:2181


#Redis=========================================================
#非集群
snsoft.redis=true
snsoft.redis.host=172.18.3.186
snsoft.redis.port=6379
#集群
#snsoft.redis.cluster.nodes=127.0.0.1:7000,127.0.0.1:7001,127.0.0.1:7002,127.0.0.1:7003,127.0.0.1:7004,127.0.0.1:7005

#Redis-分码服务===================================================
snsoft.mc.redis=true
snsoft.mc.redis.host=10.8.6.1
snsoft.mc.redis.port=6379


#MongoTemplate=================================================
#系统默认
#1、日志存储及查询使用
snsoft.mongo=true
snsoft.mongo.uri=mongodb://10.8.5.30:27017/n10

#禁用Redis缓存通知
#SQL.DisableRedisSqlUpdateNotifier=true

#Auto
#登录回话时长，默认30分钟；单位秒
Login.Session.Interval=28800
#UI层不缓存，包括：1、界面定义；2、菜单定义；3、码表定义；
UI.NoCache=true
#标识是测试环境
sn.test=true

#MQ Cache 非集群
SN-MQ.Comm.cache=true
#snsoft.mq.cache.host=10.8.6.1
SN-MQ.Comm.cache.host=127.0.0.1
SN-MQ.Comm.cache.port=6379


#MQ MongoDB 
SN-MQ.Comm.mongo=true
SN-MQ.Comm.mongo.uri=mongodb://10.8.5.30:27017/n10
```

## WorkSpace.xml

帐套文件，必须含有默认的00帐套。

示例：

```
<?xml version="1.0" encoding="UTF-8"?>
<!-- type= 
1:SqlServer 
2:Oracle 
4:MySql 
-->

<workspace-list>

    <workspace id="00" title="开发环境(mysql)">
        <datasource id="DEFAULT" host="10.8.5.50" port="3306" database="snadk" user="snadk" password="snadk" type="4" />
        <datasource id="CONFIG" host="10.8.5.50" port="3306" database="snadk" user="snadk" password="snadk" type="4" />
        <datasource id="UCODECFG" host="10.8.5.50" port="3306" database="snadk" user="snadk" password="snadk" type="4" />
        <datasource id="HELP" host="10.8.5.50" port="3306" database="snadk" user="snadk" password="snadk" type="4" />
    </workspace>

    <workspace id="N10DEVORACLE" title="开发环境(oracle)">
        <datasource id="CONFIG" host="10.8.5.1" port="1521" database="orcl" user="n10_dev_config" password="sinolink" type="2" />
        <datasource id="UCODECFG" host="10.8.5.1" port="1521" database="orcl" user="n10_dev_ucodecfg" password="sinolink" type="2" />
    </workspace>

    <workspace id="LOCAL" title="N9升级(本地)">
        <datasource id="CONFIG" host="127.0.0.1" port="3306" database="n10test" user="root" password="root" type="4" />
        <datasource id="UCODECFG" host="127.0.0.1" port="3306" database="n10test" user="root" password="root" type="4" />
    </workspace>
</workspace-list>
```

## Spring-Configs.xml

用于配置启动后的Spring-Bean参数、选项。

示例：

```
<beans xmlns="http://www.springframework.org/schema/beans" xmlns:amq="http://activemq.apache.org/schema/core" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:context="http://www.springframework.org/schema/context"
    xmlns:sn="http://snsoft.cn/schema/config"
    xmlns:p="http://www.springframework.org/schema/p"
    xsi:schemaLocation="http://www.springframework.org/schema/beans 
      http://www.springframework.org/schema/beans/spring-beans-3.0.xsd
      http://activemq.apache.org/schema/core 
      http://activemq.apache.org/schema/core/activemq-core.xsd
      http://www.springframework.org/schema/context 
      http://www.springframework.org/schema/context/spring-context-3.0.xsd 
      http://snsoft.cn/schema/config
      http://snsoft.cn/schema/config.xsd
      ">
    <sn:option name="Diag.TraceLevel">9</sn:option>
    <sn:option name="Languages">zh_CN:简体中文,en:English</sn:option>
    <sn:option name="FSID.DOCROOT">file:/temp/attach/</sn:option>
    <sn:option name="FSID.FTPROOT">ftp://sinolinktest:test.2016@10.8.1.11/Attachments/N10/</sn:option>
    <sn:option name="Diag._IgnorePWD">true</sn:option>

</beans>
```

## TimerTask.xml

定时任务定义文件。

示例：

```
<?xml version="1.0" encoding="UTF-8"?>
 <timertask-list>
        <timertask id="50000" name="SN-MQ.PushTimer" 
         work-time="0:0-24:0" interval="10"
         auto-start="true"
         thread = "true"
         task-type="bean"
         disabled="true"
        >SN-MQ.MQPushTimer</timertask>
</timertask-list>
```

## ShardingRule.xml

分表分库规则。

示例：

```
#Workspace.xml
<datasource id="SHARRDING" database="snsoft80_demo_sharding" type="sharding"/>
```

```
#ShardingRule.xml
<?xml version="1.0" encoding="UTF-8"?>

<data-partion-rules>

    <datasource id="snsoft80_demo_sharding">

        <db-master type="mysql" password="111111" user="root" database="snsoft80_demo" host="127.0.0.1"/>

        <db-node id="dn001" type="4" password="111111" user="root" database="snsoft80_demo_part01" host="127.0.0.1" port="3306"/>

        <db-node id="dn02" type="4" password="111111" user="root" database="snsoft80_demo_part02" host="127.0.0.1" port="3306"/>

        <table rule="snsoft.dx.sharding.rulealg.ShardingRuleSuffixAlgorithm.new?DBIDPos=0&TBLIDPos=2" tbl-nodes="*_01,*_02" db-nodes="dn02" by-column="dicticode" name="gxtest"/>

        <table rule="snsoft.dx.sharding.rulealg.ShardingRuleSuffixAlgorithm.new?DBIDPos=0&DBIDSize=3&TBLIDPos=3&TBLIDSize=3" tbl-nodes="*_001,*_002" db-nodes="dn001,dn02" by-column="id" name="mdef"/>

        <table rule="snsoft.dx.sharding.rulealg.ShardingRuleSuffixAlgorithm.new?DBIDPos=0&DBIDSize=3&TBLIDPos=3&TBLIDSize=3" tbl-nodes="*_001,*_002" db-nodes="dn001,dn02" by-column="code" name="gdef"/>

    </datasource>

</data-partion-rules>
```



