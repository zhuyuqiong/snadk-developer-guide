# Chapter 4. 日志系统

本系统统一使用slf4j并指向logback；

a. 开发环境：默认使用snadk-utils下的logback.xml，可以通过-Dlogback.configurationFile指定logback的配置文件；

b. System.properties中配置以下三项，用于指定日志使用slf4j

  i. org.freemarker.loggerLibrary=SLF4J







  ii. dubbo.application.logger=slf4j







  iii. org.jboss.logging.provider=slf4j

c. 其余参见日志规范7点；

