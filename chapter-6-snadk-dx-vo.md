# SNADK-DX-VO

a. JPA注解

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

c. Mapper：VO拷贝；

d. Validation：VO校验；

e. JAXB：XML与Schema，VO与XML转换；

f. Jackson：VO与JSON转换；

g. Excel、DBF、TXT导入转换VO；

