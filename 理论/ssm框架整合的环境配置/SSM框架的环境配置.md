# SSM框架整合的环境配置：

## 1. 添加依赖：

（1） mysql 驱动  

```
<!-- MySQL 数据库连接驱动 -->
<dependency>
<groupId>mysql</groupId>
<artifactId>mysql-connector-java</artifactId>
<version>5.1.43</version>
</dependency>  
```

（2） JDBC 数据源连接池： Druid  

```
<!-- JDBC 数据源连接池 -->
<dependency>
<groupId>com.alibaba</groupId>
<artifactId>druid</artifactId>
<version>1.1.1</version>
</dependency>
```

（3） Mybatis 框架依赖  

```
<!-- MyBatis 框架依赖 -->
<dependency>
<groupId>org.mybatis</groupId>
<artifactId>mybatis</artifactId>
<version>3.4.1</version>
</dependency>
```

（4） Spring 相关依赖配置  

```
<!-- Spring 框架依赖的 JAR 配置 -->
<dependency>
<groupId>org.springframework</groupId>
<artifactId>spring-context</artifactId>
<version>4.3.9.RELEASE</version>
</dependency>
<dependency>
<groupId>org.springframework</groupId>
<artifactId>spring-aop</artifactId>
<version>4.3.9.RELEASE</version>
</dependency>
<dependency>
<groupId>org.springframework</groupId>
<artifactId>spring-core</artifactId>
<version>4.3.9.RELEASE</version>
</dependency>
<dependency>
<groupId>org.springframework</groupId>
<artifactId>spring-beans</artifactId>
<version>4.3.9.RELEASE</version>
</dependency>
<dependency>
<groupId>org.springframework</groupId>
<artifactId>spring-jdbc</artifactId>
<version>4.3.9.RELEASE</version>
</dependency>
<dependency>
<groupId>org.springframework</groupId>
<artifactId>spring-tx</artifactId>
<version>4.3.9.RELEASE</version>
</dependency>
<dependency>
<groupId>org.springframework</groupId>
<artifactId>spring-web</artifactId>
<version>4.3.9.RELEASE</version>
</dependency>
<dependency>
<groupId>org.springframework</groupId>
<artifactId>spring-webmvc</artifactId>
<version>4.3.9.RELEASE</version>
</dependency>
<dependency>
<groupId>org.springframework</groupId>
<artifactId>spring-oxm</artifactId>
<version>4.3.9.RELEASE</version>
</dependency>
```

（5） Spring AOP 依赖  

```
<!-- Spring AOP 支持-->
<dependency>
<groupId>org.aspectj</groupId>
<artifactId>aspectjweaver</artifactId>
<version>1.8.9</version>
</dependency>
```

（6） Mybatis 与 Spring 整合依赖  

```
<!-- MyBatis 与 Spring 整合依赖 -->
<dependency>
<groupId>org.mybatis</groupId>
<artifactId>mybatis-spring</artifactId>
<version>1.3.0</version>
</dependency>
```

（7） 添加项目对 JSP 的支持  

```
<!-- servlet 及 jstl 标签库依赖的 JAR 配置 -->
<dependency>
<groupId>javax.servlet</groupId>
<artifactId>javax.servlet-api</artifactId>
<version>3.1.0</version>
</dependency>
<dependency>
<groupId>javax.servlet.jsp.jstl</groupId>
<artifactId>jstl-api</artifactId>
<version>1.2</version>
</dependency>
<dependency>
<groupId>org.apache.taglibs</groupId>
<artifactId>taglibs-standard-spec</artifactId>
<version>1.2.1</version>
</dependency>
<dependency>
<groupId>org.apache.taglibs</groupId>
<artifactId>taglibs-standard-impl</artifactId>
<version>1.2.1</version>
</dependency>
```

（8） Jackson 插件依赖  （给Springmvc用的。Jackson可以将Java对象转成Json字符串）

