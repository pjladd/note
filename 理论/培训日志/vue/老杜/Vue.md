# Vue

## 01-Vue 程序初体验

### 1-第一个Vue程序.html

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>第一个Vue程序</title>
    <!-- 安装vue：当你使用script进行Vue安装之后，上下文中就注册了一个全局变量：Vue -->
    <script src="../js/vue.js"></script>
</head>
<body>
    <!-- 指定Vue实例的挂载位置。 -->
    <!-- <div id="app"></div> -->
    <hr>
    <div id="app"></div>

    <script>
        /* 
        第一步：创建Vue实例
        1. 为什么要new Vue()，直接调用Vue()函数不行吗？
            不行，因为直接调用Vue()函数，不创建实例的话，会出现以下错误：
                Vue is a constructor and should be called with the `new` keyword
        2. 关于Vue构造函数的参数：options？
            option翻译为选项
            options翻译为多个选项
            Vue框架要求这个options参数必须是一个纯粹的JS对象：{}
            在{}对象中可以编写大量的key:value对。
            一个key:value对就是一个配置项。
            主要是通过options这个参数来给Vue实例指定多个配置项。
        3. 关于template配置项：
            template翻译为：模板。
            template配置项用来指定什么？用来指定模板语句，模板语句是一个字符串形式的。
            什么是模板语句？
                Vue框架自己制定了一些具有特殊含义的特殊符号。
                Vue的模板语句是Vue框架自己搞的一套语法规则。
                我们写Vue模板语句的时候，不能乱写，要遵守Vue框架的模板语法规则。
            模板语句可以是一个纯粹的HTML代码，也可以是Vue中的特殊规则。也可以是HTML代码 + Vue的特殊规则。
            template后面的模板语句会被Vue框架的编译器进行编译，转换成浏览器能够识别的HTML代码。
        */
        const myVue = new Vue({
            template : '<h1>Hello Vue!!!!!</h1>'
        })

        /* 
        第二步：将Vue实例挂载到id='app'的元素位置。
        1. Vue实例都有一个$mount()方法，这个方法的作用是什么？
            将Vue实例挂载到指定位置。因为Vue对象是存在于内存中，为了能将Vue对象展现到页面上，需要将Vue对象挂载到html元素上。
        2. #app 显然是ID选择器。这个语法借鉴了CSS。
        */
        myVue.$mount('#app')
        //myVue.$mount(document.getElementById('app'))
    </script>
</body>
</html>
```

### 2-模板语句的数据来源.html

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>模板语句的数据来源</title>
    <!-- 安装Vue -->
    <script src="../js/vue.js"></script>
</head>
<body>
    <!-- 指定挂载位置 -->
    <div id="app"></div>
    <!-- vue程序 -->
    <script>
        /* 
        模板语句的数据来源：
            1. 谁可以给模板语句提供数据支持呢？data选项。
            2. data选项的类型是什么？Object | Function （对象或者函数）
            3. data配置项的专业叫法：Vue 实例的数据对象.（data实际上是给整个Vue实例提供数据来源的。）
            4. 如果data是对象的话，对象必须是纯粹的对象 (含有零个或多个的 key/value 对)
            5. data数据如何插入到模板语句当中？
                {{}} 这是Vue框架自己搞的一套语法，别的框架看不懂的，浏览器也是不能够识别的。
                Vue框架自己是能够看懂的。这种语法在Vue框架中被称为：模板语法中的插值语法。（有的人把他叫做胡子语法。）
                怎么用？
                    {{data的key}}
                插值语法的小细节：
                    {这里不能有其它字符包括空格{
                    }这里不能有其它字符包括空格}
            
        */
        new Vue({
            template : `<h1>最近非常火爆的电视剧{{name}}，它的上映日期是{{releaseTime}}。主角是{{lead.name}}，年龄是{{lead.age}}岁。
                其他演员包括：{{actors[0].name}}({{actors[0].age}}岁)，{{actors[1].name}}({{actors[1].age}}岁)。{{a.b.c.d.e.name}}
                </h1>`,
            data : {
                name : '狂飙!!!',
                releaseTime : '2023年1月2日',
                lead : {
                    name : '高启强',
                    age : 41
                },
                actors : [
                    {
                        name : '安欣',
                        age : 41
                    },
                    {
                        name : '高启兰',
                        age : 29
                    }
                ],
                a : {
                    b : {
                        c : {
                            d : {
                                e : {
                                    name : '呵呵'
                                }
                            }
                        }
                    }
                }
            }
        }).$mount('#app')
    </script>
</body>
</html>
```

### 3-template配置项详解.html

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>template配置项详解</title>
    <!-- 安装Vue -->
    <script src="../js/vue.js"></script>
</head>
<body>
    <!-- 指定挂载位置 -->
    <!-- 注意：以下代码就是只有Vue框架能够看懂的代码了。下面的代码就是一个模板语句。这个代码是需要Vue框架编译，然后渲染的。 -->
    <div id="app">
        <div>
            <h1>{{msg}}</h1>
            <h1>{{name}}</h1>
        </div>
    </div>

    <!-- vue程序 -->
    <script>
        // Vue.config是Vue的全局配置对象。
        // productionTip属性可以设置是否生成生产提示信息。
        // 默认值：true。如果是false则表示阻止生成提示信息。
        //Vue.config.productionTip = false

        /* 
        关于模板语句：
        只要data中的数据发生变化，与这个数据相关的模板语句一定会重新编译，重新渲染。
        
        关于template配置项：
            1.template后面指定的是模板语句，但是模板语句中只能有一个根节点（根html标签）。
            2.只要data变，template就会重新编译，重新渲染，因为tamplate中有模板语句。
            3.如果使用template配置项的话，指定挂载位置的元素会被替换，也就是将挂载位置的所有html代码(包括挂载位置的那个标签)替换为tamplate中的内容。
            4.好消息：目前我们可以不使用template来编写模板语句。这些模板语句可以直接写到html标签中。Vue框架能够找到并编译，然后渲染。
            5.如果没有使用template配置项，而是直接将模板语句编写到HTML标签中，指定的挂载位置就不会被替换了。
        
        关于$mount('#app')：
            在Vue中有一个配置项：el
            el配置项和$mount()可以达到同样的效果。所以可以不使用$mount('#app')的方式进行挂载了。
            el配置项的作用？
                告诉Vue实例去接管哪个容器(容器就是挂载位置，也就是内部有模板语句的html标签)。
                el : '#app'，表示让Vue实例去接管id='app'的容器。
                el : '#app' 的作用就等价于$mount('#app')  
            el其实是element的缩写。被翻译为元素。
            
         如果一段html代码中，含有Vue模板语句，如果这段html代码没有被Vue对象接管，则这段html代码就不能被Vue框架编译和渲染，则这段html代码中的Vue模板语句就会被浏览器理解为普通字符串显示出来。
        */
        new Vue({
            // 下面这个是错误的，因为根标签有2个，都是<h1>
            //template : '<h1>{{msg}}</h1><h1>动力节点老杜</h1>',
            //下面这个是正确的，因为根标签只有一个，根标签是<div>
            /* template : '
            <div>
                <h1>{{msg}}</h1>
                <h1>{{name}}</h1>
            </div>
            ', */
            data : {
                msg : 'Hello Vue!!!!!!!',
                name : 'a动力节点老杜!!!!!!'
            },
            el : '#app'
            //el : document.getElementById('app')
        })
        //}).$mount('#app')
        
    </script>
</body>
</html>
```

### 4-Vue实例和容器是一夫一妻制.html

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Vue实例 和 容器 的关系是：一夫一妻制。一个Vue对象只能接管一个容器，一个容器只能被一个Vue对象接管。Vue对象和容器是一对一关系。</title>
    <!-- 安装Vue -->
    <script src="../js/vue.js"></script>
</head>
<body>
    <!-- 准备容器 -->
    <div class="app">
        <h1>{{msg}}</h1>
    </div>

    <div class="app">
        <h1>{{msg}}</h1>
    </div>

    <!-- 准备容器 -->
    <div id="app2">
        <h1>{{name}}</h1>
    </div>

    <!-- vue程序 -->
    <script>
        /* 
            验证：一个Vue实例可以接管多个容器吗？
                不能。一个Vue实例只能接管一个容器。一旦接管到容器之后，即使后面有相同的容器，Vue也是不管的。因为Vue实例已经“娶到媳妇”了。
        */
        new Vue({
            el : '.app',
            data : {
                msg : 'Hello Vue!'
            }
        })

        new Vue({
            el : '#app2',
            data : {
                name : 'zhangsan'
            }
        })

        // 这个Vue实例想去接管 id='app2'的容器，但是这个容器已经被上面那个Vue接管了。他只能“打光棍”了。
        new Vue({
            el : '#app2',
            data : {
                name : 'jackson'
            }
        })
        
    </script>


</body>
</html>
```



## 02-Vue核心技术

### 1-模板语法之插值.html

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>模板语法之插值语法{{}}，注意：插值语法{{}}是要写在标签体中的。</title>
    <!-- 安装Vue -->
    <script src="../js/vue.js"></script>
</head>
<body>
    <!-- 
        主要研究：{{这里可以写什么}}
        1. 在data中声明的变量、函数等都可以。
        2. 常量都可以。
        3. 只要是合法的javascript表达式，都可以。
        4. 模板表达式都被放在沙盒中，只能访问全局变量的一个白名单，如 Math 和 Date 等。这句话的意思是：白名单中的东西都能在{{}}中访问到。也就是说，白名单中的东西都能写在{{}}中。白名单中的内容如下：
            'Infinity,undefined,NaN,isFinite,isNaN,' 
            'parseFloat,parseInt,decodeURI,decodeURIComponent,encodeURI,encodeURIComponent,' 
            'Math,Number,Date,Array,Object,Boolean,String,RegExp,Map,Set,JSON,Intl,' 
            'require'
     -->
    <!-- 准备容器 -->
    <div id="app">
        <!-- 在data中声明的 -->
        <!-- 这里就可以看做在使用msg变量。 -->
        <h1>{{msg}}</h1>
        <h1>{{sayHello()}}</h1>
        <!-- <h1>{{i}}</h1> -->
        <!-- <h1>{{sum()}}</h1> -->

        <!-- 常量 -->
        <h1>{{100}}</h1>
        <h1>{{'hello vue!'}}</h1>
        <h1>{{3.14}}</h1>

        <!-- javascript表达式 -->
        <h1>{{1 + 1}}</h1>
        <h1>{{'hello' + 'vue'}}</h1>
        <h1>{{msg + 1}}</h1>
        <h1>{{'msg' + 1}}</h1>
        <h1>{{gender ? '男' : '女'}}</h1>
        <h1>{{number + 1}}</h1>
        <h1>{{'number' + 1}}</h1>
        <h1>{{msg.split('').reverse().join('')}}</h1>

        <!-- 错误的：不是表达式，这是语句。 -->
        <!-- <h1>{{var i = 100}}</h1> -->

        <!-- 在白名单里面的 -->
        <h1>{{Date}}</h1>
        <h1>{{Date.now()}}</h1>
        <h1>{{Math}}</h1>
        <h1>{{Math.ceil(3.14)}}</h1>

    </div>

    <!-- vue程序 -->
    <script>

        // 用户自定义的一个全局变量
        var i = 100
        // 用户自定义的一个全局函数
        function sum(){
            console.log('sum.....');
        }

        new Vue({
            el : '#app',
            data : {
                number : 1,
                gender : true,
                msg : 'abcdef',  // 为了方便沟通，以后我们把msg叫做变量。（这行代码就可以看做是变量的声明。）
                sayHello : function(){
                    console.log('hello vue!');
                }
            }
        })
    </script>
