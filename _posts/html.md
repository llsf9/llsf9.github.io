***“标签存在的意义不仅是他们呈现出来的样式，而是让浏览器更好的阅读”***

[TOC]

## 共通标签

### HTML骨架

```
<html>
    <head>...</head>
    <body>...</body>
</html>
```
1. \<html\>\</html\>称为根标签，所有的网页标签都在\<html\>\</html\>中。
2. \<head\> 标签用于定义文档的头部，它是所有头部元素的容器。头部元素有\<title\>、\<script\>、\<style\>、\<link\>、 \<meta\>等标签，头部标签在下一小节中会有详细介绍。
3. 在\<body\>和\</body>标签之间的内容是网页的主要内容，如\<h1>、\<p>、\<a>、\<img>等网页内容标签，在这里的标签中的内容会在浏览器中显示出来。
---
### 列表
- ul...li
  **无序列表**。
  
  <u>ul元素中不能放除li的其他标签。但li元素里可以放其他标签</u>



- ol...li
  **有序列表**。默认从1开始。



- dl...dt...dd

  自定义列表

  ```html
  <dl>
  	<dt>概念</dt>
  	<dd>定义1</dd>
    <dd>定义2</dd>
  </dl>
  ```

  网页底部的帮助中心，服务支持列表多为自定义列表

---
### 逻辑板块
- div
  划分独立的逻辑板块。
- span
---
### 表格
 ```html
<table>
 <caption>标题</caption>
 
 <thead>
 	<tr>                      //分割每列
  	<th>表头</th>           //表头默认居中粗体
  </tr>
 </thead>
 
 <tbody>
  <tr>
   <td>表格</td>
  </tr>
 </tbody>
 
</table>
 ```
tr里只能有td或th标签，但td和th里可以放其他标签

 html属性表格默认无表格线。可通过css添加。

属性  
 - summary：table属性。表格摘要。语义化属性。
 - border：设置边框宽度。默认为0
 - cellspacing:设置单元格与单元格边框之间的空白间距。默认为2。
 - cellpadding：单元格内容和单元格边框之间的空白边距。默认为1。
 - width
 - height
 - align：表格在网页中的水平对齐方式
合并属性

- rowspan：跨行合并。参数为共有几格合并一起。
- colspan：跨列合并。参数为共有几格合并一起。

---
### 超链接 \<a>
1. 属性
  - href：链接地址。
  - title:此超链接事件的目的。语义化属性。   
  - target:链接打开方式。默认直接在本窗口打开（self）。
      1.  _blank：打开新窗口。
     2. view_frame:在制定框架打开。
     3.  self:本窗口打开

