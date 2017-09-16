# Chapter 3. Git

Git是一个基于命令行操作的分布式版本控制工具，它的主要特性在于：

* 区分本地仓库和远程仓库，每一处都是完整的独立副本。

        因此在操作上会区分commit（提交到本地仓库）和push（提交远程仓库）

* 基于branch和merge模型设计
   Git官方鼓励我们建立本地branch，基于本地branch开发完成后合并至master。在push远程仓库时，只需要处理master即可，不需要将本地branch全部退给远程仓库。
* 体积小、性能高
* 分布式，每一处都是完整的代码副本
* 基于工作区操作
* 开源免费

 



## 安装Git









a. Git；

b. 客户端（自行选择，使用其一）

i. SourceTree；

1. 需要设置提交人员的简体名称；

ii. Eclipse自带插件；

1. 需要设置提交人员的简体名称；

c. 账号的设置；

d. 操作步骤：暂存-提交-推送-拉取；

1、Git相关（ftp/software软件安装包/Git和Svn/Git/）：

a\)Git-2.8.2-64-bit.exe；

b\)TortoiseGit-2.2.0.0-64bit.msi或SourceTreeSetup\_1.9.5.0.exe；

在指定的ftp目录下找到上述安装包，依次按步骤顺序安装Git，步骤b\)中的可视化软件可选择性安装。稍后的Git用户相关配置由相关人员配置。

Git使用文档：【ftp/software软件安装包/Git和Svn/Git/git使用手册.docx】