</body>
</html>
```

### 2-模板语法之指令.html

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>模板语法之指令语法 v-??? </title>
    <!-- 安装Vue -->
    <script src="../js/vue.js"></script>
</head>
<body>
    <!-- 
        指令语法：
            1. 什么是指令？有什么作用？
                指令的职责是，当表达式的值改变时，将其产生的连带影响，响应式地作用于 DOM
            2. Vue框架中的所有指令的名字都以“v-”开始。
            3. 插值{{}}是写在标签体当中的，那么指令写在哪里呢？
                Vue框架中所有的指令都是以HTML标签的属性形式存在的，也就是说指令的书写位置是写在HTML标签的属性的位置。例如：
                    <span 指令是写在这里的>{{这里是插值语法的位置}}</span>
                    注意：虽然指令是写在标签的属性位置上，但是这个指令浏览器是无法直接看懂的。
                    是需要先让Vue框架进行编译的，编译之后的内容浏览器是可以看懂的。
            4. 指令的语法规则：
                指令的一个完整的语法格式：v-指令名:参数="表达式"  注意：参数和表达式都不是必须的，要看具体的指令需不需要。
                指令的使用：
                    <HTML标签 v-指令名:参数="表达式"></HTML标签>
                    指令中表达式的位置可以写的东西有哪些?
                        答：和之前在插值语法{{}}中可以写的东西相同。
                        但是需要注意的是：在指令中的表达式位置写的东西不能外层再添加一个{{}}
                    不是所有的指令都有参数和表达式：
                        有的指令，不需要参数，也不需要表达式，例如：v-once
                        有的指令，不需要参数，但是需要表达式，例如：v-if="表达式"
                        有的指令，既需要参数，又需要表达式，例如：v-bind:参数="表达式"
            5. v-once 指令
                作用：只渲染元素一次(只在第一次打开页面的时候渲染)。(比如之后如果data中的相关的数据改变了，v-once修饰的这个html元素及其所有的子节点将被视为静态内容并跳过，不会再进行渲染) 这可以用于优化更新性能。
            
            6. v-if="表达式" 指令
                作用：表达式的执行结果必须得是一个布尔类型的数据：true或者false
                    true：这个指令所在的标签，会被渲染到浏览器当中。
                    false：这个指令所在的标签，不会被渲染到浏览器当中。
     -->
    <!-- 准备一个容器 -->
    <div id="app">
        <h1>{{msg}}</h1>
        <h1 v-once>{{msg}}</h1>
        <h1 v-if="a > b">v-if测试：{{msg}}</h1>
    </div>
    <!-- vue程序 -->
    <script>
        new Vue({
            el : '#app',
            data : {
                msg : 'Hello Vue!',
                a : 10,
                b : 11
            }
        })
    </script>
</body>
</html>
```

### 3-v-bind指令详解.html

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>v-bind指令详解（它是一个负责动态绑定的指令）</title>
    <!-- 安装Vue -->
    <script src="../js/vue.js"></script>
</head>
<body>
    <!-- 
        v-bind指令详解
            1. 这个指令是干啥的？
                它可以让HTML标签的某个属性的值产生动态的效果。
            2. v-bind指令的语法格式：
                <HTML标签 v-bind:参数="表达式"></HTML标签>
            3. v-bind指令的编译原理？
                编译前：
                    <HTML标签 v-bind:参数="表达式"></HTML标签>
                编译后：
                    <HTML标签 参数="表达式的执行结果"></HTML标签>
                注意两项：
                    第一：在编译的时候v-bind后面的“参数名”会被编译为HTML标签的“属性名”
                    第二：表达式会关联data，当data发生改变之后，表达式的执行结果就会发生变化。
                    所以，连带的就会产生动态效果。
            4. v-bind因为很常用，所以Vue框架对该指令提供了一种简写方式：
                只是针对v-bind提供了以下简写方式：
                    <img :src="imgPath">
            
            5. 什么时候使用插值语法？什么时候使用指令？
                凡是标签体当中的内容要想动态，需要使用插值语法。
                只要向让HTML标签的属性动态，需要使用指令语法。
     -->
    <!-- 准备一个容器 -->
    <div id="app">
        <!-- 注意：以下代码中 msg 是变量名。 -->
        <!-- 注意：原则上v-bind指令后面的这个参数名可以随便写，可以随便写的意思是不会报错。 -->
        <!-- 虽然可以随便写，但大部分情况下，这个参数名还是需要写成该HTML标签支持的属性名。这样才会有意义。 -->
        <span v-bind:xyz="msg"></span>
        
        <!-- <span v-bind:xyz="msg"></span> 编译后为：<span xyz="Hello Vue!"></span> -->

        <!-- 这个表达式带有单引号，这个'msg'就不是变量了，是常量。 -->
        <span v-bind:xyz="'msg'"></span>

        <!-- v-bind实战 -->
        <img src="../img/1.jpg"> <br>
        <img v-bind:src="imgPath"> <br>

        <!-- v-bind简写形式 -->
        <img :src="imgPath"> <br>

        <!-- 这是一个普通的文本框 -->
        <input type="text" name="username" value="zhangsan"> <br>
        <!-- 以下文本框可以让value这个数据变成动态的：这个就是典型的动态数据绑定。 -->
        <input type="text" name="username" :value="username"> <br>

        <!-- 使用v-bind也可以让超链接的地址动态 -->
        <a href="https://www.baidu.com">走起</a> <br>
        <a :href="url">走起2</a> <br>

        <!-- 不能采用以下写法吗？ -->
        <!-- 
            不能这样，报错了，信息如下：
            Interpolation inside attributes has been removed. 
            Use v-bind or the colon shorthand instead. For example, 
            instead of <div id="{{ val }}">, use <div :id="val">
            
            属性内部插值这种语法已经被移除了。（可能Vue在以前的版本中是支持这种写法的，但是现在不允许了。）
            请使用v-bind或冒号速记来代替。
            请使用 <div :id="val"> 来代替 <div id="{{ val }}">

         -->
        <!-- <a href="{{url}}">走起3</a>  -->

        <h1>{{msg}}</h1>

    </div>
    <!-- vue程序 -->
    <script>
        
        // 赋值的过程就可以看做是一种绑定的过程。
        //let i = 100

        new Vue({
            el : '#app',
            data : {
                msg : 'Hello Vue!',
                imgPath : '../img/1.jpg',
                username : 'jackson',
                url : 'https://www.baidu.com'
            }
        })
    </script>
</body>
</html>
```

### 4-v-model指令详解.html

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>v-model指令详解</title>
    <!-- 安装Vue -->
    <script src="../js/vue.js"></script>
</head>
<body>
    <!-- 
        v-bind和v-model的区别和联系
            1. v-bind和v-model这两个指令都可以完成数据绑定。
            2. v-bind是单向数据绑定。
                data ===> 视图
            3. v-model是双向数据绑定。
                data <===> 视图
            4. v-bind可以使用在任何HTML标签当中。v-model只能使用在表单类元素上，例如：
                input标签、select标签、textarea标签。
                为什么v-model的使用会有这个限制呢？
                    因为表单类的元素才能给用户提供交互输入的界面。
                v-model指令通常只用在value属性上面。
            5. v-bind和v-model都有简写方式：
                v-bind简写方式：
                    v-bind:参数="表达式"    简写为      :参数="表达式"
                v-model简写方式：v-model:默认后面跟的是value属性
                    v-model:value="表达式"  简写为      v-model="表达式"
     -->
    <!-- 准备一个容器 -->
    <div id="app">
        v-bind指令：<input type="text" v-bind:value="name1"><br>
        v-model指令：<input type="text" v-model:value="name2"><br>

        <!-- 以下报错了，因为v-model不能使用在这种元素上。 -->
        <!-- <a v-model:href="url">百度</a> -->

        v-bind指令：<input type="text" :value="name1"><br>
        v-model指令：<input type="text" v-model="name2"><br>

        消息1：<input type="text" :value="msg"><br>
        消息2：<input type="text" v-model="msg"><br>
    </div>

    <!-- vue程序 -->
    <script>
        new Vue({
            el : '#app',
            data : {
                name1 : 'zhangsan',
                name2 : 'wangwu',
                url : 'https://www.baidu.com',
                msg : 'Hello Vue!'
            }
        })
    </script>
</body>
</html>
```

### 5-初识MVVM分层思想.html

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>初识MVVM分层思想</title>
    <script src="../js/vue.js"></script>
</head>
<body>
    <!-- 
        1. MVVM是什么？
            M：Model（模型/数据）
            V：View（视图）
            VM：ViewModel（视图模型）：VM是MVVM中的核心部分。（它起到一个核心的非常重要的作用。）
            MVVM是目前前端开发领域当中非常流行的开发思想。(一种架构模式。)
            目前前端的大部分主流框架都实现了这个MVVM思想，例如Vue，React等。
        2. Vue框架遵循MVVM吗？
            虽然没有完全遵循 MVVM 模型，但是 Vue 的设计也受到了它的启发。
            Vue框架基本上也是符合MVVM思想的。

        3. MVVM模型当中倡导了Model和View进行了分离，为什么要分离？
            假如Model和View不分离，使用最原始的原生的javascript代码写项目：
                如果数据发生任意的改动，接下来我们需要编写大篇幅的操作DOM元素的JS代码。

            将Model和View分离之后，出现了一个VM核心，这个VM把所有的脏活累活给做了，
            也就是说，当Model发生改变之后，VM自动去更新View。当View发生改动之后，
            VM自动去更新Model。我们再也不需要编写操作DOM的JS代码了。开发效率提高了很多。
     -->
     <!-- 准备容器 -->
     <!-- View V-->
     <div id="app">
        姓名：<input type="text" v-model="name">
     </div>

     <!-- vue程序 -->
     <script>
        // ViewModel  VM
        const vm = new Vue({
            el : '#app',
            // Model  M
            data : {
                name : 'zhangsan'
            }
        })
     </script>
</body>
</html>
```

### 6-认识vm.html

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>认识vm</title>
    <!-- 安装Vue -->
    <script src="../js/vue.js"></script>
</head>
<body>
    <!-- 
        1. 通过Vue实例都可以访问哪些属性？(通过vm都可以vm. 什么。)
            Vue实例中的属性很多，有的以 $ 开始，有的以 _ 开始。
            所有以 $ 开始的属性，可以看做是公开的属性，这些属性是供程序员使用的。
            所有以 _ 开始的属性，可以看做是私有的属性，这些属性是Vue框架底层使用的。一般我们程序员很少使用。
            通过vm也可以访问Vue实例对象的原型对象上的属性，例如：vm.$delete...
        2. 
     -->
    <div id="app">
        <h1>{{msg}}</h1>
    </div>
    <script>

        let dataObj = {
            msg : 'Hello Vue!'
        }

        const vm = new Vue({
            el : '#app',
            data : dataObj
        })

        // 按说msg是dataObj对象的属性。
        console.log('dataObj的msg', dataObj.msg);

        // 为什么msg属性可以通过vm来访问呢？
        // 这是因为Vue框架底层使用了数据代理机制。
        // 要想搞明白数据代理机制，必须有一个基础知识点要学会：Object.defineProperty()。
        console.log('vm的msg', vm.msg);
        

    </script>
</body>
</html>
```

### 7-Object的defineProperty.html

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Object.defineProperty()</title>
</head>
<body>
    <!-- 
        Object.defineProperty()
        1. 这个方法是ES5新增的。
        2. 这个方法的作用是：给对象新增属性，或者设置对象原有的属性。
        3. 怎么用？
            Object.defineProperty(给哪个对象新增属性, '新增的这个属性名叫啥', {给新增的属性设置相关的配置项key:value对})
        4. 第三个参数是属性相关的配置项，配置项都有哪些？每个配置项的作用是啥？
            value 配置项：给属性指定值
            writable 配置项：设置该属性的值是否可以被修改。true表示可以修改。false表示不能修改。
            getter方法 配置项：不需要我们手动调用的。当读取属性值的时候，getter方法被自动调用。
                * getter方法的返回值非常重要，这个返回值就代表这个属性它的值。
            setter方法 配置项：不需要我们手动调用的。当修改属性值的时候，setter方法被自动调用。
                * setter方法上是有一个参数的，这个参数可以接收传过来的值。
            注意：当配置项当中有setter和getter的时候，value和writable配置项都不能存在。
     -->
     <script>

        // 这是一个普通的对象
        let phone = {}

        // 临时变量
        let temp

        // 给上面的phone对象新增一个color属性
        Object.defineProperty(phone, 'color', {
            //value : '太空灰',
            //writable : true,
            // getter方法配置项
            get : function(){
                console.log('getter方法执行了@@@');
                //return '动态'
                //return this.color
                return temp
            },
            // setter方法配置项
            set : function(val){
                console.log('setter方法执行了@@@',val);
                //this.color = val
                temp = val
            }
        })

     </script>
