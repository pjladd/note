## SpringMVC

### ModelAndView类介绍：

​	ModelAndView类只继承了Object类，与别的类都没关系。
​	ModelAndView类中定义了成员变量：private Object view; 和 private ModelMap model;
​	ModelAndView类中定义的setViewName(String s)和setView(View v)都是用来给成员变量view设置值，setViewName(String s)是设置一个String对象的地址给成员变量view，
​	setView(View v)是设置一个View对象的地址给成员变量view。
​	ModelAndView类中定义的getViewName()和getView()都是用来获取成员变量view的值，getViewName()是只有在成员变量view指向的是一个String对象时才返回非null值(否则返回null)，
​	getView()是只有在成员变量view指向的是一个View对象时才返回非null值(否则返回null)。
​	getModelInternal()、getModelMap()、getModel()都是用来获取成员变量model的值。
​	addObject(String attributeName, Object attributeValue)是用来往成员变量model指向的map对象中存入键值对。

### ModelMap类： ModelMap是Map，但不是Model。

ExtendModelMap类： 是Map，也是Model。

BindingAwareModelMap类： 是ExtendModelMap类的子类。

### Dispatcher中的doDispatch()方法源码解析：

```
1. DispatcherServlet对象根据接收到的HttpServletRequest对象，去获取与这个请求匹配的HandlerExecutionChain对象
     								                 ( 若干个HandlerInterceptor对象(拦截器) + 一个Handler对象(就是@Controller修饰的一个类的对象) )。

2. DispatcherServlet对象获取与这个HandlerExecutionChain对象中的Handler对象匹配的HandlerAdapter对象。

3. 这个HandlerAdapter对象找出请求匹配的是这个Handler对象中的哪个方法，接着会创建出一个BindingAwareModelMap对象，然后叫这个Handler对象去调用这个方法(如果这个方法中定义了Model
   或Map类型的参数，则HandlerAdapter对象会将创建出来的这个BindingAwareModelMap对象传进去)。 
   注：匹配的方法就是满足如下条件的方法：
   	 请求路径中在项目名与后面跟请求参数的?之间的部分是(或者匹配)" @Controller修饰的类上的@RequestMapping的value属性值+方法上的@RequestMapping的value属性值"的
   	 并且请求方式是满足method属性值(没有写method属性则表示任何请求方式皆可)
   	 并且请求参数是包含了以params属性值为名字的参数
   	 并且请求头是包含了以headers属性值为名字的请求头。

4. HandlerAdapter对象把Handler对象调用完方法后的返回值和在上一步中创建出来的那个BindingAwareModelMap对象交给一个ServletHandlerMethodInvoker对象。ServletHandlerMethodInvoker对象
   会：

         1. 如果返回值为一个String对象，则ServletHandlerMethodInvoker对象会创建出一个ModelAndView对象，然后将这个String对象的地址存到这个ModelAndView对象的成员变量view中。
            并判断BindingAwareModelMap对象中有没有键值对，如果有，就将BindingAwareModelMap对象中的键值对复制一份到这个ModelAndView对象的成员变量model指向的Map对象中。然后将
             这个ModelAndView对象返回给HandlerAdapter对象。
         2. 如果返回值为一个Map对象，则ServletHandlerMethodInvoker对象会创建出一个ModelAndView对象，然后将这个Map对象中的键值对复制一份到这个ModelAndView对象的成员变量
            model指向的Map对象中。并判断BindingAwareModelMap对象中有没有键值对，如果有，就将BindingAwareModelMap对象中的键值对复制一份到这个ModelAndView对象的成员变量model
             指向的Map对象中。然后将这个ModelAndView对象返回给HandlerAdapter对象。
         3. 如果返回值为一个Model对象(通过Model的继承树，可以知道这个Model对象一定是一个ExtendModelMap对象)，则ServletHandlerMethodInvoker对象会创建出一个ModelAndView对象，
            然后将这个Model对象中的键值对复制一份到这个ModelAndView对象的成员变量model指向的Map对象中。并判断BindingAwareModelMap对象中有没有键值对，如果有，就将
             BindingAwareModelMap对象中的键值对复制一份到这个ModelAndView对象的成员变量model指向的Map对象中。然后将这个ModelAndView对象返回给HandlerAdapter对象。
         4. 如果返回值为一个ModelAndView对象，则ServletHandlerMethodInvoker对象会判断BindingAwareModelMap对象中有没有键值对，如果有，就将BindingAwareModelMap对象中的键值对复
            制一份到这个ModelAndView对象的成员变量model指向的Map对象中。然后将这个ModelAndView对象返回给HandlerAdapter对象。

5. HandlerAdapter对象将这个ModelAndView对象返回。

6. DispatcherServlet对象获取到ModelAndView对象后，会按着在springmvc.xml中配置的各个ViewResolver对象的优先级，找能处理这个ModelAndView对象调用getViewName()方法后的返回值的
   ViewResolver对象(一旦找到就不再继续寻找),然后将ModelAndView对象调用getViewName()方法后的返回值交给这个ViewResolver对象，ViewResolver对象拿到getViewName()方法的返回值后，
   会去判断这个返回值中是以什么开头的：

   1. 如果是以" redirect: "开头的，就会创建出一个RedirectView对象，然后将这个返回值中"redirect:"后面的部分赋给这个RedirectView对象的成员变量url。然后返回这个
      RedirectView对象。

   2. 如果是以" forward: "开头的，就会创建出一个InternalResourceView对象，然后将这个返回值中"forward:"后面的部分赋给这个InternalResourceView对象的成员变量url。
      然后返回这个InternalResourceView对象。

   3. 如果既不是以" redirect: "开头也不是以" forward: "开头的，并且这个ViewResolver对象的实际类型是InternalResourceViewResolver，就会创建出一个InternalResourceView对象，
      然后将在springmvc配置文件中配置的
      <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">     
      <property name="prefix" value="/WEB-INF/view/"></property>
      <property name="suffix" value=".jsp"></property>                              
      </bean> 
           中的prefix属性的值，suffix属性的值与getViewName()方法的返回值拼在一起，再将这个拼接成的字符串赋给这个InternalResourceView对象的成员变量url，然后返回这个
      InternalResourceView对象。

      如果既不是以" redirect: "开头也不是以" forward: "开头的，并且这个ViewResolver对象的实际类型是AbstractTemplateViewResolver，就会创建出一个AbstractTemplateView对象。
      如果这个AbstractTemplateView对象是一个FreeMarkerView对象，就会到springmvc.xml中配置的
      <bean class="org.springframework.web.servlet.view.freemarker.FreeMarkerViewResolver"  p:prefix="/" p:suffix=".ftl">
      ...
      </bean> 中获取p:prefix，p:suffix属性的值与getViewName()方法的返回值拼在一起，再将这个拼接成的字符串赋给这个FreeMarkerView对象的成员变量url，然后返回这个
      FreeMarkerView对象。

7. DispatcherServlet对象拿到View对象后，将ModelAndView对象调用getModelInternal()方法后的返回值交给这个View对象，

   1. 如果这个View对象是一个RedirectView对象，则这个View对象会将"/项目名" 与 它的成员变量url的值 与 "?getModelInternal()方法的返回值(是一个Map对象)中的各个键值对" 拼成
      一个字符串。然后这个View对象将状态码为302的，location头的值为这个字符串的响应发送到客户端。
   2. 如果这个View对象是一个InternalResourceView对象，则这个View对象会在拿到getModelInternal()方法的返回值(是一个Map对象)后，就将这个Map中的各个键值对设置到request域中
      (即调用request.setAttribute("键"，"值"))。然后将request对象转发给成员变量url所对应的东西。
   3. 如果这个View对象是一个FreeMarkerView对象，则这个View对象会在拿到getModelInternal()方法的返回值(是一个Map对象)后，
          看：<bean id="freemarkerConfig"  class="org.springframework.web.servlet.view.freemarker.FreeMarkerConfigurer">
      	<property name="templateLoaderPaths"> 
      		<list>
      		    <value>/WEB-INF/ftl/</value>
      		    <value>classpath:/ftl/</value>
      		</list>
      	</property>
      	...
      </bean> 中的<property name="templateLoaderPaths">中的内容，并按着<list>中的<value>的先后顺序看哪个<value>中的内容拼上FreeMarkerView对象的成员变量url的值之后
      得到的路径能对应到一个文件，一旦找到了内容拼上FreeMarkerView对象的成员变量url的值之后得到的路径能对应到一个文件的<value>之后就不再继续寻找。然后就获取路径对
      应的文件的内容，将获取到的内容中的${...}用具体的数据代替，最后利用response.getWriter()得到的流对象将获取到的内容输出到客户端。
```




