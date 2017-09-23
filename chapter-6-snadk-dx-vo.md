# SNADK-DX-VO

在与关系型数据库进行数据存取操作时，我们要求使用VO对象方式编程。通过在VO对象中标注的一系列注解，平台底层可以统一管理VO对象的事务和VO对象的数据合法性校验。

## JPA注解

i. Table：表名

ii. Column：列

iii. Id：主键

iv. OneToOne：一对一关系（扩展表）

v. OneToMany：一对多关系（子表）

vi. JoinColumn：关连列（拷贝主表字段）

b. 相关注解

i. 屏蔽spring-data的注解：spring.Transient，设置在字段上；

ii. 屏蔽Jackson的注解：JsonIgnore，设置在字段上及get方法上；

iii. 屏蔽XML的注解：XmlTransient，设置在get方法上，同时不能出现在类注解XmlType的propOrder属性中；

## Mapper：VO拷贝

```
snsoft/res/vomapper/vomapper*.xml
```

## Validation：VO校验

VO校验采用Java标准Validation方案，在需要校验的Field上打上javax.validation.constraints 中注解。

例如：

```
public class User extends BcodeVO
{
    @NotNull
    private String usercode;
}
```

注解校验的实现方法可参见

```
#Service
snsoft.dx.vo.validate.service.ValidateService
#以及其实现类
snsoft.dx.vo.validate.service.impl.ValidateServiceImpl
#测试类
snsoftx.test.adk.validation.ValidationTest
```

e. JAXB：XML与Schema，VO与XML转换；

f. Jackson：VO与JSON转换；

g. Excel、DBF、TXT导入转换VO；