</body>
</html>
```

### 8-数据代理机制.html

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>数据代理机制</title>
    <script src="../js/vue.js"></script>
</head>
<body>

    <div id="app">
        <h1>{{msg}}</h1>
    </div>
    
    <script>
        const vm = new Vue({
            el : '#app',
            data : {
                msg : 'Hello Vue!'
            }
        })
    </script>

    <!-- 
        1. 什么是数据代理机制？
            通过访问 代理对象的属性 来间接访问 目标对象的属性。
            数据代理机制的实现需要依靠：Object.defineProperty()方法。
        2. ES6新特性：
            在对象中的函数/方法 :function 是可以省略的。
     -->
     <script>

        // 目标对象
        let target = {
            name : 'zhangsan'
        }

        // 代理对象
        let proxy = {}

        // 如果要实现数据代理机制的话，就需要给proxy新增一个name属性。
        // 注意：代理对象新增的这个属性的名字 和 目标对象的属性名要一致。
        Object.defineProperty(proxy, 'name', {
            // get : function(){
            //     // 间接访问目标对象的属性
            //     return target.name
            // },
            // set : function(val){
            //     target.name = val
            // }

            get(){
                console.log('getter方法执行了@@@@');
                return target.name
            },
            set(val){
                target.name = val
            }
        })

        // let target = {
        //     name : 'zhangsan'
        // }

        // const vm = new Vue({
        //     el : '#app',
        //     data : target
        // })
     </script>
</body>
</html>
```

### 9-Vue数据代理机制对属性名的要求.html

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Vue数据代理机制对属性名的要求</title>
    <!-- 安装Vue -->
    <script src="../js/vue.js"></script>
</head>
<body>
    <!-- 
        1. Vue实例不会给以_和$开始的属性名做数据代理。
        
        2. 为什么？
            如果允许给_或$开始的属性名做数据代理的话。
            vm这个Vue实例上可能会出现_xxx或$xxx属性，
            而这个属性名可能会和Vue框架自身的属性名冲突。

        3. 在Vue当中，给data对象的属性名命名的时候，不能以_或$开始。
     -->
    <!-- 容器 -->
    <div id="app">
        <h1>{{msg}}</h1>
    </div>
    <!-- vue程序 -->
    <script>
        const vm = new Vue({
            el : '#app',
            data : {
                msg : 'Hello Vue!',
                _name : 'zhangsan',
                $age : 20
            }
        })
    </script>
</body>
</html>
```

### 10-手写Vue框架数据代理的实现.html

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>手写Vue框架数据代理的实现</title>
    <!-- 安装我们自己的Vue -->
    <script src="../js/myvue.js"></script>
    <!-- 安装Vue -->
    <!-- <script src="../js/vue.js"></script> -->
</head>
<body>
    <!-- 容器 -->
    <!-- <div id="app">
        <h1>{{msg}}</h1>
    </div> -->

    <!-- Vue代码 -->
    <script>
        // const vm = new Vue({
        //     el : '#app',
        //     data : {
        //         msg : 'Hello Vue!',
        //         name : 'jackson',
        //         age : 30
        //     }
        // })

        const vm = new Vue({
            data : {
                msg : 'Hello Vue!',
                _name : 'jackson',
                $age : 30
            }
        })

    </script>

</body>
</html>
```

### 11-解读Vue框架源代码.html

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>解读Vue框架源代码</title>
    <!-- 安装Vue -->
    <script src="../js/vue.js"></script>
</head>
<body>
    <!-- 
        Vue框架源代码中关键性代码：
        1. var data = vm.$options.data;
            注意：这是获取data。程序执行到这里的时候vm上还没有 _data 属性。
        2. data = vm._data = isFunction(data) ? getData(data, vm) : data || {};
            程序执行完这个代码之后，vm对象上多了一个_data这样的属性。
            通过以上源码解读，可以得知data不一定是一个{}，也可以是一个函数。
            代码含义：
                如果data是函数，则调用getData(data, vm)来获取data。
                如果data不是函数，则直接将data返回，给data变量。并且同时将data赋值给vm._data属性了。
            有一个疑问？
                程序执行到这里，为什么要给vm扩展一个_data属性呢？
                    _data属性，以"_"开始，足以说明，这个属性是人家Vue框架底层需要访问的。
                    Vue框架底层它使用vm._data这个属性干啥呢？
                        vm._data是啥？
                            vm._data 是：{
                                            name : 'jackson',
                                            age : 35
                                        }
                vm._data 这个属性直接指向了底层真实的data对象。通过_data访问的name和age是不会走数据代理机制的。
                通过vm._data方式获取name和age的时候，是不会走getter和setter方法的。
            
            注意：对于Vue实例vm来说，不仅有_data这个属性，还有一个$data这个属性。
                   _data 是框架内部使用的，可以看做私有的。
                   $data 这是Vue框架对外公开的一个属性，是给我们程序员使用。

        3. 重点函数：
            function isReserved(str) {
                var c = (str + '').charCodeAt(0);
                return c === 0x24 || c === 0x5f;
            }
            这个函数是用来判断字符串是否以 _ 和 $ 开始的。
            true表示以_或$开始的。
            false表示不是以_或$开始的。
        4. proxy(vm, "_data", key);
            通过这行代码直接进入代理机制（数据代理）。
        5. 重点函数proxy
            function proxy(target, sourceKey, key) { // target是vm，sourceKey是"_data"，key是"age"
                sharedPropertyDefinition.get = function proxyGetter() {
                    return this["_data"]["age"];
                };
                sharedPropertyDefinition.set = function proxySetter(val) {
                    this["_data"]["age"] = val;
                };
                Object.defineProperty(vm, 'age', sharedPropertyDefinition);
            }
     -->
     
    <!-- 容器 -->
    <div id="app">
        <h1>姓名：{{name}}</h1>
        <h1>年龄：{{age}}岁</h1>
    </div>

    <!-- vue代码 -->
    <script>

        function isReserved(str) {
            var c = (str + '').charCodeAt(0);
            return c === 0x24 || c === 0x5f;
        }

        const vm = new Vue({
            el : '#app',
            data : {
                name : 'jackson',
                age : 35
            }
        })

        // 如果我们程序员不想走代理的方式读取data，想直接读取data当中的数据，可以通过_data和$data属性来访问。
        // 建议使用$data这个属性。
        console.log('name = ' + vm.$data.name)
        console.log('age = ' + vm.$data.age)
        
    </script>
</body>
</html>
```

### 12-data也可以是一个函数.html

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>data也可以是一个函数</title>
    <!-- 安装Vue -->
    <script src="../js/vue.js"></script>
</head>
<body>
    <!-- 容器 -->
    <div id="app">
        <h1>{{msg}}</h1>
    </div>
    <!-- vue代码 -->
    <script>
        const vm = new Vue({
            el : '#app',
            // data : {
            //     msg : 'Hello Vue!'
            // }
            // data functions should return an object：data函数应该返回一个对象。
            // data 也可以是一个函数。
            // 如果是函数的话，必须使用return语句返回{}对象。
            // data可以是直接的对象，也可以是一个函数，什么时候使用直接的对象？什么时候使用函数呢？（等你学到组件的时候自然就明白了。）
            // data : function(){
            //     return {
            //         msg : 'Hello Vue!'
            //     }
            // }

            // 在对象当中，函数的 :function 可以省略
            data(){
                return {
                    msg : 'Hello Zhangsan!'
                }
            }
        })

        // 关于配置项：enumerable、configurable
        let phone = {
            name : '苹果X'
        }

        // 给phone对象新增一个color属性
        Object.defineProperty(phone, 'color', {
            value : '奶奶灰',
            
            // true表示该属性是可以遍历的。（可枚举的，可迭代的。）
            // false表示该属性是不可遍历的。
            enumerable : false,

            // true表示该属性是可以被删除的。
            // false表示该属性是不可以被删除的。
            configurable : false
        })

    </script>
</body>
</html>
```

### 13-事件绑定.html

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Vue的事件绑定</title>
    <!-- 安装Vue -->
    <script src="../js/vue.js"></script>
</head>
<body>
    <!-- 
        Vue事件处理:
            1.指令的语法格式：
                <标签 v-指令名:参数名="表达式">{{插值语法}}</标签>
                “表达式”位置都可以写什么？
                    常量、JS表达式、Vue实例所管理的XXX
            2. 在Vue当中完成事件绑定需要哪个指令呢？
                v-on指令。
                语法格式：
                    v-on:事件名="表达式"
                例如：
                    v-on:click="表达式" 表示当发生鼠标单击事件之后，执行表达式。
                    v-on:keydown="表达式" 表示当发生键盘按下事件之后，执行表达式。
            3. 在Vue当中，所有事件所关联的回调函数，需要在Vue实例的配置项methods中进行定义。
                methods是一个对象：{}
                在这个methods对象中可以定义多个回调函数。
            4. v-on指令也有简写形式
                v-on:click 简写为 @click
                v-on:keydown 简写为 @keydown
                v-on:mouseover 简写为 @mouseover
                ....
            5. 绑定的回调函数，如果函数调用时不需要传递任何参数，小括号()可以省略。
            6. Vue在调用回调函数的时候，会自动给回调函数传递一个对象，这个对象是：当前发生的事件对象。
            7. 在绑定回调函数的时候，可以在回调函数的参数上使用 $event 占位符，Vue框架看到这个 $event 占位符之后，会自动将当前事件以对象的形式传过去。
     -->
    <!-- 容器 -->
    <div id="app">
        <h1>{{msg}}</h1>
        <!-- 使用javascript原生代码如何完成事件绑定。 -->
        <button onclick="alert('hello')">hello</button>
        <!-- 使用Vue来完成事件绑定 -->
        <!-- 以下是错误的，因为alert()并没有被Vue实例管理。 -->
        <!-- <button v-on:click="alert('hello')">hello</button> -->
        <!-- 以下是错误的，因为sayHello()并没有被Vue实例管理。 -->
        <!-- <button v-on:click="sayHello()">hello</button> -->
        <!-- 正确的写法 -->
        <button v-on:click="sayHello()">hello</button>
        <!-- v-on指令的简写形式 -->
        <button @click="sayHi()">hi button</button>
        <button @click="sayHi($event, 'jack')">hi button2</button>
        <!-- 绑定的回调函数，如果不需要传任何参数，小括号() 可以省略 -->
        <button @click="sayWhat">what button</button>
    </div>
    <!-- vue代码 -->
    <script>
        // 自定义一个函数
        // function sayHello(){
        //     alert('hello')
        // }

        const vm = new Vue({
            el : '#app',
            data : {
                msg : 'Vue的事件绑定'
            },
            methods : {
                // 回调函数
                // sayHello : function(){
                //     alert('hello')
                // }
                // : function 可以省略
                sayHello(){
                    alert('hello2')
                },
                sayHi(event, name){
                    console.log(name, event)
                    //alert("hi " + name)
                },
                sayWhat(event){
                    //console.log(event)
                    //console.log(event.target)
                    //console.log(event.target.innerText)
                    //alert('what...')
                }
            }
        })
    </script>
</body>
</html>
```

### 14-关于事件回调函数中的this.html

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>关于事件回调函数中的this</title>
    <!-- 安装Vue -->
    <script src="../js/vue.js"></script>
</head>
<body>
    <!-- 容器 -->
    <div id="app">
        <h1>{{msg}}</h1>
        <h1>计数器：{{counter}}</h1>
        <button @click="counter++">点击我加1</button>
        <button @click="add">点击我加1</button>
        <button @click="add2">点击我加1（箭头函数）</button>
    </div>
    <!-- vue代码 -->
    <script>
        const vm = new Vue({
            el : '#app',
            data : {
                msg : '关于事件回调函数中的this',
                counter : 0
            },
            // 1.methods对象中的方法可以通过vm去访问吗？可以。
            // 2.methods对象中的方法有没有做数据代理呢？没有。
            methods : {
                add(){
                    //counter++; // 错误的。
                    // 在这里需要操作counter变量？怎么办？
                    //console.log(vm === this)
                    //console.log(this)
                    this.counter++;
                    //vm.counter++;
                },
                add2:()=>{
                    //this.counter++;
                    //console.log(this === vm)
                    //箭头函数中没有this，箭头函数中的this是从父级作用域当中继承过来的。
                    //对于当前程序来说，父级作用域是全局作用域:window
                    console.log(this)
                },
                sayHi(){
                    alert('hi...')
                }
            }
        })

    </script>
</body>
</html>
```

### 15-methods实现原理.html

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>methods实现原理</title>
    <!-- 引入我们自己的vue.js -->
    <script src="../js/myvue.js"></script>
