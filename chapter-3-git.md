# Chapter 3. Git

Git是一个分布式版本控制工具，它的主要特性在于：

* 区分本地仓库和远程仓库，每一处都是完整的独立副本。

  因此在操作上会区分commit（提交到本地仓库）和push（提交远程仓库）

* 基于branch和merge模型设计  
   Git官方鼓励我们建立本地branch，基于本地branch开发完成后合并至master。在push远程仓库时，只需要处理master即可，不需要将本地branch全部退给远程仓库。

* 体积小、性能高

* 分布式，每一处都是完整的代码副本

* 基于工作区操作

* 开源免费

Git官方有一个操作教程，有兴趣的同学可以体验一下shell方式的操作过程：[Try Git](https://try.github.io/)。

## 安装Git

在如下地址下载Git工具后安装：

[https://git-scm.com/downloads](https://git-scm.com/downloads)

或`ftp/software软件安装包/Git和Svn/Git/`

安装完成后，右键菜单中选择 Git Bash 生成ssh密钥（用于同远程仓库验证）

在shell中输入：

```
ssh-keygen -t rsa -C "你的名字@snsoft.com.cn"
```

注意需要将命令中的邮箱替换为你的邮箱，执行完成后会在你的Windows用户文件夹下生成`.ssh`文件夹。里面是公钥和私钥文件如下：

```
id_rsa
id_rsa.pub
```

同时需要将公司提供的`known_hosts` 文件和`config` 文件拷贝到`.ssh` 文件夹下。

config文件内容：

```
Host "sino"
HostName "git.sino-clink.com.cn"
User "git"
IdentityFile "~/.ssh/sino_rsa"

Host "snsoftadk"
HostName "adk-git.sino-clink.com.cn"
User "git"
IdentityFile "~/.ssh/sino_rsa"
```

可以看到，config文件中用于标识身份验证的文件名为 `sinorsa`，因此需要将刚刚生成的两个密钥文件改为`sino_rsa,sino_rsa.pub`

同时将公钥`sino_rsa.pub` 复制一份重命名为`你的名字@snsoft.com.cn.pub`，这个文件需要发送给相关人员开通权限。

## 安装Git GUI工具

在如下地址下载Git可视化工具安装：

[https://git-scm.com/downloads/guis](https://git-scm.com/downloads/guis)或公司FTP `ftp/software软件安装包/Git和Svn/Git/`

windows下Git可视化工具主要选择有以下几种：

* SourceTree
* TortoiseGit
* Eclipse插件

我们推荐使用SourceTree或者Eclipse自带插件。

### SourceTree设置

SoucreTree中菜单选择`工具-选项`

在选项中需要配置**用户全名、用户邮箱和SSH密钥文件路径。**

SSH客户端选择**OpenSSH**

> 注意：需要设置提交人员的简体名称

### SourceTree使用

首选要克隆一个远程仓库到本地。这里需要设置远程仓库的URL以及本地仓库的存放路径。

克隆完成后，你就得到了一个本地仓库。其中：

* 文件状态：展示本地文件修改清单

* 分支：展示本地仓库所有分支

* 远程：展示远程仓库所有分支

* 右侧列表则展示当前分支的操作日志

### Eclipse自带插件

Eclipse插件主要使用两个视图 Git Staging 和 Git Repositories

* Git Staging：文件状态展示、Commit操作
* Git Repositories：仓库展示、Push操作

> 注意：需要设置提交人员的简体名称

### 操作步骤

暂存-提交-推送-拉取；

