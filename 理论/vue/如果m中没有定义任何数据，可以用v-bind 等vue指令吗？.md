# 如果m中没有定义任何数据，可以用v-bind: 等vue指令吗？

答：m中没有定义任何数据的时候，可不可以用vue指令，是由这个vue指令会不会去m中找数据决定的。如果会去m中找数据，此时如果找不到数据，就会报错。

vue指令不会根据字符串到m中找数据。



### 示例1：

下图中用了vue插值表达式{{}}，并且在m中并没有定义数据，但是不会报错。因为{{}}中的内容是个字符串(用' '引起来了)，插值表达式{{}}并不会根据字符串到m中找数据，所以尽管m中没有定义数据，也不会报错。

![image-20230401214551860](C:\Users\patrick\AppData\Roaming\Typora\typora-user-images\image-20230401214551860.png)

### 示例2：

下图中，m中没有定义任何数据(data中无内容)，并且在<span>的class属性前面用了v-bind: 指令，此时要注意：一定要将style1和style2用引号引起来，作为两个字符串，否则v-bind:会根据style1和style2到m中找数据，就会导致报错。

![image-20230401210514990](C:\Users\patrick\AppData\Roaming\Typora\typora-user-images\image-20230401210514990.png)