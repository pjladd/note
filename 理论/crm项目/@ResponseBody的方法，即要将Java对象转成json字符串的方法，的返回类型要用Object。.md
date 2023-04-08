# @ResponseBody的方法，即要将Java对象转成json字符串的方法，的返回类型要用Object，这样代码更通用。

### 说明：

例如：返回的实际对象是Strudent对象，返回值类型是Object，是将实际返回的对象(即Student对象)转成json字符串，并不会将Student转为Object对象后再转成json字符串。

例如：

![image-20230323150946295](C:\Users\patrick\AppData\Roaming\Typora\typora-user-images\image-20230323150946295.png)