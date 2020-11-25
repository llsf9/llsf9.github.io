---
layout: article
title: 《JavaScript DOM编程艺术》--JavaScript图片库
mathjax: true
tag: Js
---

## 《JavaScript DOM编程艺术》--JavaScript图片库


## 第四章 案例研究：JavaScript图片库

### 4.1 标记

1.为图片创建一个链接清单

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="utf-8">
	<title>My Gallery</title>
</head>
<body>
	<h1>Snapshots</h1>
	<ul>
		<li>
			<a href="1.jpg" title="A Host">Host</a>
		</li>
		<li>
			<a href="2.jpg" title="A Queen">Snow</a>
		</li>
		<li>
			<a href="3.jpg" title="A jinjya">Jinjya</a>
		</li>
		<li>
			<a href="4.jpg" title="A Tera">Tera</a>
		</li>
	</ul>
</body>
</html>
```
> **希望改进的地方**
> 1 点击链接时留在这个页面
> 2 点击链接时能在这个网页上同时看到那个图片和原有的图片清单
> 改进方法
> 1 增加一个占位符图片，为预览图片预留区域 
> 2 点击链接时拦截这个网页的默认行为
> 3 点击链接时把占位符图片替换为相应的图片

2.添加占位符图片 
在末尾添加
```html
<img id="placeholder" src="5.jpg">
```
![效果](https://upload-images.jianshu.io/upload_images/19597758-6d6c223f525cd450.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 4.2 设计JavaScript函数
> 目的
> - 获取预览图片的href
> - 将占位符图片的src改为预览图片的href

1.设whicpic为预览图片的元素节点
2.创建placeholder为占位符图片的元素节点
3.替换
```js
function showPic(whicpic){
			var source=whicpic.getAttribute("href");
			var placeholder=
			document.getElementById("placeholder");
			placeholder.setAttribute("src",source);
		}
```

### 4.3 应用这个JavaScript函数
1.加入事件处理函数

> **事件处理函数**：在特定时间调用特定的Js代码

我们还需要元素节点做参数，this关键字可以帮我们解决这个问题
> **this**：这个对象。当前例子中，this表示这个<a>元素节点
```html
onclick="showPic(this);"
```
> 注意：js代码在一对引号中
> 2.阻止浏览器的默认行为
> 使函数返回false，浏览器便会认为这个链接没有被点击
```html
onclick="showPic(this);return false;"
```
3.将每个链接添加上事件处理函数

```html
<ul>
		<li>
			<a href="1.jpg" title="A Host" onclick="showPic(this);return false;">Host</a>
		</li>
		<li>
			<a href="2.jpg" title="A Queen"  onclick="showPic(this);return false;">Snow</a>
		</li>
		<li>
			<a href="3.jpg" title="A jinjya"  onclick="showPic(this);return false;">Jinjya</a>
		</li>
		<li>
			<a href="4.jpg" title="A Tera"  onclick="showPic(this);return false;">Tera</a>
		</li>
	</ul>
```
![效果](https://upload-images.jianshu.io/upload_images/19597758-d198316c6cb02406.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 4.4 对函数进行扩展
先学习几个新的DOM属性
#### 4.4.1 childNodes属性
获取任何一个元素的所有子元素，是一个包含这个元素的所有子元素的***数组***。
其中，
1.孙节点（子节点的子节点）不属于此范围
2.子节点中的文本包括在这一个子节点中
3.换行被视为一个文本节点
```js
/*例*/
function conutBodyChildren(){
	var body_elements=document.getElementsByTagName("body")[0];
	alert(body_elements.childNodes.length);
}
window.onload=conutBodyChildren();
```
> onload事件处理函数：使js函数在页面加载时执行

>**为什么这个onload和之前的onclick语法不同？**
>在html中和在JavaScript中的语法格式不同。

#### 4.4.2 nodeType属性
返回节点的nodeType属性（数字）
- 元素节点->1
- 属性节点->2
- 文本节点->3

将之前的代码改一下
```js
/*例*/
alert(body_elements.nodeType);
```
#### 4.4.3 在标记里增加一段描述
> 目的
>
> - 添加一个占位符文字，使它显示图片的标题

在末端添加
```html
<p id="description">Choose a picture</p>
```
#### 4.4.5 nodeValue属性
nodeValue返回一个节点的值。而想要获取文本值时，需要从这个元素节点的文本节点中获取。
这个例子中，包含在<p>元素里的文本是<p>元素的第一个子节点的nodeValue属性值。
以下这个语句可以显示<p>的文本值
```js
var description=document.getElementById("description");
alert(description.childNode[0].nodeValue);
```
但是以下这个语句只能显示null
```js
alert(description.nodeValue);
```
#### 4.4.6 firstChild和lastChild属性
- node.firstChild
  等同于`node.childNode[0]`
- node.lastChild
  等同于`node.cildNode[node.childNode.length-1]`

#### 4.4.7 利用nodeValue属性刷新这段描述
在function showpic最后加上
```js
var description=document.getElementById("description");
var text=whicpic.getAttribute("title");
description.firstChild.nodeValue=text;
```
> 第二行之后若改成
> ```js
> var text=whicpic.getAttribute("title".firstChild.nodeValue);
> description=text;
> ```
> 便会失败。因为text应该对应的是对象，而不是一个值。（类似指针？）

## 第六章 案例研究：图片库改进版

### 6.2 他支持平稳退化吗？

```html
<li>
			<a href="1.jpg" title="A Host" onclick="showPic(this);return false;">Host</a>
