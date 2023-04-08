## [linux 解决mysql：ERROR 1045 (28000): Access denied for user 'root'@'localhost' (using password: NO/YES)]

解决方法：

1.  

   ```
   sudo vim /etc/my.cnf
   ```

　　在[mysqld]下添加skip-grant-tables，保存。

```
skip-grant-tables
```

![image-20230209125844503](C:\Users\patrick\AppData\Roaming\Typora\typora-user-images\image-20230209125844503.png)

2. 重启mysql

   ```
   sudo service mysqld restart
   ```

   重启之后输入mysql即可进入mysql。

   这样做问题已经解决，但是mysql没有密码了，但最起码mysql能进去了，navicat也能连上mysql了。只能这样用用了。别的更好的解决办法待补充。