```
<!-- 加载 jackson 插件依赖 -->
<dependency>
<groupId>com.fasterxml.jackson.core</groupId>
<artifactId>jackson-core</artifactId>
<version>2.7.3</version>
</dependency>
<dependency>
<groupId>com.fasterxml.jackson.core</groupId>
<artifactId>jackson-databind</artifactId>
<version>2.7.3</version>
</dependency>
<dependency>
<groupId>com.fasterxml.jackson.core</groupId>
<artifactId>jackson-annotations</artifactId>
<version>2.7.3</version>
</dependency>
```

（9） poi 依赖  （用于java操作办公文件，如：word，excel，pdf等。因为java的IO流只能操作文本文件，不能操作办公文件）

```
<!--poi 依赖-->
<dependency>
<groupId>org.apache.poi</groupId>
<artifactId>poi</artifactId>
<version>3.15</version>
</dependency>  
```

（10） fileupload 依赖  

```
<!-- 文件上传 -->
<dependency>
<groupId>commons-fileupload</groupId>
<artifactId>commons-fileupload</artifactId>
<version>1.3.1</version>
</dependency>
```

（11） Log4j 依赖  （用于查看操作日志）

```
<!-- Log4j2 依赖的 JAR 配置 -->
<dependency>
<groupId>org.apache.logging.log4j</groupId>
<artifactId>log4j-api</artifactId>
<version>2.3</version>
</dependency>
<dependency>
<groupId>org.apache.logging.log4j</groupId>
<artifactId>log4j-core</artifactId>
<version>2.3</version>
</dependency>
```



## 2.添加相关配置  

### （1） MyBatis 配置  

mybatis-config.xml： 

```
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
"http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
<settings>
<setting name="logImpl" value="STDOUT_LOGGING"/>
</settings>
<typeAliases>
<package name="com.bjpowernode.crm.model"/>
</typeAliases>

<!--这个配置的作用是配置xxxmapper.xml的位置，好让框架找到xxxmapper.xml-->
<mappers>            
<package name="com.bjpowernode.crm.mapper"/>
</mappers>

</configuration>
```

### （2） 配置数据连接和事务  

applicationContext-datasource.xml：

```java
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
xmlns:aop="http://www.springframework.org/schema/aop"
xmlns:context="http://www.springframework.org/schema/context"
xmlns:tx="http://www.springframework.org/schema/tx"
xsi:schemaLocation="http://www.springframework.org/schema/beans
http://www.springframework.org/schema/beans/spring-beans.xsd
http://www.springframework.org/schema/context
http://www.springframework.org/schema/context/spring-context-4.3.xsd
http://www.springframework.org/schema/aop http://www.springframework.org/schema/aop/spring-aop-4.3.xsd
http://www.springframework.org/schema/tx http://www.springframework.org/schema/tx/spring-tx-4.3.xsd">
<!-- 配置数据源 -->
<bean id="dataSource" class="org.springframework.jdbc.datasource.DriverManagerDataSource">
<property name="driverClassName" value="com.mysql.jdbc.Driver"/>
<property name="username" value="root"/>
<property name="password" value="123456"/>
<property name="url"
value="jdbc:mysql://192.168.223.133:3306/crm_db?useSSL=false&amp;useUnicode=true&amp;characterEncoding=UTF-8"/>
</bean>
<!-- 配置 SqlSessionFactory -->
<bean id="sqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean">
<!-- 必须注入属性 dataSource -->
<property name="dataSource" ref="dataSource"/>
<!-- 如果 mybatis 没有特殊的配置(比如别名等)， configLocation 可以省去 ;否则， 不能省略-->
<property name="configLocation" value="classpath:mybatis-config.xml"/>
</bean>
<!-- mapper 注解扫描器配置,扫描@MapperScan 注解,自动生成代码对象 -->
<bean id="mapperScanner" class="org.mybatis.spring.mapper.MapperScannerConfigurer">
<property name="basePackage" value="com.bjpowernode.crm.mapper"/>
<property name="sqlSessionFactoryBeanName" value="sqlSessionFactory"/>
</bean>
<!-- 配置事务管理器 -->
<bean id="transactionManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
<property name="dataSource" ref="dataSource"/>
</bean>
<!-- 配置事务 -->
<aop:config>
<aop:pointcut expression="execution(* com.bjpowernode.crm..service.*.*(..))" id="allMethodPointcut"/>
<aop:advisor advice-ref="txAdvice" pointcut-ref="allMethodPointcut"/>
</aop:config>
<tx:advice id="txAdvice" transaction-manager="transactionManager">
<tx:attributes>
<tx:method name="add*" propagation="REQUIRED" rollback-for="Exception"/>
<tx:method name="save*" propagation="REQUIRED" rollback-for="Exception"/>
<tx:method name="edit*" propagation="REQUIRED" rollback-for="Exception"/>
<tx:method name="update*" propagation="REQUIRED" rollback-for="Exception"/>
<tx:method name="delete*" propagation="REQUIRED" rollback-for="Exception"/>
<tx:method name="do*" propagation="REQUIRED" rollback-for="Exception"/>
<tx:method name="*" propagation="REQUIRED" read-only="true"/>
</tx:attributes>
</tx:advice>
</beans>
```

