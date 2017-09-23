# SNADK-DX-DB

Database的使用原则

* **谁new谁关闭**

在程序中要求的写法如下：

```java
import snsoft.commons.dx.Database;
#创建db
Database db = AppContext.getUserSession(true).newDatabaseByTable(String table, boolean checkNull);
try{
    ... 
}finally{
    db.close();
}
```

由于JDK1.7新特性，try block中创建的对象可以实现java.lang.AutoCloseable接口来自动关闭，因此写法可以省略为如下：

```java
import snsoft.commons.dx.Database;
#创建db

try (Database db = AppContext.getUserSession(true).newDatabaseByTable(String table, boolean checkNull)){
    ... 
}
```

i. 谁new谁关闭 try\\(Database db = ;\\)；

ii. 谁起事务谁提交try{}finally{}；

b. 事务

i. 单表存储，不需要启用事务，程序自动处理；

ii. 多表存储，需要在最外层Service启用相关事务；

c. DefaultDAO：VO的CRUD；