</head>
<body>
    <!-- vue程序 -->
    <script>
        const vm = new Vue({
            data : {
                msg : 'hello vue!'
            },
            methods : {
                sayHi(){
                    //console.log(this === vm)
                    console.log(this.msg)
                    //alert('hi')
                },
                sayHello(){
                    alert('hello')
                },
                sayWhat : () => {
                    //console.log(this === vm)
                    console.log(this)
                }
            }
        })
        
    </script>
</body>
</html>
```

### 16-事件修饰符.html

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>事件修饰符</title>
    <!-- 安装Vue -->
    <script src="../js/vue.js"></script>
    <style>
        .divList{
            width: 300px;
            height: 200px;
            background-color: aquamarine;
            overflow: auto;
        }
        .item{
            width: 300px;
            height: 200px;
        }
    </style>
</head>
<body>
    <!-- 
        Vue当中提供的事件修饰符：
        .stop ： 停止事件冒泡，等同于 event.stopPropagation()。
        .prevent ： 等同于 event.preventDefault() 阻止事件的默认行为。
        .capture ：添加事件监听器时使用事件捕获模式
                    添加事件监听器包括两种不同的方式：
                        一种是从内到外添加。（事件冒泡模式）
                        一种是从外到内添加。（事件捕获模式）
        .self ：这个事件如果是“我自己元素”上发生的事件，这个事件不是别人给我传递过来的事件，则执行对应的程序。
        .once ： 事件只发生一次
        .passive ：passive翻译为顺从/不抵抗。无需等待，直接继续（立即）执行事件的默认行为。
                    .passive 和 .prevent 修饰符是对立的。不可以共存。（如果一起用，就会报错。）
                    .prevent：阻止事件的默认行为。
                    .passive：解除阻止。
     -->        
    <!-- 容器 -->
    <div id="app">
        <h1>{{msg}}</h1>

        <!-- 阻止事件的默认行为 -->
        <a href="https://www.baidu.com" @click.prevent="yi">百度</a> <br><br>

        <!-- 停止事件冒泡 -->
        <div @click="san">
            <div @click.stop="er">
                <button @click="yi">事件冒泡</button>
            </div>
        </div>

        <br><br>

        <!-- 添加事件监听器时使用事件捕获模式 -->
        <div @click.capture="san">
            <!-- 这里没有添加.capture修饰符，以下这个元素，以及这个元素的子元素，都会默认采用冒泡模式。 -->
            <div @click="er">
                <button @click="yi">添加事件监听器的时候采用事件捕获模式</button>
            </div>
        </div>
        
        <br>
        <br>
        <!-- .self修饰符 -->
        <div @click="san">
            <div @click.self="er">
                <button @click="yi">self修饰符</button>
            </div>
        </div>

        <br>
        <br>
        <!-- 在Vue当中，事件修饰符是可以多个联合使用的。
            但是需要注意：
                @click.self.stop：先.self，再.stop
                @click.stop.self：先.stop，再.self
         -->
        <div @click="san">
            <div @click="er">
                <button @click.self.stop="yi">self修饰符</button>
            </div>
        </div>

        <br>
        <br>
        <!-- .once修饰符：事件只发生一次 -->
        <button @click.once="yi">事件只发生一次</button>

        <!-- .passive修饰符 -->
        <div class="divList" @wheel.passive="testPassive">
            <div class="item">div1</div>
            <div class="item">div2</div>
            <div class="item">div3</div>
        </div>

    </div>
    <!-- vue代码 -->
    <script>
        const vm = new Vue({
            el : '#app',
            data : {
                msg : '事件修饰符'
            },
            methods : {
                yi(event){
                    //alert('去百度！！！!!!')
                    // 手动调用事件对象的preventDefault()方法，可以阻止事件的默认行为。
                    // 在Vue当中，这种事件的默认行为可以不采用手动调用DOM的方式来完成，可以使用事件修饰符:prevent。
                    //event.preventDefault();
                    alert(1)
                },
                er(){
                    alert(2)
                },
                san(){
                    alert(3)
                },
                testPassive(event){
                    for(let i = 0; i < 100000; i++){
                        console.log('test passive')
                    }
                    // 阻止事件的默认行为
                    //event.preventDefault()
                }
            }
        })
    </script>
</body>
</html>
```

### 17-按键修饰符.html

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>按键修饰符</title>
    <script src="../js/vue.js"></script>
</head>
<body>
    <!-- 
        9个比较常用的按键修饰符：
            .enter
            .tab （必须配合keydown事件使用。）
            .delete (捕获“删除”和“退格”键)
            .esc
            .space
            .up
            .down
            .left
            .right
        怎么获取某个键的按键修饰符？
            第一步：通过event.key获取这个键的真实名字。
            第二步：将这个真实名字以kebab-case风格进行命名。
                PageDown是真实名字。经过命名之后：page-down
        按键修饰符是可以自定义的？
            通过Vue的全局配置对象config来进行按键修饰符的自定义。
            语法规则：
                Vue.config.keyCodes.按键修饰符的名字 = 键值
        系统修饰键：4个比较特殊的键
            ctrl、alt、shift、meta
            对于keydown事件来说：只要按下ctrl键，keydown事件就会触发。
            对于keyup事件来说：需要按下ctrl键，并且加上按下组合键，然后松开组合键之后，keyup事件才能触发。
     -->
    <div id="app">
        <h1>{{msg}}</h1>
        回车键：<input type="text" @keyup.enter="getInfo"><br>
        回车键（键值）：<input type="text" @keyup.13="getInfo"><br>
        delete键：<input type="text" @keyup.delete="getInfo"><br>
        esc键：<input type="text" @keyup.esc="getInfo"><br>
        space键：<input type="text" @keyup.space="getInfo"><br>
        up键：<input type="text" @keyup.up="getInfo"><br>
        down键：<input type="text" @keyup.down="getInfo"><br>
        left键：<input type="text" @keyup.left="getInfo"><br>
        right键：<input type="text" @keyup.right="getInfo"><br>
        <!-- tab键无法触发keyup事件。只能触发keydown事件。 -->
        tab键： <input type="text" @keyup.tab="getInfo"><br>
        tab键（keydown）： <input type="text" @keydown.tab="getInfo"><br>
        PageDown键： <input type="text" @keyup.page-down="getInfo"><br>
        huiche键： <input type="text" @keyup.huiche="getInfo"><br>
        ctrl键(keydown)： <input type="text" @keydown.ctrl="getInfo"><br>
        ctrl键(keyup)： <input type="text" @keyup.ctrl="getInfo"><br>
        ctrl键(keyup)： <input type="text" @keyup.ctrl.i="getInfo"><br>
    </div>

    <script>

        // 自定义了一个按键修饰符：.huiche 。代表回车键。
        Vue.config.keyCodes.huiche = 13

        const vm = new Vue({
            el : '#app',
            data : {
                msg : '按键修饰符'
            },
            methods : {
                getInfo(event){
                    // 当用户键入回车键的时候，获取用户输入的信息。
                    //if(event.keyCode === 13){
                        console.log(event.target.value)
                    //}
                    console.log(event.key)
                }
            }
        })
    </script>
</body>
</html>
```

### 18-反转字符串.html

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>反转字符串</title>
    <script src="../js/vue.js"></script>
</head>
<body>
    <div id="app">
        <h1>{{msg}}</h1>
        输入的信息：<input type="text" v-model="info"> <br>
        <!-- 
            三个问题：
                1. 可读性差。
                2. 代码没有得到复用。
                3. 难以维护。
         -->
        反转的信息：{{info.split('').reverse().join('')}} <br>
        反转的信息：{{info.split('').reverse().join('')}} <br>
        反转的信息：{{info.split('').reverse().join('')}} <br>
        反转的信息：{{info.split('').reverse().join('')}} <br>
        反转的信息：{{info.split('').reverse().join('')}} <br>
    </div>
    <script>
        const vm = new Vue({
            el : '#app',
            data : {
                msg : '计算属性-反转字符串案例',
                info : ''
            }
        })
    </script>
</body>
</html>
```

### 19-反转字符串methods实现.html

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>反转字符串methods实现</title>
    <script src="../js/vue.js"></script>
</head>
<body>
    <div id="app">
        <h1>{{msg}}</h1>
        输入的信息：<input type="text" v-model="info"> <br>
        <!-- 在插值语法中可以调用方法，小括号不能省略。这个方法需要是Vue实例所管理的。 -->
        反转的信息：{{reverseInfo()}} <br>
        反转的信息：{{reverseInfo()}} <br>
        反转的信息：{{reverseInfo()}} <br>
        反转的信息：{{reverseInfo()}} <br>
    </div>
    <script>
        const vm = new Vue({
            el : '#app',
            data : {
                msg : '计算属性-反转字符串案例',
                info : ''
            },
            methods : {
                // 反转信息的方法
                reverseInfo(){
                    console.log('@')
                    return this.info.split('').reverse().join('');
                }
            }
        })
    </script>
</body>
</html>
```

### 20-反转字符串计算属性实现.html

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>反转字符串计算属性实现</title>
    <script src="../js/vue.js"></script>
</head>
<body>
    <!-- 
        计算属性：
        1. 什么是计算属性？
            使用Vue的原有属性，经过一系列的运算/计算，最终得到了一个全新的属性，叫做计算属性。
            Vue的原有属性: data对象当中的属性可以叫做Vue的原有属性。
            全新的属性: 表示生成了一个新的属性，和data中的属性无关了，新的属性也有自己的属性名和属性值。
        2. 计算属性怎么用？
            语法格式：需要一个新的配置项 computed
                computed : {
                    // 这是一个计算属性
                    计算属性1 : {
                        // setter 和 getter方法。
                        // 当读取计算属性1的值的时候，getter方法被自动调用。
                        get(){

                        },
                        // 当修改计算属性1的值的时候，setter方法被自动调用。
                        set(val){

                        }
                    },
                    // 这是另一个计算属性
                    计算属性2 : {},
                }
        3. 计算属性的作用？
            代码得到了复用。
            代码更加便于维护了。
            代码的执行效率高了。
     -->
    <div id="app">
        <h1>{{msg}}</h1>
        输入的信息：<input type="text" v-model="info"> <br>
        反转的信息：{{reversedInfo}}<br>
        反转的信息：{{reversedInfo}}<br>
        反转的信息：{{reversedInfo}}<br>
        反转的信息：{{reversedInfo}}<br>
        反转的信息：{{reversedInfo}}<br>
        {{hehe}} <br>
        {{hehe}} <br>
        {{hehe}} <br>
        {{hehe}} <br>
        {{hehe}} <br>
        {{hello()}} <br>
        {{hello()}} <br>
        {{hello()}} <br>
        {{hello()}} <br>
        {{hello()}} <br>
    </div>
    <script>
        const vm = new Vue({
            el : '#app',
            data : {
                msg : '计算属性-反转字符串案例',
                info : ''
            },
            methods : {
                hello(){
                    console.log('hello方法执行了')
                    return 'hello'
                }
            },
            computed : {
                // 可以定义多个计算属性
                hehe : {
                    // get方法的调用时机包括两个
                    // 第一个时机：第一次访问这个属性的时候。
                    // 第二个时机：该计算属性所关联的Vue原有属性的值发生变化时，getter方法会被重新调用一次。
                    get(){
                        console.log('getter方法调用了')
                        //console.log(this === vm)
                        return 'haha' + this.info
                    },
                    // 不能使用箭头函数，使用箭头函数会导致this的指向是：window
                    // get:()=>{
                    //     console.log('getter方法调用了')
                    //     console.log(this === vm)
                    //     return 'haha'
                    // },
                    set(val){
                        console.log('setter方法调用了')
                        //console.log(this === vm)
                    }
                },
                // 完整写法
                /* reversedInfo : { 
                    get(){
                        return this.info.split('').reverse().join('')
                    },
                    // 当修改计算属性的时候，set方法被自动调用。
                    set(val){
                        //console.log('setter方法被调用了。')
                        // 不能这么做，这样做就递归了。
                        //this.reversedInfo = val
                        // 怎么修改计算属性呢？原理：计算属性的值变还是不变，取决于计算属性关联的Vue原始属性的值。
                        // 也就是说：reversedInfo变还是不变，取决于info属性的值变不变。
                        // 本质上：修改计算属性，实际上就是通过修改Vue的原始属性来实现的。
                        this.info = val.split('').reverse().join('')
                    }
                } */

                // 简写形式：set不需要的时候。
                reversedInfo(){ 
                    return this.info.split('').reverse().join('')
                }
            }
        })
    </script>
</body>
</html>
```

