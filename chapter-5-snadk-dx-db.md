# SNADK-DX-DB

本章节介绍一下SNADK中使用关系型数据库存取的相关内容。

## Database的使用原则

本节的目的是强调Database的使用原则，主要是为了向各位同学介绍底层实现。因此如下代码片段并不是应用层Database的使用方式，而只是底层实现方式。在应用层，我们按照FunctionalInterface有更好的封装。

* **谁new谁关闭**

在程序中的写法如下：

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
try (Database db = AppContext.getUserSession(true).newDatabaseByTable(String table, boolean checkNull))
{
    db.beginTrans();
    boolean rollback = true;
    try{
        ...
        rollback= false; 
    } finally {
        db.commitTrans(rollback);
    }
}
```

## FunctionalInterface封装

通过Java 1.8新的lambda表达式特性，我们对Database的使用进行了封装，向应用层开发屏蔽了获取Database对象、事务管理等实现。在应用层只需要关系我拿Database可以做什么，不需要关心获取的方式以及事务管理。

目前封装有针对写数据源操作的方法：

```
//按表获取db执行逻辑
snsoft.dx.DBUtils.trans(String table, Function<Database,T> function);
snsoft.dx.DBUtils.trans(String table, Consumer<Database> function);

//按数据源获取db执行逻辑
snsoft.dx.DBUtils.transForDataSource(String dataSource, Function<Database,T> function);
snsoft.dx.DBUtils.transForDataSource(String dataSource, Consumer<Database> function);



//以下是例子
DBUtils.trans("bcode", db -> {
    list.forEach(btype -> createRootBcode(bname, btype.getBtype());
    return true;
});
```

对读数据源操作的方法：

```
//按表获取只读db执行逻辑
snsoft.dx.DBUtils.read(String table, Function<Database,T> function);
```

## 事务

从上一节我们已经了解到使用Database对象进行数据库操作时，事务已交由平台底层实现。而数据库存取还有一种方式，就是使用DAO存取，这种方式在应用层可能会出现，使用时的事务就尤为需要注意。

* **单DAO存储时，不需要启用事务，程序自动处理**

相关程序实现参见：

```java
snsoft.dx.DefaultDAO#saveRecord
```

* **多DAO存储时，需要在最外层Service启用事务**

通过UserSession获取db后启用事务，在DAO实现中，会从UserSession中获取同一个db实例。

## DefaultDAO

该类是VO的CRUD方法，是非线程安全的，因此注意不要使用注入的方式使用。

常用的写法例子：

```java
public void save(WCodeVO[] records)
{
    DefaultDAO<WCodeVO> dao = new DefaultDAO<>();
    dao.save(records);
}
```