</li>
```

支持。根据源代码，即使用户的浏览器不支持js，根据href的属性仍能打开图片。

### 6.3 他的JavaScript与HTML标记是分离的吗

不是。很明显，onclick事件处理函数放到了标签中。

#### 6.3.1 添加事件处理函数

> 目标：
>
> - 检查当前浏览器是否理解getElementsByTagName
> - 检查当前浏览器是否理解getElementById
> - 检查当前网页是否存在一个id为imagegallery的元素
> - 遍历imagegallery元素中的所有链接
> - 设置onclick事件处理函数

1.对象检测

```js
if(!document.getElementsByTagName 		 	||!document.getElementById){
		return false;
}
```

检查完DOM之后，我们还要确定一下imagegallery这个id是否还存在

```js
if(!document.getElementById("imagegallery")){
		return false;
}
```

2.变量

```js
var gallery=document.getElementById("imagegallery");
var links=gallery.getElementsByTagName("a");
```

3.4.添加外部事件处理函数

```js
for(vai i=0;i<links.length;i++){
		links[i].onclik=function(){
			showPic(this);
			return false;
		}
	}
```

5.完成JavaScript函数

```js
function prepare(){
	if(!document.getElementsByTagName || !document.getElementById){
		return false;
	}
	if(!document.getElementById("imagegallery")){
		return false;
	}
	var gallery=document.getElementById("imagegallery");
	var links=gallery.getElementsByTagName("a");
	for(vai i=0;i<links.length;i++){
		links[i].onclik=function(){
			showPic(this);
			return false;
		}
	}
}
```

#### 6.3.2 共享onload事件

想把多个函数逐一绑定在onload事件上的方法

1.创建匿名函数容纳多个函数，再把匿名函数绑定到onload上：

```js
window.onload=function(){
	firstFunction();
	secondFuction();
}
```

2.addLoadEvent函数

​	把现有的window.onload事件处理函数的值存入变量oldonload。如果这个事件处理函数上还没有绑定任何函数，就像平时一样把新函数添加给他。如果这个事件处理函数上已经绑定了一些函数，就把新函数追加到现有指令的末尾。

```js
function addLoadEvent(func){
	var oldonload = window.onload;
	if(typeof window.onload != "function"){
		window.onload=func;
	}
	else{
		window.onload=function(){
			oldonload();
			func();
		}
	}
} 
addLoadEvent(firstFunction);
addloadEvent(secondFunction);
```

因此，为了以后的拓展，我们的的代码可以加上

```js
addLoadEvent(prepareGallery);
```

### 6.4 不要做太多假设

在图片库的showPic函数中，我们使用了placeholder和description元素，却没有检查其存在性，因此修改为：

```js
function showPic(whicpic){
	if(document.getElementById("placeholder")){
		return false;
	}//若不存在占位符图片就离开
	var source=whicpic.getAttribute("href");
	var placeholder=document.getElementById("placeholder");
	placeholder.setAttribute("src",source);
	if(document.getElementById("description")){
		var description=document.getElementById("description");
		var text=whicpic.getAttribute("title");
		description.firstChild.nodeValue=text;
	}//若不存在占位符文字就不显示图片标题
}
```

这样的问题是如果没有占位符图片，showPic不会正常执行；而且prepareGallery我们阻止了浏览器的默认行为，这时点击链接没有任何变化。

基于平稳退化的思想，我们可以使当showPic返回true时阻止默认行为，而返回false时不阻止。把最后改为：

```js
links[i].onclik=function(){
			return !showPic(this);
}
```

### 6.5 优化（三元操作符，nodeName)

1.检查title属性是否真的存在。若不存在，则将text变量的值设为空字符串

```js
if(whicpic.getAttribute("title")){
		var text=whicpic.getAttribute("title");
}
else{
		var text="";
}
```

或者用三元操作符

```js
var text=whicpic.getAttribute("title") ? whicpic.getAttribute("title"):"";
```

> 三元操作符
>
> ```js
> variable=condition?if true:if false;
> ```

2.检查placeholder是否为一张图片

```js
if(placeholder.nodeName!="IMG"){
		return false;
}
```

> nodeName:
>
> 总是返回一个大写字母的值，即使元素在文档里是小写字母

3.检查description的第一个子元素的值为文本内容

```js
		if(description.firstChild.nodetype==3){
			description.firstChild.nodeValue=text;
		}