### 21-侦听属性的变化.html

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>侦听/监视 属性的变化</title>
    <script src="../js/vue.js"></script>
</head>
<body>
    <div id="app">
        <h1>{{msg}}</h1>
        数字：<input type="text" v-model="number"><br>
        数字：<input type="text" v-model="a.b"><br>
        数字：<input type="text" v-model="a.c"><br>
        数字：<input type="text" v-model="a.d.e.f"><br>
        数字(后期添加监视)：<input type="text" v-model="number2"><br>
    </div>
    <script>
        const vm = new Vue({
            el : '#app',
            data : {
                number2 : 0,
                msg : '侦听属性的变化',
                number : 0,
                // a属性中保存的值是一个对象的内存地址。
                // a = 0x2356
                a : {
                    b : 0,
                    c : 0,
                    d : {
                        e : {
                            f : 0
                        }
                    }
                }
            },
            computed : {
                hehe(){
                    return 'haha' + this.number
                }
            },
            watch : {
                // 可以监视多个属性
                // 监视哪个属性，请把这个属性的名字拿过来即可。
                // 可以监视Vue的原有属性
                /* number : {
                    // 初始化的时候，调用一次handler方法。
                    immediate : true,
                    // 这里有一个固定写死的方法，方法名必须叫做：handler
                    // handler方法什么时候被调用呢？当被监视的属性发生变化的时候，handler就会自动调用一次。
                    // handler方法上有两个参数：第一个参数newValue，第二个参数是oldValue
                    // newValue是属性值改变之后的新值。
                    // oldValue是属性值改变之前的旧值。
                    handler(newValue, oldValue){
                        console.log(newValue, oldValue)
                        // this是当前的Vue实例。
                        // 如果该函数是箭头函数，这个this是window对象。不建议使用箭头函数。
                        console.log(this)
                    }
                }, */
                // 无法监视b属性，因为b属性压根不存在。
                /* b : {  
                    handler(newValue, oldValue){
                        console.log('@')
                    } 
                } */
                
                // 如果监视的属性具有多级结构，一定要添加单引号：'a.b'
                /* 'a.b' : {  
                    handler(newValue, oldValue){
                        console.log('@')
                    } 
                },

                'a.c' : {  
                    handler(newValue, oldValue){
                        console.log('@')
                    } 
                }, */

                a : {
                    // 启用深度监视，默认是不开启深度监视的。
                    // 什么时候开启深度监视：当你需要监视一个具有多级结构的属性，并且监视所有的属性，需要启用深度监视。
                    deep : true,  

                    handler(newValue, oldValue){
                        console.log('@')
                    } 
                },

                // 注意：监视某个属性的时候，也有简写形式，什么时候启用简写形式？
                // 当只有handler回调函数的时候，可以使用简写形式。
                number(newValue, oldValue){
                    console.log(newValue, oldValue)
                }

                // 也可以监视计算属性
                /* hehe : {
                    handler(a , b){
                        console.log(a, b)
                    }
                } */
            }
        })

        // 如何后期添加监视？调用Vue相关的API即可。
        // 语法：vm.$watch('被监视的属性名', {})
        /* vm.$watch('number2', {
            immediate : true,
            deep : true,
            handler(newValue, oldValue){
                console.log(newValue, oldValue)
            }
        }) */

        // 这是后期添加监视的简写形式。
        vm.$watch('number2', function(newValue, oldValue){
            console.log(newValue, oldValue)
        })

    </script>
</body>
</html>
```

### 22-比较大小的案例watch实现.html

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>比较大小的案例watch实现</title>
    <script src="../js/vue.js"></script>
</head>
<body>
    <div id="app">
        <h1>{{msg}}</h1>
        数值1：<input type="number" v-model="num1"><br>
        数值2：<input type="number" v-model="num2"><br>
        比较大小：{{compareResult}}
    </div>
    <script>
        const vm = new Vue({
            el : '#app',
            data : {
                msg : '比较大小的案例',
                num1 : 0,
                num2 : 0,
                compareResult : ''
            },
            watch : {
                // 监视num1
                num1 : {
                    immediate : true,
                    /* handler(newValue, oldValue){
                        console.log(newValue, oldValue)
                    } */
                    handler(val){
                        //console.log(val)
                        let result = val - this.num2
                        // 这个箭头函数也不是Vue管理的。是javascript引擎负责管理的。调用这个箭头函数的还是window。
                        // 箭头函数没有this，只能向上一级找this，上一级是num1，num1是Vue实例的属性，所以this是Vue实例。
                        setTimeout(() => {
                            console.log(this)
                            if(result == 0){
                                this.compareResult = val + ' = ' + this.num2
                            }else if(result > 0){
                                this.compareResult = val + ' > ' + this.num2
                            }else {
                                this.compareResult = val + ' < ' + this.num2
                            }    
                        }, 1000 * 3)
                        
                    }
                },
                // 监视num2
                num2 : {
                    immediate : true,
                    /* handler(newValue, oldValue){
                        console.log(newValue, oldValue)
                    } */
                    handler(val){
                        //console.log(val)
                        let result = this.num1 - val
                        /* setTimeout(() => {
                            // 虽然这个函数是箭头函数，但是this是Vue实例。
                            console.log(this)
                            if(result == 0){
                                this.compareResult = this.num1 + ' = ' + val
                            }else if(result > 0){
                                this.compareResult = this.num1 + ' > ' + val
                            }else {
                                this.compareResult = this.num1 + ' < ' + val
                            }    
                        }, 1000 * 3) */

                        // 这里虽然是普通函数，但是这个函数并不是Vue管理的。是window负责调用的。
                        // 所以这个普通函数当中的this是window。
                        setTimeout(function(){
                            // 虽然这个函数是普通函数，但是this是window。
                            console.log(this)
                            if(result == 0){
                                this.compareResult = this.num1 + ' = ' + val
                            }else if(result > 0){
                                this.compareResult = this.num1 + ' > ' + val
                            }else {
                                this.compareResult = this.num1 + ' < ' + val
                            }    
                        }, 1000 * 3)
                        
                    }
                }

            }
        })
    </script>
</body>
</html>
```

### 23-比较大小的案例computed实现.html

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>比较大小的案例computed实现</title>
    <script src="../js/vue.js"></script>
</head>
<body>
    <!-- 
        1. computed和watch如果都能够完成某个功能，优先选择computed。
        2. 有一种情况下，必须使用watch，computed无法完成！
            如果在程序当中采用了异步的方式，只能使用watch。
        3. 什么时候使用箭头函数？什么时候使用普通函数？
            看看这个函数是否属于Vue管理的。
            是Vue管理的函数：统一写普通函数。
            不是Vue管理的函数：统一写箭头函数。
     -->
    <div id="app">
        <h1>{{msg}}</h1>
        数值1：<input type="number" v-model="num1"><br>
        数值2：<input type="number" v-model="num2"><br>
        比较大小：{{compareResult}}
    </div>
    <script>
        const vm = new Vue({
            el : '#app',
            data : {
                msg : '比较大小的案例',
                num1 : 0,
                num2 : 0
            },
            computed : {
                // 计算属性的简写形式
                compareResult(){
                    let result = this.num1 - this.num2
                    // 这里采用了异步方式，这里的箭头函数是javascript引擎去调用。所以最终return的时候，也会将值返回给javascript引擎。
                    setTimeout(() => {
                        if(result == 0){
                            return this.num1 + ' = ' + this.num2
                        }else if(result > 0){
                            return  this.num1 + ' > ' + this.num2
                        }else {
                            return  this.num1 + ' < ' + this.num2
                        }    
                    }, 1000 * 3)
                    
                }
            }
        })
    </script>
</body>
</html>
```

### 24-Class绑定之字符串形式.html

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Class绑定之字符串形式</title>
    <script src="../js/vue.js"></script>
    <style>
        .static{
            border: 1px solid black;
            background-color: aquamarine;
        }
        .big{
            width: 200px;
            height: 200px;
        }
        .small{
            width: 100px;
            height: 100px;
        }
    </style>
</head>
<body>
    <div id="app">
        <h1>{{msg}}</h1>
        <!-- 静态写法 -->
        <div class="static small">{{msg}}</div>
        <br><br>
        <button @click="changeBig">变大</button>
        <button @click="changeSmall">变小</button>
        <!-- 动态写法：动静都有 -->
        <!-- 适用场景：如果确定动态绑定的样式个数只有1个，但是名字不确定。 -->
        <div class="static" :class="c1">{{msg}}</div>
    </div>
    <script>
        const vm = new Vue({
            el : '#app',
            data : {
                msg : 'Class绑定之字符串形式',
                c1 : 'small'
            },
            methods: {
                changeBig(){
                    this.c1 = 'big'
                },
                changeSmall(){
                    this.c1 = 'small'
                }
            },
        })
    </script>
</body>
</html>
```

### 25-Class绑定之数组形式.html

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Class绑定之数组形式</title>
    <script src="../js/vue.js"></script>
    <style>
        .static {
            border: 1px solid black;
            width: 100px;
            height: 100px;
        }
        .active {
            background-color: green;
        }
        .text-danger {
            color: red;
        }
    </style>
</head>
<body>
    <div id="app">
        <h1>{{msg}}</h1>
        <!-- 静态写法 -->
        <div class="static active text-danger">{{msg}}</div>
        <br>
        <!-- 动态写法：动静结合 -->
        <div class="static" :class="['active','text-danger']">{{msg}}</div>
        <br>
        <div class="static" :class="[c1, c2]">{{msg}}</div>
        <br>
        <!-- 适用场景：当样式的个数不确定，并且样式的名字也不确定的时候，可以采用数组形式。 -->
        <div class="static" :class="classArray">{{msg}}</div>

    </div>
    <script>
        const vm = new Vue({
            el : '#app',
            data : {
                msg : 'Class绑定之数组形式',
                c1 : 'active',
                c2 : 'text-danger',
                classArray : ['active', 'text-danger']
            }
        })
    </script>
</body>
</html>
```

### 26-Class绑定之对象形式.html

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Class绑定之对象形式</title>
    <script src="../js/vue.js"></script>
    <style>
        .static {
            border: 1px solid black;
            width: 100px;
            height: 100px;
        }
        .active {
            background-color: green;
        }
        .text-danger {
            color: red;
        }
    </style>
</head>
<body>
    <div id="app">
        <h1>{{msg}}</h1>
        <!-- 动态写法：动静结合 -->
        <!-- 对象形式的适用场景：样式的个数是固定的，样式的名字也是固定的，但是需要动态的决定样式用还是不用。 -->
        <div class="static" :class="classObj">{{msg}}</div>
        <br>
        <div class="static" :class="{active:true,'text-danger':false}">{{msg}}</div>
    </div>
    <script>
        const vm = new Vue({
            el : '#app',
            data : {
                msg : 'Class绑定之对象形式',
                classObj : {
                    // 该对象中属性的名字必须和样式名一致。
                    active : false,
                    'text-danger' : true
                }
            }
        })
    </script>
</body>
</html>
```

### 27-Style绑定.html

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Style绑定</title>
    <script src="../js/vue.js"></script>
    <style>
        .static {
            border: 1px solid black;
            width: 100px;
            height: 100px;
        }
    </style>
</head>
<body>
    <div id="app">
        <h1>{{msg}}</h1>
        <!-- 静态写法 -->
        <div class="static" style="background-color: green;">{{msg}}</div>
        <br>
        <!-- 动态写法：字符串形式 -->
        <div class="static" :style="myStyle">{{msg}}</div>
        <br>
        <!-- 动态写法：对象形式 -->
        <div class="static" :style="{backgroundColor: 'gray'}">{{msg}}</div>
        <br>
        <div class="static" :style="styleObj1">{{msg}}</div>
        <br>
        <!-- 动态写法：数组形式 -->
        <div class="static" :style="styleArray">{{msg}}</div>
    </div>
    <script>
        const vm = new Vue({
            el : '#app',
            data : {
                msg : 'Style绑定',
                myStyle : 'background-color: gray;',
                styleObj1 : {
                    backgroundColor: 'green'
                },
                styleArray : [
                    {backgroundColor: 'green'},
                    {color : 'red'}
                ]
            }
        })
    </script>
