---
layout: article
title: 《JavaScript DOM编程艺术》
mathjax: true
tag: Js
---

## 《JavaScript DOM编程艺术》


## 第二章 准备

### 2.1 准备工作

- 插入方法
1.将js代码放到文档<head>中的<script>标签中
```html
<head>
  <script>
```
2.放到文档最后，</body>之前**（推荐：能使网页加载更快）**
> <script>标签中已经不需要传统的type="text/javascript"。因为默认即为js。

### 2.2 语法
#### 2.2.3 变量
1.变量的声明
`var mood;`
2.变量的赋值
`mood=13;`
#### 2.2.4 数据类型
> js是弱类型语言，因此不需要声明变量的数据类型。以下的数据类型的变量的声明和赋值语法均相同。

1.字符串（单引号和双引号均可）
2.数值
3.布尔值（false或true。不需要引号）
4.数组
- 声明
  1.`var sue=Array();`
  2.`var sue=[];`
- 赋值
  1`.var sue=Array("a", "b", "c");`
  2.`var sue=["a", "b", "c"];`
  3.（已声明的）`sue[0]="a";`
- 关联数组（不推荐使用）
  ```js
  var arr=Array();
  arr[a]="a";
  arr[b]=1997;
  arr[c]=false;
  ```
  给Array类型的对象添加了三个属性->应该使用通用对象Object

5.对象
将关联数组改为
```js
/*obeject第一种创建方式*/
var arr=Object();
arr.a="a";
arr.b=1997;
arr.c=false;
```
或**花括号创建法**
```js
/*object第二种创建方式*/
var arr={a:"a", b:1997, c=false};
```
> 用对象来替代传统数组的意味是可以通过文字而不是数字来引用它们。这大大提高了脚本的可读性。

### 2.3 操作
- \+
加号不仅用于运算，也用于字符串的拼接
```js
var Hello = "Good" + "morning";
```
### 2.6 函数
```js
function multiply(num1, num2){
  var total=num1*num2;
  alert(total);
}
multiply(10,2);
```
##### 变量的作用域
*如果某个函数中使用了var，则变量被视为局部变量，只存在于函数中；反之没有使用var，变量会被视为全局变量。且若脚本里已存在一个与之同名的全局变量，这个函数的行为会改变这个全局变量*

### 2.7 对象
- 属性：隶属于某个特定对象的变量
```js
Person.age;
```
- 方法：只有某个特定对象才能调用的函数
```js
Person.walk();
```
- 实例：对象的具体个体（**new**关键词）
```js
var jenny=new Person;
jenny.age;
jenny.walk();
```
#### 2.7.1 内建对象
#### 2.7.2 宿主对象

## 第三章 节点
### 3.4 节点
#### 3.4.1 元素节点
网页文档中的一切元素例如<html><head><body>
#### 3.4.2 文本节点
包含有文本的元素节点，其中文本的具体内容称为文本节点。**并非所有元素节点具有文本节点，但所有文本节点一定被包含在元素节点中**。
#### 3.4.3 属性节点
包含有属性的元素节点，其中属性的具体内容称为属性节点。**并非所有元素节点具有属性节点，但所有属性节点一定被包含在元素节点中**。
#### 3.4.5 获取元素
1.**getElementById**
document对象的特有函数。getElementById方法内有一个参数，就是你想获得的元素的id值，这个id值必须放在单引号或双引号内
```js
/*例*/
document. getElementById("purchases");
```
这个调用将返回一个对象，这个对象对应着document对象里一个独一无二的元素。
> 事实上，文档中的每一个元素都是一个对象

2.**getElementsByTagName**
```js
/*例*/
document. getElementsByTagName("li");
```
这个调用将返回一个对象数组，每个对象分别对应着document对象中的有着给定标签的一个元素。使用中括号便可分别调用每个对象。
**特殊**：getElementsByTagName允许把一个通配符作为参数。例如
```js
var items = document.getElementsByTagName("*");
```
items数组将包含文档中的所有元素节点

