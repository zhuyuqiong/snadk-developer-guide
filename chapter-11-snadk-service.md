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


c. 远程服务：Remoteable注解（接口类或接口方法上）

d. 注入：

i. 自动类型匹配：AutoWired；

ii. 指定名称：Resource；

iii. 动态获取：SpringBeanUtil.getBeanByName\\(\\)（底层有些服务提供factory或impl可以直接使用）；

a. 默认的接口DataAccessService\(DefaultDataAccessService\)（仅供参考）；





