# 在m中定义的方法中如果要将m中定义的数据进行数学运算，需要将m中定义的数据进行parse，否则得到的是字符串的连接。

示例：下图代码，calculate方法中没有将num1和num2进行parse，得到的num1+num2的结果就是字符串的连接。![image-20230401193506642](C:\Users\patrick\AppData\Roaming\Typora\typora-user-images\image-20230401193506642.png)

![image-20230401193552770](C:\Users\patrick\AppData\Roaming\Typora\typora-user-images\image-20230401193552770.png)

应该修改为：

![image-20230401194018380](C:\Users\patrick\AppData\Roaming\Typora\typora-user-images\image-20230401194018380.png)

![image-20230401194114000](C:\Users\patrick\AppData\Roaming\Typora\typora-user-images\image-20230401194114000.png)