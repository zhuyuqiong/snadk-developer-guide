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

### Logger变量是否应该声明为 static?

声明Logger变量是否为static，目前官方给出的意见是两者各有优缺，交给各位开发同学选择。

We`used`to recommend that loggers members be declared as instance variables instead of static. After further analysis,**we no longer recommend one approach over the other.**

Here is a summary of the pros and cons of each approach.

| static 优点  | static缺点 |
| :---- | :--- |
| 1. static写法更为常见和成熟 </br>2. CPU占用更少: loggers 只在主类初始化时加载一次</br>3. 内存占用更低: logger 声明只占用一个引用 | 1. 无法在应用间通过某种logger仓库技术共享logger实例</br>2. 无法IOC |
| non-static优点 | non-static缺点 |
| 1. 可以在应用间共享logger实例</br>2. 支持IOC | 1. 写法不常见</br>2. CPU占用更高：每次创建主类实例时都会加载 2. 内存占用更高：主类的每个实例都会创建一个引用 |

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
package some.package;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import java.lang.invoke.MethodHandles;

public class MyClass {
  final static Logger logger = LoggerFactory.getLogger(MethodHandles.lookup().lookupClass());
  ... etc
}
```

This pattern can be cut and pasted across classes.

