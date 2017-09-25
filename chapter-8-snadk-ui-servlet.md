# SNADK-UI-Servlet

所有远程调用在服务端经过UIInvokeServlet处理，根据请求类型调用不同的invoke方法。目前底层invoke分为以下几种：

* UI\_INVOKE：UIListener中方法调用。底层实现标准方法可以在`snsoft.ui.UIInvoke`中查看。
* SV\_INVOKE：服务组件方法调用。
* ST\_INVOKE：远程静态方法调用。
* FLOW\_INVOKE：流程调用。
* WS\_INVOKE：WS调用。

b. FileSystemServlet：文件读写；

i. DxFileSystem

ii. FtpFileSystem

iii. LocalFileSystem

