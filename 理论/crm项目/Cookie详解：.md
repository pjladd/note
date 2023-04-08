# Cookie详解：

只要服务器应用带到浏览器的cookie没过期，下次浏览器再次发送请求给服务器上的这个应用时，请求中就一定会带有这个cookie（注意，这个cookie在浏览器中还是存在的，带过来的是一个副本）。这是http协议规定的。

注意：响应是不会自动带上cookie的，要想在响应中带上cookie，要用如下代码，：

```
				  Cookie c1=new Cookie("loginAct",user.getLoginAct());
                    c1.setMaxAge(10*24*60*60); //设置cookie的过期时间
                    response.addCookie(c1);
                    Cookie c2=new Cookie("loginPwd",user.getLoginPwd());
                    c2.setMaxAge(10*24*60*60);
                    response.addCookie(c2);
                    
```



## 把浏览器上的没过期的cookie删除

实现方式：响应上带cookie到浏览器，利用覆盖，实现把浏览器上存着的没有过期的cookie删除。因为浏览器会自动将已经过期的cookie删除。

覆盖：带到浏览器上的cookie会将浏览器上已经存在的同名cookie覆盖掉，也就是将name属性值相同的cookie覆盖掉。

是否覆盖和cookie的value属性值无关，value属性值可以随便是几，是否覆盖是取决于name属性值是否相同。

```
  				   浏览器上已经存在着两个cookie，一个cookie的名字为"loginAct"，另一个cookie的名字为"loginPwd"
  				   
  				   Cookie c1=new Cookie("loginAct","1");
                    c1.setMaxAge(0);//设置cookie的过期时间为0，意味着已经过期
                    response.addCookie(c1);
                    Cookie c2=new Cookie("loginPwd","1");
                    c2.setMaxAge(0);//设置cookie的过期时间为0，意味着已经过期
                    response.addCookie(c2);
```



## 会话cookie

会话Cookie，过期时间是到浏览器关闭时(maxAge = -1)，是生存在内存中的cookie，不是在硬盘中。会话Cookie是服务器自动颁发给浏览器的，不用我们手工创建的。会话Cookie的maxAge值默认是-1，也就是说仅当前浏览器使用，不将该Cookie存在硬盘中。会话cookie的过期时间是在浏览器关闭时。

Jsessionid属于会话Cookie。



## 持久化的cookie

还有一种Cookie是持久化的Cookie，生存在硬盘上，而不是内存中。手工创建，并且过期时间为正数的Cookie就是持久Cookie。

创建一个持久化的cookie：

```
  Cookie c1=new Cookie("loginAct",user.getLoginAct());
  c1.setMaxAge(10*24*60*60); //设置cookie的过期时间为10天
  response.addCookie(c1);

```

  上述代码中创建的这个name属性值为loginAct的cookie就是一个持久化的cookie。
