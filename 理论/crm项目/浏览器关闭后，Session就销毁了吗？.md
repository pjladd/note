# 浏览器关闭后，Session就销毁了吗？



JsessionId的生存时间：第一次发送到浏览器 到 浏览器关闭。浏览器关闭后jsessionid这个cookie就消失了。就找不到这个jsessionid对应的session了。重新打开浏览器，浏览器收到响应的时候，就会收到一个新的jsessionid，就是对应了一个新的session。之前的那个session还会在服务器上。一个session如果达到30分钟没被使用，就会被销毁。没被使用的意思是，服务器没有接收到这个session对应的Jsessionid的请求。

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
