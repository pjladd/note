# idea中的web项目  与  部署到tomcat中的项目  的结构的对应关系：

![image-20230314203350797](C:\Users\patrick\AppData\Roaming\Typora\typora-user-images\image-20230314203350797.png)

tomcat中的每个项目的根目录下，除WEB-INF文件夹外的文件都是能被外界通过 ip地址+文件路径 直接访问的，所以不安全。

所以一般都将页面放在项目目录下的WEB-INF目录里，因为WEB-INF的东西外界是无法直接访问的，页面放在这里，外界就无法直接访问页面了，就能防止外界对页面中的数据进行破坏。页面放在WEB-INF下，外界想要访问的话，就需要通过controller访问，可以在controller代码里面做各种验证操作。

注意：不要将css，img，js文件放在WEB-INF里面，因为页面中是要用到这些东西，如果放在WEB-INF里面的话，页面中使用的时候也要通过controller才能访问到css，img，js，这样很不利于操作。css，img，js这些内容就算被外界直接访问到，他们也不能对数据进行破坏什么的，所以被外界直接访问到也无所谓。所以css，img，js这些东西只要直接放在项目的根目录下就可以了。

注意主页也是放在WEB-INF中，主页也是要通过controller访问的。

所以正确的项目结构是这样的：

![image-20230316144208136](C:\Users\patrick\AppData\Roaming\Typora\typora-user-images\image-20230316144208136.png)





### WEB-INF中的内容外界无法访问的意思是：

浏览器或浏览器中执行的代码(如js代码)访问不到WEB-INF中的内容。