```

最终的showPic函数为：

```js
function showPic(whicpic){
	if()
	if(!document.getElementById("placeholder")){
		return false;
	}
	var source=whicpic.getAttribute("href");
	var placeholder=document.getElementById("placeholder");
	if(placeholder.nodeName!="IMG"){
		return false;
	}
	placeholder.setAttribute("src",source);
	if(document.getElementById("description")){
		var description=document.getElementById("description");
		if(whicpic.getAttribute("title")){
			var text=whicpic.getAttribute("title");
		}
		else{
			var text="";
		}
		if(description.firstChild.nodetype==3){
			description.firstChild.nodeValue=text;
		}
	}
	return true;
}
```

### 6.6 键盘访问

有视力残疾的用户往往无法看到鼠标指针，他们更喜欢用键盘。

可以利用onkeypress处理键盘事件，几乎按下每个键都会触发onkeypress：

```js
links[i].onclick=function(){
	return !showPic(this);
}
links[i].onkeypress=links[i].onclick;
```

> 小心onkeypress
>
> 最终我们决定不使用上列代码。
>
> 在某些浏览器中甚至TAB都会触发onkeypress，这导致键盘用户永远无法离开这个链接。
>
> onclick其实已经完美支持键盘，当用tab切换链接，并按下enter键就会触发onclick事件。使用onclick绰绰有余。

### 6.8 DOM Core和HTML-DOM 

至此我们使用的几个DOM方法并不专属于js，任何一个支持dom的语言都可以使用他们。这些都是DOM Core的组成部分

而类似于onclick这样的属性属于HTML-DOM在DOM Core出现前就为人们所熟悉了。类似的，HTML-DOM可以将以下的语句：

```js
document.getElementsByTagName("form");
```

简化为

```js
document.form
```

以及将，

```js
element.getAttribute("src");
```

简化为

```js
element.src
```

还有

```js
placeholder.setAttribute("src",source)
```

简化为

```js
placeholer.src=source
```

### 7.3 重回图片库

HTML文件中有一个图片和一段文字只是为js文件服务的，若把结构和行为彻底分开就再好不过了。

我们可以编写一个函数，使他在文档加载时被调用并创建图片和一段文字

```js
window.onload=function(){
	var placeholder=document.createElement("img");
	var description=document.createElement("p");
	var desctxt=document.createTextNode("Choose a picture");
	document.body.appendChild(placeholder);
	document.body.appendChild(description);
	placeholder.setAttribute("src","images/5.jpg");
	placeholder.setAttribute("id","placeholder");
	description.appendChild(desctxt);
	description.setAttribute("id","description");
}
```

> 但这一切都是由于我们要插入的恰好在是在<body>的末端。我们的真实想法是，让新创建的元素紧跟在图片清单后面。

#### 7.3.1 在已有元素前插入一个新元素（insertBefore( ),parentNode）

```js
parentElement.insertBefore(newElement,targetElement);
```

比如这一句可以把元素插在图片清单前：

```js
var gallery=document.getElementById("imagegallery");
gallery.parentNode.insertBefore(placeholder,gallery);
gallery.parentNode.insertBefore(description,gallery);
```

#### 7.3.2 在现有方法后插入一个新元素（nextSibling，lastChild)

DOM并没有提供insertAfter方法，但我们可以自建一个

1.编写insertAfter函数

```js
function insertAfter(newElement,targetElement){
	var parent=targetElement.parentNode;
	if(parent.lastChild=="targetElement"){
		parent.appendChild(newElement);
	}
	else{  	
    	parent.insertBefore(newElement,targetElement.nextSibling);
	}
}
```

2.使用insertAfter函数

将之前的创建空白符的函数整合在一起；

```js
function preparePlaceholder(){
	var placeholder=document.createElement("img");
	var description=document.createElement("p");
	var desctxt=document.createTextNode("Choose a picture");
	insertAfter(placeholder,imagegallery);
	insertAfter(description,placeholder);
	placeholder.setAttribute("src","images/5.jpg");
	placeholder.setAttribute("id","placeholder");
	description.appendChild(desctxt);
	description.setAttribute("id","description");	
}
```

并且为了检测对象，我们又在开头加了几行；

```js
if(!document.createElement){
		return false;
	}
if(!document.createTextNode){
  return false;
}
if(!document.getElementById){
  return false;
}
if(!document.getElementById("imagegallery")){
  return false;
}
```

### 7.4 Ajax

Ajax可以只更新页面的一部分内容，而不会打断用户的浏览体验

#### 7.4.1 XMLHttpRequest对象

没看懂

#### 7.4.3 Hijax



