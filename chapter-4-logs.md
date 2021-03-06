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

**开发环境**：默认使用snadk-utils下的logback.xml，可以通过一下方式指定logback的配置文件：

```
-Dlogback.configurationFile=D:/snsoft90/snconfig/logback.xml
或
-Dlogging.config=D:/snsoft90/snconfig/logback.xml
```

有些**三方功能**，需要特殊设置指定使用slf4j（在snsoft/System.properties中设置，也可以通过JVM属性—D指定），如下：

```
#设置Freemarker使用slf4j（logback）
org.freemarker.loggerLibrary=SLF4J

#设置Dubbo使用slf4j（logback）
dubbo.application.logger=slf4j

#设置Hibernate(Validator)使用slf4j（logback）
org.jboss.logging.provider=slf4j
```

## 日志规范

### 索引性

日志是面向读者的：打印的信息应该可以明确进行定位  
    错误：`ERROR: Save failure - SQLException .....`  
    正确：`ERROR: Save failure - Entity=Person, Data=[id=123 surname="Mario"] - SQLException....`

### 环境分类

匹配日志等级和执行环境（ERROR，WARN，INFO，DEBUG）

1. 开发阶段：任何有意义的信息
2. 集成阶段：自己的功能DEBUG级别，三方功能WARN（如果有需要INFO）级别
3. 成品阶段：自己的功能INFO级别，三方功能WARN级别；

### 调试日志

提交前去除编码帮助日志

```
logger.debug("Enter in aMethod");
if ("no".equals(aParam)) 
{
    logger.debug("User says no");
}
```

类似于这种代码在提交前需要删除。

### Debug日志判断

因为Debug日志很多，而且会创建很多的字符串对象，而在生产环境不启用，故Debug消息之前检查日志等级。

```
if (logger.isDebugEnabled())
{
    logger.debug (…….)
}
```

### 记录日志的方式

了解你的logger，否则可能会带来巨大的开销  
错误：`logger.info("Person name is " + person.getName());`  
正确：`logger.info("Person name is {}", person.getName());`  
前一种方式，在记录日志时创建日志信息，但是实际上该日志可能被过滤，根本就没有记录；  
后一种方式，在记录日志时，并不创建日志信息，在真正记录时才创建日志信息，可以减少字符串对象的创建。

### logger命名规范

获取Logger对象的方式必须使用类名，如：

```
Logger logger = LoggerFactory.getLogger(XXXX.class);
```

这样可以对logger按照类包名进行归类，方便配置、管理。

### 异常记录规范

catch到的异常，在继续抛出时，必须封装到当前的异常对象中，严禁丢失。

```
try
{
    ....
}catch(Exception e1)
{
    logger.error("msg",e1);
    throw new XXXXException("msg",e1);
}
```



