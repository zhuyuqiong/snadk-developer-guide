## 工程

### 工程的标准结构

一个标准结构的模块应当分为：

1. 服务组件，用于提供各种Service以及实现，包括xxx-api和xxx-impl。根据需要可以合并为一个。
2. UI组件，用于同客户端交互、界面展示等，包括xxx-ui。根据需要可以没有。
3. js组件，用于实现客户端js，包括xxx-xjs。根据需要可以没有。

### 工作空间

目前提供的标准eclipse workspace位置如下：

```
ftp/开发环境/底层workspace/snsoft_adk_ws2.zip
```

解压缩到目录：`D:\snsoft90`下，改名为`snsoft_adk_ws`

### 导入Maven工程

Maven工程下仅存在pom.xml文件和src目录。不在包含eclipse的.project和.classpath等工程描述文件。目前SNADK相关工程是按照功能划分多个组件，每个组件下划分多个模块：

```
#SNADK
.
|—— snadk-core     //核心组件
|    |—— snadk-bas     //基础服务
|    |—— snadk-bpm     //工作流程
|    |—— snadk-dx     //数据服务
|    └── snadk-util     //util工程
|── snadk-dubbo     //dubbo服务注册和调用
|—— snadk-sso     //登陆
|—— snadk-ui     //UI组件
|    |—— snadk-ui     //界面展示、请求调度
|    └── snadk-prt     //打印服务
|—— snadk-approval     //审批流程
|—— snadk-cmc     //管控中心
|—— snadk-help     //帮助中心
|—— snadk-cli     //webstart客户端
|    |—— snadk-cli-app     
|    |—— snadk-cli-launcher
|    |—— snadk-cli-tools
└── snadk-xjs     //js客户端

#java2js     //js编译
.
└── snadk-tools     //辅助工具
     |—— snadk-jparser     //java解析
     └── snadk-java2js     //js转换
```

### 生成工程

目前工程只需要pom.xml和src目录，因此只需复制`snadk-blank`中内容，修改pom.xml文件为新工程名称和依赖后，导入WorkSpace即可。

