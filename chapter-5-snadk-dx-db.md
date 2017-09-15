# Chapter 5. SNADK-DX-DB

  a. Database的使用规则：

```java
    AppContext.getUserSession(true).newDatabaseByTable();
```

      i. 谁new谁关闭 try\\(Database db = ;\\)；



      ii. 谁起事务谁提交try{}finally{}；



  b. 事务



      i. 单表存储，不需要启用事务，程序自动处理；



      ii. 多表存储，需要在最外层Service启用相关事务；



  c. DefaultDAO：VO的CRUD；



