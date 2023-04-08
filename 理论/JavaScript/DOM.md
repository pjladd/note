# DOM

## 1.0 为什么会有Dom，Dom的作用是什么？

DOM是JS操作网页的接口，全称为“文档对象模型”（Document Object Model）。它的作用是将网页转为一个JS对象，从而可以进行各种操作（比如增删内容）。从本质上说，它将web页面和脚本或编程语言连接起来了。DOM对象是JS对象。

在 DOM 中，所有 HTML 元素都被定义为对象。

```
文档对象模型：
			文档：文档表示的就是整个的HTML网页文档
			对象：对象表示将网页中的每一个部分都转换为了一个对象。
			模型：使用模型来表示对象之间的关系，这样方便我们获取对象
```

## 1.1 Document类型

一个Document对象表示一个HTML页面。

在JS当中有一个内置的Document对象叫做:document，document能直接拿来使用。

## 1.2 Element类型

一个Element 对象表示网页中的一个HTML元素。

## 1.3 NODE

Node 接口在 JavaScript中被实现为 Node 类型。
在 JavaScript中，所有节点类型都继承 Node 类型，因此所有节点类型都共享相同的基本属性和方法。

```
节点类型	                        值	                     对应常量
文档节点（Document）	               9	                  Node.DOCUMENT_NODE
元素节点（Element）	               1	                  Node.ELEMENT_NODE
属性节点（Attr）	                   2	                  Node.ATTRIBUTE_NODE
文本节点（Text）	                   3	                  Node.TEXT_NODE
文档类型节点（DocumentType）	     10	                     Node.DOCUMENT_TYPE_NODE
注释节点（Comment）	               8	                  Node.COMMENT_NODE
文档片断节点（DocumentFragment）	 11	                    Node.DOCUMENT_FRAGMENT_NODE
```

由上表可知Document类型，Element类型都是Node类型，都继承了Node类型。

## 1.4  Document类型常用属性

```
documentElement：始终指向HTML页面中的<html>元素。
body：直接指向<body>元素
doctype：访问<!DOCTYPE>, 浏览器支持不一致，很少使用
title：获取文档的标题
URL：取得完整的URL
domain：取得域名，并且可以进行设置，在跨域访问中经常会用到。
referrer：取得链接到当前页面的那个页面的URL，即来源页面的URL。
images：获取所有的img对象，返回HTMLCollection类数组对象
forms：获取所有的form对象，返回HTMLCollection类数组对象
links：获取文档中所有带href属性的<a>元素
```

## 1.5   Document类型常用方法

### 查找元素：

```
方法	                                            描述
document.getElementById(id)	                     通过元素 id 来查找元素
document.getElementsByTagName(name)              通过标签名来查找元素
document.getElementsByClassName(name)	         通过类名来查找元素
document.querySelector()	                     返回文档中匹配指定的CSS选择器的第一元素
```

### 添加元素：

```
document.createElement(element)
```

## 1.6   Element类型常用属性

```
attributes：返回一个与该元素相关的所有属性的集合。
classList：返回该元素包含的 class 属性的集合。
className：获取或设置指定元素的 class 属性的值。
clientHeight：获取元素内部的高度，包含内边距，但不包括水平滚动条、边框和外边距。
clientTop：返回该元素距离它上边界的高度。
clientLeft：返回该元素距离它左边界的宽度。
clientWidth：返回该元素它内部的宽度，包括内边距，但不包括垂直滚动条、边框和外边距。
innerHTML：设置或获取 HTML 语法表示的元素的后代。
tagName：返回当前元素的标签名。
```

## 1.7   Element类型常用方法

```
方法	                                                 描述
element.innerHTML = new html content	             改变元素的 innerHTML
element.attribute = value	                         修改属性的值
element.getAttribute()	                             返回元素节点的指定属性值。
element.setAttribute(attribute, value)	             设置或改变 HTML 元素的属性值
element.style.property = new style	                 改变 HTML 元素的样式
```

