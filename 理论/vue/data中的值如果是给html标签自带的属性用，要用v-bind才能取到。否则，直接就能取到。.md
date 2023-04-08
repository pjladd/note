# data中的值如果是给html标签自带的属性用，要用v-bind才能取到。否则，直接就能取到，不用加v-bind。

```
下图中的{{str1}}，是<p>标签中的内容，并不是在<p>的属性中，所以能直接取到data中的值。
下图中的v-html不是<p>的属性，所以可以直接取到data中的值。
```

![image-20230331141313890](C:\Users\patrick\AppData\Roaming\Typora\typora-user-images\image-20230331141313890.png)