​	


​	






------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
### Springmvc中只需要一个配置文件，名字可以任意起(可以起为springmvc.xml)。在springmvc.xml中一定要写<mvc:annotation-driven />与<mvc:default-servlet-handler/>。

### DispatcherServlet : 被称为前端控制器或核心控制器。

​	DispatcherServlet对象是由Tomcat创建的。
​	如果开发工具是STS，则在web.xml中配置DispatcherServlet时，不用手动进行配置，可以用Alt + /生成。
​        自动生成的DispatcherServlet的配置中：
	     1. <param-name>contextConfigLocation</param-name>下面的<param-value></param-value>的内容是写Springmvc配置文件的路径，如：<param-value>classpath:springmvc.xml</param-value>
		在Tomcat要去创建DispatcherServlet对象时，会到web.xml中读取DispatcherServlet的配置信息，当它读到<param-name>contextConfigLocation</param-name>时，就会将springmvc的IOC容
		器对象也创建出来。

	     2. <load-on-startup>1</load-on-startup>：有了这个配置，Tomcat启动时就会将DispatcherServlet对象创建出来，而不再是在DispatcherServlet第一次被请求时创建。
	                                              1代表优先级，如果web.xml中有多个<servlet>中都配置了<load-on-startup>时，tomcat根据优先级的值，来确定创建这些
						      Servlet的对象的顺序：值越小，对应的Servlet的对象越早被创建。
	
	     3. <url-parttern></url-parttern>中的内容写  /  而不要写  /*  ，目的是不想与以.jsp结尾的请求路径匹配， /*是匹配任意的请求路径，/是匹配不以.jsp结尾的所有请求路径，
	                                                                                                           .do 是匹配以.do结尾的所有请求路径。

​		

### 用@Controller修饰的类被称为"请求处理器或控制器"，用@Controller修饰的类的类名要以"Handler"结尾(这是一种规范)。包含请求处理器类的包的包名取为"xxx.handler"。


@RequestMapping：
	可以写的位置： 1. 类名上  2. 方法上

	value属性的值要以"/"开头。value属性值只会匹配请求路径中的项目名到后面跟请求参数的?号之间的内容。                     
	value属性的属性值还可以是ant风格的路径(含有匹配符(?或*或**)的路径)： ?匹配1个任意字符，*匹配0个或多个任意字符，**匹配0个或多个目录，  
			 还可以是包含了占位符({...})的路径，如RequestMapping("/test/{aaa}")，一个占位符一定要能对应到路径中的一个目录上才行。我们可以在当前的方法中使用到请求路径中的
			 与占位符对应的内容：在方法的参数列表中定义参数，然后在参数的类型前面写上@pathVariable("占位符名")，如： @pathVariable("aaa") Integer id
			 系统就会将请求路径中的与这个占位符对应的内容传给这个参数。
	
	method属性的属性值可选的范围是：RequestMethod.Get、RequestMethod.Post、RequestMethod.Put、RequestMethod.Delete，如果method属性要写多个属性值则可以写成：
																    method = {RequestMethod.Get, RequestMethod.Post}。
	
	    params属性的属性值是任意的字符串，如果param属性要写多个属性值则写成例如：params = {"aaa", "bbb"}。
	
	headers属性的属性值是任意的字符串，如果headers属性要写多个属性值则写成例如：headers = {"aaa", "bbb"}。
	
	@Controller修饰的类中的每个方法上都要写上@RequestMapping。


补：请求参数是且仅是HttpServletRequest.getParameter()能获取到的东西。
如果请求匹配到的是Handler类中的一个"参数列表中含有未被注解修饰的参数"的方法，则系统就会为这些没有被注解修饰的参数到这个请求中找与它们名字相同的请求参数，如果找到了，
	就将找到的这个请求参数的值传给方法中的名字和这个请求参数的名字相同的那个参数。
	注：参数列表中如果有一个未被注解修饰的，参数类型为Integer[]，参数名为id的参数，则系统会创建出一个Integer[]对象，然后将请求中的所有名字为id的请求参数的值放入这个Integer[]对象
	    中，然后将这个Integer[]对象传给这个参数。
	

@RequestParam:
	可以写的位置： 方法的参数旁边
	如果请求匹配到的是Handler类中的一个"参数列表中含有被@RequestParam注解修饰的参数"的方法，则系统就会为这些被@RequestParam注解修饰的参数到这个请求中找以修饰它们的
	@RequestParam的value属性值为名字的请求参数。如果找到了，就将找到的这个请求参数的值传给方法中的和这个请求参数对应的那个参数。

	required属性：如果没有写required属性，则系统会自动隐式写上，并且设置值为true。
		      required=true: 当系统在请求中没找到和这个@RequestParam的value属性值对应的请求参数时，会报错。
		      required=false: 当系统在请求中没找到和这个@RequestParam的value属性值对应的请求参数时，不会报错。


​	
@RequestHeader:
​        可以写的位置： 方法的参数旁边
​	如果请求匹配到的是Handler类中的一个"参数列表中含有被@RequestHeader注解修饰的参数"的方法，则系统就会为这些被@RequestHeader注解修饰的参数到请求中找以修饰它们的@RequestHeader的
​	value属性值为"键"的请求头。如果找到了，就将找到的这个请求头的"值"传给方法中的和这个请求头对应的那个参数。

@CookieValue:
	可以写的位置： 方法的参数旁边
	如果请求匹配到的是Handler类中的一个"参数列表中含有被@CookieValue注解修饰的参数"的方法，则系统就会为这些被@CookieValue注解修饰的参数到请求中的Cookie请求头的"值"中找以修饰它们的
	@CookieValue的value属性值为"键"的键值对。如果找到了，就将找到的这个键值对的"值"传给方法中的和这个键值对对应的那个参数。
	注意：“ 找以修饰它们的@CookieValue的value属性值为"键"的键值对 ”的时候，是找与value属性值一模一样的"键",是严格区分大小写的。
	

如果请求匹配到的是Handler类中的一个"参数列表中含有JavaBean类型的参数"的方法，则系统会为这些参数创建各个JavaBean对象，然后到请求中为这些JavaBean对象的各个属性找名字和他们相同的请求参数。
如果找到了，就将找到的这个请求参数的值设置给和这个请求参数对应的那个属性(是通过set方法进行设置的)。最后将这些JavaBean对象传给方法中的对应的参数。
注：请求中如果含有名字为xx[6]的请求参数，如果这个请求匹配到的是Handler类中的一个"参数列表中含有JavaBean类型的参数"的方法，则当系统为JavaBean对象的属性到请求中找名字和它相同的请求参
    数时，如果发现xx是和JavaBean对象的一个属性的属性名相同，但是这个属性的类型不是List，就会抛出异常。
          如果发现xx是和JavaBean对象的一个属性的属性名相同，并且这个属性的类型是List，则系统就让名为xx[6]的请求参数的值成为这个List类型的属性指向的List对象中的下标为6的格子中的元素。
    
    

如果请求匹配到的是Handler类中的一个"参数列表中含有HttpServletRequest/HttpServletResponse/HttpSession类型的参数"的方法，则系统会将HttpServletRequest对象/HttpServletResponse对象
/HttpSession对象传进来。

注意：在redirect:后面不能写项目名。


REST风格的请求路径：没有后面带请求参数的?号的请求路径。

http规范中提出： 查询是发送get请求。(如果Handler中的一个方法中是要到数据库中查询数据的，则这个方法上的RequestMapping中的method属性值要设置为RequestMethod.GET。)
	         添加是发送post请求。
	         删除时发送delete请求。
	         修改是发送put请求。

HttpServletRequest.getMethod()的返回值就是这个请求对象的请求方式。
HttpMethodRequestWrapper类实现了HttpServletRequest接口。
HiddenHttpMethodFilter：HiddenHttpMethodFilter对象会更改请求方式是POST的，并且含有名为"_method"的请求参数的请求对象的请求方式(要更改成的请求方式就是请求对象的名为"_method"的参数值)。
			源码解析(可以不看)：
			HiddenHttpMethodFilter对象获取到HttpServletRequest对象后会判断请求方式是否为POST，如果是，就创建出一个HttpMethodRequestWrapper对象，并将获取到的HttpServletRequest
			对象的地址赋给HttpMethodRequestWrapper对象的成员变量request，将HttpServletRequest对象中的名为"_method"的参数的值赋给HttpMethodRequestWrapper对象的成员变量method。
			然后将这个HttpMethodRequestWrapper对象给到下一个过滤器或Servlet。
			注： HttpMethodRequestWrapper类对getMethod()进行了重写(重写后的方法的方法体中的内容是：返回成员变量method的值)。
在配置文件中配置<filter>时，<url-pattern>一定要写/* 。


能用包装类型的就不要用基本类型(尤其是成员变量和方法的形参，不要用基本类型)。




Springmvc中提供的表单标签：
	要使用之前，请先导入标签库：<%@ taglib uri="http://www.springframework.org/tags/form" prefix="form" %>

	<form:form action="/springmvccrud/addEmployee" method="post" >                等价于               <form action="/springmvccrud/addEmployee" method="post">
	
	<form:input path="lastName"/>                                                 等价于               <input type="text" name="lastName"/>
	
	<form:radiobuttons path="gender" items="${Map对象}"/>                         等价于               <input type="radio" name="gender" value="0"> 女
	设这个Map对象中的内容是： "0" = "女"                                                               <input type="radio" name="gender" value="1"> 男              
				  "1" = "男" 
	
	    <form:select path="department.id" items="${requestScope.depts }" itemValue="id" itemLabel="departmentName" />       //注意：itemValue与itemLabel属性值中是没有${}的
	
	等价于 
	
	<select name="department.id">
	     <c:forEach items="${requestScope.depts }" var="dept">
		<option value="${dept.id}">${dept.departmentName }</option>
	     </c:forEach>
	    </select>
	
	    <form:form>表单标签会到request域中获取"键"为modelAttribute属性的属性值的键值对的"值"。(modelAttribute属性是被系统隐式写上的，并且设置值为"command")
	如果获取不到就会报错。
	如果获取到了，<form:form>就会为内部的每一个标签，到获取到的"值"指向的对象中看是否含有以这个标签的path属性值为名字的属性，
		如果不含有，就报错。
		如果包含，<form:form>内部的每一个标签就会到这个"值"指向的对象中获取名字与自己的path属性值相同的属性的值。
			如果这个标签是有value属性的，则会将获取到的属性值隐式地设置给value属性。
			无论这个标签有没有value属性，它都会将这个获取到的属性值在标签中显示出来。

注：Springmvc中提供的表单标签是可以和html标签混合使用的。

在一个使用了Springmvc框架的项目中要想访问项目中的静态资源，就一定要在springmvc.xml中配置：<mvc:default-servlet-handler default-servlet-name="default" />，否则就访问不到静态资源。


实现抽象方法的时候如果生成的方法的参数名是类似arg0这样的，原因就是：没有连接源码。

拦截器对象就是HandlerInterceptor对象。

### 创建拦截器类的方式：

​	方式1. 继承HandlerInterceptorAdapter类。(HandlerInterceptorAdapter类实现了HandlerInterceptor接口,都是空实现)
​	方式2. 实现HandlerInterceptor接口

DispatcherServlet类的doDispatch()方法中的：
	if (!mappedHandler.applyPreHandle(processedRequest, response)) {   //就是HandlerExecutionChain对象对内部的各个拦截器对象的preHandle()方法的调用
		return;
	}

	mappedHandler.applyPostHandle(processedRequest, response, mv);     //就是HandlerExecutionChain对象对内部的各个拦截器对象的postHandle()方法的调用
	
	triggerAfterCompletion(processedRequest, response, mappedHandler, ex);  在1030行  //就是HandlerExecutionChain对象对内部的各个拦截器对象的afterCompletion()方法的调用

创建拦截器类后需要给这个拦截器类在springmvc.xml中进行配置：
	<mvc:interceptors>
		<bean class="com.xukan.interceptors.MyFirstInterceptor"></bean>  //这个<bean>没有写在<mvc:interceptor>中，就表示HandlerExecutionChain对象无论如何都会调用这个拦截器对象
		<mvc:interceptor>                                                                                                                                            的各个方法。
			<mvc:mapping path="/xxx"/>         
			<bean class="com.xukan.interceptors.MyInterceptor2"> 
			//当且仅当请求路径中在项目名与后面跟请求参数的?之间的部分是/xxx时，HandlerExecutionChain对象才会调用这个拦截器对象的各个方法。
		</mvc:interceptor>
		<mvc:interceptor>
			<mvc:mapping path="/aaa"/>
			<mvc:exclude-mapping path="/bbb"/>
			<bean class="com.xukan.interceptors.MyInterceptor3"></bean>
		</mvc:interceptor>
	</mvc:interceptors>
	

	注：HandlerExecutionChain对象中的List<HandlerInterceptor>类型的成员变量interceptorList中存放HandlerInterceptor对象的顺序就是按配置文件中HandlerInterceptor对象的配置顺序。
	    HandlerExecutionChain对象中的HandlerInterceptor[]类型的成员变量interceptors中存放HandlerInterceptor对象的顺序就是按配置文件中HandlerInterceptor对象的配置顺序。
	
	    <mvc:interceptor>里面一定要写<mvc:mapping>标签，不写就报错。
	    并且写的时候要按如下顺序，否则报错：
				先写<mvc:mapping>
				再写<mvc:exclude-mapping>
				再写<bean>


DispatcherServlet类中有一个List<HandlerExceptionResolver>类型的成员变量handlerExceptionResolvers。
	( 如果你没有在springmvc.xml中写<mvc:annotation-driven />，并且你没有为任何HandlerExceptionResolver对象配置<bean>，则这个成员变量中会有3个对象：
	  AnnotationMethodHandlerExceptionResolver对象、 ResponseStatusExceptionResolver对象、 DefaultHandlerExceptionResolver对象。
	  如果你在springmvc.xml中写了<mvc:annotation-driven />，并且你没有为任何HandlerExceptionResolver对象配置<bean>，则这个成员变量中会有3个对象：
	  ExceptionHandlerExceptionResolver对象，ResponseStatusExceptionResolver对象、 DefaultHandlerExceptionResolver对象。
	  由于AnnotationMethodHandlerExceptionResolver类已过时，所以如果你没有为任何HandlerExceptionResolver对象配置<bean>，那么就一定要在springmvc.xml中
	  写上<mvc:annotation-driven />。 )
在DispatcherServlet.doDispatch()方法中的processDispatchResult()中的processHandlerException();中会遍历这个成员变量中的各个HandlerExceptionResolver对象，让各个HandlerExceptionResolver对
象去调用resolveException()方法。


如果你在springmvc.xml中为一些HandlerExceptionResolver对象配置了<bean>，则DispatcherServlet类的成员变量handlerExceptionResolvers中就只会包含你配置的这些HandlerExceptionResolver对象。

如果你在springmvc.xml中配置了SimpleMappingExceptionResolver对象
	   <bean class="org.springframework.web.servlet.handler.SimpleMappingExceptionResolver">
		<property name="exceptionMappings">
			<props>
				<prop key="java.lang.NullPointerException">xxx</prop>   
			</props>
		</property>
	   </bean>
	
则当Handler中的一个方法中抛出了NullPointException时，系统会将springmvc.xml中配置的
     <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">     
	  <property name="prefix" value="/WEB-INF/view/"></property>
	  <property name="suffix" value=".jsp"></property>                              
     </bean> 
中的prefix属性的值，suffix属性的值与xxx拼成一个字符串。然后叫 项目名/拼成的字符串.jsp 输出响应给浏览器。注：在 项目名/拼成的字符串.jsp 中可以用${exception}获取到抛出的异常的信
息。如果你在<bean class="org.springframework.web.servlet.handler.SimpleMappingExceptionResolver"></bean>中写了<property name="exceptioAttribute" value="aaa">，则在
项目名/拼成的字符串.jsp 中就要用${aaa}才能获取到抛出的异常的信息。


出现了404，但是在控制台没有出现"No Mapping Found"，则说明请求并没有被DispatcherServlet获取到。

只有在项目中导入了jackson的相关jar包，才可以在Handler类中使用@ResponseBody注解。Handler类中的一个方法如果使用了@ResponseBody，这个方法可以返回任意类型的返回值(实际开发中常常将返回值
的类型定义为Object)。系统会将这个返回值转成一个Json字符串，然后调用response.getWriter().write(这个Json字符串); 发到客户端的响应的内容就只有这个Json字符串。

补：每一个ViewResolver实现类都实现了Ordered接口，每一个ViewResolver实现类中都具有成员变量order，并且初始值都是Integer.MAX_VALUE，成员变量order代表所属的ViewResolver对象的优先级，
    order的值越小，所属的ViewResolver对象的优先级越高。
---------------------------------------------------------------------------------spring整合springmvc-------------------------------------------------------------------------------
在学Springmvc时学到的对象才能配置到springmvc.xml中。除此以外的对象都是配置到spring.xml中。

Springmvc的IOC容器是Spring的IOC容器的子容器。子容器能访问父容器，但是父类器不能访问子容器。

步骤： 
	1. 让Spring的IOC容器对象也在Tomcat启动时被创建：
	     利用监听器，监听ServletContext的创建，当ServletContext被创建时，将Spring的IOC容器对象创建出来。
	2. 将Spring的IOC容器对象放到ServletContext域中。

	要实现上面两个步骤，只需要在web.xml中，写上如下配置：
	<context-param>
		<param-name>contextConfigLocation</param-name>
		<param-value>classpath:spring.xml</param-value>
	</context-param>
	
	<listener>
		<listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
	</listener>
	这样当ContextLoaderListener对象监听到ServletContext对象被创建，就会去获取spring.xml然后将Spring的IOC容器对象创建出来，并把Spring的IOC容器放到
	ServletContext域中。("键"是WebApplicationContext类中的一个常量：WebApplicationContext.ROOT_WEB_APPLICATION_CONTEXT_ATTRIBUTE)
	
	3. 在springmvc.xml中写：
		<context:component-scan base-package="包名" use-default-filters="false">
			<context:include-filter type="annotation" expression="org.springframework.stereotype.Controller"/>
		</context:component-scan>
	
	   在spring.xml中写：
		<context:component-scan base-package="包名" use-default-filters="true" >
			<context:exclude-filter type="annotation" expression="org.springframework.stereotype.Controller"/>
		</context:component-scan>

从ServletContext对象中获取Spring的IOC容器对象的两种方式: 
	方式1；ApplicationContext applicationContext = (ApplicationContext)ServletContext对象.getAttribute("WebApplicationContext.ROOT_WEB_APPLICATION_CONTEXT_ATTRIBUTE");

	方式2；ApplicationContext applicationContext = WebApplicationContextUtils.getWebApplicationContext(ServletContext对象); //这种方式就不用进行强制转换了，比较方便

要处理乱码问题，就在web.xml中进行如下配置(注意这个<filter>一定要是第一个配置的<filter>):
  <filter>
  	<filter-name>CharacterEncodingFilter</filter-name>
  	<filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
	<init-param>
  		<param-name>encoding</param-name>
  		<param-value>UTF-8</param-value>    //指定字符集
  	</init-param>
  </filter>
  <filter-mapping>
  	<filter-name>CharacterEncodingFilter</filter-name>
  	<url-pattern>/*</url-pattern>
  </filter-mapping>

-------------------------------------------------------------------------草稿--------------------------------------------------------------------
	当Handler中的一个方法中抛出异常时(由于抛出了异常导致Handler中的这个方法没有正常执行结束，最终就会导致HandlerAdapter对象返回给DispatcherServlet的ModelAndView
	对象是null)，DispatcherServlet会判断刚刚执行的Handler中的那个方法有没有抛出异常，如果发现跑出来异常，就会springmvc.xml中配置的
	     <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">     
		  <property name="prefix" value="/WEB-INF/view/"></property>
		  <property name="suffix" value=".jsp"></property>                              
	     </bean> 
	中的prefix属性的值，suffix属性的值与xxx拼成一个字符串。然后叫 项目名/拼成的字符串.jsp 输出响应给浏览器。注：在 项目名/拼成的字符串.jsp 中可以用${exception}获取到抛出的异常的信
	息。如果你在这个<bean class="org.springframework.web.servlet.handler.SimpleMappingExceptionResolver"></bean>中写了<property name="exceptionAttribute" value="aaa" />，则在
	项目名/拼成的字符串.jsp 中就要用${aaa}才能获取到抛出的异常的信息。


	当系统是为JavaBean对象的一个List类型属性到请求中找名字和它相同的请求参数时，会看看请求中名字形如xx[6]的请求参数(如果有的话)的xx是否和这个List类型属性的属性名是相同的。如果是相同的，
	就让名为xx[6]的请求参数的值成为JavaBean对象的这个List类型的属性指向的List对象中的第6个元素。




6. DispatcherServlet对象获取到ModelAndView对象后，会按着在springmvc.xml中配置的各个ViewResolver对象的优先级，找能处理这个ModelAndView对象调用getViewName()方法后的返回值的ViewResolver
   对象(一旦找到就不再继续寻找),然后将ModelAndView对象调用getViewName()方法后的返回值交给这个ViewResolver对象，ViewResolver对象拿到getViewName()方法的返回值后，会去判断这个返回值中是
   以什么开头的：
		1. 如果是以" redirect: "开头的，就会创建出一个RedirectView对象，然后将这个返回值中"redirect:"后面的部分赋给这个RedirectView对象的成员变量url。然后返回这个
		   RedirectView对象。
		2. 如果是以" forward: "开头的，就会创建出一个InternalResourceView对象，然后将这个返回值中"forward:"后面的部分赋给这个InternalResourceView对象的成员变量url。
		   然后返回这个InternalResourceView对象。
		3. 如果既不是以" redirect: "开头也不是以" forward: "开头的，并且这个ViewResolver对象的实际类型是InternalResourceViewResolver，就会创建出一个InternalResourceView对象，
		   然后将在springmvc配置文件中配置的
		   <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">     
			<property name="prefix" value="/WEB-INF/view/"></property>
			<property name="suffix" value=".jsp"></property>                              
		   </bean> 
	           中的prefix属性的值，suffix属性的值与getViewName()方法的返回值拼在一起，再将这个拼接成的字符串赋给这个InternalResourceView对象的成员变量url，然后返回这个
		   InternalResourceView对象。

		   如果既不是以" redirect: "开头也不是以" forward: "开头的，并且这个ViewResolver对象的实际类型是AbstractTemplateViewResolver，就会创建出一个AbstractTemplateView对象。
		   如果这个AbstractTemplateView对象是一个FreeMarkerView对象，就会到springmvc.xml中配置的
		   <bean class="org.springframework.web.servlet.view.freemarker.FreeMarkerViewResolver"  p:prefix="/" p:suffix=".ftl">
			...
		   </bean> 中获取p:prefix，p:suffix属性的值与getViewName()方法的返回值拼在一起，再将这个拼接成的字符串赋给这个FreeMarkerView对象的成员变量url，然后返回这个
		   FreeMarkerView对象。

7. DispatcherServlet对象拿到View对象后，将ModelAndView对象调用getModelInternal()方法后的返回值交给这个View对象，
		1. 如果这个View对象是一个RedirectView对象，则这个View对象会将"/项目名" 与 它的成员变量url的值 与 "?getModelInternal()方法的返回值(是一个Map对象)中的各个键值对" 拼成
		   一个字符串。然后这个View对象将状态码为302的，location头的值为这个字符串的响应发送到客户端。
		2. 如果这个View对象是一个InternalResourceView对象，则这个View对象会在拿到getModelInternal()方法的返回值(是一个Map对象)后，就将这个Map中的各个键值对设置到request域中
		   (即调用request.setAttribute("键"，"值"))。然后将request对象转发给成员变量url所对应的东西。
		3. 如果这个View对象是一个FreeMarkerView对象，则这个View对象会在拿到getModelInternal()方法的返回值(是一个Map对象)后，
                   会看：<bean id="freemarkerConfig"  class="org.springframework.web.servlet.view.freemarker.FreeMarkerConfigurer">
				<property name="templateLoaderPaths"> 
					<list>
					    <value>/WEB-INF/ftl/</value>
					    <value>classpath:/ftl/</value>
					</list>
				</property>
				...
			</bean> 中的<property name="templateLoaderPaths">中的内容，并按着<list>中的<value>的先后顺序看哪个<value>中的内容拼上FreeMarkerView对象的成员变量url的值之后
			得到的路径能对应到一个文件，一旦找到内容拼上FreeMarkerView对象的成员变量url的值之后得到的路径能对应到一个文件的<value>就不再继续寻找。然后就获取路径对应的文
			件的内容，将获取到的内容中的${...}用具体的数据代替，最后利用response.getWriter()得到的流对象将获取到的内容输出到客户端。
			

------------------------------------------------------------原版------------------------------------------------------
6. DispatcherServlet对象获取到ModelAndView对象后，将ModelAndView对象调用getViewName()方法后的返回值交给ViewResolver对象，ViewResolver对象拿到getViewName()方法的返回值后，
	   会去判断这个返回值中是以什么开头的：
		1. 如果是以" redirect: "开头的，就会创建出一个RedirectView对象，然后将这个返回值中"redirect:"后面的部分赋给这个RedirectView对象的成员变量url。然后返回这个
		   RedirectView对象。
		2. 如果是以" forward: "开头的，就会创建出一个InternalResourceView对象，然后将这个返回值中"forward:"后面的部分赋给这个InternalResourceView对象的成员变量url。
		   然后返回这个InternalResourceView对象。
		3. 如果既不是以" redirect: "开头也不是以" forward: "开头的，就会创建出一个InternalResourceView对象，然后将在springmvc配置文件中配置的
		   <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">     
			<property name="prefix" value="/WEB-INF/view/"></property>
			<property name="suffix" value=".jsp"></property>                              
		   </bean> 
	           中的prefix属性的值，suffix属性的值与getViewName()方法的返回值拼在一起，再将这个拼接成的字符串赋给这个InternalResourceView对象的成员变量url，然后返回这个
		   InternalResourceView对象。
	
	7. DispatcherServlet对象拿到View对象后，将ModelAndView对象调用getModelInternal()方法后的返回值交给这个View对象，
		1. 如果这个View对象是一个RedirectView对象，则这个View对象会将"/项目名" 与 它的成员变量url的值 与 "?getModelInternal()方法的返回值(是一个Map对象)中的各个键值对" 拼成
		   一个字符串。然后这个View对象将状态码为302的，location头的值为这个字符串的响应发送到客户端。
		2. 如果这个View对象是一个InternalResourceView对象，则这个View对象会在拿到getModelInternal()方法的返回值(是一个Map对象)后，就将这个Map中的各个键值对设置到request域中
		   (即调用request.setAttribute("键"，"值"))。然后将request对象转发给成员变量url所对应的东西。