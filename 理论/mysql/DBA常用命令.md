# DBA常用命令

重点掌握：
		数据的导入和导出（数据的备份）
		其它命令了解一下即可。（其它命令见 / 培训日志 / mysql / 《MYSQL培训日志》中的DBA命令部分，复制粘贴即可）
	

## 1. 数据导出

​	注意：在windows的dos命令窗口中：
​		mysqldump bjpowernode(数据库名)>D:\bjpowernode.sql(指定导出生成的文件名) -uroot -p123456
​	
​	可以导出指定的表吗？
​		mysqldump bjpowernode(数据库名) emp(表名)>D:\bjpowernode.sql(指定导出生成的文件名) -uroot -p123456

## 2. 数据导入

​	注意：需要先登录到mysql数据库服务器上。
​	然后创建数据库：create database bjpowernode;
​	使用数据库：use bjpowernode
​	然后初始化数据库：source   D:\bjpowernode.sql(.sql的文件名) 
​                                    可以直接将.sql文件拖入mysql命令窗口中，会自动识别拖入的.sql文件的文件名。  