</body>
</html>
```

### 28-条件渲染.html

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>条件渲染</title>
    <script src="../js/vue.js"></script>
</head>
<body>
    <div id="app">
        <h1>{{msg}}</h1>
        <!-- 
            v-if指令的值：true/false
                true: 表示该元素会被渲染到页面上。
                false: 表示该元素不会被渲染到页面上。（注意：不是修改了CSS样式，是这个元素压根没有加载）
         -->
        <div v-if="false">{{msg}}</div>

        <div v-if="2 === 1">{{msg}}</div>

        <button @click="counter++">点我加1</button>

        <h3>{{counter}}</h3>

        <img :src="imgPath1" v-if="counter % 2 === 1">
        <!-- 提醒：v-if和v-else之间不能断开。 -->
        <!-- <div></div> -->
        <!-- <img :src="imgPath2" v-if="counter % 2 === 0"> -->
        <!-- 为了提高效率，可以使用v-else指令 -->
        <img :src="imgPath2" v-else>

        <br><br>

        温度：<input type="number" v-model="temprature"><br><br>

        <!-- 天气：<span v-if="temprature <= 10">寒冷</span>
        <span v-if="temprature > 10 && temprature <= 25">凉爽</span>
        <span v-if="temprature > 25">炎热</span> -->

        天气：<span v-if="temprature <= 10">寒冷</span>
        <!-- v-if v-else-if v-else三者在使用的时候，中间不能断开。 -->
        <!-- <br> -->
        <span v-else-if="temprature <= 25">凉爽</span>
        <span v-else>炎热</span>

        <br><br><br>

        <!-- 
            v-show指令是通过修改元素的CSS样式的display属性来达到显示和隐藏的。
            v-if和v-show应该如何选择？
                1. 如果一个元素在页面上被频繁的隐藏和显示，建议使用v-show，因为此时使用v-if开销比较大。
                2. v-if的优点：页面加载速度快，提高了页面的渲染效率。
         -->
        <div v-show="false">你可以看到我吗？</div>

        <!-- template标签/元素只是起到占位的作用，不会真正的出现在页面上，也不会影响页面的结构。 -->
        <template v-if="counter === 10">
            <input type="text">
            <input type="checkbox">
            <input type="radio">            
        </template>

    </div>
    <script>
        const vm = new Vue({
            el : '#app',
            data : {
                msg : '条件渲染',
                counter : 1,
                imgPath1 : '../img/1.jpg',
                imgPath2 : '../img/2.jpg',
                temprature : 0
            }
        })
    </script>
</body>
</html>
```

### 29-列表渲染.html

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>列表渲染</title>
    <script src="../js/vue.js"></script>
</head>
<body>
    <div id="app">
        <h1>{{msg}}</h1>

        <h2>遍历对象的属性</h2>
        <ul>
            <li v-for="(value, propertyName) of user">
                {{propertyName}},{{value}}
            </li>
        </ul>

        <h2>遍历字符串</h2>
        <ul>
            <li v-for="(c,index) of str">
                {{index}},{{c}}
            </li>
        </ul>

        <h2>遍历指定的次数</h2>
        <ul>
            <li v-for="(num,index) of counter">
                {{index}}, {{num}}
            </li>
        </ul>


        <h2>遍历数组</h2>
        <!-- 静态列表 -->
        <ul>
            <li>张三</li>
            <li>李四</li>
            <li>王五</li>
        </ul>

        <!-- 动态列表 -->
        <ul>
            <!-- 
                1. v-for要写在循环项上。
                2. v-for的语法规则：
                    v-for="(变量名,index) in/of 数组"
                    变量名 代表了 数组中的每一个元素
             -->
            <li v-for="fdsafds in names">
                {{fdsafds}}
            </li>
        </ul>

        <ul>
            <li v-for="name of names">
                {{name}}
            </li>
        </ul>

        <ul>
            <li v-for="(name,index) of names">
                {{name}}-{{index}}
            </li>
        </ul>

        <ul>
            <li v-for="(vip,index) of vips">
                会员名：{{vip.name}}，年龄：{{vip.age}}岁
            </li>
        </ul>

        <table>
            <tr>
                <th>序号</th>
                <th>会员名</th>
                <th>年龄</th>
                <th>选择</th>
            </tr>
            <tr v-for="(vip,index) in vips">
                <td>{{index+1}}</td>
                <td>{{vip.name}}</td>
                <td>{{vip.age}}</td>
                <td><input type="checkbox"></td>
            </tr>
        </table>
    </div>
    <script>
        const vm = new Vue({
            el : '#app',
            data : {
                msg : '列表渲染',
                names : ['jack','lucy','james'],
                vips : [
                    {id:'111',name:'jack',age:20},
                    {id:'222',name:'lucy',age:30},
                    {id:'333',name:'james',age:40}
                ],
                user : {
                    id : '111',
                    name : '张三',
                    gender : '男'
                },
                str : '动力节点',
                counter : 10
            }
        })
    </script>
</body>
</html>
```

### 30-虚拟dom与diff算法.html

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>虚拟dom与diff算法</title>
    <script src="../js/vue.js"></script>
    <style>
        th,td{border: 1px solid black;}
    </style>
</head>
<body>
    <div id="app">
        <h1>{{msg}}</h1>
        <table>
            <tr>
                <th>序号</th>
                <th>英雄</th>
                <th>能量值</th>
                <th>选择</th>
            </tr>
            <!-- 
                v-for指令所在的标签中，还有一个非常重要的属性：
                    :key
                如果没有指定 :key 属性，会自动拿index作为key。
                这个key是这个dom元素的身份证号/唯一标识。

                分析以下：采用 index 作为key存在什么问题？
                    第一个问题：效率低。
                    第二个问题：非常严重了。产生了错乱。尤其是对数组当中的某些元素进行操作。（非末尾元素。）
                怎么解决这个问题？
                    建议使用对象的id作为key
             -->
            <tr v-for="(hero,index) in heros" :key="hero.id">
                <td>{{index+1}}</td>
                <td>{{hero.name}}</td>
                <td>{{hero.power}}</td>
                <td><input type="checkbox"></td>
            </tr>
        </table>

        <button @click="add">添加英雄麦文</button>
    </div>
    <script>
        const vm = new Vue({
            el : '#app',
            data : {
                msg : '虚拟dom与diff算法',
                heros : [
                    {id:'101',name:'艾格文',power:10000},
                    {id:'102',name:'麦迪文',power:9000},
                    {id:'103',name:'古尔丹',power:8000},
                    {id:'104',name:'萨尔',power:6000}
                ]
            },
            methods : {
                add(){
                    this.heros.unshift({id:'105',name:'麦文',power:9100})
                }
            }
        })
    </script>
</body>
</html>
```

### 31-列表过滤.html

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>列表过滤</title>
    <script src="../js/vue.js"></script>
    <style>
        th,td{border: 1px solid black;}
    </style>
</head>
<body>
    <div id="app">
        <h1>{{msg}}</h1>
        <input type="text" placeholder="请输入搜索关键字" v-model="keyword">
        <table>
            <tr>
                <th>序号</th>
                <th>英雄</th>
                <th>能量值</th>
                <th>选择</th>
            </tr>
            <tr v-for="(hero,index) in filteredHeros" :key="hero.id">
                <td>{{index+1}}</td>
                <td>{{hero.name}}</td>
                <td>{{hero.power}}</td>
                <td><input type="checkbox"></td>
            </tr>
        </table>
    </div>
    <script>
        const vm = new Vue({
            el : '#app',
            data : {
                keyword : '',
                msg : '列表过滤',
                heros : [
                    {id:'101',name:'艾格文',power:10000},
                    {id:'102',name:'麦迪文',power:9000},
                    {id:'103',name:'古尔丹',power:8000},
                    {id:'104',name:'萨尔',power:6000}
                ],
                filteredHeros : []
            },
            watch : {
                /* keyword(val){
                    // 执行过滤规则
                    this.filteredHeros = this.heros.filter((hero) => {
                        return hero.name.indexOf(val) >= 0
                    })
                } */
                
                keyword : {
                    immediate : true,
                    handler(val){
                        this.filteredHeros = this.heros.filter((hero) => {
                            return hero.name.indexOf(val) >= 0
                        })
                    }
                }
            }
        })

        // 回顾filter
        let arr = [1,2,3,4,5,6,7,8,9]

        // filter不会破坏原数组的结构，会生成一个全新的数组。
        let newArr = arr.filter((num) => {
            //return 过滤规则
            return num < 5
        })

        console.log(newArr)
    </script>
</body>
</html>
```

### 32-列表过滤计算属性实现.html

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>列表过滤计算属性实现</title>
    <script src="../js/vue.js"></script>
    <style>
        th,td{border: 1px solid black;}
    </style>
</head>
<body>
    <div id="app">
        <h1>{{msg}}</h1>
        <input type="text" placeholder="请输入搜索关键字" v-model="keyword">
        <table>
            <tr>
                <th>序号</th>
                <th>英雄</th>
                <th>能量值</th>
                <th>选择</th>
            </tr>
            <tr v-for="(hero,index) in filteredHeros" :key="hero.id">
                <td>{{index+1}}</td>
                <td>{{hero.name}}</td>
                <td>{{hero.power}}</td>
                <td><input type="checkbox"></td>
            </tr>
        </table>
    </div>
    <script>
        const vm = new Vue({
            el : '#app',
            data : {
                keyword : '',
                msg : '列表过滤',
                heros : [
                    {id:'101',name:'艾格文',power:10000},
                    {id:'102',name:'麦迪文',power:9000},
                    {id:'103',name:'古尔丹',power:8000},
                    {id:'104',name:'萨尔',power:6000}
                ]
            },
            computed : {
                filteredHeros(){
                    // 执行过滤
                    return this.heros.filter((hero) => {
                        return hero.name.indexOf(this.keyword) >= 0
                    })
                }
            }
        })
    </script>
</body>
</html>
```

### 33-列表排序.html

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>列表排序</title>
    <script src="../js/vue.js"></script>
    <style>
        th,td{border: 1px solid black;}
    </style>
</head>
<body>
    <div id="app">
        <h1>{{msg}}</h1>
        <input type="text" placeholder="请输入搜索关键字" v-model="keyword">
        <br>
        <button @click="type = 1">升序</button>
        <button @click="type = 2">降序</button>
        <button @click="type = 0">原序</button>
        <table>
            <tr>
                <th>序号</th>
                <th>英雄</th>
                <th>能量值</th>
                <th>选择</th>
            </tr>
            <tr v-for="(hero,index) in filteredHeros" :key="hero.id">
                <td>{{index+1}}</td>
                <td>{{hero.name}}</td>
                <td>{{hero.power}}</td>
                <td><input type="checkbox"></td>
            </tr>
        </table>
    </div>
    <script>
        const vm = new Vue({
            el : '#app',
            data : {
                type : 0,
                keyword : '',
                msg : '列表排序',
                heros : [
                    {id:'101',name:'艾格文',power:10000},
                    {id:'102',name:'麦迪文',power:9000},
                    {id:'103',name:'古尔丹',power:8000},
                    {id:'104',name:'萨尔',power:11000}
                ]
            },
            computed : {
                filteredHeros(){
                    // 执行过滤
                    const arr = this.heros.filter((hero) => {
                        return hero.name.indexOf(this.keyword) >= 0
                    })
                    // 排序
                    if(this.type === 1){
                        arr.sort((a, b) => {
                            return a.power - b.power
                        })
                    }else if(this.type == 2){
                        arr.sort((a, b) => {
                            return b.power - a.power
                        })
                    }
                    
                    // 返回
                    return arr
                }
            }
        })

        // 回顾sort方法
        let arr = [8,9,5,4,1,2,3]

        // sort方法排序之后，不会生成一个新的数组，是在原数组的基础之上进行排序，会影响原数组的结构。
        arr.sort((a, b) => {
            return b - a
        })

        console.log(arr)
    </script>
