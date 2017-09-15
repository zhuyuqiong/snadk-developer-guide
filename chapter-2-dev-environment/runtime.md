## 2.3 运行环境

i. Tomcat7+；

      ii. SpringBoot：标准



          1. boot-ui；



          2. boot-server；



      iii. 默认规则



          1. SN.ConfigPath：指定环境变量，开发环境与单元测试环境可以共用；



          2. snconfig目录下的标准文件



              a. System.properties：用于设置启用参数；



              b. WorkSpace.xml：必须含有默认的00帐套；



              c. Spring-Configs.xml：用于配置启动后的Spring-Bean参数；



              d. TimerTask.xml：定时任务定义文件；



              e. ShardingRule.xml：分表分库规则；



