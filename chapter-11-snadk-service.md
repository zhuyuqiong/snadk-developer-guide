# SNADK-Service

在平台MVC架构中，Controller由Servlet统一实现，而业务逻辑则由Service层实现。

## Service

声明一个Service组件都通过注解实现，目前平台提供了两个注解：  
    1. SpringBean  
    2. org.springframework.stereotype.Service

### SpringBean

当一个Service需要对外暴露时使用SpringBean注解，打了该注解的Service接口对应实现会通过dubbo对外发布，在调用方调用时随机选取服务提供方。  
该注解打在interface上。

### spring.Service

当一个Service不需要对外暴露，仅仅在用于本地服务调用时使用Service注解。  
该注解打在实现上。

## DAO层

DAO层也需要使用注解来标记服务组件，平台提供spring.Repository注解实现DAO层的Bean注入。  
该注解打在DAO实现上。

```
org.springframework.stereotype.Repository
```

## 远程服务

针对客户端调用服务端的远程调用服务，不仅要注解Service，平台还提供Remoteable注解实现。

该注解打在接口或接口方法上。

## Bean注入

**Bean自动注入**可以使用Spring标准注入方式：

* 自动类型匹配：AutoWired
* 指定名称：Resource

建议注入第三方Bean时可以使用AutoWired，而注入业务层Bean时，都按照Resource指定名称的方式实现。

**Bean动态获取**

有时我们会遇到某些Bean不能自动注入的情况，此时可以通过`SpringBeanUtil.getBeanByName`方式按照名字获取Bean。

而底层有些服务在interface中提供了factory或impl，可以直接使用，不需要注入Bean。

