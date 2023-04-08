# Js 和 JSON



## Js中创建对象的方式：

### 1.通过“字面量”方式创建对象

（1）对象字面量：就是{ }里面包含了表达这个具体事物（对象）的属性和方法。

使用花括号`{ }`来创建对象，`{ }`中用来定义对象中的属性。属性是一个个 键:值 对的组合，其中键（属性名称）始终是字符串类型的，而值（属性值）则可以是任意类型，例如字符串、数组、函数或其它对象等。不同的属性之间使用逗号进行分隔。

注意：键一定是字符串类型，键可以用" "引起来，也可以不用" "引起来。但是在以下情况下一定需要为键(属性名)添加引号：

- 属性名为 JavaScript 中的保留字；

- 属性名中包含空格或特殊字符（除字母、数字、_ 和 $ 以外的任何字符）；

- 属性名以数字开头。

  

  注：js中不区分双引号" "和单引号' '

```
//利用字面量创建对象{}
//var obj={};//创建空的对象
var obj={
    name:'李四',   //也可以写成 'name' : '李四'
    age:18,
    say:function(){
        console.log('我会说话');
    }
}
//(1)里面的属性或者方法必须以键值对的形式创建： 键(属性名) : 值(属性值)
//(2)多个属性或者方法中间用逗号隔开的
//(3)方法冒号后面跟的是一个匿名函数
```

（2）使用对象

1. 调用对象的属性 我们采取 对象名.属性名，其中.这个小点我们可以理解为“的”

   ```
   console.log(obj.name)//李四
   console.log(obj.age)//18
   ```

2. 调用属性还有另一种方法 对象名['属性名']

   ```
   console.log(obj[name])//李四
   console.log(obj[age])//18
   ```

3. 调用对象的方法 say 对象名.方法名（）

   ```
   obj.say()//我会说话    ps：注意一定不要漏掉小括号
   ```



#### 补充，使用"[ ]"字面量来创建数组：如果是创建数组的话，可以直接使用方括号`[ ]`来定义数组，`[ ]`中为数组中的各个元素，多个元素之间使用逗号`,`进行分隔。示例代码如下：

```
var fruits = [ "apple", "orange", "mango" ];
```

如果是对象数组，则示例代码如下：

```
var objs = [{...},{...},{...}] 
```

如果是二维数组，则示例代码如下：

```
var nums = [[1, 2], [3, 4]];
```

注：js中，数组也是对象，即Array对象，只是创建数组对象的时候不能用字面量{ }，而要用字面量[  ]。



### 2.通过object方式创建

```
var obj=new Object();//创建了一个空的对象
//假设其中有name,age属性,bark方法
obj.name='张三'；
obj.age=18;
obj.bark=function(){
 	...
}
```

### 3.通过“构造函数”方式创建

```
//我们需要创建四大天王的对象
//相同的属性 名字，年龄，性别，   都会唱歌
//构造函数的语法格式
function 构造函数名（）{
    this.属性=值;
    this.方法=function(){
    }
}
new 构造函数名();


示例：function Star(name,age,sex){
    this.name=name;
    this.age=age;
    this.sex=sex;
    this.sing=function(sang){
    console.log(sang);
    }
}

var ldh=new Star('刘德华',28,'男')//调用函数返回的是一个对象
//console.log(typeof ldh)//Object
console.log(ldh.name)//调用
ldh.sing('北京欢迎你')
//1.构造函数名字首字母要大写
//2.我们构造函数不需要return 就可以返回结果
//3.我们调用构造函数必须使用new
var zxy=new Star('张学友',38,'男')
console.log(zxy.name)//张学友
console.log(zxy['age'])//18
zxy.sing('白兰花')

1.构造函数名字首字母要大写
2.我们构造函数不需要return 就可以返回结果
3.我们调用构造函数必须使用new
4.我们只要new Star（）调用函数就创建一个对象ldh{ }
5.我们属性和方法前面必须添加this
```



## JSON

JSON是一种有格式的字符串。用来表示JS对象。

可以调用静态方法JSON.stringify( )将一个js对象转成它对应的JSON字符串。

```
var obj = {a:"hello", b:"world"}
var json = JSON.stringify(obj)
```

可以调用静态方法JSON.parse( )将一个JSON字符串转成一个js对象

```
var json = '{"a":"hello", "b":"world"}'
var obj = JSON.parse(json)
```

JSON字符串的格式和通过字面量方式创建对象时的对象的写法很像。在写JSON字符串时要注意以下几点：

（1） 必须是字符串
（2） 格式参考以字面量方式创建对象时的对象的写法
（3） 字符串的内容中不允许出现单引号，只有最外面可以用单引号引起来，如：'{ "name" : "admin" }' 是可以的，因为' '在最外面。除最外面这个位置以外的其它位置都不允许出现单引号' '。
（4） 对象格式的key部分必须放在双引号中
（5） 不允许出现函数、undefined、NaN、可以出现null
（6） 不允许出现没有意义的逗号

示例：

```
	（n为错，y为对）
	
	var json = {"name":"admin","age":18};   // n，违反了1
	var json = "{'name':'admin'}";          // n，违反了3，4
	var json = "['hello',123,true]";        // n，违反了3
	var json = `["hello",123,true]`;        // y
	var json = '{"name":"admin"}';          // y
	var json = '{"name":"admin",}';         // n，违反了6
	var json = '{"name":"admin","show":undefined}';  // n，违反了5
	var json = '[{"name":"admin"},{"name":"zhangsan"},]';   // n，违反了6
	var json = '[{"name":"admin"},{"name":"zhangsan"}]';   // y
```

