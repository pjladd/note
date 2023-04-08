```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <!-- 引入vuejs框架 -->
    <script src="./lib/vue-2.4.0.js"></script>
    
</head>
<body>
    
    <div id="app">
        
        <input type="text" :value="str1"/>
        
        <input type="button" value="点击1" v-on:click="fun1"/>

        <input type="button" value="点击2" onclick="fun12()"/>

        <input type="button" value="点击3" @click="fun2"/>
    </div>
    
    <script>
    
        function fun12(){

            alert("abc1");

        }

        var vm = new Vue({

            el : "#app",    
            data : {
                "str1" : "aaa"
            },
            //methods:表示vuejs中对于绑定事件函数的定义，可以同时定义多个函数，多个函数之间使用逗号来进行分隔
            methods:{

                fun1(){

                    alert("abc2");

                },
                fun2(){

                    alert("aaaaaa");

                }

            }

        });

    </script>

</body>
</html>
```

