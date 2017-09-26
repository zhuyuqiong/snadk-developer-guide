# SNADK-UI-Servlet

本章节主要介绍一下同日常开发密切相关的平台层常用Sevlet，以及其对应业务场景的使用方法。

## UIInvokeServlet

所有远程调用在服务端经过UIInvokeServlet处理，根据请求类型调用不同的invoke方法。目前底层invoke分为以下几种：

* UI\_INVOKE：UIListener中方法调用。
* SV\_INVOKE：服务组件方法调用。
* ST\_INVOKE：远程静态方法调用。
* FLOW\_INVOKE：流程调用。
* WS\_INVOKE：WS调用。

本章节仅对几种调用方法做简单介绍，实际应用中，调用方式可以更加灵活。更详细的规范需参见**帮助中心-远程方法调用**菜单的示例。

### UI\_INVOKE

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

#服务端UI监听
public class RInvokeDemoUIListener extends snsoft.ui.DefaultUIListener 
{
    public static String echo(UIEvent event,String value)
    {
        return "RInvokeDemoUIListener.echo:"+value;
    }

    static public String progInvoke(UIEvent event,int count)
    {
        UserSession userSession = UserSession.factory.getUserSession();
        Progress progress = userSession.getRunProgress();                    //服务端进度条！！
        System.out.println("调用RInvokeDemoUIListener.progInvoke。。。。");
        progress.setProgressTitle("TestUIInvoke.progInvoke。。。。", null);
        for(int i=0;i<count;i++)
        {
            progress.addProgressMessage("Step "+i);
            progress.setProgress("setp-"+i, i+1, count);
            try { Thread.sleep(500);} catch( Throwable ex){}
        }
        return "RInvokeDemoUIListener.progInvoke:count="+count;
    }
}
```

### SV\_INVOKE

此类型是服务组件方法调用，该类型是目前推广使用的远程请求方式。这种调用方式将客户端调用和服务端Service的绑定定义在客户端Service上。这样就实现一处修改，处处生效的效果。

该类型使用的标准方式如下：

```
 //1.服务端定义Service interface
 @Remotable//与方法注解选择其一
 @SpringBean(name="SN.HELP.TestService",...)
 public interface snsoft.demo.service.TestService {
           @Remotable//与类注解选择其一
           public String echo(String text);
 }
 //2.服务端实现Service
 public class snsoft.demo.service.impl.TestServiceImpl implements  snsoft.demo.service.TestService{
           public String echo(String text){...}
 }
 //3.客户端js中定义
 @js.JSCode(remoteBean="SN.HELP.TestService")
 public interface TestService {
       public String echo(String text);
}
 //4.客户端调用
 TestService s = RInvoke.newBean(TestService.class);
 s.echo("abc");
```

### ST\_INVOKE

远程静态方法调用，该类型调用不推荐开发使用。因其需要按字符串方式声明调用方法的全路径，导致后期修改以及阅读维护代码十分困难。

改类型使用标准方法如下：

b. FileSystemServlet：文件读写；

i. DxFileSystem

ii. FtpFileSystem

iii. LocalFileSystem

