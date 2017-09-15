# Chapter 2. 开发环境

## 基础环境要求

SNADK使用[maven](http://maven.apache.org/)作为构建工具，Eclipse作为开发工具，[Git](https://git-scm.com/)作为版本控制工具。相关工具知识可前往对应官方网站了解补充。

* Java 使用jdk1.8作为开发版本，低版本jdk与依赖中部分jar包不兼容。
* Maven 3.0或以上版本
* Git
* \*MySQL
* \*Redis
* \*Zookeeper
* \*ActiveMQ

> 注：\*号标记的为可选安装。

## 代码签出

  
@font-face{  
font-family:"Times New Roman";  
}  
  
@font-face{  
font-family:"宋体";  
}  
  
@list l0:level1{  
mso-level-number-format:decimal;  
mso-level-suffix:tab;  
mso-level-text:"%1、";  
mso-level-tab-stop:none;  
mso-level-number-position:left;  
margin-left:18.0000pt;text-indent:-18.0000pt;font-family:'Times New Roman';}  
  
@list l0:level2{  
mso-level-number-format:alpha-lower;  
mso-level-suffix:tab;  
mso-level-text:"%2\)";  
mso-level-tab-stop:none;  
mso-level-number-position:left;  
margin-left:42.0000pt;text-indent:-21.0000pt;font-family:'Times New Roman';}  
  
@list l0:level3{  
mso-level-number-format:lower-roman;  
mso-level-suffix:tab;  
mso-level-text:"%3.";  
mso-level-tab-stop:none;  
mso-level-number-position:right;  
margin-left:63.0000pt;text-indent:-21.0000pt;font-family:'Times New Roman';}  
  
@list l0:level4{  
mso-level-number-format:decimal;  
mso-level-suffix:tab;  
mso-level-text:"%4.";  
mso-level-tab-stop:none;  
mso-level-number-position:left;  
margin-left:84.0000pt;text-indent:-21.0000pt;font-family:'Times New Roman';}  
  
@list l0:level5{  
mso-level-number-format:alpha-lower;  
mso-level-suffix:tab;  
mso-level-text:"%5\)";  
mso-level-tab-stop:none;  
mso-level-number-position:left;  
margin-left:105.0000pt;text-indent:-21.0000pt;font-family:'Times New Roman';}  
  
@list l0:level6{  
mso-level-number-format:lower-roman;  
mso-level-suffix:tab;  
mso-level-text:"%6.";  
mso-level-tab-stop:none;  
mso-level-number-position:right;  
margin-left:126.0000pt;text-indent:-21.0000pt;font-family:'Times New Roman';}  
  
@list l0:level7{  
mso-level-number-format:decimal;  
mso-level-suffix:tab;  
mso-level-text:"%7.";  
mso-level-tab-stop:none;  
mso-level-number-position:left;  
margin-left:147.0000pt;text-indent:-21.0000pt;font-family:'Times New Roman';}  
  
@list l0:level8{  
mso-level-number-format:alpha-lower;  
mso-level-suffix:tab;  
mso-level-text:"%8\)";  
mso-level-tab-stop:none;  
mso-level-number-position:left;  
margin-left:168.0000pt;text-indent:-21.0000pt;font-family:'Times New Roman';}  
  
@list l0:level9{  
mso-level-number-format:lower-roman;  
mso-level-suffix:tab;  
mso-level-text:"%9.";  
mso-level-tab-stop:none;  
mso-level-number-position:right;  
margin-left:189.0000pt;text-indent:-21.0000pt;font-family:'Times New Roman';}  
  
p.MsoNormal{  
mso-style-name:正文;  
mso-style-parent:"";  
margin:0pt;  
margin-bottom:.0001pt;  
mso-pagination:none;  
text-align:justify;  
text-justify:inter-ideograph;  
line-height:150%;  
font-family:'Times New Roman';  
mso-fareast-font-family:宋体;  
font-size:12.0000pt;  
mso-font-kerning:1.0000pt;  
}  
  
p.MsoFooter{  
mso-style-name:页脚;  
mso-style-noshow:yes;  
margin:0pt;  
margin-bottom:.0001pt;  
layout-grid-mode:char;  
mso-pagination:none;  
text-align:left;  
font-family:'Times New Roman';  
mso-fareast-font-family:宋体;  
font-size:9.0000pt;  
mso-font-kerning:1.0000pt;  
}  
  
p.MsoHeader{  
mso-style-name:页眉;  
margin:0pt;  
margin-bottom:.0001pt;  
border-bottom:1.0000pt solid windowtext;  
mso-border-bottom-alt:0.7500pt solid windowtext;  
padding:0pt 0pt 1pt 0pt ;  
layout-grid-mode:char;  
mso-pagination:none;  
text-align:center;  
font-family:'Times New Roman';  
mso-fareast-font-family:宋体;  
font-size:9.0000pt;  
mso-font-kerning:1.0000pt;  
}  
  
span.msoIns{  
mso-style-type:export-only;  
mso-style-name:"";  
text-decoration:underline;  
text-underline:single;  
color:blue;  
}  
  
span.msoDel{  
mso-style-type:export-only;  
mso-style-name:"";  
text-decoration:line-through;  
color:red;  
}  
@page{mso-page-border-surround-header:no;  
	mso-page-border-surround-footer:no;}@page Section0{  
}  
div.Section0{page:Section0;}

1、底层源文件目录：D:\snsoft90；

创建上述目录通过以下地址可以签出SNADK最新源码：

```
git clone snsoftadk:snsoft_adk.git
```

## 分支

我们使用 master 作为主干版本的开发，使用分支作为维护版本。

可以通过？？来查看所有版本的标签。

