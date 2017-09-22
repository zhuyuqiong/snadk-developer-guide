# LogBack

LogBack是一个日志框架，它与slf4j都出自Ceki Gülcü之手。据原作者描述，LogBack相比log4j实现效率更高，具有更好的处理I/O异常的能力，以及原生支持slf4j等特性。

## **LogBack的结构**

LogBack被分为3个组件，logback-core, logback-classic 和 logback-access。

其中logback-core提供了LogBack的核心功能，是另外两个组件的基础。

logback-classic则实现了Slf4j的API，所以当想配合Slf4j使用时，需要将logback-classic加入classpath。

logback-access是为了集成Servlet环境而准备的，可提供HTTP-access的日志接口。

## SLF4J与LogBack结合原理

我们从java代码最简单的获取logger开始

```
Logger logger = LoggerFactory.getLogger(xxx.class.getName());
```

LoggerFactory是slf4j的日志工厂，获取logger方法就来自这里。

```
public static Logger getLogger(String name) {
    ILoggerFactory iLoggerFactory = getILoggerFactory();
    return iLoggerFactory.getLogger(name);
}
```

这个方法里面有分为两个过程。第一个过程是获取ILoggerFactory，就是真正的日志工厂。第二个过程就是从真正的日志工厂中获取logger。  
第一个过程又分为三个部分。

**第一个部分加载org/slf4j/impl/StaticLoggerBinder.class文件**

```
paths = ClassLoader.getSystemResources(STATIC_LOGGER_BINDER_PATH);
//STATIC_LOGGER_BINDER_PATH = "org/slf4j/impl/StaticLoggerBinder.class"
```

**第二部分随机选取一个StaticLoggerBinder.class来创建一个单例**  
当项目中存在多个StaticLoggerBinder.class文件时，运行项目会出现以下日志：

```
SLF4J: Class path contains multiple SLF4J bindings.
SLF4J: Found binding in [jar:file:/C:/Users/jiangmitiao/.m2/repository/ch/qos/logback/logback-classic/1.1.3/logback-classic-1.1.3.jar!/org/slf4j/impl/StaticLoggerBinder.class]
SLF4J: Found binding in [jar:file:/C:/Users/jiangmitiao/.m2/repository/org/slf4j/slf4j-log4j12/1.7.12/slf4j-log4j12-1.7.12.jar!/org/slf4j/impl/StaticLoggerBinder.class]
SLF4J: See http://www.slf4j.org/codes.html#multiple_bindings for an explanation.
SLF4J: Actual binding is of type [ch.qos.logback.classic.util.ContextSelectorStaticBinder]
```

最后会随机选择一个StaticLoggerBinder.class来创建一个单例

```
StaticLoggerBinder.getSingleton()
```

**第三部分返回一个ILoggerFactory实例**

```
StaticLoggerBinder.getSingleton().getLoggerFactory();
```

所以slf4j与其他实际的日志框架的集成jar包中，都会含有这样的一个`org/slf4j/impl/StaticLoggerBinder.class`类文件，并且提供一个ILoggerFactory的实现。

第二个过程就是每一个和slf4j集成的日志框架中实现ILoggerFactory方法getLogger\(\)的实例所做的事了。

## Logger, Appenders ,Layouts



