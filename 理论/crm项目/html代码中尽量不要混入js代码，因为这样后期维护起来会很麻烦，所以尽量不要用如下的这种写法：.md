# html代码中尽量不要混入js代码，因为这样后期维护起来会很麻烦，

所以尽量不要用如下的这种写法：

![image-20230323201100992](C:\Users\patrick\AppData\Roaming\Typora\typora-user-images\image-20230323201100992.png)

```
上图中的onclick属性的值是一个js函数，其它的都是html代码，这样将js代码和html代码混在一起不好。
```

应该将html代码和js代码分开写，可以用如下的这种方式写：

![image-20230323201704226](C:\Users\patrick\AppData\Roaming\Typora\typora-user-images\image-20230323201704226.png)