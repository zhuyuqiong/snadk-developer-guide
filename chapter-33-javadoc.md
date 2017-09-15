# Chapter 33. JavaDoc

写文档注释时需要使用 /\*\* .... \*/ 限定。只有这种方式的注释才会生成到JavaDoc API文档中。

由JavaDoc生成的API文档是 HTML 格式，而这些 HTML 格式的标识符并不是 JavaDoc加的，而是我们在写注释的时候写上去的。所以在注释里可以加HTML标签作为样式控制。

比如，你可以用&lt;a href&gt;&lt;/a&gt;来加入超链接。需要换行时，不是敲入一个回车符，而是写入 &lt;br&gt;。如果要分段，就应该在段前写入 &lt;p&gt;。

## JavaDoc格式规范

### Java类注释规范说明

标明开发该类模块的作者：

`@author`

标明该类模块的版本：

`@version`

从以下版本开始，可以跟JDK版本，日期，无固定值：

`@since`

已过时或者废弃：

`@deprecated`

序列化标记，很不常用的属性：

> 经过我对文档的初步翻译是：public或者protected类实现了Serializable就打上@serial exclude
>
> private或者package-private类则打上@serial include（@serialField用于序列化ObjectStreamField组件，@serialData）

`@serial`

添加“参见”标题：

`@see`

```java
    /**
     * @see 这是一个注释
     * @see <a href="www.baidu.com">这是一个超链接</a>
     * @see java.lang.String#toString() 这是个方法链接
     * @see #hashCode() 这是个方法链接（当前类可以省略）
     * @see Snake 这是个类链接(同包的类可以省略)
     */
    public void test();
```

用于生成html文档根目录：

`{@docRoot}`

### Java方法注释规范说明

可以用于生成被标记的常量字段的值：

`{@value}`

##### 直接用于常量字段

```java
    /**
     * 默认表名，值为{@value}
     */
    public static final String TBLNAME = "model";
```

生成之后：

```
String org.springframework.samples.websocket.snake.SnakeUtils.TBLNAME : "model"

默认表名，值为"model"
```

##### 用于引用的方式

```java
    /**
     * 
     * @return 返回表名：{@value #TBLNAME}
     */
    public String testJavaDoc();
```

生成之后：

```java
String org.springframework.samples.websocket.snake.SnakeUtils.testJavaDoc()

Returns:返回表名："model"
```

接口中的注释在实现类中自动继承：

`{@inheritDoc}`

作用是一样的，生成的文档样式不一样，后一个会好看一点，可以加类连接：

`{@link}，{@linkplain}`

用于显示原始输入样式：

`<pre>`

意义完全一样，官方解释说throws更符合语法：

`@throws，@exception`

方法的参数说明：

`@param`

对函数返回值的注释：

`@return`

用于表示计算机源代码或者其他机器可以阅读的文本内容：

> 类似于html&lt;code&gt;标签，用于表示计算机源代码或者其他机器可以阅读的文本内容。该标签等同于&lt;code&gt;{@literal}&lt;/code&gt;里面可以直接过滤掉HTML的标签，可在这个代码块里面的text部分，可以直接书写代码，即使使用了&lt;b&gt;Hello&lt;/b&gt;，在HTML里面也不会识别成为加粗的Hello，而还是原来的代码段&lt;b&gt;Hello&lt;/b&gt;的格式输出以不用&lt;和&gt;来显示（&lt;和&gt;）

`{@code}`

用于解析特定字符（&lt;,&gt;）：

`{@literal}`

@see

参见对类说明

{@docRoot}

## 参考文档

Oracle官方Java编程规范：[http://www.oracle.com/technetwork/java/codeconvtoc-136057.html](http://www.oracle.com/technetwork/java/codeconvtoc-136057.html)

[http://88250.b3log.org/when-the-little-things-count-javadoc](http://88250.b3log.org/when-the-little-things-count-javadoc)

