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
a. 开发环境：默认使用snadk-utils下的logback.xml，可以通过一下方式指定logback的配置文件：
```
-Dlogback.configurationFile=D:/snsoft90/snconfig/logback.xml
或
-Dlogging.config=D:/snsoft90/snconfig/logback.xml
```
b. 有些三方功能，需要特殊设置指定使用slf4j（在snsoft/System.properties中设置，也可以通过JVM属性—D指定），如下：
```
#设置Freemarker使用slf4j（logback）
org.freemarker.loggerLibrary=SLF4J

#设置Dubbo使用slf4j（logback）
dubbo.application.logger=slf4j

#设置Hibernate(Validator)使用slf4j（logback）
org.jboss.logging.provider=slf4j
```
c. 其余参见日志规范7点；

