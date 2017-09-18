# Chapter 4. 日志系统
## 总体说明

本系统统一使用slf4j并指向logback，特殊情况需单独指定（在snsoft/System.properties中设置，也可以通过JVM属性—D指定），如下：
```
#设置Freemarker使用slf4j（logback）
org.freemarker.loggerLibrary=SLF4J

#设置Dubbo使用slf4j（logback）
dubbo.application.logger=slf4j

#设置Hibernate(Validator)使用slf4j（logback）
org.jboss.logging.provider=slf4j
```
a. 开发环境：默认使用snadk-utils下的logback.xml，可以通过-Dlogback.configurationFile指定logback的配置文件；
logging.config=D:/snsoft90/snconfig/logback.xml

b. System.properties中配置以下三项，用于指定日志使用slf4j

  i. org.freemarker.loggerLibrary=SLF4J
  ii. dubbo.application.logger=slf4j
  iii. org.jboss.logging.provider=slf4j

c. 其余参见日志规范7点；

