# SNADK-DX-DB

本章节介绍一下SNADK中使用关系型数据库存取的相关内容。

## Database的使用原则

* **谁new谁关闭**

在程序中要求的写法如下：

```java
import snsoft.dx.Database;
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
import snsoft.dx.Database;
#创建db

try (Database db = AppContext.getUserSession(true).newDatabaseByTable(String table, boolean checkNull)){
    ... 
}
```

* **谁起事务谁提交**

```java
import snsoft.dx.Database;
#创建db
boolean rollback = true;
try (Database db = AppContext.getUserSession(true).newDatabaseByTable(String table, boolean checkNull)){
    db.beginTrans();
    ...
    rollback rollback= false; 
}finally{
    db.commitTrans();
}
```

## 事务

* **单DAO存储时，不需要启用事务，程序自动处理**

相关程序实现参见：

```java
snsoft.dx.DefaultDAO#saveRecord
```

* **多DAO存储时，需要在最外层Service启用事务**

## DefaultDAO

VO的CRUD方法，该类是非线程安全的，因此注意不要使用注入的方式使用。

常用的写法例子：

```java
public void save(WCodeVO[] records)
{
    DefaultDAO<WCodeVO> dao = new DefaultDAO<>();
    dao.save(records);
}
```



