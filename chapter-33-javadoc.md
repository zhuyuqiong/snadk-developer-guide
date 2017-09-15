# Chapter 33. JavaDoc

写文档注释时需要使用 /\*\* .... \*/ 限定。只有这种方式的注释才会生成到JavaDoc API文档中。

由JavaDoc生成的API文档是 HTML 格式，而这些 HTML 格式的标识符并不是 JavaDoc加的，而是我们在写注释的时候写上去的。所以在注释里可以加HTML标签作为样式控制。

比如，你可以用&lt;a href&gt;&lt;/a&gt;来加入超链接。需要换行时，不是敲入一个回车符，而是写入 &lt;br&gt;。如果要分段，就应该在段前写入 &lt;p&gt;。



## JavaDoc格式规范



参考Oracle官方Java编程规范：

[http://www.oracle.com/technetwork/java/codeconvtoc-136057.html](http://www.oracle.com/technetwork/java/codeconvtoc-136057.html)

