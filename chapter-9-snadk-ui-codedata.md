# SNADK-UI-CodeData

CodeData指的是码表，是包括码表定义、辅助录入一系列功能的统称。新版底层中，我们将用于界面的码名映射和辅助录入区分开，两者各司其职，从而避免旧版中界面辅助录入列较多，导致码名映射效率不高的问题。

而且，辅助录入和码名映射理应是两个功能，只是一般情况下会成对出现。

## 定义

CodeData定义分为文件和数据库两部分：

* 文件定义：snsoft/codedata/CoderData\*.xml
* 数据库定义：codetbl,codetbla,codetblc 一共三张表

在【开发工具-码表定义】菜单中，我们可以查询到文件定义和数据库定义合并后的码表定义结果集。并且在界面录入属性后，可以将对应属性保存到数据库中。从开发层面来说，我们要求开发使用文件定义的方式，本菜单仅用于开发速查使用。在发布产品时，一般不会发布数据库配置。

## CodeData.xsd

同所有xml格式定义一样，CodeData的定义也有其约束文件：CodeData.xsd。其中定义了xml文件中可用的元素以及其属性，开发在配置CodeData时，请严格按照约束配置。否则解析xml文件时，xsd校验是无法通过的。

？？补充元素以及属性的含义表格

### &lt;column&gt;

配置码名映射的列。该元素仅仅用于CodeData码名映射，或者一些简单码表的辅助录入列。

我们推荐这里配置：编码、名称两列。当配置列数较多时，请开发考虑使用aidinputer属性和aiprops属性指定合适的辅助录入器以及辅助录入界面定义。

## 字典

？？？

## 辅助录入

在帮助中心，我们提供了很全面的辅助录入示例，你可以参见页面：91.AidForAll，该页面列举了日期、文件、大文本、附件、分级辅助录入等常用控件。

### 客户端监听

客户端区分Table中辅助录入和DialogPane中辅助录入，一共有如下两种事件：

* TableListener.itemAidInputing
* DialogPaneListener.itemAidInputing

```
#一个改写辅助录入属性的例子
if( e.item.name=="gcode" )
{    
    xjs.ui.util.SelectCodeDialog select = (SelectCodeDialog)((xjs.ui.InputField)e.item).aidInputer;
    CodeData codeData = select.codeData;
    // CodeData codeData = (CodeData)e.item.selectOptions;//aidInputer中没有时，需要这样取codedata          
    codeData.setLoadParameter("dclass", dclass);
}
```

在itemAdiInputing事件中我们可以改写辅助录入的属性，甚至使用动态码表章节介绍的功能设置Column使用动态获取的辅助录入。

### 动态码表

有些时候业务上会要求界面上的列使用的辅助录入根据某个选项设置，甚至界面的列就是动态创建的。此时我们就会运用到动态码表的技术。动态码表相关的代码如下：

```
#客户端远程Service
xjs.ui.aid.AidInfoService
#客户端Aid工具类
xjs.ui.aid.AidInfo
xjs.ui.aid.AidInfoService.AidInfoParam
#服务端Service
snsoft.ui.aid.service.AidInfoService
#服务端实现
snsoft.ui.aid.service.impl.AidInfoServiceImpl
```

其中我们日常使用`xjs.ui.aid.AidInfo,xjs.ui.aid.AidInfoService.AidInfoParam`即可。其它类列示出来方便各位开发同学了解其实现原理。

常见的使用方式如下：

```
AidInfoParam param = new AidInfoParam("#00.users", null);
AidInfo aidInfo = AidInfo.createAidInfo(param);
if (aidInfo.aidInputer != null)//此时判断是弹出辅助录入
{
    c.setAidInputer(aidInfo.aidInputer);
}
if (aidInfo.selectOptions != null)//或者是下拉选择
{
    c.setSelectOptions(aidInfo.toCodeData());
}
```

e. 相关接口：参见类图；？？

## 界面配置

在界面配置辅助录入或码表时，我们有以下几点要求：

* 共享界面配置：主界面列与共享界面列都要配置相同的码表及显示名属性

i. 主界面：供服务端数据加载时获取名称使用？？

ii. 客户端：供动态录入时获取名称使用？？

配置文件/数据库定义的码表：

```
#00.users
```

当数据源非数据库表时，我们往往需要在服务端提供静态方法或Service来返回码表数据，此时界面配置方式为：

```
//codedata中
jmethod:服务端静态方法
service:服务组件.方法
```



