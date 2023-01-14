使用Navicat连接
1. 打开本地navicat，点击数据库连接，点击 SSH

Host：填远程服务器的ip地址

Port： 填远程服务器的端口（注意不是mysql的端口）

User Name：填远程服务器的用户名（阿里云服务器操作系统不同用户名不同，Windows用户名为administrator，Linux用户名为root。）

Password：填远程服务器的连接密码

⚠️注意：以上填写的都是远程服务器的相关信息

![](https://img-blog.csdnimg.cn/fcb810b8e52941f7b8885355556a3895.png)

2. 不要关闭该连接窗口，点击左上角的 General

Connection Name：填任意名称

Host：填localhost或者127.0.0.1

Port： 填远程服务器上的mysql开放端口，一般情况下是3306

User Name：填远程服务器上的mysql的用户名

Password： 填远程服务器上的mysql的密码

![](https://img-blog.csdnimg.cn/6bf2ecce3677433a9d4b3f3909400292.png)

3. 点击右下角 ***\*连接测试\****

![](https://img-blog.csdnimg.cn/14b7ac3c8a584989a9d89c3a38c32712.png)

4. ***\*save\**** 即可，双击左侧连接名称，至此远程数据库连接成功！