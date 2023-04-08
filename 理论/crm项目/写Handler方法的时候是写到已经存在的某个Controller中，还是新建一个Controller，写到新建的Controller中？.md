写Handler方法的时候是写到已经存在的某个Controller中，还是新建一个Controller，写到新建的Controller中？

判断依据：是看请求通过这个Handler方法，浏览器最终得到的响应是位于哪个文件夹。浏览器最终得到的响应是位于同一个文件夹中的那些Handler方法，应该写在同一个Controller中。一个文件夹对应一个Controller，并且Controller的名称就是 " 对应的那个文件夹名 + Controller "。

例如：有个IndexController，里面已经有了一个Handler方法，通过这个Handler方法，浏览器最终得到的响应是项目首页index.jsp(首页不是登录页面)。现在要写一个Handler方法，通过这个Handler方法，浏览器最终得到的页面要为登录页面。index.jsp位于pages文件夹中。登录页面位于pages/settings/qx/user中。pages和pages/settings/qx/user不是同一个文件夹，所以，要应该先新建一个Controller，然后在这个Controller中写这个Handler方法。

![image-20230316163841960](C:\Users\patrick\AppData\Roaming\Typora\typora-user-images\image-20230316163841960.png)

根据上图可知：应该新建一个Controller叫UserController，里面写一个Handler方法，方法名可以起名为login(起的方法名只要见名知意即可)。