### （3） springmvc 配置  

applicationContext-mvc.xml：

```
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
xmlns:context="http://www.springframework.org/schema/context"
xmlns:p="http://www.springframework.org/schema/p"
xmlns:util="http://www.springframework.org/schema/util"
xmlns:aop="http://www.springframework.org/schema/aop"
xmlns:tx="http://www.springframework.org/schema/tx"
xmlns:mvc="http://www.springframework.org/schema/mvc"
xsi:schemaLocation="
http://www.springframework.org/schema/beans
http://www.springframework.org/schema/beans/spring-beans.xsd
http://www.springframework.org/schema/context
http://www.springframework.org/schema/context/spring-context.xsd
http://www.springframework.org/schema/tx
http://www.springframework.org/schema/tx/spring-tx.xsd
http://www.springframework.org/schema/aop
http://www.springframework.org/schema/aop/spring-aop.xsd
http://www.springframework.org/schema/mvc
http://www.springframework.org/schema/mvc/spring-mvc.xsd
http://www.springframework.org/schema/util
http://www.springframework.org/schema/util/spring-util.xsd">
<!-- dispatcherServlet截获所有URL请求，如果是对静态资源的请求，就将请求交给web容器 -->
<mvc:default-servlet-handler />
<!-- spring mvc 扫描包下的controller，只扫描controller包是因为只想把controller包下的component放入springmvc容器中。-->
<context:component-scan base-package="com.bjpowernode.crm.web.controller"/>
<!-- 配置注解驱动 -->
<mvc:annotation-driven/>
<!-- 配置视图解析器 -->
<bean id="viewResolver"
class="org.springframework.web.servlet.view.InternalResourceViewResolver">
<property name="prefix" value="/WEB-INF/pages/"/>
<property name="suffix" value=".jsp"/>
</bean>
<!-- 配置文件上传解析器 id:必须是multipartResolver-->
<!--<bean id="multipartResolver" class="org.springframework.web.multipart.commons.CommonsMultipartResolver">
    <property name="maxUploadSize" value="#{1024*1024*80}"/>
    <property name="defaultEncoding" value="utf-8"/>
</bean>-->
</beans>
```

### （4） spring 总配置文件

applicationContext.xml：

