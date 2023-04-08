# dispatcherservlet对请求的处理和web容器对请求的处理的区别：

一个请求如果是交给dispatcherservlet处理，则是根据请求路径去找Handler进行处理。如果是将一个请求交给web容器（如：tomcat）进行处理，则是：根据这个请求路径到项目的目录下找对应的资源。

对于静态资源(css，js，img)而言，用它们的时候如果还要通过controller才能访问，则在写html的时候，用它们就太麻烦了。所以这些东西是在html中直接引用的。所以要将（css，js，img）放在项目根目录下，不能放在WEB-INF中。由于dispatcherServlet配置了一个请求路径 / ,这代表dispatcherServlet会拦截所有请求，此时会产生一个问题就是访问静态资源的请求会被dispatcherServlet拦截，去匹配Handler方法。这样肯定是匹配不到的。所以要解决这个问题，就是要让dispatcherServlet不要去管访问静态资源的请求，要dispatcherServlet将这个请求还给web容器(tomcat)去处理，tomcat处理请求是根据这个请求地址在项目根目录下找文件的，不是去匹配handler的。



### 举个例子：例如有请求http://127.0.0.1/crm/img/first.jpg发到服务器

如果是tomcat处理这个请求的话，过程如下：

```
http://127.0.0.1/crm/img/first.jpg

是在webapps中找到crm文件夹，然后找img文件夹，然后找first.jpg。

```

如果是dispatcherServlet处理这个请求的话，过程如下：

```
http://127.0.0.1/crm/img/first.jpg

在contoller中找RequestMapping配置的是 "/img/first.jpg" 的handler方法。
```



想要dispatcherServlet不要去管访问静态资源的请求，要dispatcherServlet将这个请求还给web容器(tomcat)去处理，则只需要在springmvc的配置文件中配置：

```
<mvc:default-servlet-handler />
```

