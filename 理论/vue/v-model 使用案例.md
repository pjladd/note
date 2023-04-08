# v-model: 使用案例（实现一个计算器）

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script src="C:\Users\patrick\Desktop\项目2\code\lib\vue-2.4.0.js"></script>
    <script>Vue.config.productionTip= false </script>
</head>
<body>
    <div id="app">
        <input type="text" v-model:value="num1" />
        <select v-model:value="operation">
            <option value="+">+</option>
            <option value="-">-</option>
            <option value="*">*</option>
            <option value="/">/</option>
        </select>
        <input type="text" v-model:value="num2"/>
        <input type="button" value="=" @click="calculate"/>
        <input type="text" v-model:value="result" />
    </div>
   

    <script>
        var vm = new Vue({
                el:"#app",
                data:{
                    num1 : 0,
                    num2 : 0,
                    operation : "+",
                    result : 0
                },
                methods:{
                    calculate() {
                        if(this.operation == "+") {
                            this.result = parseInt(this.num1) + parseInt(this.num2) ;
                        } else if(this.operation == "-") {
                            this.result = parseInt(this.num1) - parseInt(this.num2) ;
                        } else if(this.operation == "*") {
                            this.result = parseInt(this.num1) * parseInt(this.num2) ;
                        } else if(this.operation == "/") {
                            this.result = parseInt(this.num1) / parseInt(this.num2) ;
                        } 
                    }
                }
                
            });
    </script>

 
</body>
</html>
```

测试：

![image-20230401195832620](C:\Users\patrick\AppData\Roaming\Typora\typora-user-images\image-20230401195832620.png)