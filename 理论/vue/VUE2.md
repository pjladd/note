# VUE2

### 1) 环境准备

#### 安装脚手架

```
npm install -g @vue/cli
```

* -g 参数表示全局安装，这样在任意目录都可以使用 vue 脚本创建项目

执行之后，在Node.js的目录下会生成vue.cmd，这个vue.cmd的作用是用来创建项目。

#### 创建项目

1. 创建一个文件夹，用来存要创建的项目。这里创建一个文件夹，文件夹名为第3章，路径为D:\2022.js\代码\第3章

2. 打开cmd，切换到D:\2022.js\代码\第3章，执行命令：

   ```
   vue ui      意思是以图像界面的方式引导你创建项目
   ```

   执行后，会自动打开一个浏览器，页面如下：

   ![image-20230404160731679](C:\Users\patrick\AppData\Roaming\Typora\typora-user-images\image-20230404160731679.png)

​	  点击Create，出现以下界面后，点击在此创建新项目。

![image-20230404160827955](C:\Users\patrick\AppData\Roaming\Typora\typora-user-images\image-20230404160827955.png)

​	   输入项目名。这里是将项目命名为client。包管理器选择npm，点击下一步。

​				![image-20230404160936516](C:\Users\patrick\AppData\Roaming\Typora\typora-user-images\image-20230404160936516.png)

​	     选择手动，点击下一步。

![image-20230404161412964](C:\Users\patrick\AppData\Roaming\Typora\typora-user-images\image-20230404161412964.png)

​      这个页面的作用就类似maven中的添加依赖，就是让你选择要添加哪些依赖。我们要做的就是在它已经选择的依赖的基础上增加上Router和Vuex即可。点击下一步。

![image-20230404161608769](C:\Users\patrick\AppData\Roaming\Typora\typora-user-images\image-20230404161608769.png)

![image-20230404161740458](C:\Users\patrick\AppData\Roaming\Typora\typora-user-images\image-20230404161740458.png)

Router的作用是实现组件之间的跳转。Vuex的作用是实现组件之间的数据共享。开发一个Vue项目，Router和Vuex这两个依赖是必不可少的。



选择vue的版本，这里选择2.x。linter选择第一项。点击创建项目。

![image-20230404162217142](C:\Users\patrick\AppData\Roaming\Typora\typora-user-images\image-20230404162217142.png)



点击创建项目不保存预设。

![image-20230404164341174](C:\Users\patrick\AppData\Roaming\Typora\typora-user-images\image-20230404164341174.png)



等待几分钟出现如下页面，表示项目创建成功：

![image-20230404164609331](C:\Users\patrick\AppData\Roaming\Typora\typora-user-images\image-20230404164609331.png)

点击右上角的" 安装devtools "。devtools是一个开发者工具，本质是一个浏览器插件，可以用它来调试vue代码，查看组件。

如果安装不下来，就直接进入这个网址安装devtools：

```
https://devtools.vuejs.org/guide/installation.html
```



#### 启动项目

打开cmd，切换到项目根目录。这里项目根目录是D:\2022.js\代码\第3章\client

执行如下命令：

```
num run serve
```

出现如下界面表示项目启动成功。

![image-20230404165631225](C:\Users\patrick\AppData\Roaming\Typora\typora-user-images\image-20230404165631225.png)

点击local：后面的网址访问一下client这个项目。出现如下页面，这个页面就是项目的首页：

![image-20230404165903991](C:\Users\patrick\AppData\Roaming\Typora\typora-user-images\image-20230404165903991.png)



#### 修改项目端口号

由于项目占用的是8080端口，与后端的tomcat服务器端口号冲突了，所以要改一下项目的端口号。

打开client项目的根目录文件夹，找到里面的vue.config.js文件，打开后在里面添加如下代码：

```
devServer: {
    port: 7070        将端口号设置为7070
}
```

修改后，重新启动项目。



代理 

...