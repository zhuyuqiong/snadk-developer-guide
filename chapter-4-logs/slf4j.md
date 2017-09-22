# SLF4J

**JAVA简单日志门面**（Simple Logging Facade for Java，缩写[SLF4J](https://www.slf4j.org/index.html)），是一套封装Logging 框架的API，以Facade模式实现。它不是具体的日志解决方案，它只服务于各种各样的日志系统。可以在软件部署的时候决定要使用的 Logging 框架，目前主要支持的有[Java Logging API](https://zh.wikipedia.org/w/index.php?title=Java_Logging_API&action=edit&redlink=1)、[log4j](https://zh.wikipedia.org/wiki/Log4j)及[logback](https://zh.wikipedia.org/w/index.php?title=Logback&action=edit&redlink=1)等框架。以[MIT 授权](https://zh.wikipedia.org/w/index.php?title=MIT_授權&action=edit&redlink=1)方式发布。

SLF4J 的作者就是 log4j 的作者 Ceki Gülcü，他宣称 SLF4J 比 log4j 更有效率。

## 特性

### Level

log4j 提供 TRACE, DEBUG, INFO, WARN, ERROR 5个级别日志等级。

### 占位符

传统的日志中，我们大量使用字符串拼接的方式，如果当前系统日志Level不需要记录Debug等级的信息，就会浪费时间在产生不必要的信息上。

```
logger.debug("There are now " + count + " user accounts: " + userAccountList);
```

或者会使用是否debug模式的判断：

```
if (logger.isDebugEnabled()) {
    logger.debug("There are now " + count + " user accounts: " + userAccountList);
}
```

而slf4j提供了一种新的记录方式，就是使用**占位符**，在代码中表示为"{}"。"{}"会在运行时被某个提供的实际字符串所替换。这不仅降低了你代码中字符串连接次数，而且还节省了新建的String对象。

```
logger.debug("There are now {} user accounts: {}", count, userAccountList);
```



