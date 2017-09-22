# LogBack

LogBack是一个日志框架，它与slf4j都出自Ceki Gülcü之手。

## **LogBack的结构**

LogBack被分为3个组件，logback-core, logback-classic 和 logback-access。

其中logback-core提供了LogBack的核心功能，是另外两个组件的基础。

logback-classic则实现了Slf4j的API，所以当想配合Slf4j使用时，需要将logback-classic加入classpath。

logback-access是为了集成Servlet环境而准备的，可提供HTTP-access的日志接口。



