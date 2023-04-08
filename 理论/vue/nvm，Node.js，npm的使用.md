### 1) 安装 nvm（下载nvm-setup.exe，双击安装）

nvm 即 (node version manager)，好处是方便切换 node.js 版本

#### 安装注意事项

1. 要卸载掉现有的 nodejs

2. 提示选择 nvm 和 nodejs 目录时，一定要避免目录中出现空格。默认安装的路径有空格，如下图所示，所以一定要改为另一个路径。

   ![image-20230402211921475](C:\Users\patrick\AppData\Roaming\Typora\typora-user-images\image-20230402211921475.png)

3. nvm的命令是要在cmd窗口中执行的。注意：执行nvm命令的cmd窗口一定要以【管理员身份运行】。

   安装好nvm之后，才能在cmd窗口中执行nvm命令。

4. 首次用cmd执行nvm命令时，要先执行如下命令，来设置好国内镜像地址：

```
nvm node_mirror http://npm.taobao.org/mirrors/node/
nvm npm_mirror https://npm.taobao.org/mirrors/npm/
```



#### 首先查看用nvm可以下载到哪些Node.js的可用版本：

```
nvm list available
```

输出如下：（LTS的意思是长期支持版，也就是说LTS这一列的所有版本都是长期支持版，推荐下载LTS版本。）

```
|   CURRENT    |     LTS      |  OLD STABLE  | OLD UNSTABLE |
|--------------|--------------|--------------|--------------|
|    18.7.0    |   16.16.0    |   0.12.18    |   0.11.16    |
|    18.6.0    |   16.15.1    |   0.12.17    |   0.11.15    |
|    18.5.0    |   16.15.0    |   0.12.16    |   0.11.14    |
|    18.4.0    |   16.14.2    |   0.12.15    |   0.11.13    |
|    18.3.0    |   16.14.1    |   0.12.14    |   0.11.12    |
|    18.2.0    |   16.14.0    |   0.12.13    |   0.11.11    |
|    18.1.0    |   16.13.2    |   0.12.12    |   0.11.10    |
|    18.0.0    |   16.13.1    |   0.12.11    |    0.11.9    |
|    17.9.1    |   16.13.0    |   0.12.10    |    0.11.8    |
|    17.9.0    |   14.20.0    |    0.12.9    |    0.11.7    |
|    17.8.0    |   14.19.3    |    0.12.8    |    0.11.6    |
|    17.7.2    |   14.19.2    |    0.12.7    |    0.11.5    |
|    17.7.1    |   14.19.1    |    0.12.6    |    0.11.4    |
|    17.7.0    |   14.19.0    |    0.12.5    |    0.11.3    |
|    17.6.0    |   14.18.3    |    0.12.4    |    0.11.2    |
|    17.5.0    |   14.18.2    |    0.12.3    |    0.11.1    |
|    17.4.0    |   14.18.1    |    0.12.2    |    0.11.0    |
|    17.3.1    |   14.18.0    |    0.12.1    |    0.9.12    |
|    17.3.0    |   14.17.6    |    0.12.0    |    0.9.11    |
|    17.2.0    |   14.17.5    |   0.10.48    |    0.9.10    |
```



#### 安装指定版本的Node.js：（安装好的Node.js的位置位于：安装nvm的文件夹中）

```
nvm install 版本号

如：nvm install 16.16.0
```



#### 执行 `nvm list` 会列出已安装的Node.js的版本：

![image-20230402214722892](C:\Users\patrick\AppData\Roaming\Typora\typora-user-images\image-20230402214722892.png)



#### 切换到指定版本的Node.js

```
nvm use 版本号

如：nvm use 16.16.0
```



安装好nvm后，nvm的环境变量会自动添加，不用手动添加。但需要手动添加Node.js的PATH环境变量。也就是需要把安装nvm时，给Node.js设置的路径设置到PATH环境变量中。如下图所示的这个路径：

![image-20230402215705421](C:\Users\patrick\AppData\Roaming\Typora\typora-user-images\image-20230402215705421.png)

配置好Node.js的PATH环境变量后，才能在cmd中执行Node.js命令，否则是执行不了的。

可以在cmd中执行如下代码测试是否已经配置好了Node.js的PATH环境变量：

```
node  -v       作用是查看当前使用的Node.js的版本号

npm  -v        查看当前安装的Node.js中包含着的npm的版本。 注：Node.js中包含着npm，所以安装好了Node.js，npm也就装好了。
```