3.**getElementsByClassName**
```js
/*例*/
document.getElementsByClassName("sale");
```
返回具有相同类名的元素的数组
**特殊**：可以查找带有多个类名的元素。只要在字符串参数中用空格分割类名即可。（无序匹配）
```js
/*例*/
document.getElementsByClassName("sale important");
```
### 3.5 获取和设置属性
#### 3.5.1 getAttribute
getAttribute方法不属于document对象，它只能通过元素节点调用。
```js
/*例*/
var paras = document.getElementsByTagName("p");
for(var i =0;i<paras.length;i++){
  alert(paras[i].getAttribute("title"));
}
```
返回对象的指定属性内容

#### 3.5.3 setAttribut
setAttribute()允许我们对属性节点的值作出修改
```
/*例*/
var shopping=document.getElementById("purchases");
shopping.setAttribute("title","a list of goods");
```
若属性本身并不存在，setAttribute实际完成了两项操作：先创建这个属性，然后设置它的值；如果用于本身就有这个属性的元素节点上，这个属性的值就会被覆盖掉。
> 通过setAttribute对文档进行修改后，用浏览器的查看源代码看到的仍然是改变前的属性值。也就是说setAttribute做出的修改并不会反映在文档本身的源代码中。
> 这源于DOM的工作方式：先加载文档的静态内容，再动态刷新，动态刷新并不影响文档的静态内容。

## 第五章 最佳实践
### 5.2 平稳退化
### 5.3 向css学习
#### 5.3.2 渐进增强

### 5.4 分离JavaScript

类似于使用style属性，在html文档里使用诸如onclick之类的属性也是一种<u>既没效率又容易引发问题的做法</u>

我们可以在外部Js文件里把一个事件添加到html文档中的某个元素上：

```js
/*例*/
getElementById(id).event=action;
```

当我们想让一个链接从新窗口打开，我们可以用onclick和open（）配合，并阻止浏览器的默认行为：

```js
/*例*/
var links= document.getElementsByTagName("a");
for(var i=0;i<links.length;i++){
	if (links[i].getAttribute("class")=="popup"){
		links[i].onclick=function(){
			popup(this.getAttribute("href"));
			return false;
		}
	}
}
function pop(winURL){
	window.open(winURL,"popup","width=320,height=480");
}
```

还有个问题需要解决：如果把这段代码放入外部文件，他们将无法正常运行，因为它很可能在文档加载完成前被加载。没有完整的DOM,getElementById等方法就不能正常工作。

必须让这些代码在HTML文档全部加载到浏览器之后马上开始执行：

```js
/*例*/
window.onload=prepareLinks;
function prepareLinks(){
  var links= document.getElementsByTagName("a");
  for(var i=0;i<links.length;i++){
    if (links[i].getAttribute("class")=="popup"){
      links[i].onclick=function(){
        popup(this.getAttribute("href"));
        return false;
      }
    }
  }
}
function pop(winURL){
	window.open(winURL,"popup","width=320,height=480");
}
```

### 5.5 向后兼容
#### 5.5.1 对象检测

针对浏览器不支持js的问题，最简单的解决方法是检测浏览器对js的支持程度：

```js
function myFunction(){
	if (document.getElementbyId){
		statement using getElementById
	}
}
```

> 注意：在使用对象检测时，方法后面的圆括号一定要删掉

如此一来造成的后果是我们会增加一对花括号，为了方便阅读和理解，将测试条件改为"如果你不理解请离开"更为易懂

```js
/*例*/
window.onload=prepareLinks;
function prepareLinks(){
	if(!document.getElementByTagName){
		return false;
	}
  var links= document.getElementsByTagName("a");
  for(var i=0;i<links.length;i++){
    if (links[i].getAttribute("class")=="popup"){
      links[i].onclick=function(){
        popup(this.getAttribute("href"));
        return false;
      }
    }
  }
}
function pop(winURL){
	window.open(winURL,"popup","width=320,height=480");
}
```



