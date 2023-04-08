# Controller中的Handler方法的@RequestMapping的value写的时候是有规范的：

handler方法返回的东西有两种：

```
第一种：handler方法返回的是一个页面

第二种：handler方法返回的是一个json字符串
```



## 1. handler方法返回的是一个页面

这种handler方法的@RequestMapping的value值写的是：

​									浏览器最终得到的响应所在的文件夹的路径 + Handler方法名。

示例：

​		有个方法名为regist的handler方法要返回的是一个页面，页面为regist.jsp。

```
public String regist() {
		.
		.
		.
		
	return "regist";
}
```

在regist.jsp中有如下代码：

```
<script type="text/javascript">
		window.location.href = "settings/qx/user/toXXX.do";//也就是重定向
</script>
```

浏览器最终得到的响应是xxx.jsp。

xxx.jsp的路径为：WEB-INF/pages/settings/qx/user/xxx.jsp

所以xxx.jsp所在的文件夹的路径为：WEB-INF/pages/settings/qx/user/ ，由于所有页面都是在WEB-INF/pages下，所以WEB-INF/pages这部分就不要了。

这个handler方法的RequestMapping的value就写：

```
  /settings/qx/user/regist    ：其中/settings/qx/user浏览器最终得到的响应xxx.jsp所在的文件夹的路径，  regist为方法名

  即： @requestMapping("/settings/qx/user/regist")
```



注意：@RequestMapping的value是写浏览器最终得到的响应所在的文件夹的路径，而不是handler方法返回的页面所在的文件夹的路径。如上面的例子中，并不是写handler方法返回的regist.jsp所在的文件夹的路径。



## 2. handler方法返回的是json字符串

此时，服务器返回给浏览器的响应就是这个json字符串。这种响应是要被一个页面接收的。

这种handler方法的@RequestMapping的value值写的是：要接收响应的页面所在的文件夹的路径 + Handler方法名。

比如：有个方法名为login的handler方法要返回的是个json字符串，响应的接收方是login.jsp，login.jsp的路径为：WEB-INF/pages/settings/qx/user/login.jsp

所以login.jsp所在的文件夹的路径为：WEB-INF/pages/settings/qx/user/ ，由于所有页面都是在WEB-INF/pages下，所以WEB-INF/pages这部分就不要了。

这个handler方法的@RequestMapping的value就写：

```
  /settings/qx/user/login            ：其中/settings/qx/user为接收响应的页面所在的文件夹的路径，login为方法名
  
  即： @requestMapping("/settings/qx/user/login")
```

![image-20230323124314245](C:\Users\patrick\AppData\Roaming\Typora\typora-user-images\image-20230323124314245.png)



### 如果一个响应的内容是json字符串，该如何判断这个响应要被哪个页面接收？

答：一般是：请求是在哪个页面中发出的，则就是哪个页面接收响应。

```
响应内容是json字符串，所以对应的请求一定是异步请求。因为异步请求的响应内容是json字符串。同步请求的响应内容一定是一个页面。
```

