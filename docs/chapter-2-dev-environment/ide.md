## 2.1 IDE

### Eclipse

在IDE的选择上，我们仍使用eclipse作为首选，要求版本为`eclipse-neon`或以上。

开发同学可以通过以下方式获取Eclipse

```
ftp/software软件安装包/IDE集成开发环境/Eclipse/eclipse-jee-neon-R-win32-x86_64.zip
```

或者 [eclipse.org](https://www.eclipse.org/downloads/)

### CodeFormat

代码风格使用标准代码格式，主要约束 类/方法等语句块{}位置、缩进个数以及代码折行方式。

eclipse中参见如下图片位置导入标准格式，其他IDE以此为参照设置，保证整个平台代码风格统一。

![](/assets/code-format.png)

### CodeTemplate

eclipse中代码标准模版参见下图设置，主要约束类注释格式和方法注释格式，其他IDE参照标准格式设置。

> 注意：注释作者名改成自己的。

![](assets/code-template.png)

### SaveActions

IDE中存盘事件需设置自动格式化、import、自动注解。

Eclipse中参见下图设置：

![](assets/save-actions.png)

### Maven

Maven的setting在工作空间下，里面的jar包仓库按需自己指定位置。

![](assets/maven-setting.png)

注意修改文件后更新Eclipse里的Maven：

![](assets/maven-eclipse.png)

### Intellij Idea

4.0.0版本底层开始，源码中不再包含IDE相关的描述文件，只包含pom文件描述工程间依赖，因此目前源码可以支持除eclipse以外的其他IDE，有兴趣的同学可以进行尝试。

