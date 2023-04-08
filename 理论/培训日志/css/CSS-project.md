# CSS

## 1.1   CSS课堂笔记

1、什么是CSS？
	Cascading Style Sheet
	层叠样式表语言（不是编程语言，属于样式表语言，没有变量、数据类型、控制语句...）
	CSS其实是专门用来修饰HTML的，让HTML更好看。
	CSS是HTML的化妆品。

2、CSS是为HTML服务的，所以HTML还是主体，CSS是依附在HTML上的，
所以进行CSS的开发，我们还是需要新建html/htm文件。

3、在HTML中怎么嵌入CSS样式呢？三种方式
	第一种方式：内联定义
	第二种方式：定义内部样式块对象
	第三种方式：链入外部样式表文件（这种方式最常用！）

4、关于选择器的优先级：

	标签选择器优先级最低。
	其次是类选择器。
	最高优先级是id选择器。

## 1.2   演练

### 001-HTML中嵌入CSS样式的第一种方式.html：

```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title>HTML中嵌入CSS样式的第一种方式：内联定义</title>
	</head>
	<body>
		
		<!-- 
			内联定义语法格式？
				<标签 style="样式名 : 样式值; 
							样式名 : 样式值; 
							样式名 : 样式值;"></标签>
				
				style：风格，样式。
				任何一个HTML标签都可以指定style属性。
		 -->
		<div id="div1" style="background-color : #CCCC33; 
							width : 300px; 
							height: 300px;
							position : absolute;
							top: 100px;
							left: 100px;
							border-style : solid;
							border-color : red;
							border-width : 1px;">
			
		</div>
		
	</body>
</html>

```

### 002-HTML中嵌入CSS样式的第二种方式.html：

```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title>HTML中嵌入CSS样式的第二种方式：定义内部样式块对象</title>
		
		<!-- head标签中使用style标签，定义样式块对象 -->
		<style type="text/css">
			/*
				这是CSS的注释！！！！！！
				在CSS的地盘中，和java的注释相同！！！！
			*/
		   /* 
		   这里应该怎么写样式，语法是什么？
				选择器 {
					样式名 : 样式值;
					样式名 : 样式值;
					样式名 : 样式值;
					样式名 : 样式值;
					样式名 : 样式值;
					....
				}
				
				CSS中常见的选择器包括：最常用的三种选择器。
					标签选择器
					id选择器
					class选择器
		   */
		  /* 
		  标签选择器，很简单：
			标签名 {}
		  */
			div{ /* 作用于所有的div元素*/
				background-color: aqua;
				width: 100px;
				height: 100px;
				border-color: red;
				border-style: solid;
				border-width: 10px;
			}
			/* ID选择器
				#id{} 只作用于id这个元素
			 */
			#username {
				width: 400px;
				height: 30px;
				border-color: black;
				border-style: solid;
				border-width: 1px;
			}
			
			/* 类选择器
				.class {} 样式作用于当前网页中某一类的标签
			 */
			.student {
				font-size: 12px;
				color: #FF0000;
			}
		 
		</style>
		
	</head>
	<body>
		
		<div>
			
		</div>
		
		<div>
			
		</div>
		
		<div>
			
		</div>
		
		<br>
		<br>
		<br>
		
		<!-- 怎么才能让样式作用于某1个标签，可以使用id选择器 -->
		<input type="text" id="username" />
		
		<hr>
		
		<!-- class属性，任何一个标签都有，class相同的，可以看做是同一类标签。 -->
		<span class="student">文本内容span</span>
		
		<p class="student">文本内容：段落p标签</p>
		
		<br><br><br><br><br><br><br><br><br><br><br>
		
	</body>
</html>

```

### 003-HTML中嵌入CSS样式的第三种方式.html：

```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title>HTML中嵌入CSS样式的第三种方式:链入外部样式表文件</title>
		
		<!-- 引入外部独立的CSS样式表文件 -->
		<!-- 在web前端开发中，这种方式是最常用的！ -->
		<link rel="stylesheet" type="text/css" href="css/1.css"/>
		
	</head>
	<body>
		<div id="div1">
			
		</div>
		
		<input type="text" class="myinput" />
		<input type="text" class="myinput"/>
		<input type="text" id="username" class="myinput"/>
		
		
	</body>
</html>

```

### 004-隐藏样式.html：

```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title>隐藏样式</title>
		<style type="text/css">
			#citysOfChina {
				display: none; /* 隐藏*/
			}
			
			input {
				display: block; /* 显示*/
			}
			
			ul {
				/* list-style-type: circle; */
				list-style-type: none;
			}
			
			ol {
				/* list-style-type: none; */
				list-style-type : upper-roman;
			}
		</style>
	</head>
	<body>
		
		<ol>
			<li>水果</li>
			<li>蔬菜</li>
			<li>茶</li>
		</ol>
		
		<ul>
			<li>中国
				<ul id="citysOfChina">
					<li>北京</li>
					<li>天津</li>
				</ul>
			</li>
			<li>美国</li>
			<li>日本</li>
		</ul>
		
		<input type="text" />
		
	</body>
</html>

```

### 005-文本装饰样式.html：

```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title>文本装饰样式</title>
		<style type="text/css">
			#baidu {
				text-decoration : underline;
				/* text-decoration : overline; */
				/* text-decoration : line-through; */
				/* text-decoration : blink; */
			}
			
			#baidu2 {
				text-decoration: none;
			}
		</style>
	</head>
	<body>
		
		<div id="baidu">百度</div>
		
		<a id="baidu2" href="http://www.baidu.com">百度</a>
		
		
	</body>
</html>

```

