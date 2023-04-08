# Cookie与Session的联系

JsessionID是用cookie保存的。

首次访问服务器，服务器发送给客户端的cookie的内容就是JsessionId

**1）第一次访问服务器的时候，会在响应头里面看到Set-Cookie信息（只有在首次访问服务器的时候才会在响应头中出现该信息）**

![image-20230216110926064](C:\Users\patrick\AppData\Roaming\Typora\typora-user-images\image-20230216110926064.png)

上面的图JSESSIONID=ghco9xdnaco31gmafukxchph;Path=/acr，

浏览器会根据响应头的set-cookie信息设置浏览器的cookie并保存之

注意此cookie由于没有设置cookie有效日期，所以在关闭浏览器的情况下会丢失掉这个cookie。

**2）当再次请求的时候（非首次请求），浏览器会在请求头里将JsessionId这个cookie发送给服务器(每次请求都是这样)**

![image-20230216130048760](C:\Users\patrick\AppData\Roaming\Typora\typora-user-images\image-20230216130048760.png)

```
（JSESSIONID=ghco9xdnaco31gmafukxchph）
```

**3）为什么除了首次请求之外每次请求都会发送这个cookie呢（在这里确切地说是发送这个jsessionid）？**

事实上当用户访问服务器的时候会为每一个用户开启一个session，浏览器是怎么判断这个session到底是属于哪个用户呢？jsessionid的作用就体现出来了：jsessionid就是用来判断当前用户对应于哪个session。换句话说服务器识别session的方法是通过jsessionid来告诉服务器该客户端的session在内存的什么地方。

事实上`jsessionid ==request.getSession().getId()`

**4)总结，jsessionid的工作流程可以简单用下面的图表示：**

![image-20230216130504764](C:\Users\patrick\AppData\Roaming\Typora\typora-user-images\image-20230216130504764.png)