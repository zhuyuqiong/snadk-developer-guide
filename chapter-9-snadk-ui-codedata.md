# SNADK-UI-CodeData

CodeData指的是码表，是包括码表定义、辅助录入一系列功能的统称。新版底层中，我们将用于界面的码名映射和辅助录入区分开，两者各司其职，从而避免旧版中界面辅助录入列较多，导致码名映射效率不高的问题。

## 定义

CodeData定义分为文件和数据库两部分：

* 文件定义：snsoft/codedata/CoderData\*.xml
* 数据库定义：codetbl,codetbla,codetblc 一共三张表

在【开发工具-码表定义】菜单中，我们可以查询到文件定义和数据库定义合并后的码表定义结果集。并且在界面录入属性后，可以将对应属性保存到数据库中。从开发层面来说，我们要求开发使用文件定义的方式，在发布产品时，一般不会发布数据库配置。

b. 码表

i. 字典；

ii. 推荐标准：码、名两列；

c. 辅助录入

i. 参见页面：xxx；

ii. ComponentListener.itemAidInputing；

d. 动态码表

i. AidInfoService；

ii. AidInfo；

iii. AidInfoParam；

e. 相关接口：参见类图；

f. 共享界面：主界面列与共享界面列都要配置相同的码表及显示名属性；

i. 主界面：供服务端数据加载时获取名称使用；

ii. 客户端：供动态录入时获取名称使用；

```
codedata中
jmethod:服务端静态方法
service:服务组件
```