### 5.6 性能考虑

#### 5.6.1 尽量少访问DOM和尽量减少标记

1.避免重复用DOM函数做同一件事，更好的处理方法是使用变量储存他们

2.避免在文档中做太多标记，增加DOM搜索的工作量

#### 5.6.2 合并和放置脚本

1.尽量把多个js文件合并成一个文件，减少请求数量

2.把脚本放置于</body>前，加快文档加载

#### 5.6.3 压缩脚本

利用软件删除不必要的注释空格，缩短变量名。

- 优点：减小文件大小
- 缺点：大大降低可读性
- 解决方法：准备两个版本，精简版本上传，正常版本本地修改

## 第七章 动态创建标记

### 7.1 一些传统方法

#### 7.1.1 document.write

```html
<body>
	<script>
		documrnt.write("<p>This is inserted.</p>")
	</script>
</body>
```

document.write最大的缺点是他违背了行为应该与表现分离的原则。我们应该避免使用它。

#### 7.1.2 innerHTML属性

当想插入文档一段话时就可以使用：

```js
testdiv.innerHTML="<p>I inserted <em>this</em> 	content.</p>";
```

但是这个技术无法区分插入一段内容和修改一段内容。即使原文档有内容，最终效果也是一样的。

而DOM就可以提供更为精确的方法和属性。

### 7.2 DOM方法

> 在DOM看来，一个文档就是一棵节点树。你并不是在创建标记，而实在改变DOM节点树。

#### 7.2.1 createElement方法

当我们想在testdiv中添加一个p元素节点时，我们要做两件事

1.创建一个新的元素

2.把这个新元素插入节点树

创建元素由creatElement完成：

```js
var para=document.createElement("p");
```

现在pare包含一个指向刚创建的元素的引用。这个p虽然已经存在了，但它还不是任何一棵DOM节点树的组成，它只是游荡在JavaScript世界里的一个孤儿。这种情况被称为***文档碎片***，还无法显示在浏览器的窗口画面里。

#### 7.2.2 appendChild方法

把新创建的节点插入到元素节点的子节点中；

```js
var para=document.createElement("p");
var testdiv = document.getElementById("testdiv");
testdiv.appendChild("para");
```

#### 7.2.3 creatTextNode方法

现在我们想把一些文本放入到p元素中，但creatElement方法帮不上忙，它只能创建元素节点。你需要创建一个文本节点，createTextNode可以做到:

```js
var txt=document.creatTextNode("Hello World");
```

与creatElement的性质一样，现在变量txt包含指向新创建的文本节点的引用。这个节点现在也是js世界的一个孤儿，它还未被插入到任何一个文档的节点树。

appendChild依然可以帮我们插入它到p元素节点中：

```js
para.appendChild(txt);
```

#### 7.2.4 一个更复杂的组合

