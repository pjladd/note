# Thymeleaf详解

Thymeleaf是一个流行的模板引擎，该模板引擎采用Java语言开发；

![blob.png](http://www.bjpowernode.com/ueditor/php/upload/image/20190213/1550023164733920.png)

 

   模板引擎是一个技术名词，是跨领域跨平台的概念，在Java语言体系下有模板引擎，在C#、PHP语言体系下也有模板引擎，在JavaScript中也会用到模板引擎技术；

Java生态下的模板引擎有 Thymeleaf 、Freemaker、Velocity、Beetl（国产） 等；

Thymeleaf 它是基于HTML的，Thymeleaf模板本身也是一个html页面，Thymeleaf 要寄托在HTML的标签下实现对数据的展示；

Spring boot 集成了thymeleaf模板技术，并且spring boot官方也推荐使用thymeleaf来替代JSP技术；

Thymeleaf是另外的一种模板技术，它本身并不属于SpringBoot，SpringBoot只是很好地集成这种模板技术，作为前端页面的数据展示；

Thymeleaf旨在提供⼀个优雅的、⾼度可维护的创建模板的⽅式，为了实现这⼀⽬标，Thymeleaf建⽴在⾃然模板的概念上，将其逻辑注⼊到模板⽂件中，不会影响模板设计原型。 这改善了设计的沟通，弥合了设计和开发团队之间的差距。

 

![blob.png](http://www.bjpowernode.com/ueditor/php/upload/image/20190213/1550023177902303.png)

 

   对于Spring框架模块,一个允许你集成你最喜欢的工具的平台,并且能够插入自己的功能,Thymeleaf是理想的现代JVM HTML5 web开发工具，虽然它可以做得多。

简单说， Thymeleaf 是一个跟 Velocity、FreeMarker 类似的模板引擎，它可以完全替代 JSP。

**Thymeleaf与JSP的区别在于，不运行项目之前，Thymeleaf也是纯HTML（不需要服务端的支持）而JSP需要进行一定的转换，这样就方便前端人员进行独立的设计、调试。相较与其他的模板引擎，它有如下三个极吸引人的特点：**

1）Thymeleaf 在有网络和无网络的环境下皆可运行，即它可以让美工在浏览器查看页面的静态效果，也可以让程序员在服务器查看带数据的动态页面效果。这是由于它支持 html 原型，然后在 html 标签里增加额外的属性来达到模板+数据的展示方式。浏览器解释 html 时会忽略未定义的标签属性，所以 thymeleaf 的模板可以静态地运行，当有数据返回到页面时，Thymeleaf 标签会动态地替换掉静态内容，使页面动态显示。

2）Thymeleaf 开箱即用的特性。它提供标准和spring标准两种方言，可以直接套用模板实现JSTL、 OGNL表达式效果，避免每天套模板、修改jstl、标签的困扰，同时开发人员也可以扩展和创建自定义的方言。

3）Thymeleaf 提供spring标准方言和一个与 SpringMVC 完美集成的可选模块，可以快速的实现表单绑定、属性编辑器、国际化等功能。

4）Thymeleaf可以实现与jsp完全一样的功能；