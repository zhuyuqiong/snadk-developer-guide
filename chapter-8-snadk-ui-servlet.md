# SNADK-UI-Servlet

所有远程调用在服务端经过UIInvokeServlet处理，根据请求类型调用不同的invoke方法。目前底层invoke分为以下几种：

* UI\_INVOKE：UIListener中方法调用。
* SV\_INVOKE：服务组件方法调用。
* ST\_INVOKE：远程静态方法调用。
* FLOW\_INVOKE：流程调用。
* WS\_INVOKE：WS调用。

本章节仅对几种调用方法做简单介绍，实际应用中，调用方式可以更加灵活。更详细的规范需参见**帮助中心-远程方法调用**菜单的示例。

## UI\_INVOKE

客户端请求使用底层实现标准方法可以在`snsoft.ui.UIInvoke`中查看。

该类型调用来自客户端使用Component中uiinvoke方法的远程请求，示例如下：

```
#普通方式
comp.uiInvoke("echo", "[ABC123]");
#进度条方式
ProgressParam pm = new ProgressParam();
pm.title = "调用UI层RInvokeDemoUIListener方法progInvoke";
pm.runMethod = "progInvoke";
pm.options = 1 | 2;
comp.uiInvoke(pm, 6);
```

b. FileSystemServlet：文件读写；

i. DxFileSystem

ii. FtpFileSystem

iii. LocalFileSystem