</body>
</html>
```

### 34-表单数据的收集.html

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>表单数据的收集</title>
    <script src="../js/vue.js"></script>
</head>
<body>
    <div id="app">
        <h1>{{msg}}</h1>
        <form @submit.prevent="send">
            用户名：<input type="text" v-model.trim="user.username"><br><br>
            密码：<input type="password" v-model="user.password"><br><br>
            年龄：<input type="number" v-model.number="user.age"><br><br>
            性别：
                男<input type="radio" name="gender" value="1" v-model="user.gender">
                女<input type="radio" name="gender" value="0" v-model="user.gender"><br><br>
            爱好：
            <!-- 注意：对于checkbox来说，如果没有手动指定value，那么会拿这个标签的checked属性的值作为value -->
                旅游<input type="checkbox" v-model="user.interest" value="travel">
                运动<input type="checkbox" v-model="user.interest" value="sport">
                唱歌<input type="checkbox" v-model="user.interest" value="sing"><br><br>
            学历：
                <select v-model="user.grade">
                    <option value="">请选择学历</option>
                    <option value="zk">专科</option>
                    <option value="bk">本科</option>
                    <option value="ss">硕士</option>
                </select><br><br>
            简介：
                <textarea cols="50" rows="15" v-model.lazy="user.introduce"></textarea><br><br>
            <input type="checkbox" v-model="user.accept">阅读并接受协议<br><br>
            <!-- <button @click.prevent="send">注册</button> -->
            <button>注册</button>
        </form>
    </div>
    <script>
        const vm = new Vue({
            el : '#app',
            data : {
                user : {
                    username : '',
                    password : '',
                    age : '',
                    gender : '1',
                    interest : ['travel'],
                    grade : 'ss',
                    introduce : '',
                    accept : ''
                },
                msg : '表单数据的收集'
            },
            methods : {
                send(){
                    alert('ajax...!!!!')
                    // 将数据收集好，发送给服务器。
                    //console.log(JSON.stringify(this.$data))
                    console.log(JSON.stringify(this.user))
                }
            }
        })
    </script>
</body>
</html>
```

### 35-过滤器.html

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>过滤器</title>
    <script src="../js/vue.js"></script>
</head>
<body>
    <!-- 
        需求：
            从服务器端返回了一个商品的价格price，这个price的值可能是这几种情况：''、null、undefined、60.5
            要求：
                如果是''、null、undefined ，页面上统一显示为 - 
                如果不是 ''、null、undefined，则页面上显示真实的数字即可。 
        在Vue3当中，已经将过滤器语法废弃了。
     -->
    <div id="app">
        <h1>{{msg}}</h1>
        <h2>商品价格：{{formatPrice}}</h2>
        <h2>商品价格：{{formatPrice2()}}</h2>
        <h2>商品价格：{{price | filterA | filterB(3)}}</h2>
        <input type="text" :value="price | filterA | filterB(3)">
    </div>

    <hr>

    <div id="app2">
        <h2>商品价格：{{price | filterA | filterB(3)}}</h2>
    </div>

    <script>

        // 配置全局的过滤器。
        Vue.filter('filterA', function(val){
            if(val === null || val === undefined || val === ''){
                return '-'
            }
            return val
        })

        Vue.filter('filterB', function(val, number){
            return val.toFixed(number)
        })

        const vm2 = new Vue({
            el : '#app2',
            data : {
                price : 20.3
            }
        })

        const vm = new Vue({
            el : '#app',
            data : {
                msg : '过滤器',
                price : 50.6
            },
            methods: {
                formatPrice2(){
                    if(this.price === '' || this.price === undefined || this.price === null){
                        return '-'
                    }
                    return this.price
                }
            },
            computed : {
                formatPrice(){
                    if(this.price === '' || this.price === undefined || this.price === null){
                        return '-'
                    }
                    return this.price
                }
            },
            /* filters : {
                // 局部过滤器
                filterA(val){
                    if(val === null || val === undefined || val === ''){
                        return '-'
                    }
                    return val
                },
                filterB(val, number){
                    // 确保传递过来的数据val，保留两位小数。
                    return val.toFixed(number)
                }
            } */
        })
    </script>
</body>
</html>
```

### 36-Vue的其它指令.html

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Vue的其它指令</title>
    <script src="../js/vue.js"></script>
</head>
<body>
    <div id="app">
        <h1>{{msg}},test</h1>
        <!-- 
            v-text指令：
                可以将指令的内容拿出来填充到标签体当中。和JS的innerText一样。
                这种填充是以覆盖的形式进行的。先清空标签体当中原有的内容，填充新的内容。
                即使内容是一段HTML代码，这种方式也不会将HTML代码解析并执行。只会当做普通
                文本来处理。
         -->
        <h1 v-text="msg">test</h1>
        <h1 v-text="name">test</h1>
        <h1 v-text="s1"></h1>

        <!-- 
            v-html指令：
                和v-text一样，也是填充标签体内容。也是采用覆盖的形式进行。
                只不过v-html会将内容当做一段HTML代码解析并执行。
         -->
         <h1 v-html="s1"></h1>
    </div>
    <script>
        const vm = new Vue({
            el : '#app',
            data : {
                msg : 'Vue的其它指令',
                name : 'jack',
                s1 : '<h1>欢迎大家学习Vue！</h1>'
            }
        })
    </script>
</body>
</html>
```

### 37-Vue的其它指令.html

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Vue的其它指令</title>
    <style>
        [v-cloak] {
            display: none;
        }
    </style>
</head>
<body>
    <div id="app">
        <h1 v-cloak>{{msg}}</h1>
    </div>

    <script>
        setTimeout(() => {
            let scriptElt = document.createElement('script')
            scriptElt.src = '../js/vue.js'
            document.head.append(scriptElt)
        }, 3000)

        setTimeout(() => {
            const vm = new Vue({
                el : '#app',
                data : {
                    msg : 'Vue的其它指令'
                }
            })
        }, 4000)
    </script>
</body>
</html>
```

### 38-Vue的其它指令.html

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Vue的其它指令</title>
    <script src="../js/vue.js"></script>
</head>
<body>
    <div id="app">
        <h1 v-cloak>{{msg}}</h1>
        <h1 v-pre>欢迎学习Vue框架！</h1>
        <h1 v-pre>{{msg}}</h1>
        <ul>
            <li v-for="user,index of users" :key="index" v-once>
                {{user}}
            </li>
        </ul>

        <ul>
            <li v-for="user,index of users" :key="index">
                {{user}}
            </li>
        </ul>
    </div>

    <script>
        const vm = new Vue({
            el : '#app',
            data : {
                msg : 'Vue的其它指令',
                users : ['jack', 'lucy', 'james']
            }
        })
    </script>
</body>
</html>
```

### 39-自定义指令.html

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>自定义指令</title>
    <script src="../js/vue.js"></script>
</head>
<body>
    <div id="app">
        <h1>自定义指令</h1>
        <div v-text="msg"></div>
        <div v-text-danger="msg"></div>
        用户名：<input type="text" v-bind:value="username">
        <!-- 
            需要一个指令，可以和v-bind指令完成相同的功能，同时将该元素的父级元素的背景色设置为蓝色。
         -->
        <div>
            用户名：<input type="text" v-bind-blue="username">
        </div>
    </div>

    <div id="app2">
        <div v-text-danger="msg"></div>
        <div>
            用户名：<input type="text" v-bind-blue="username">
        </div>
    </div>

    <script>
        // 定义全局的指令
        // 函数式
        Vue.directive('text-danger', function(element, binding){
            //对于自定义指令来说，函数体当中的this是window，而不是vue实例。
            console.log(this)
            element.innerText = binding.value
            element.style.color = 'red'
        })

        // 对象式
        Vue.directive('bind-blue', {
            bind(element, binding){
                element.value = binding.value
                console.log(this)
            },
            inserted(element, binding){
                element.parentNode.style.backgroundColor = 'skyblue'
                console.log(this)
            },
            update(element, binding){
                element.value = binding.value
                console.log(this)
            }
        })

        const vm2 = new Vue({
            el : '#app2',
            data : {
                msg : '欢迎学习Vue框架！',
                username : 'lucy'
            }
        })

        const vm = new Vue({
            el : '#app',
            data : {
                msg : '自定义指令',
                username : 'jackson'
            },
            directives : {
                // 指令1
                // 指令2
                // ...
                // 关于指令的名字：1. v- 不需要写。 2. Vue官方建议指令的名字要全部小写。如果是多个单词的话，请使用 - 进行衔接。
                // 这个回调函数的执行时机包括两个：第一个：标签和指令第一次绑定的时候。第二个：模板被重新解析的时候。
                // 这个回调函数有两个参数：第一个参数是真实的dom元素。 第二个参数是标签与指令之间绑定关系的对象。
                // 这种方式属于函数式方式。
                /* 'text-danger' : function(element, binding){
                    console.log('@')
                    element.innerText = binding.value
                    element.style.color = 'red'
                }, */
                /* 'bind-blue' : function(element, binding){
                    element.value = binding.value
                    console.log(element)
                    // 为什么是null，原因是这个函数在执行的时候，指令和元素完成了绑定，但是只是在内存当中完成了绑定，元素还没有被插入到页面当中。
                    console.log(element.parentNode)
                    element.parentNode.style.backgroundColor = 'blue'
                } */

                // 对象式
                /* 'bind-blue' : {
                    // 这个对象中三个方法的名字不能随便写。
                    // 这三个函数将来都会被自动调用。
                    // 元素与指令初次绑定的时候，自动调用bind
                    // 注意：在特定的时间节点调用特定的函数，这种被调用的函数称为钩子函数。
                    bind(element, binding){
                        element.value = binding.value
                    },
                    // 元素被插入到页面之后，这个函数自动被调用。
                    inserted(element, binding){
                        element.parentNode.style.backgroundColor = 'blue'
                    },
                    // 当模板重新解析的时候，这个函数会被自动调用。
                    update(element, binding){
                        element.value = binding.value
                    }
                } */
            }
        })
    </script>
</body>
</html>
```

### 40-响应式与数据劫持.html

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>响应式与数据劫持</title>
    <script src="../js/vue.js"></script>
</head>
<body>
    <div id="app">
        <h1>{{msg}}</h1>
        <div>姓名：{{name}}</div>
        <div>年龄：{{age}}岁</div>
        <div>数字：{{a.b.c.e}}</div>
        <div>邮箱：{{a.email}}</div>
    </div>
    <script>
        const vm = new Vue({
            el : '#app',
            data : {
                msg : '响应式与数据劫持',
                name : 'jackson',
                age : 20,
                a : {
                    b : {
                        c : {
                            e : 1
                        }
                    }
                }
            }
        })

        // 测试：后期给Vue实例动态的追加的一些属性，会添加响应式处理吗？
        // 目前来看，通过这种方式后期给vm追加的属性并没有添加响应式处理。
        //vm.$data.a.email = 'jack@126.com'

        // 如果你想给后期追加的属性添加响应式处理的话，调用以下两个方法都可以：
        // Vue.set() 、 vm.$set()
        //Vue.set(目标对象, 属性名, 属性值)
        //Vue.set(vm.$data.a, 'email', 'jack@126.com')
        //Vue.set(vm.a, 'email', 'jack@123.com')
        vm.$set(vm.a, 'email', 'jack@456.com')

        // 避免在运行时向Vue实例或其根$data添加响应式
        // 不能直接给vm / vm.$data 追加响应式属性。只能在声明时提前定义好。
        //Vue.set(vm, 'x', '1')
        //Vue.set(vm.$data, 'x', '1')

    </script>
</body>
</html>
```

### 41-数组的响应式处理.html

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>数组的响应式处理</title>
    <script src="../js/vue.js"></script>
</head>
<body>
    <!-- 
        1. 通过数组的下标去修改数组中的元素，默认情况下是没有添加响应式处理的。怎么解决？
        
        2. 第一种方案：
            vm.$set(数组对象, 下标, 值)
            Vue.set(数组对象, 下标, 值)

        3. 第二种方案：
            push()
            pop()
            reverse()
            splice()
            shift()
            unshift()
            sort()

            在Vue当中，通过以上的7个方法来给数组添加响应式处理。
     -->
    <div id="app">
        <h1>{{msg}}</h1>
        <ul>
            <li v-for="user in users">
                {{user}}
            </li>
        </ul>
        <ul>
            <li v-for="vip in vips" :key="vip.id">
                {{vip.name}}
            </li>
        </ul>
    </div>
    <script>
        const vm = new Vue({
            el : '#app',
            data : {
                msg : '数组的响应式处理',
                users : ['jack', 'lucy', 'james'],
                vips : [
                    {id:'111', name:'zhangsan'},
                    {id:'222', name:'lisi'}
                ]
            }
        })
    </script>