![思路](https://s2.ax1x.com/2020/02/13/1qTZgH.png)

根据上述步骤编写出来的js代码

```js
window.onload=function (){
	var para=document.createElement("p");
	var txt1=document.createTextNode("This is ");
	var emphasis=document.createElement("em");
	var txt2=document.createTextNode("my ");
	var txt3=document.createTextNode("content.");
	para.appendChild(txt1);
	emphasis.appendChild(txt2);
	para.appendChild(emphasis);
	para.appendChild(txt3);
	var testdiv=document.getElementById("testdiv");
	testdiv.appendChild(para);
}
```

### 7.4 Ajax

Ajax可以只更新页面的一部分内容，而不会打断用户的浏览体验

#### 7.4.1 XMLHttpRequest对象

没看懂

#### 7.4.3 Hijax



## 第八章 充实文档的内容（explanation）

### 8.1 不应该做什么

不要用js把一些重要的内容添加在网页上。那些缺乏js的用户永远看不到，而且搜索引擎的机器人也检测不到js内容。

### 8.3 内容

```html
<!DOCTYPE html>
<html>
<head>
	<title>Test</title>
</head>
<body>
	<h1>What is the Document Object Model></h1>

	<p>The <abbr title="World Wide Web Consortium">W3C</abbr> defines the <abbr title="Document Object Model">DOM</abbr> as :</p>

	<blockquote cite="http://www.w3.org/DOM/">

	<p>A platform- and language-neutral interface that will allow programs and scripts to dynamically access and update the content,structure and style of documents.</p>

	</blockquote>

	<p>It is an <abbr title="Application Programming Interface">API</abbr> that can be used to navigate <abbr title="Hypertext Markup Language">HTML</abbr> and <abbr title="eXtensible Markup Language">XML</abbr> documents.</p>

	<script type="text/javascript" src="./test.js"></script>
</body>
</html>
```

> <abbr>
>
> 缩略语

#### 8.3.2 css

```css
body{
	font-family: "Helvetica","Arial",sans-serif;
	font-size: 10pt;
}
abbr{
	text-decoration: none;
	border: 0;
	font-style: normal;
}
```

### 8.4 显示缩略语列表

![1X4RWF.png](https://s2.ax1x.com/2020/02/14/1X4RWF.png)

1.遍历这份文档中的所有abbr元素

```js
	var abbreviations=document.getElementsByTagName("abbr");
	if(abbreviations.length<1){
		return false;
	}
```

不一定所有文档都有缩略语，当没有缩略语时立刻停止这个函数

2.3.保存每个abbr元素的title和包含的文本

```js
	var defs=new Array();
	for(var i=0;i<abbreviations.length;i++){
		var definition=abbreviations[i].getAttribute("title");
		var key=abbreviations[i].lastChild.nodeValue;
		defs[key]=definition;
	}
```

书中方法将title和文本形成了关联数组。

而关于文本部分，根据缩略语的特性，前端很可能将它放在<em></em>中来做提示，因此用lastChild比较保险

4.创建一个定义列表元素

```js
var dlist=document.createElement("dl");
```

5.6.7.8.9.10.11

```js
	for(key in defs){
		var definition=defs[key];
		var dtitle=document.createElement("dt");
		var dtitle_text=document.createTextNode(key);
		dtitle.appendChild(dtitle_text);
		var ddesc=document.createElement("dd");
		var ddesc_text=document.createTextNode(definition);
		ddesc.appendChild(ddesc_text);
		dlist.appendChild(dtitle);
		dlist.appendChild(ddesc);
	}
```

> for/in循环：
>
> 遍历关联数组/对象的每个属性。

12.插入这个列表元素

直接插入有些突兀，我们可以在他之前先加一个h2标题：

```js
	var header=document.createElement("h2");
	var header_text=document.createTextNode("Abbreviations");
	header.appendChild(header_text);
	document.body.appendChild(header);
	document.body.appendChild(dlist);
```

至此，按照步骤这个函数已经初步完成：

```js
function displayAbbreviations(){
	var abbreviations=document.getElementsByTagName("abbr");
	if(abbreviations.length<1){
		return false;
	}
	var defs=new Array();
	for(var i=0;i<abbreviations.length;i++){
		var definition=abbreviations[i].getAttribute("title");
		var key=abbreviations[i].lastChild.nodeValue;
		defs[key]=definition;
	}
	var dlist=document.createElement("dl");
	for(key in defs){
		var definition=defs[key];
		var dtitle=document.createElement("dt");
		var dtitle_text=document.createTextNode(key);
		dtitle.appendChild(dtitle_text);
		var ddesc=document.createElement("dd");
		var ddesc_text=document.createTextNode(definition);
		ddesc.appendChild(ddesc_text);
		dlist.appendChild(dtitle);
		dlist.appendChild(ddesc);
	}
	var header=document.createElement("h2");
	var header_text=document.createTextNode("Abbreviations");
	header.appendChild(header_text);
	document.body.appendChild(header);
	document.body.appendChild(dlist);
}
```

但这个函数还有需要改进的部分

- 检查兼容性

  1.DOM方法存在性的检测

  2.添加注释

  3.添加addEvent.js文件

  4.将两个js文件关联到文档中

完成以上步骤后最终函数为（addLoadEvent文件省略）：

```js
function displayAbbreviations(){
	//对象检测
	if(!document.getElementsByTagName || !document.createElement 
		|| !document.createTextNode){
		return false;
	}
	//遍历abbr及存在性
	var abbreviations=document.getElementsByTagName("abbr");
	if(abbreviations.length<1){
		return false;
	}
	//存储title和文本内容
	var defs=new Array();
	for(var i=0;i<abbreviations.length;i++){
		var definition=abbreviations[i].getAttribute("title");
		var key=abbreviations[i].lastChild.nodeValue;
		defs[key]=definition;
	}
	//创建列表，插入文本内容
	var dlist=document.createElement("dl");
	for(key in defs){
		var definition=defs[key];
		var dtitle=document.createElement("dt");
		var dtitle_text=document.createTextNode(key);
		dtitle.appendChild(dtitle_text);
		var ddesc=document.createElement("dd");
		var ddesc_text=document.createTextNode(definition);
		ddesc.appendChild(ddesc_text);
		dlist.appendChild(dtitle);
		dlist.appendChild(ddesc);
	}
	//向文档插入标题和列表
	var header=document.createElement("h2");
	var header_text=document.createTextNode("Abbreviations");
	header.appendChild(header_text);
	document.body.appendChild(header);
	document.body.appendChild(dlist);
}
```



以下是没有用书本的关联数组的我自己的写法：

```js
window.onload=function displayAbbreviations(){
	var abbr=document.getElementsByTagName("abbr");
	var defs=new Array();
	var key=new Array();
	for(var i=0;i<abbr.length;i++){
		defs[i]=abbr[i].getAttribute("title");
		key[i]=abbr[i].firstChild.nodeValue;
	}
	var dl=document.createElement("dl");
	for(var i=0;i<abbr.length;i++){
		var dt=document.createElement("dt");
		var dt_title=document.createTextNode(key[i]);
		dt.appendChild(dt_title);
		var dd=document.createElement("dd");
		var dd_title=document.createTextNode(defs[i]);
		dd.appendChild(dd_title);
		dl.appendChild(dt);
		dl.appendChild(dd);
	}
	document.body.appendChild(dl);
}
```

#### 8.4.3 一个浏览器的地雷

在IE7之前是不支持abbr文法的，因此js无法获取abbr元素节点。

我们应该实现函数的平稳退化。

由于IE浏览器在统计abbr元素的子节点个数时总会返回一个错误值---0。因此我们添加：

```js
	for(var i=0;i<abbreviations.length;i++){
		if(abbreviations[i].childNodes.length<1){
			return continue;
		}
		var definition=abbreviations[i].getAttribute("title");
		var key=abbreviations[i].lastChild.nodeValue;
		defs[key]=definition;
	}

```

因为要检测abbr元素的子节点个数，而不是数组的子节点，因此要在for文中检测。并且要保证所有的abbr元素节点都不存在，才是真的在ie前期版本中。因此这里用的是continue而不是false。

以及在第二个for文后：

```js
if(dlist.childNodes.length<1){
		return false;
	}
```

如果所有abbr元素节点都不存在，那第二个for文根本无法执行（defs为空），因此如果dlist中没有子节点，则结束函数，说明这个浏览器真的不支持abbr。

最终完成函数：

```js
function displayAbbreviations(){
	//对象检测
	if(!document.getElementsByTagName || !document.createElement 
		|| !document.createTextNode){
		return false;
	}
	//遍历abbr及存在性
	var abbreviations=document.getElementsByTagName("abbr");
	if(abbreviations.length<1){
		return false;
	}
	//存储title和文本内容
	var defs=new Array();
	for(var i=0;i<abbreviations.length;i++){
		if(abbreviations[i].childNodes.length<1){
			return continue;
		}
		var definition=abbreviations[i].getAttribute("title");
		var key=abbreviations[i].lastChild.nodeValue;
		defs[key]=definition;
	}
	//创建列表，插入文本内容
	var dlist=document.createElement("dl");
	for(key in defs){
		var definition=defs[key];
		var dtitle=document.createElement("dt");
		var dtitle_text=document.createTextNode(key);
		dtitle.appendChild(dtitle_text);
		var ddesc=document.createElement("dd");
		var ddesc_text=document.createTextNode(definition);
		ddesc.appendChild(ddesc_text);
		dlist.appendChild(dtitle);
		dlist.appendChild(ddesc);
	}
	if(dlist.childNodes.length<1){
		return false;
	}
	//向文档插入标题和列表
	var header=document.createElement("h2");
	var header_text=document.createTextNode("Abbreviations");
	header.appendChild(header_text);
	document.body.appendChild(header);
	document.body.appendChild(dlist);
}
```

### 8.5 显示文献来源链接表

1.查找你的元素

查找blackquote元素很简单。以及当这个blackquote没有给出链接时，我们就不必显示链接表：

```js
	var quotes=document.getElementsByTagName("blockquote");
	for(var i=0;i<quotes.length;i++){
		if(!quotes[i].getAttribute("cite")){
			continue;
		}
    var url=quotes[i].getAttribute("cite");
	}
```

还有一个问题；我们想把链接显示在引用文献的后面。而blackquote里面还有p元素，我们要把他调用出来。但是在这两个元素之间还有换行符，它也属于节点之一，我们无法直接使用firstchild或lastchild。我们可以先把所有元素找出来，再选取最后一个。

```js
		var quotesElements=quotes[i].getElementsByTagName("*");
		var elem=quotesElements[quotesElements.length-1];

```

2.创建链接

```js
		var links=document.createElement("a");
		var links_text=document.createTextNode("source");
		links.appendChild(links_text);
		links.setAttribute("href",url);
```

3.插入链接

我们可以再插入一个<sup>上标元素，让链接看起来更舒服；

```js
		var superscript=document.createElement("sup");
		superscript.appendChild(links);
		elem.appendChild(superscript);
```

最后的完整函数：

```js
function displayCitations(){
	var quotes=document.getElementsByTagName("blockquote");
	for(var i=0;i<quotes.length;i++){
		//DOM对象检测
		if(!document.getElementsByTagName || !document.createElement 
		|| !document.createTextNode){
			return false;
		}
		//cite属性存在性检测
		if(!quotes[i].getAttribute("cite")){
			continue;
		}
		//调用cite属性
		var url=quotes[i].getAttribute("cite");
		//调用p元素
		var quotesElements=quotes[i].getElementsByTagName("*");
		var elem=quotesElements[quotesElements.length-1];
		//创建链接
		var links=document.createElement("a");
		var links_text=document.createTextNode("source");
		links.appendChild(links_text);
		links.setAttribute("href",url);
		//插入链接
		var superscript=document.createElement("sup");
		superscript.appendChild(links);
		elem.appendChild(superscript);
	}
}

addLoadEvent(displayCitations);
```

![1x9Qyj.png](https://s2.ax1x.com/2020/02/15/1x9Qyj.png)



## 第九章 CSS-DOM

### 9.1 三位一体的网页

- 结构层

  HTML，XHTML

- 表示层

  CSS

- 行为层

  Js，DOM

### 9.2 style属性

每个元素节点都有一个属性style。style属性包含着元素的样式，查询style属性不会返回一个简单的字符串而是一个对象。往事都被存放在这个style对象里。

```js
element.style.property
```

例如：

```js
para.style.color
```

而当样式名由连字符时，不管有多少个，都将他们后面的字母变成驼峰命名法。如font-family:

```js
para.style.fontFamily
```

同样的，background-color对应着backgroundColor，margin-top-width对应着marginTopWidth．

DOM在表示样式属性时采用的单位大部分和css样式表里的设置相同。

#### 内嵌样式

在外部样式表里生命的样式不会进入style对象，在文档<head>部分里声明的样式也是如此。DOM无法提取到他们的属性。

#### 9.2.2 设置样式

style对象不仅可以用来调用，还可以设置：

```js
para.style.color="black";
```

### 9.3 何时该用DOM脚本设置样式

#### 9.3.1 根据元素在节点树里的位置来设置样式（getNextElement）

比如想找到每个h1元素后面的元素，并改变他的样式：

```js
var headers=document.getElementByTagName("h1");
```

nextSibling只能找到下一个节点，但不一定是元素节点，我们可以写一个判断函数:

```js
function getNextElement(node){
	//如果这个节点就是元素节点，直接返回
	if(node.nodeType==1){
		return node;
	}
	//如果存在下一个节点且不为元素节点，继续递归下一个
	if(node.nextSibling){
		return getNextElement(node.nextSibling);
	}
	//下一个节点不存在
	return null;
}
var elem=getNextElement(headers[i].nextSibling);
```

这样我们就可以设置h1后面的元素elem的样式了：

```js
elem.style.fontWeight="bold";
elem.style.fontSize="1.2em";
```

#### 9.3.2 根据某种条件反复设置某种样式

js非常擅长利用for遍历所有元素。

#### 9.3.3 响应事件

CSS中有许多伪属性使我们可以进行时间（:hover等），但不同浏览器对他们的支持程度不一，但却对js完美支持。这种情况我们应该考虑：

- 这个问题最简单的解决方案是什么
- 哪种解决方案会得到更多浏览器的支持

### 9.4 className属性

比如之前的修改h1标题后的元素节点：我们可以有更简单的方式：

```css
.intro{
	font-weight:bold;
	font-size:1.2em;
}
```

```js
elem.setAttribute("class","intro");
```

就可以达到同样的效果。

而还有更简单的方法是更新className属性。这是个可读可写的属性，凡是元素节点就有这个属性。上面的语法可以写成：

```js
elem.className="intro";
```

如果我们想保留原class的样式，可以变为(请注意，第一个字符为空格)：

```js
elem.className+=" intro";
```

以上，我们可以封装一个函数addClass：

```js
function addClass(element,value){
	if(element.className==NULL){
		element.className=value;
	}
	else{
		element.className+=" ";
		element.className+=value;
	}
}
```

这确保了表示层和行为层分离的更加彻底。

#### 对函数进行抽象

再如刚才的对h1后面元素的样式进行改变的函数，与其让他们定死为h1和intro，不如将他们封装为函数，这样以后同样的操作时我们也能使用。

## 第十章 用JavaScript实现动画效果

#### 10.1.1 位置

首先设置一个元素的位置：

```js
function positionMessage(){
	if(!document.getElementById || !document.getElementById("message")){
		return false;
	}
	var elem=document.getElementById("message");
	elem.style.position="absolute";
	elem.style.left="50px";
	elem.style.top="100px";
}
```

想去移动也很简单

```js
function moveMessage(){
	if(!document.getElementById || !document.getElementById("message")){
		return false;
	}
	var elem=document.getElementById("message");
	elem.style.left="200px";
}

addLoadEvent(positionMessage);
addLoadEvent(moveMessage);
```

但这样最终呈现的没有动的过程。

#### 10.1.2 时间(setTimeout,clearTimeout)

setTimeout能够让某个函数在经过一段预定的时间后才开始执行：

```js
setTimeout("function",interval);
```

第一个参数是字符串，为执行函数的名字。第二个参数是以毫秒为单位的预定时间。

与之相对的，还有一个可以取消这个函数的函数：

```js
clearTimeout(variable);
```

他可以取消setTimeout在等待期间取消其行为。参数为保存着setTimeout函数的返回值的变量。

之前的函数我们可以改为:

```js
function positionMessage(){
	if(!document.getElementById || !document.getElementById("message")){
		return false;
	}
	var elem=document.getElementById("message");
	elem.style.position="absolute";
	elem.style.left="50px";
	elem.style.top="100px";
	movement=setTimeout("moveMessage()", 5000);
}
addLoadEvent(positionMessage);
```

setTimeout已经被执行，movement只是保存着这个函数返回值。而这时如果我执行`clearTimeout(movement);`就可以取消这个行为。

并且，**movement我没有加var，因此他是全局变量**。我可以随时在外部停止他。

#### 10.1.3 时间递增量

1.获得元素的当前位置

```js
	var elem=document.getElementById("message");
	var xpos=parseInt(elem.style.left);
	var ypos=parseInt(elem.style.top);
```

2.如果已经到达目的地，则退出

```js
	if(xpos==200 && ypos==100){
		return true;
	}
```

3.如果尚未到达，则再移近一点

```js
else{
		if(xpos<200){
			xpos++;
		}
		else if(xpos>200){
			xpos--;
		}
		if(ypos<100){
			ypos++;
		}
		else if(ypos>100){
			ypos--;
		}
	}
	elem.style.left=xpos+"px";//注意这里
	elem.style.top=ypos+"px";
```

4.经过一段间隔后重复上述步骤

```js
movement=setTimeout("moveMessage()",10);
```

#### 10.1.4 抽象

首先把很明显能发现的元素id，目的地等抽象化：

```js
if(!document.getElementById || !document.getElementById(elementID)){
		return false;
	}
	var elem=document.getElementById(elementID);
	var xpos=parseInt(elem.style.left);
	var ypos=parseInt(elem.style.top);
	if(xpos==final_x && ypos==final_y){
		return true;
	}
	else{
		if(xpos<final_x){
			xpos++;
		}
		else if(xpos>final_x){
			xpos--;
		}
		if(ypos<final_y){
			ypos++;
		}
		else if(ypos>final_y){
			ypos--;
		}
	}
	elem.style.left=xpos+"px";
	elem.style.top=ypos+"px";
```

但是接下来出现了问题：使用setTimeout函数要重新写函数名，这么多参数要怎么办？

首先明确，elementID是字符串，要多出一个引号，因此写法如下：

```js
	var repeat="moveElement('"+elementID+"',"+final_x+","+final_y+","+interval+")";
	movement=setTimeout(repeat,interval);
```

最终函数为；

```js
function moveElement(elementID,final_x,final_y,interval){
	if(!document.getElementById || !document.getElementById(elementID)){
		return false;
	}
	var elem=document.getElementById(elementID);
	var xpos=parseInt(elem.style.left);
	var ypos=parseInt(elem.style.top);
	if(xpos==final_x && ypos==final_y){
		return true;
	}
	else{
		if(xpos<final_x){
			xpos++;
		}
		else if(xpos>final_x){
			xpos--;
		}
		if(ypos<final_y){
			ypos++;
		}
		else if(ypos>final_y){
			ypos--;
		}
	}
	elem.style.left=xpos+"px";
	elem.style.top=ypos+"px";
	var repeat="moveElement('"+elementID+"',"+final_x+","+final_y+","+interval+")";
	movement=setTimeout(repeat,interval);
}
```

### 10.2 实用的动画

#### 10.2.1 提出问题

我们希望有一个网页的三个链接，当我们鼠标在链接上时，我们能看见他们的缩略图

#### 10.2.4 JavaScript

我们可以用一个包含四个缩略图的长图，当在某个链接上时使长图移动，并配合overflow属性，只显示出一个缩略图，达成滚动图效果。





---

## 后记-本书中的一些注意事项

1.addLoadEvent.js

在html中的script宣言里，必须放在其他js文件之前。不然浏览器会报错。
