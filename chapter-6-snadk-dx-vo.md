# SNADK-DX-VO

在与关系型数据库进行数据存取操作时，我们要求使用VO对象方式编程。通过在VO对象中标注的一系列注解，平台底层可以统一管理VO对象的事务和VO对象的数据合法性校验。

**在将VO与数据库表进行映射时，要求使用JPA注解实现。**

## JPA注解

### @Table

用于标注VO对象同数据库表的映射，`name`属性可选填写。当VO名与数据库表名不一致时必须指定，否则使用小写VO类名作为表名。

```
@Table(name = "users")
public class User extends BcodeVO
{...}
```

### @Column

用于标注VO对象的属性同数据库表列的映射关系，`name`属性可选填写。当属性名与列名不一致时必须指定，否则使用小写属性名作为列名。

```
@Column
private int     wadmin;
@Column
private Date    bedate;
```

### @Id

标识列为表的主键。

```
@Table(name = "users")
public class User extends BcodeVO
{
    @Id
    @Column
    private String    usercode;
    ...
}
```

### @OneToOne,@OneToMany,@JoinColumn

用于标识主子表关系的注解。

**OneToOne**：一对一关系（扩展表）

**OneToMany**：一对多关系（子表）

**JoinColumn**：关连列（拷贝主表字段）

JoinColumn有若干属性需要关注：name 属性标识为目标表（子表）关系字段，referencedColumnName属性标识当前表（主表）关系字段。

下面是一个表关系映射的的示例：

```
@Table(name = "decmessage")
public class DecMessage extends VO
{
    @Id
    @Column
    private String                    id;//主键
    @OneToMany
    @JoinColumn(name = "refid", referencedColumnName = "id")
    private List<DecContainerType>    decContainer;//一对多关系
    @OneToOne
    @JoinColumn(name = "id")
    private DecSupplementListType    decSupplement;//一对一关系
    ...
}
@Table(name = "deccontainer")
public class DecContainerType
{
    @Id
    @Column
    protected String        id;//主键
    @Column
    protected String        refid;//拷贝主表字段
    ...
}
@Table(name = "decsupplement")
public class DecSupplementListType
{
    @Id
    @Column
    protected String    id;//主键以及关系字段
    ...
}
```

## 其他相关注解

在实际使用中，平台目前应用到了Spring、Jackson、Xml等技术来做数据绑定。因此，与相关技术配合的一些注解需要各位开发同学了解。

### 屏蔽类注解

当我们使用VO对象同Spring-data、Jackson、Xml转换时，有些字段我们并不需要转换到相应数据结构中。此时就需要使用一些屏蔽类的注解来实现该功能。

* 屏蔽spring-data的注解：`spring.Transient`，设置在字段上
* 屏蔽Jackson的注解：`JsonIgnore`，设置在字段上及get方法上
* 屏蔽XML的注解：`XmlTransient`，设置在get方法上，同时不能出现在类注解XmlType的propOrder属性中

## Mapper：VO拷贝

在实际业务中，两个VO实体进行上下游数据拷贝是频繁出现的业务场景。目前在平台中支持通过XML定义来支撑这一场景。

### vomapper.xml定义

平台中会扫描如下目录中的xml文件，将对应配置加载到缓存中进行VO对象拷贝操作。

```
snsoft/res/vomapper/vomapper*.xml
```

#### 标签

* &lt;mapper&gt;：定义拷贝映射的实体class
* &lt;m&gt;：定义实体中字段映射关系

以上拷贝映射在定义时支持嵌套。

关于vomapper.xml的定义方式可参见列子：`vomapper_template.xml`

```
<?xml version="1.0" encoding="UTF-8"?>
<!-- 类名的全名与简写名称同等使用 -->
<mapper xmlns="http://www.snsoft.com.cn" 
        xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
        xsi:schemaLocation="http://www.snsoft.com.cn vomapper.xsd "
        fromClass="a.vo.AClass" toClass="a.appvo.BClass">
    <!-- 同名不拷贝：只定义fm -->
    <m fm="field0" />

    <!-- 同名拷贝（默认，可以不配置） -->
    <m fm="field" to="field" />

    <!-- 非同名拷贝 -->
    <m fm="field1" to="field2" />

    <!-- 码表：转换为名称 -->
    <m fm="field3" to="field3" codeDefId="#xxx" />

    <!-- 码表：转换为名称，指定分隔符分隔多值 -->
    <m fm="field4" to="field4" codeDefId="#xxx" codeDeli="," />

    <!-- 默认值：常量 -->
    <m to="field5" dftValue="1" />

    <!-- 日期、时间类默认值：参见SimpleDateFormat 将宏的返回值转换为字段的值。 -->
    <m to="field6" dftMacro="YYYY-MM-DD" />

    <!-- VO字段对应关系 -->
    <m fm="vfield1" to="vfield2">
        <mapper>
            <m fm="xx" to="yy" />
        </mapper>
    </m>

    <!-- 集合字段对应关系 -->
    <m fm="cfield1" to="cfield2">
        <mapper fromClass="a.vo.A1Class" toClass="a.appvo.B1Class">
            <!-- 子表拷贝主表字段 -->
            <m fm="AClass.field1" to="field2" />
        </mapper>
    </m>
</mapper>
```

### Mapper实现

在程序中，我们可以使用`MapperService`来实现VO对象拷贝：

```
/**
 *@param F 拷贝源VO
 *@param T 目标VO
 */
snsoft.dx.vo.convert.service.MapperService.mapper(F, T)
```

## Validation：VO校验

VO校验采用Java标准Validation方案，在需要校验的Field上打上javax.validation.constraints 中注解。

例如：

```
public class User extends BcodeVO
{
    @NotNull
    private String usercode;
    ...
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

## VO相关数据绑定

VO的数据绑定目前平台实现了如下几种方式，对应功能都可以在**帮助中心-数据功能**中找到例子。

### VO与XML转换

使用JAXB进行转换，示例参考帮助中心。如下是简单的说明：

```
//解析xml的类
org.springframework.oxm.jaxb.Jaxb2Marshaller
//解绑
Jaxb2Marshaller marshaller = new Jaxb2Marshaller();
marshaller.setClassesToBeBound(SignatureType.class);
try (InputStream in = new ClassPathResource("snsoft/convert/vomapper_signature.xml").getInputStream())
{
      Source source = new StreamSource(in);
      signatureType = (SignatureType) marshaller.unmarshal(source);
      System.out.println(signatureType);
}
DecMain decMainout = new DecMain();
mapperService.mapper(signatureType, decMainout);
//绑定
Jaxb2Marshaller marshaller = new Jaxb2Marshaller();
marshaller.setClassesToBeBound(SignatureType.class);
Result result = new StreamResult(System.out);
marshaller.marshal(signatureType, result);
```

### VO与JSON转换

平台使用Jackson框架进行json数据转换，示例参考帮助中心。如下是简单说明：

```
#解析json的类
com.fasterxml.jackson.databind.ObjectMapper

//绑定
ObjectMapper mapper = new ObjectMapper();
String json = mapper.writeValueAsString(signatureType);
```

### Excel、DBF、TXT导入转换VO