```
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
xmlns:context="http://www.springframework.org/schema/context"
xmlns:p="http://www.springframework.org/schema/p"
xmlns:aop="http://www.springframework.org/schema/aop"
xmlns:tx="http://www.springframework.org/schema/tx"
xmlns:task="http://www.springframework.org/schema/task"
xsi:schemaLocation="
http://www.springframework.org/schema/beans
http://www.springframework.org/schema/beans/spring-beans.xsd
http://www.springframework.org/schema/context
http://www.springframework.org/schema/context/spring-context.xsd
http://www.springframework.org/schema/tx
http://www.springframework.org/schema/tx/spring-tx.xsd
http://www.springframework.org/schema/aop
http://www.springframework.org/schema/aop/spring-aop.xsd">
<!-- 加载系统配置文件
<context:property-placeholder location="classpath:*.properties" />-->
<!-- 扫描注解 这里只扫描service包，因为controller包是由springmvc容器扫描，不用spring容器扫描。 -->
<context:component-scan base-package="com.bjpowernode.crm.service" />
<!-- 导入数据相关配置 -->
<import resource="applicationContext-datasource.xml" />
</beans>
```

### （5） web.xml 配置  （web.xml是web项目的核心配置文件，web.xml是web项目的标志，看一个项目是不是web项目，就看有没有web.xml文件）

项目一启动，就会加载web.xml。其它配置文件(如：spring总配置文件、springmvc配置文件)是因为加载了web.xml而被加载的。

```
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xmlns="http://java.sun.com/xml/ns/javaee"
         xsi:schemaLocation="http://java.sun.com/xml/ns/javaee
http://java.sun.com/xml/ns/javaee/web-app_3_0.xsd"
         id="dataservice" version="3.0">
  <display-name>dataservice application</display-name>
  <!-- spring监听器加载applicationContext.xml配置文件 -->
  <context-param>
    <param-name>contextConfigLocation</param-name>
    <param-value>classpath:applicationContext.xml</param-value>   <!-- 加载spring总配置文件 -->
  </context-param>
  <listener>
    <listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
  </listener>
  <!-- spring字符过滤器 -->
  <filter>
    <filter-name>encodingFilter</filter-name>
    <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
    <init-param>
      <param-name>encoding</param-name>
      <param-value>UTF-8</param-value>
    </init-param>
  </filter>
  <filter-mapping>
    <filter-name>encodingFilter</filter-name>
    <url-pattern>/*</url-pattern>
  </filter-mapping>
  <!-- Spring mvc分发servlet -->
  <servlet>
    <servlet-name>dispatcher</servlet-name>
    <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
    <init-param>
      <param-name>contextConfigLocation</param-name>
      <param-value>classpath:applicationContext-mvc.xml</param-value>  <!-- 加载springmvc配置文件 -->
    </init-param>
    <load-on-startup>1</load-on-startup>
  </servlet>
  <servlet-mapping>
    <servlet-name>dispatcher</servlet-name>
    <url-pattern>/</url-pattern>
  </servlet-mapping>
  <servlet-mapping>
    <servlet-name>dispatcher</servlet-name>
    <url-pattern>*.do</url-pattern>
  </servlet-mapping>
  <!-- 欢迎页，默认进入index controller -->
  <welcome-file-list>
  
  	<!-- 配置了这个之后，以后地址栏上只打项目名(项目名后面如果没有跟任何东西)，在点击回车的时候，会自动在项目名后面加上/。请	求的是: ip地址/项目名/
    比如：输入http://127.0.0.1/crm，点击回车，地址栏会变成：http://127.0.0.1/crm/，然后发送请求。 也就是说请求的是		http://127.0.0.1/crm/ -->
  	 
  	<welcome-file>/</welcome-file>     
  	
  </welcome-file-list>
</web-app>

```

### （6） 设置 maven 对配置文件进行编译。(因为maven默认只编译.java文件。)

pom.xml：

```
<resources>
            <resource>
                <directory>src/main/java</directory>
                <includes>
                    <include>**/*.xml</include>
                </includes>
            </resource>
            <resource>
                <directory>src/main/resources</directory>
                <includes>
                    <include>**/*.*</include>
                </includes>
            </resource>
</resources>
```

放的位置是pom.xml的<build></build>中，因为编译是构建(build)的一部分。构建(build)的过程包括：编译、运行、打包、部署...
