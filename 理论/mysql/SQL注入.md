# SQL注入

```
 	用户名：fdsa
    密码：fdsa' or '1'='1
    
    提示登录成功
```

如上所示，用户输入的密码中含有SQL语句关键字or和=。

当用户提供的信息中含有SQL语句关键字，并且用户提供的信息是参与SQL语句的编译过程，则此时就会发生SQL注入的问题。

### 导致SQL注入的根本原因是什么？

​        用户输入的信息中含有sql语句的关键字，并且这些关键字参与sql语句的编译过程，导致sql语句的原意被扭曲，进而造成sql注入。

### 解决SQL注入问题？

​	只要用户提供的信息不参与SQL语句的编译过程，问题就解决了。因为即使用户提供的信息中含有SQL语句的关键字，但是没有参与编  	译，就不会起作用。要想用户信息不参与SQL语句的编译，那么必须使用java.sql.PreparedStatement。

```
PreparedStatement接口继承了java.sql.Statement
PreparedStatement是属于预编译的数据库操作对象。
PreparedStatement的原理是：预先对SQL语句的框架进行编译，然后再给SQL语句传“值”。

对比一下Statement和PreparedStatement?
    - Statement存在sql注入问题，PreparedStatement解决了SQL注入问题。
    - Statement是编译一次执行一次。PreparedStatement是编译一次，可执行N次。PreparedStatement效率较高一些。
    - PreparedStatement会在编译阶段做类型的安全检查。
      综上所述：PreparedStatement使用较多。只有极少数的情况下需要使用Statement
      
什么情况下必须使用Statement呢？
      业务方面要求必须支持SQL注入的时候。
      Statement支持SQL注入，凡是业务方面要求是需要进行sql语句拼接的，必须使用Statement。
```

用了PreparedStatement之后的测试结果：

```
      用户名：fdas
      密码：fdsa' or '1'='1
      
 
 	  提示登录失败
```