### 2) 检查 npm

npm 是 js 的包管理器，就类似于 java 中的 maven，要确保它使用的是国内镜像

检查镜像：

```
npm get registry
```

如果返回的不是 `https://registry.npm.taobao.org/`，需要做如下设置

```
npm config set registry https://registry.npm.taobao.org/
```



### 3) 搭建前端服务器（比如：后端开发需要tomcat服务器，前端开发也需要服务器）

新建一个用于保存前端项目代码的 client 文件夹，然后打开cmd，切换到新创建的这个client文件夹路径，执行如下命令：

```
npm install express --save-dev      这个命令的意思是安装一个依赖（类似于后端的maven添加依赖），依赖的名字叫做express，express是一个前端用的web服务器（类似于后端用的web服务器tomcat），参数--save-dev是用于指定express这个依赖只在开发过程中存在，将来前端项目打包的时候，这个依赖不会被打到包内，因为express是一个服务器，不需要被打到包内。
```

express依赖安装成功后，在client文件夹中会生成以下3个东西：

![image-20230403204839880](C:\Users\patrick\AppData\Roaming\Typora\typora-user-images\image-20230403204839880.png)

其中package.json就类似于maven中的pom.xml，里面是当前安装的所有依赖的信息。如下图所示：

![image-20230403205227119](C:\Users\patrick\AppData\Roaming\Typora\typora-user-images\image-20230403205227119.png)

上图中的"devDependencies"的"dev"的意思是：它中的依赖只有在开发时才存在。

package.json中的依赖所相关的js包都为于node_modules这个文件夹中。



#### 如何启动express服务器？

要先编写一段js代码，要通过这段js代码才能启动express服务器。

编写代码前，要先修改一下package.json 文件，修改为如下内容：

```
{
  "type": "module",
  "devDependencies": {
    "express": "^4.18.1"
  }
}
```

"type": "module"的作用是：让写js代码的时候可以使用import语法。如下图所示：

![image-20230403211306076](C:\Users\patrick\AppData\Roaming\Typora\typora-user-images\image-20230403211306076.png)





#### 启动express服务器

创建一个js文件，文件名无所谓，这里起名为main.js。这里是将main.js放在了client文件夹中。

编写 main.js 代码

```js
import express from 'express'    意思是导入了一个名为express的方法
const app = express()            调用express()方法，返回值为一个代表了express服务器的对象

app.listen(7070)                 设置服务器的监听端口为7070
```

在cmd中切换到main.js所在的文件夹的路径，然后执行main.js。（作用就是运行前端服务器）

```
node main.js
```

执行后没有任何信息，就表示前端服务器成功运行。

测试：在浏览器中输入：localhost:7070访问一下这个expess服务器。运行结果如下图所示：

![image-20230403212923815](C:\Users\patrick\AppData\Roaming\Typora\typora-user-images\image-20230403212923815.png)

产生上图所示的这个结果的原因是：express服务器中，没有资源映射，内部没有静态资源。



#### 添加静态资源的映射：

在main.js中加入如下代码：

```
app.use(express.static('./'))                   调用use方法，use方法可以用来添加静态资源。experss.static()的作用是指定静态资源的所在目录，要传给experss.static()的参数是字符串(静态资源的所在目录)。'./'的意思是当前目录，也就是main.js所在的目录。这段代码的作用就是设置当前目录为静态资源目录。
```

main.js:

```js
import express from 'express'    意思是导入了一个名为express的方法
const app = express()            调用express()方法，返回值为一个代表了express服务器的对象

app.use(express.static('./'))    设置当前目录为静态资源目录。
app.listen(7070)                 设置服务器的监听端口为7070
```

在当前目录下创建一个静态资源：

例如创建一个index.html。随便写点内容。例如就写如下内容：

![image-20230403214907458](C:\Users\patrick\AppData\Roaming\Typora\typora-user-images\image-20230403214907458.png)

注意：静态资源创建或修改是不用重启express服务器的，直接刷新页面即可。



由于修改了main.js的内容，所以需要重启服务器：

​	 	先退出服务器：

```
 ctrl c 
```

​     	再运行服务器：

```
 node main.js
```



测试：

​	在浏览器中输入localhost:7070/index.html，结果如下：

![image-20230403215228621](C:\Users\patrick\AppData\Roaming\Typora\typora-user-images\image-20230403215228621.png)

为什么是输入：localhost:7070/index.html？

因为index.html和express服务器位于同一个文件夹中。
