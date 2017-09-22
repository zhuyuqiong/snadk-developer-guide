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
|—— snadk-core
|    |—— snadk-bas
|    |—— snadk-bpm
|    |—— snadk-dx
|    └── snadk-util
|── snadk-dubbo
|—— snadk-sso
|—— snadk-ui
|    |—— snadk-ui
|    └── snadk-prt
|—— snadk-approval
|—— snadk-cmc
|—— snadk-cli
|    |—— snadk-cli-app
|    |—— snadk-cli-launcher
|    |—— snadk-cli-tools
└── snadk-xjs

#java2js
.
└── snadk-tools
     |—— snadk-jparser
     └── snadk-java2js
```

### 生成工程



