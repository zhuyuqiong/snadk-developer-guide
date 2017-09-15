# Chapter 1. Documentation

本章描述了关于SNADK Developer Guide的简介。旨在帮助你更好的理解本指南，如果对此不敢兴趣，可以跳过本章节。

## 1.1 关于

本指南使用GitBook平台开发，指南最新版可在 [https://zhuyuqiong.gitbooks.io/snadk-developer-guide/content](https://zhuyuqiong.gitbooks.io/snadk-developer-guide/content) 下载阅读。

GitBook是一款基于Markdown语法的开源Book制作平台，关于GitBook相关知识可在[https://help.gitbook.com/](https://help.gitbook.com/ "GitBook-Help") 中了解。

本指南源码托管在[https://github.com/ ](https://github.com/ "Github")上，读者可使用 git clone [https://github.com/zhuyuqiong/snadk-developer-guide.git](https://github.com/zhuyuqiong/snadk-developer-guide.git) 获取源码。

Copies of this document may be made for your own use and for distribution to others, provided that you do not charge any fee for such copies and further provided that each copy contains this Copyright Notice, whether distributed in print or electronically.

## 1.2 版本控制

**新功能的开发**和**稳定性的提高**对产品都很重要。SNADK采用如下版本开发模式保障两者。

#### 2个版本并行开发 {#2个版本并行开发}

* BugFix版本：低版本，比如4.0.x。是GA版本，线上使用的版本，只会BugFix，升级第三位版本号。
* 新功能版本：高版本，比如4.1.x。加新功能的版本，会给对新功能有需求的应用试用。

4.1.x的新功能基本稳定后，进入4.1.x试用阶段。找足够多的应用试用4.1.x版本。

在4.1.x够稳定后：

* 4.1.x成为GA版本，只BugFix，推广使用此版本。如何可行，可以推进应用在期望的时间点内升级到GA版本。
* 4.0.x不再开发，应用碰到Bug让直接升级。（称为“夕阳条款”）
* 从4.1.x拉成分支4.2.0，作为新功能开发版本。

#### 优势 {#优势}

* 保持GA版本是稳定的！因为：
  * 只会作BugFix
  * 成为GA版本前有试用阶段
* 新功能可以高版本中快速响应，并让应用能试用新功能。
* 不会版本过多，导致开发和维护成本剧增

#### 用户要配合的职责 {#用户要配合的职责}

由于开发只会BugFix GA版本，所以用户需要积极跟进升级到GA版本，以Fix发现的问题。

定期升级版本给用户带来了不安。但这是一个假命题，说明如下：

* GA经过一个试用阶段保持稳定。
* GA版本有Bug会火速Fix
* 相对出问题才升级到GA版本（可以跨了多个版本）定期升级平摊风险（类似小步快跑）。经历过周期长的大项目的同学会有这样的经历，三方库版本长时间不升级，结果出了问题不得不升级到新版本（跨了多个版本）风险巨大。

## 1.3 帮助支持

当你在使用中发现问题时，可尝试在本指南中查找说明，或在帮助中心中寻找示例。同时我们欢迎各位同学积极反馈问题，推动SNADK不断完善和进步。