</body>
</html>

```

### 42-Vue的生命周期.html

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Vue的生命周期</title>
    <script src="../js/vue.js"></script>
</head>
<body>
    <div id="app">
        <h1>{{msg}}</h1>
        <h3>计数器：{{counter}}</h3>
        <h3 v-text="counter"></h3>
        <button @click="add">点我加1</button>
        <button @click="destroy">点我销毁</button>
    </div>
    <script>
        const vm = new Vue({
            el : '#app',
            data : {
                msg : 'Vue生命周期',
                counter : 1
            },
            methods: {
                add(){
                    console.log('add....')
                    this.counter++
                },
                destroy(){
                    // 销毁vm
                    this.$destroy()
                },
                /* m(){
                    console.log('m....')
                } */
            },
            watch : {
                counter(){
                    console.log('counter被监视一次！')
                }
            },
            /*
            1.初始阶段
                el有，template也有，最终编译template模板语句。
                el有，template没有，最终编译el模板语句。
                el没有的时候，需要手动调用 vm.$mount(el) 进行手动挂载，然后流程才能继续。此时如果template有，最终编译template模板语句。
                el没有的时候，需要手动调用 vm.$mount(el) 进行手动挂载，然后流程才能继续。此时如果没有template，最终编译el模板语句。

                结论：
                    流程要想继续：el必须存在。
                    el和template同时存在，优先选择template。如果没有template，才会选择el。
            */
            beforeCreate() {
                // 创建前
                // 创建前指的是：数据代理和数据监测的创建前。
                // 此时还无法访问data当中的数据。包括methods也是无法访问的。
                console.log('beforeCreate', this.counter)
                // 调用methods报错了，不存在。
                //this.m()
            },
            created() {
                // 创建后
                // 创建后表示数据代理和数据监测创建完毕，可以访问data中的数据了。
                console.log('created', this.counter)
                // 可以访问methods了。
                //this.m()
            },
            // 2.挂载阶段
            beforeMount() {
                // 挂载前
                console.log('beforeMount')
            },
            mounted() {
                // 挂载后
                console.log('mounted')
                console.log(this.$el)
                console.log(this.$el instanceof HTMLElement)
            },
            // 3.更新阶段
            beforeUpdate() {
                // 更新前
                console.log('beforeUpdate')
            },
            updated() {
                // 更新后
                console.log('updated')
            },
            // 4.销毁阶段
            beforeDestroy() {
                // 销毁前
                console.log('beforeDestroy')
                console.log(this)
                this.counter = 1000
            },
            destroyed() {
                // 销毁后
                console.log('destroyed')
                console.log(this)
            },
        })
    </script>
</body>
</html>
```

### 43-测试el和template配置项.html

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>测试el和template配置项</title>
    <script src="../js/vue.js"></script>
</head>
<body>
    <div id="app">
        <h1>{{msg}}</h1>
    </div>

    <script>
        const vm = new Vue({
            el : '#app',
            /* template : `
                <h1>{{s}}</h1>
            `, */
            data : {
                msg : '测试el和template配置项',
                s : 'template配置项!!!!'
            }
        })
        
        // 手动挂载
        //vm.$mount('#app')

    </script>
</body>
</html>
```

## 03-Vue组件化开发

### 1-第一个组件.html

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>第一个组件</title>
    <script src="../js/vue.js"></script>
</head>
<body>
    <!-- 
        组件的使用分为三步：
            第一步：创建组件
                Vue.extend({该配置项和new Vue的配置项几乎相同，略有差别})
                区别有哪些？
                    1. 创建Vue组件的时候，配置项中不能使用el配置项。（但是需要使用template配置项来配置模板语句。）
                    2. 配置项中的data不能使用直接对象的形式，必须使用function。
            第二步：注册组件
                局部注册：
                    在配置项当中使用components，语法格式：
                        components : {
                            组件的名字 : 组件对象
                        }
                全局注册：
                    Vue.component('组件的名字', 组件对象)
            第三步：使用组件
        
        小细节：
            1. 在Vue当中是可以使用自闭合标签的，但是前提必须在脚手架环境中使用。
            2. 在创建组件的时候Vue.extend()可以省略，但是底层实际上还是会调用的，在注册组件的时候会调用。
            3. 组件的名字
                第一种：全部小写
                第二种：首字母大写，后面都是小写
                第三种：kebab-case命名法（串式命名法。例如：user-login）
                第四种：CamelCase命名法（驼峰式命名法。例如：UserLogin），但是这种方式只允许在脚手架环境中使用。
                不要使用HTML内置的标签名作为组件的名字。
                在创建组件的时候，通过配置项配置一个name，这个name不是组件的名字，是设置Vue开发者工具中显示的组件的名字。
     -->
    <div id="app">
        <h1>{{msg}}</h1>
        <!-- 3. 使用组件 -->
        <userlogin></userlogin>
        <userlist></userlist>
        <userlist></userlist>
        <userlist></userlist>
        <userlogin></userlogin>

        <!-- <userlogin/> -->
    </div>

    <div id="app2">
        <userlogin></userlogin>
        <hello-world></hello-world>
        <!-- <form></form> -->
    </div>

    <script>

        /* // 创建组件
        const abc = {
            template : `<h1>测试组件的名字????</h1>`
        }

        // 全局注册组件
        Vue.component('HelloWorld', abc) */


        Vue.component('hello-world', {
            name : 'Xxxxx',
            template : `<h1>测试组件的名字%%%%%</h1>`
        })

        /* Vue.component('form', {
            template : `<h1>测试组件的名字%%%%%</h1>`
        }) */

        // 1.创建组件(结构HTML 交互JS 样式CSS)
        /* const myComponent = Vue.extend({
            template : `
            <ul>
                <li v-for="(user,index) of users" :key="user.id">
                    {{index}},{{user.name}}
                </li>
            </ul>
            `,
            data(){
                return {
                    users : [
                        {id:'001',name:'jack'},
                        {id:'002',name:'lucy'},
                        {id:'003',name:'james'}
                    ]
                }
            }
        }) */

        const myComponent = {
            template : `
            <ul>
                <li v-for="(user,index) of users" :key="user.id">
                    {{index}},{{user.name}}
                </li>
            </ul>
            `,
            data(){
                return {
                    users : [
                        {id:'001',name:'jack'},
                        {id:'002',name:'lucy'},
                        {id:'003',name:'james'}
                    ]
                }
            }
        }

        // 1. 创建组件
        /* const userLoginComponent = Vue.extend({
            template : `
            <div>
                <h3>用户登录</h3>
                <form @submit.prevent="login">
                    账号：<input type="text" v-model="username"> <br><br>
                    密码：<input type="password" v-model="password"> <br><br>
                    <button>登录</button>
                </form>
            </div>
            `,
            data(){
                return {
                    username : '',
                    password : ''
                }
            },
            methods: {
                login(){
                    alert(this.username + "," + this.password)
                }
            },
        }) */

        const userLoginComponent = {
            template : `
            <div>
                <h3>用户登录</h3>
                <form @submit.prevent="login">
                    账号：<input type="text" v-model="username"> <br><br>
                    密码：<input type="password" v-model="password"> <br><br>
                    <button>登录</button>
                </form>
            </div>
            `,
            data(){
                return {
                    username : '',
                    password : ''
                }
            },
            methods: {
                login(){
                    alert(this.username + "," + this.password)
                }
            },
        }

        // 全局注册
        Vue.component('userlogin', userLoginComponent)

        const vm2 = new Vue({
            el : '#app2'
        })

        // Vue实例
        const vm = new Vue({
            el : '#app',
            data : {
                msg : '第一个组件'
            },
            // 2. 注册组件（局部注册）
            components : {
                // userlist是组件的名字。myComponent只是一个变量名。
                userlist : myComponent,
                //userlogin : userLoginComponent
            }
        })

        /* let data = {
            counter : 1
        } */

        function data(){
            return {
                counter : 1
            }
        }

        let x = data();
        let y = data();

    </script>
</body>
</html>
```

### 2-组件嵌套.html

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>组件嵌套</title>
    <script src="../js/vue.js"></script>
</head>
<body>
    <div id="root"></div>
    <script>
        // 创建Y1组件
        const y1 = {
            template : `
                <div>
                    <h3>Y1组件</h3>
                </div>
            `
        }
        // 创建X1组件
        const x1 = {
            template : `
                <div>
                    <h3>X1组件</h3>
                </div>
            `
        }
        // 创建Y组件
        const y = {
            template : `
                <div>
                    <h2>Y组件</h2>
                    <y1></y1>
                </div>
            `,
            components : {y1}
        }
        // 创建X组件
        const x = {
            template : `
                <div>
                    <h2>X组件</h2>
                    <x1></x1>
                </div>
            `,
            components : {x1}
        }
        // 创建app组件
        const app = {
            template : `
                <div>
                    <h1>App组件</h1>
                    <x></x>
                    <y></y>
                </div>
            `,
            // 注册X组件
            components : {x,y}
        }
        // vm
        const vm = new Vue({
            el : '#root',
            template : `
                <app></app>
            `,
            // 注册app组件
            components : {app}
        })
    </script>
</body>
</html>
```

### 3-vm与vc.html

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>vm与vc</title>
    <script src="../js/vue.js"></script>
</head>
<body>
    <div id="app">
        <h1>{{msg}}</h1>
        <user></user>
        <user></user>
        <user></user>
    </div>
    <script>

        // 这个不是给Vue扩展counter属性。
        // 这个是给“Vue的原型对象”扩展一个counter属性。
        Vue.prototype.counter = 1000

        // 创建组件
        const user = Vue.extend({
            template : `
            <div>
                <h1>user组件</h1>
            </div>
            `,
            mounted(){
                // this是VueComponent实例
                // user是什么呢？？？？是一个全新的构造函数 VueComponent构造函数。
                //console.log('vc', this === user)
                // 为什么要这样设计？为了代码复用。
                // 底层实现原理：
                // VueComponent.prototype.__proto__ = Vue.prototype
                console.log('vc.counter', this.counter)
                // 这个访问不了，因为msg是vm实例上的属性。
                //console.log('vc.msg', this.msg)
            }
        })

        console.log('user.prototype.__proto__ === Vue.prototype' , user.prototype.__proto__ === Vue.prototype)

        console.log(user)

        // vm
        const vm = new Vue({
            el : '#app',
            data : {
                msg : 'vm与vc'
            },
            components : {
                user
            },
            mounted() {
                // this是Vue实例
                console.log('vm', this)
            },
        })

        console.log('vm.counter', vm.counter)
        // 本质上是这样的：
        console.log('vm.counter', vm.__proto__.counter)

        /* function test(){
            var Sub = function User(){
                this.name = 'admin'
            }
            return Sub
        }

        let a = test()
        // 通过构造函数创建对象
        console.log(new a()) */

        /* console.log(a)
        let b = test()
        console.log(b)
        console.log(a === b) */

        // prototype __proto__
        // 构造函数（函数本身又是一种类型，代表Vip类型）
        function Vip(){}

        // Vip类型/Vip构造函数，有一个 prototype 属性。
        // 这个prototype属性可以称为：显式的原型属性。
        // 通过这个显式的原型属性可以获取：原型对象
        // 获取Vip的原型对象
        let x = Vip.prototype

        // 通过Vip可以创建实例
        let a = new Vip()
        /* let b = new Vip()
        let c = new Vip() */
        // 对于实例来说，都有一个隐式的原型属性: __proto__
        // 注意：显式的(建议程序员使用的)。隐式的（不建议程序员使用的。）
        // 这种方式也可以获取到Vip的原型对象
        let y = a.__proto__
        /* b.__proto__
        c.__proto__ */

        // 原型对象只有一个，其实原型对象都是共享的。
        console.log(x === y) // true

        // 这个不是给Vip扩展属性
        // 是在给“Vip的原型对象”扩展属性
        Vip.prototype.counter = 1000

        // 通过a实例可以访问这个扩展的counter属性吗？可以访问。为什么？原理是啥？
        // 访问原理：首先去a实例上找counter属性，如果a实例上没有counter属性的话，会沿着__proto__这个原型对象去找。
        // 下面代码看起来表面上是a上有一个counter属性，实际上不是a实例上的属性，是a实例对应的原型对象上的属性counter。
        console.log(a.counter)
        //console.log(a.__proto__.counter)
        

    </script>
</body>
</html>
```

