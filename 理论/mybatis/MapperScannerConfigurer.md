# MapperScannerConfigurer



在单独使用mybatis框架的时候，在mybatis-config.xml文件中有一个配置是：

```
<mappers>...</mappers>
```

mappers标签的作用：为了让mybatis找到mapper.xml文件。

在ssm整合后，有两种方式可以代替它：

一个是使用MapperScannerConfigurer：MapperScannerConfigurer可以自动扫描到和接口同包同名的mapper.xml文件

一个是使用mapperLocation属性（位于SqlSessionFactoryBean中）:mapperLocation属性，主要用于指定mapper.xml文件所处的位置。



### MapperScannerConfigurer详解：

MapperScannerConfigurer是spring和mybatis整合的mybatis-spring的jar包中提供的一个类。也就是说MapperScannerConfigurer是位于spring和mybatis整合包里的东西，而不是mybatis中的东西。

```xml
<bean class="org.mybatis.spring.mapper.MapperScannerConfigurer">
	<property name="basePackage" value="org.mybatis.spring.sample.mapper" />
</bean>
```

这段配置的作用是：扫描org.mybatis.spring.sample.mapper下的所有接口以及所有mapper.xml文件（前提是mapper.xml与接口同包并且与接口同名），然后创建各自接口的动态代理类（也就是接口的代理实现类），然后创建代理实现类的对象，并将这些代理实现类的对象注入spring容器中。

