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

以下是两个官方说明，可以解决各位开发同学日常使用中的部分选择疑惑。

### Should Logger members of a class be declared as static?

We`used`to recommend that loggers members be declared as instance variables instead of static. After further analysis,**we no longer recommend one approach over the other.**

Here is a summary of the pros and cons of each approach.

| Advantages for declaring loggers as static | Disadvantages for declaring loggers as static |
| :--- | :--- |
| common and well-established idiomless CPU overhead: loggers are retrieved and assigned only once, at hosting class initializationless memory overhead: logger declaration will consume one reference per class | For libraries shared between applications, not possible to take advantage of repository selectors. It should be noted that if the SLF4J binding and the underlying API ships with each application \(not shared between applications\), then each application will still have its own logging environment.not IOC-friendly |
| Advantages for declaring loggers as instance variables | Disadvantages for declaring loggers as instance variables |
| Possible to take advantage of repository selectors even for libraries shared between applications. However, repository selectors only work if the underlying logging system is logback-classic. Repository selectors do not work for the SLF4J+log4j combination.IOC-friendly | Less common idiom than declaring loggers as static variableshigher CPU overhead: loggers are retrieved and assigned for each instance of the hosting classhigher memory overhead: logger declaration will consume one reference per instance of the hosting class |

### Is there a recommended idiom for declaring a logger in a class?

The following is the recommended logger declaration idiom. For reasons[explained above](https://www.slf4j.org/faq.html#declared_static), it is left to the user to determine whether loggers are declared as static variables or not.

```
package some.package;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

public class MyClass {
  final (static) Logger logger = LoggerFactory.getLogger(MyClass.class);
  ... etc
}
```

Unfortunately, given that the name of the hosting class is part of the logger declaration, the above logger declaration idiom is\_not\_resistant to cut-and-pasting between classes.

Alternatively, you can use`MethodHandles.lookup()`introduced in JDK 7 to pass the caller class.

```
package
 some
.
package
;


import
 org
.
slf4j
.
Logger
;


import
 org
.
slf4j
.
LoggerFactory
;


import
 java
.
lang
.
invoke
.
MethodHandles
;




public
class
MyClass
{


final
static
Logger
 logger 
=
LoggerFactory
.
getLogger
(
MethodHandles
.
lookup
().
lookupClass
());


...
 etc


}
```

This pattern can be cut and pasted across classes.

