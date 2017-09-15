# Chapter 33. JavaDoc

写文档注释时需要使用 /\*\* .... \*/ 限定。只有这种方式的注释才会生成到JavaDoc API文档中。

由JavaDoc生成的API文档是 HTML 格式，而这些 HTML 格式的标识符并不是 JavaDoc加的，而是我们在写注释的时候写上去的。所以在注释里可以加HTML标签作为样式控制。

比如，你可以用&lt;a href&gt;&lt;/a&gt;来加入超链接。需要换行时，不是敲入一个回车符，而是写入 &lt;br&gt;。如果要分段，就应该在段前写入 &lt;p&gt;。

## JavaDoc格式规范

#### Java类注释规范说明

```
@author
标明开发该类模块的作者
```

```
@version
标明该类模块的版本
```

```
@since
从以下版本开始，可以跟JDK版本，日期，无固定值
```



```
@deprecated
已过时或者废弃
```



```
    @serial
```

序列化标记，很不常用的属性，经过我对文档的初步翻译是， public或者protected类实现了Serializable就打上@serial exclude，private或者package-private类则打上@serial include（@serialField用于序列化ObjectStreamField组件，@serialData）

```
    @see
```

添加“参见”标题

参考Oracle官方Java编程规范：

[http://www.oracle.com/technetwork/java/codeconvtoc-136057.html](http://www.oracle.com/technetwork/java/codeconvtoc-136057.html)

