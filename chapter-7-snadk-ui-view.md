1. 功能-UI-界面

   a. 接入层：UICompBasService；

   i. 读：UICompDataLoadService

2. T\\[\\] query\\(QueryParam param\\)；

3. List&lt;T&gt; query\\(QueryParam param\\)；

4. QueryResult&lt;T&gt; query\\(QueryParam param\\)；

ii. 写：UICompDataSaveService

1. SaveResults save\\(SaveParams&lt;V&gt; records\\)；

2. void save\\(SaveParams&lt;V&gt; records\\)

3. void save\\(V\\[\\] records\\)

iii. 码名：UICompCodeNameService

iv. 初始化：UIComponentInit

v. 参数：UICompParamService

vi. 打印：UICompPrintService

vii. 用户个性：UICompUserInfoService

b. 客户端

i. 界面属性控制；







ii. 界面按钮控制；

c. 展示

```
    i. 界面定义；

    ii. XML文件（UI.xsd）；

    iii. 注：所有界面的例子；
```

d. 布局

```
    i. 单个GridTable；

    ii. 单个RecordTable；

    iii. DialogPane+GridTable；

    iv. DialogPane+RecordTable；

    v. 左右布局；

    vi. 上下布局；

    vii. Tab页面；

    viii. ProgressPane；
```