### 006-设置鼠标的悬停效果.html：

```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title>设置鼠标的悬停效果</title>
		
		<style type="text/css">
			/* :hover 是专门用来设置鼠标悬停效果的 */
			span:hover {
				color: red;
				font-size: 20px;
			}
			
			/* 注意：:hover在使用的时候，这个冒号两边都是不允许有空格的。 */
			input:hover {
				border-color: black;
			}
		</style>
		
	</head>
	<body>
		
		<span>我是一个段落</span>		
		<span>我是一个段落</span>
		
		<input type="text" />
		
	</body>
</html>

```

### 007-内边距和外边距.html：

```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title>内边距和外边距</title>
		<style type="text/css">
			#div1 {
				width: 300px;
				height: 300px;
				background-color: #00FFFF;
				border: solid 1px red;
				/* 内补丁 */
				padding-left: 20px;
			}
			#div2 {
				width: 100px;
				height: 100px;
				background-color: black;
				border: solid 1px red;
				/* 在div2这个节点顶部top打一个补丁，这个补丁离top 10px */
				/* 外补丁 */
				margin-top : 10px;
			}
		</style>
	</head>
	<body>
		
		<!-- 盒子套盒子 -->
		<!-- 如果盒子套盒子，需要定位的话，可以使用外补丁和内补丁。 -->
		<div id="div1">
			<div id="div2">
				
			</div>
		</div>
		
	</body>
</html>

```

### 008-float浮动效果.html：

```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title>float浮动效果</title>
		<style type="text/css">
			img {
				float: right;
			}
		</style>
	</head>
	<body>
		<p>
			<img src="img/lmt.gif" />
			《黛玉葬花》是文学名著《红楼梦》中的经典片段。林黛玉最怜惜花，觉得花落以后埋在土里最干净，
			说明她对美有独特的见解。她写了葬花词，以花比喻自己，在《红楼梦》中是最美丽的诗歌之一。
			贾宝玉和林黛玉在葬花的时候有一段对话，成为《红楼梦》中一场情人之间解除误会的绝唱。
			《黛玉葬花》是文学名著《红楼梦》中的经典片段。林黛玉最怜惜花，觉得花落以后埋在土里最干净，
			说明她对美有独特的见解。她写了葬花词，以花比喻自己，在《红楼梦》中是最美丽的诗歌之一。
			贾宝玉和林黛玉在葬花的时候有一段对话，成为《红楼梦》中一场情人之间解除误会的绝唱。
			《黛玉葬花》是文学名著《红楼梦》中的经典片段。林黛玉最怜惜花，觉得花落以后埋在土里最干净，
			说明她对美有独特的见解。她写了葬花词，以花比喻自己，在《红楼梦》中是最美丽的诗歌之一。
			贾宝玉和林黛玉在葬花的时候有一段对话，成为《红楼梦》中一场情人之间解除误会的绝唱。
			《黛玉葬花》是文学名著《红楼梦》中的经典片段。林黛玉最怜惜花，觉得花落以后埋在土里最干净，
			说明她对美有独特的见解。她写了葬花词，以花比喻自己，在《红楼梦》中是最美丽的诗歌之一。
			贾宝玉和林黛玉在葬花的时候有一段对话，成为《红楼梦》中一场情人之间解除误会的绝唱。
			《黛玉葬花》是文学名著《红楼梦》中的经典片段。林黛玉最怜惜花，觉得花落以后埋在土里最干净，
			说明她对美有独特的见解。她写了葬花词，以花比喻自己，在《红楼梦》中是最美丽的诗歌之一。
			贾宝玉和林黛玉在葬花的时候有一段对话，成为《红楼梦》中一场情人之间解除误会的绝唱。
			《黛玉葬花》是文学名著《红楼梦》中的经典片段。林黛玉最怜惜花，觉得花落以后埋在土里最干净，
			说明她对美有独特的见解。她写了葬花词，以花比喻自己，在《红楼梦》中是最美丽的诗歌之一。
			贾宝玉和林黛玉在葬花的时候有一段对话，成为《红楼梦》中一场情人之间解除误会的绝唱。
			《黛玉葬花》是文学名著《红楼梦》中的经典片段。林黛玉最怜惜花，觉得花落以后埋在土里最干净，
			说明她对美有独特的见解。她写了葬花词，以花比喻自己，在《红楼梦》中是最美丽的诗歌之一。
			贾宝玉和林黛玉在葬花的时候有一段对话，成为《红楼梦》中一场情人之间解除误会的绝唱。
		</p>
	</body>
</html>

```

### 009-定位样式position.html：

```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title>定位样式position</title>
		<style type="text/css">
			#div1 {
				background-color: red;
				border: solid 1px black;
				width: 100px;
				height: 100px;

				/* 定位 */				
				position: absolute;
				top: 100px;
				left: 100px;
			}
			
			#baidu:hover {
				/* 变成小手 */
				cursor: pointer ; /* 尽量不要使用hand，有浏览器兼容问题！*/
				text-decoration: underline;
				color: blue;
			}
		</style>
	</head>
	<body>
		
		<div id="div1">
			<span id="baidu">百度</span>
		</div>
		
	</body>
</html>

```

