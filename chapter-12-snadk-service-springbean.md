# Chapter 12. SNADK-SERVICE-SpringBean



a. 暴露服务：SpringBean注解（在接口上）；

b. 普通服务：spring.Service注解（在实现上），DAO层使用spring.Repository；

c. 远程服务：Remoteable注解（接口类或接口方法上）

d. 注入：

i. 自动类型匹配：AutoWired；

ii. 指定名称：Resource；

iii. 动态获取：SpringBeanUtil.getBeanByName\\(\\)（底层有些服务提供factory或impl可以直接使用）；