> ##### href自动打开默认邮箱的方法 
> [![8ikETJ.png](https://s2.ax1x.com/2020/03/10/8ikETJ.png)](https://imgchr.com/i/8ikETJ)
> 1.如果mailto后面同时有多个参数的话，第一个参数必须以“?”开头，后面的参数每一个都以“&”分隔。
> 2.仔细观察可发现，只有mailto后面是加冒号，其余均是等号。
2. 锚点定位

实现点击链接后快速跳转到本页面的某内容

```html
<a href="#id">内部跳转链接</a>
......
<p id="id">想要跳转到的内容</p>


---
### base标签\<base />

设置整体链接的默认行为。必须在head元素中。

​```html
<head>
	<base target="_blank" />
  <!--所有链接默认新窗口打开-->
</head>
```

属性

- href：规定所有链接的默认链接
- target：规定所有链接默认打开方式

---

### 图片 \<img />

属性

- 单标签

- src：图片链接。
- alt：指定图像的描述性文本，当图像不可见时（下载不成功时），可看到该属性指定的文本。
- title：提供在图像可见时对图像的描述(鼠标滑过图片时显示的文本)。
- border：边框
---
### 表单域<form>
把浏览者输入的数据传送到服务器端*
属性 
 - action ：浏览者输入的数据被传送到的地方,比如一个PHP页面(save.php)。
  - method ： 数据传送的方式（get/post）。
      - get:快速但不安全。会显示在地址栏
      - post：速度慢但较安全
注意
    所有表单控件（文本框、文本域、按钮、单选框、复选框等）都必须放在 \<form>\</form> 标签之间（否则用户输入的信息提交不到服务器上）

---

### 表单控件
- \<input />
  属性
  
  - type：text（文本输入框），button（提交按钮），password（密码输入框），checkbox（复选框），更多点击[type属性](https://www.w3cschool.cn/htmltags/att-input-type.html)。
  
  - name:为文本框/选择框命名，以对同类的单选框/复选框分组。以备后台程序使用。
  
  - value：1.为文本输入框/按钮设置默认文字。2.为选择框提交数据到服务器的值。
  
  - checked:选择框使用。当设置 checked="checked" 时，该选项被默认选中。
  
  - size：控件宽度
  
  - maxlength:规定输入最多字符数 
  
  - reset；重置该表单的所有内容 
  
    
  
    <u>同类单选框的name要用一样的才能起到效果</u>



-  \<textarea>
属性
  - cols ：多行输入域的列数。
  - rows ：多行输入域的行数。
  *这两个属性可用css样式的width和height来代替*



- \<label>
  \<label> 标签为 input 元素定义标注。如果您在 label 元素内点击文本，就会触发此控件。
  
  
  
  属性
  
  - for:规定 label 与哪个表单元素绑定(需绑定id）。
  
    方法1:直接包裹input
  
  ```html
  <label>
    输入账号：
    <input type="text" />
  </label>
  ```
  
  				方法2:for固定
  
  ```html
  <label for="two">
    输入账号：
    <input type="text" />
    输入密码：
    <input type="text" id ="two"/>
  </label>
  ```
  
  
  
- 下拉菜单\<select>
  ```html
  <select>
    <option>显示文字</option>
    <option>显示文字</option>
  </select>
  ```
  属性
  - value：option属性。向服务器发送值。  

  - selected：option属性。设置selected="selected"属性，则该选项就被默认选中。

  - multiple：select属性。设置multiple="multiple"时，可以多选。

    

---

### 文字类
- p（段落标签）
  段落。段落之间会有空白。可用css改变。
- hx（标题标签）
  共有六个等级。h1一般用于网页总标题。



- em
  表示强调。默认为斜体。
  
- i
  
  倾斜字体
  
  <u>推荐使用em，有强调的语义</u>



- strong
  表示更加强调。默认为粗体。
  
- b
  
  加粗。
  
  <u>推荐使用strong，有强调的语义</u>



- del

  表示强调。默认为删除线。

- s

  删除线

  <u>推荐使用del，有强调的语义</u>



- ins

  表示强调。默认为下划线。

- u

  下划线

  <u>推荐使用ins，有强调的语义</u>



- span  
  无语义。为了设置css样式而存在。（比如既想设一个单独的style又不想让浏览器将它阅读为段落，强调等意思时。）
- q
  引用。浏览器会为其自动加上双引号。
- blockquote
  长段引用。无引号。前后缩进。
- address
  地址信息。也可以定义一个地址（比如电子邮件地址）、签名或者文档的作者身份。默认换行和斜体。
- code
  一行代码。
- pre
  保留源代码的空格和换行符。常见应用于长段代码。

---
### 文字分割类
- br（换行标签）
单标签。换行。
- `&nbsp;`
  空格
- hr（水平线标签）
  单标签。分割线/水平线

---

### 特殊字符标签

![89ijFx.png](https://s2.ax1x.com/2020/03/09/89ijFx.png)

---

## HTML5新增标签

### 1.常用新增标签

逻辑类

- header：页面头部
- footer：页面底部
- nav：导航栏
- article：文章
- section：区域
- aside：侧边栏

表单类

- datalist:定义选项列表，与input搭配

  ```html
  <input type="text" list="data">
  <datalist id="data">
    <option>刘德华</option>
    <option>刘若英</option>
    <option>郭富城</option>
  </datalist>
  ```

  datalist不仅具有select下拉菜单的特性（点击下拉按钮会出现列表），还能实现输入字符时有提示列表（类似搜索引擎的那种列表）。在这个代码中，若我输入刘，就会出来刘德华和刘若英。

- fieldest:将表单内容包裹起来

  ```html
  	<fieldset>
  		<legend>用户登录</legend>
  		<p>用户名:<input type="text" name=""></p>
  		<p>密&nbsp;&nbsp;&nbsp;码:<input type="password" name=""></p>
  	</fieldset>
  ```

  [![8PhMse.png](https://s2.ax1x.com/2020/03/10/8PhMse.png)](https://imgchr.com/i/8PhMse)

  > legend：为fieldest元素定义标题

### 2.input type新增属性值

- email:定义输入邮箱格式。若无@提交时会提醒
- tel：定义输入手机格式。手机端会弹出数字键盘。
- number：定义输入数字格式。只能输入数字。
- url：定义输入网址格式。如果不是网址提交时会提醒。
- search：搜索框。输入框后面有一键删除的小叉号。
- range：滑块控件。
- time:时间输入框。
- date：日期输入框。
- month：年月输入框。
- week：年周输入框。
- color：颜色提取框。

### 3.input新增属性

- placeholder：占位符。可用来定义输入框内的自带文字，但不影响输入。（与value对比）
- autofocus：自动聚焦。用户进入该页面光标自动聚焦该表单控件。
- multiple：支持上传多文件。
- autocomplete:自动完成已记录内容（提交过一次的）。但是1.必须要有提交按钮2.此表单控件的name值不得为空。
- requierd：必填项。聚焦一次后仍为空的话会有提醒。
- accesskey：规定快捷键。采用alt+字母的格式。如access=“s”，则快捷键为alt+s。

### 4.多媒体标签

- embed：网络视频导入常用方法

- audio：

  属性：

  - autoplay：自动播放
  - controls：是否显示控件
  - loop：定义循环播放几次。无限时等于-1
  - src:路径

- source:提供不同路径的文件，使浏览器选择可以播放的音频/视频文件。与audio/video搭配使用。

  ```html
  <audio controls>
     <source src="horse.ogg" type="audio/ogg">
     <source src="horse.mp3" type="audio/mpeg">
   Your browser does not support the audio element.
  </audio> 
  ```

- video:本地视频播放。支持格式：oog,mp4,webm

  属性：

  - autoplay：自动播放
  - controls：是否显示控件
  - loop：定义循环播放几次。无限时等于-1
  - src:路径
  - width:宽度