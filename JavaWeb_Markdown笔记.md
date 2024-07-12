# HTML

- 基本概念

1. HTML决定网页内容
2. CSS网页的排版和样式

## B/S软件的结构

- 基本概念

1. C/S(Client Server)
2. B/S(Broswer Server)

![BS结构](.\JavaWeb_Markdown笔记图片\BS结构.png)

3. 客户端：浏览器 
4. 服务器端：WEB服务器

## 前端开发流程

![前端开发流程](.\JavaWeb_Markdown笔记图片\前端开发流程.png)

## 网页的组成部分

- 网页的组成部分：三部分组成：
  1. 内容 (结构)
  2. 表现(显示效果)
  3. 行为。

## HTML

- 基本概念

1. Hyper Text Markup Language (超文本标记语言)，简称HTML
2. HTML 通过标签来标记要显示的网页中的各个部分。网页文件本身是一种文本文件，通过在文本文件中添加标记符，可以告诉浏览器如何显示其中的内容(如:文字如何处理，画面如何安排，图片如何显示等)

- 创建HTML文件

1. Idea创建HTML
2. 设置默认浏览器
3. 编写内容

- HTML文件的书写规范

```html
<html> <!-- 表示整个html页面的开始 -->
    <head>
        <title> 标题 </title>
    </head>
    <body> 页面主体内容 </body>
</html> <!-- 表示整个html页面的结束 -->

<!-- html的注释 -->
```

```html
<!--演示-->
<!DOCTYPE html> <!-- 声明 -->
<html lang="en"> <!-- html标签表示html的开始 lang="en"英文 lang="zh_CN"中文-->
<!-- html标签一般包含两个部分 head 和 body-->
<head> <!-- head 一般包含三部分：title标签 css样式 js代码-->
  <meta charset="UTF-8">
  <title>标题</title><!--标题-->
</head>
<body><!--html的主题内容-->
hello
</body>
</html>

```

- HTML标签的基本介绍

1. 标签的基本格式

```html
<标签名> 封装的数据 </标签名>
```

2. 标签名大小写不敏感，不区分大小写

3. 标签拥有自己的属性

   - 基本属性：可以修改简单的样式

     ```html
     <body bgcolor="aqua"><!-- bgcolor 设置背景颜色-->
     hello
     </body>
     ```

   - 事件属性：设置事件响应后的代码

     ```html
     <body bgcolor="aqua"  onclick="alert('你好！')">
     hello
     </body>
     ```

4. 标签的分类

   - 双标签

     ```html
     <p> </p> <!--前面为开始标签 后面为结束标签-->
     ```

   - 单标签

     ```html
     <br/> <!--单标签 自结束标签-->
     <img src="1.jpg" />
     <br/> <!--html的换行-->
     <hr/> <!--html的水平线-->
     ```

- 标签语法

1. 标签不能相互嵌套

```html
正确:
<div><span>早安</span></div>
错误:
<div><span>早安</div></span>
```

2. 标签必须闭合

```html
<!--双标签必须有结束标签-->
正确:<div>早安，尚硅谷</div>
错误:<div>早安，尚硅谷
<!--单标签：没有文本内容的标签-->
正确:<br />
错误:<br>
```

3. 属性必须有值(不能没有值)，属性值必须加引号

```html
<button onclick="alert('你好！')"> 按钮 </button>>
```

4. 注释不能嵌套

```html 
正确:<!--双标签必须有结束标签-->
错误:<!--注释<!--内容-->-->
```

## HTML常用标签

- 不认识的标签：查找标签手册

[HTML 标签列表（功能排序） | 菜鸟教程 (runoob.com)](https://www.runoob.com/tags/ref-byfunc.html)

- font字体标签

```html
<body>
<font color="blue" face="宋体" size="7">
字体标签
    <!--
颜色、字体、大小

-->
</font>
</body>
```

- 特殊字符(字符实体)

```html
< 对应 &lt;
> 对应 &gt;  
html中多个空格只保留一个
空格的特殊字符 对应 &nbsp;
```

- 标题标签

1. 标题只有h1到h6，h1最大，h6最小
2. 对齐方式align：左对齐 居中 右对齐

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>标题标签</title>
</head>
<body>
  <h1 align="left">标题1</h1>
  <h2 align="center">标题2</h2>
  <h3 align="right">标题3</h3>
  <h4>标题4</h4>
  <h5>标题5</h5>
  <h6>标题6</h6>
  <h7>标题7</h7>
</body>
</html>
```

- **超链接**(Hypertext Reference 重点)：点击可以跳转的内容

```html
<!-- a 标签是 超链接
        href 设置连接地址
        target 设置跳转目标
          _self 当前页面
          _blank 打开新的页面
-->
<a href="https://www.baidu.com">百度</a>
<a href="https://www.google.com" target="_self">谷歌1</a>
<a href="https://www.google.com" target="_blank">谷歌2</a>
```

- 列表标签

1. 无序列表
2. 有序列表
3. 定义列表

```html
<ul> <!--unordered lis
type 可以修改符号的样式 -- 跟浏览器也有关系
t-->
  <li>奥特曼1</li> <!-- list item-->
  <li>奥特曼2</li> <!-- list item-->
  <li>奥特曼3</li> <!-- list item-->
  <li>奥特曼4</li> <!-- list item-->
</ul>

<ol> <!--uordered list-->
  <li>奥特曼1</li> <!-- list item-->
  <li>奥特曼2</li> <!-- list item-->
  <li>奥特曼3</li> <!-- list item-->
  <li>奥特曼4</li> <!-- list item-->
</ol>
```

- img标签：在html页面上显示图片

```html
<body>
<!--
width属性设量图片的宽度
height同性设复图片的高度
border周性设量图片边梅大小
alt属性设量当指定路径找不到图片时,用来代誉显示的文本内容

src属性设置图片路径(相对路径/绝对路径)
JavaSE中：
  相对路径：从工程名开始
  绝对路径：从磁盘开始
Web中：
  相对路径：
    . 当前文件的目录
    .. 当前文件的上级目录
    文件名：当前文件的所在目录的文件 相当于 ./文件名
  绝对路径：http://ip:port/工程名/资源路径
-->
  <img src="icon.png" width="192" height="192" border="1"/>
  <img src="xxx.png" width="192" height="192" alt="图片丢失" />
  <img src="icon.png" width="192" height="192"/>
  <img src="icon.png" width="192" height="192"/>
</body>
```

- 表格标签

```html
<!--
table 标签是表格标签
  border 设置表格标签
  width 设置表格宽度
  height 设置表格高度
  align 设置表格对齐方式
  cellspacing 单元格间距
tr是行标签
th是表头标签
td是单元格标签
  align 设置单元格文本对齐方式
b 是加粗标签
-->
<table align="center" border="1" width="300" height="300" cellspacing="20">
  <tr>
    <td align="center"><b>1.1</b></td>
    <th>1.2</th> <!-- <th>现成的表头标签 -->
    <td>1.3</td>
  </tr>
  <tr>
    <td>2.1</td>
    <td>2.2</td>
    <td>2.3</td>
  </tr>
  <tr>
    <td>3.1</td>
    <td>3.2</td>
    <td>3.3</td>
  </tr>
</table>
```

- 表格的跨行跨列

```htm
<!--
colspan 属性设置跨列(占的单元格宽度)
rowspan 属性设置跨行
-->
<table align="center" border="1" width="300" height="300" cellspacing="0">
  <tr>
    <td align="center" colspan="2"><b>1.1</b></td> <!--跨单元格 删除所占单元格 -->
    <td>1.3</td>
    <td>1.4</td>
    <td>1.5</td>
  </tr>
  <tr>
    <td rowspan="2">2.1</td>
    <td>2.2</td>
    <td>2.3</td>
    <td>2.4</td>
    <td>2.5</td>
  </tr>
  <tr>
    <td>3.2</td>
    <td>3.3</td>
    <td>3.4</td>
    <td>3.5</td>
  </tr>
  <tr>
    <td>4.1</td>
    <td>4.2</td>
    <td>4.3</td>
    <td>4.4</td>
    <td>4.5</td>
  </tr>
  <tr>
    <td>5.1</td>
    <td>5.2</td>
    <td>5.3</td>
    <td>5.4</td>
    <td>5.5</td>
  </tr>
</table>
```

- 了解iframe框架标签

```html
<body>
<!--
iframe 在页面开辟一个独立的区域
iframe和a标签组合使用的步要:
  1 在iframe标签中使用name属住定义一个名称
  2 在a标签的target属性上设置iframe的name的属性值
-->
单独的页面<br />
<iframe src="img标签.html" width="500" height="500" name="abc"></iframe>
<br />
<ul>
  <li> <a href="无序列表.html" target="abc"> 语法</a></li>
</ul>
</body>
```

- **表单**(重点)

表单就是html页面中，用来收集用户信息的所有元素集合然后把这些信息发送给服务器。

```html
<body>
<!--
form标签就是表单
  input type=text 是文文本输入框 value设置默认显示内容
  input type mpassword 是密码输入框 value设置默认显示内容
  input type="radio" 是单选框 name属性可以对其进行分组
  input typemcheckbox 是复选框 checked-"checked"表示默认选中
  input type=reset 是重置按钮 value属性修改按钮上的文本
  input type=submit 是提交按钮 value属性修改按钮上的文本
  input type=button 是按钮 value属性修改按钮上的文本
  input type=file 是文件上传
  input type=hidder 是隐藏域 当我们要发送某些信息，而这些信息不需要用户参与就可以使用隐藏域 (提交 的时候同时发送给服务器)
elect 标签是下拉列表框
  option 标签是下拉列表框中的选项 selected="selected"设置默认选中
textarea 表示多行文本输入框
  rows 属性设置可以显示几行的高度
  cols 属性设置每行可以显示几个字符宽度
  起始标签和结束标签的中间 是默认值
-->
<form>
  用户名：<input type="text" value="默认值" /><br/>
  用户密码：<input type="password" /><br/>
  确认密码：<input type="password" /><br/>
  性别：<input type="radio" name="sex" checked="checked"/>男 <input type="radio" name="sex" />女<br/>
  兴趣爱好：<input type="checkbox" checked="checked"/>Java <input type="checkbox" />C++ <input type="checkbox" />Python<br/>
  国籍：<select>
  <option>-</option>
  <option selected="selected">中国</option>
  <option>美国</option>
  <option>小日本</option>
</select> <br/>
  自我评价：<textarea rows="10" cols="140">默认值</textarea><br/>
  <input type="reset" value="重置" />
  <input type="submit" value="提交" />
  <input type="button" value="我是按钮" />
  <input type="file" value="提交文件" />
</form>
</body>
```

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>表单显示</title>
</head>
<body>
<!--
form标签就是表单
  input type=text 是文文本输入框 value设置默认显示内容
  input type mpassword 是密码输入框 value设置默认显示内容
  input type="radio" 是单选框 name属性可以对其进行分组
  input typemcheckbox 是复选框 checked-"checked"表示默认选中
  input type=reset 是重置按钮 value属性修改按钮上的文本
  input type=submit 是提交按钮 value属性修改按钮上的文本
  input type=button 是按钮 value属性修改按钮上的文本
  input type=file 是文件上传
  input type=hidder 是隐藏域 当我们要发送某些信息，而这些信息不需要用户参与就可以使用隐藏域 (提交 的时候同时发送给服务器)

elect 标签是下拉列表框
  option 标签是下拉列表框中的选项 selected="selected"设置默认选中
textarea 表示多行文本输入框
  rows 属性设置可以显示几行的高度
  cols 属性设置每行可以显示几个字符宽度
  起始标签和结束标签的中间 是默认值
-->
<!--
form标签是表单标签
  action届性设置提交的服务器地址
  method届性设置提交的方式GET(默认值)或POST
提交后到达的域名：https://www.baidu.com/?action=login&sex=on
https://www.baidu.com/  服务器地址
? 分隔符
action=login&sex=on 请求参数
-->
<form action="https://www.baidu.com" method="get">
  <input type="hidden" name="action" value="login" />
  <h1 align="center">用户注册</h1>
  <table>
    <tr>
      <td>用户名称：</td>
      <td><input type="text" name=username" value="默认值" /><br/>
      </td>
    </tr>
    <tr>
      <td>用户密码：</td>
      <td><input name="pwd" type="password" /><br/>
      </td>
    </tr>
    <tr>
      <td>确认密码：</td>
      <td><input name="rpwd" type="password" /><br/>
      </td>
    </tr>
    <tr>
      <td> 性别：</td>
      <td>
        <input type="radio" value="boy" name="sex" checked="checked"/>男
        <input type="radio" value="girl" name="sex" />女
      </td>
    </tr>
    <tr>
      <td>兴趣爱好：</td>
      <td>
        <input name="hobby" type="checkbox" value="Java" checked="checked"/>Java
        <input name="hobby" type="checkbox" value="Cpp"/>C++
        <input name="hobby" type="checkbox" value="Python"/>Python<br/>
      </td>
    </tr>
    <tr>
      <td>国籍：</td>
      <td>
        <select name="country">
          <option value="null">-</option>
          <option value="China" selected="selected">中国</option>
          <option value="USA">美国</option>
          <option value="JP">小日本</option>
        </select> <br/>
      </td>
    </tr>
    <tr>
      <td>自我评价：</td>
      <td>
        <textarea name="desc" rows="10" cols="30">默认值</textarea><br/>
      </td>
    </tr>
    <tr>
      <td><input type="reset" value="重置" /></td>
      <td>
        <input type="submit" value="提交" />
      </td>
      <td>
        <input type="button" value="我是按钮" />
      </td>
      <td>
        <input type="file" value="提交文件" />
      </td>
    </tr>
  </table>
</form>

</body>
</html>
```

- 表单提交的细节

1. < from >标签

```html
<--!
form标签是表单标签
  action届性设置提交的服务器地址
  method届性设置提交的方式GET(默认值)或POST
提交后到达的域名：https://www.baidu.com/?action=login&sex=on
https://www.baidu.com/  服务器地址
? 分隔符
action=login&sex=on 请求参数
-->
<form action="https://www.baidu.com" method="get">
  <input type="hidden" name="action" value="login" />
```

2. 表单提交的时候，数据没有发送给服务器的三种情况:
   - 表单项没有name属性值
   - 单选、复选(下拉列表中的option标签)都需要添加value属性，发送给服务器
   - 表单项不在提交的form标签中
3. Get请求的特点
   - 1.浏览器地址栏中的地址是: action属性[+?+请求参数]
   - 请求参数的格式是: key=value&key=value
   - 2.不安全
   - 3.它有数据长度的限制：超过100建议使用"post"，不同浏览器不同
4. Post请求的特点
   - 浏览器地址栏中只有action属性值
   - 相对于GET请求要安全
   - 理论上没有数据长度的限制

- 其他标签

div、span、p 标签的演示

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>其他标签</title>
</head>
<body>
<!--
div标签 默认独占一行
span标签 它的长度是封装数据的长度
p段落标签 默认会在段落的上方或下方各空出一行来 (如果已有就不再空)
-->
<div>标签</div>
<span>span标签</span>
<p>p标签</p>
</body>
</html>
```

# CSS

- 基本介绍

CSS 是[层叠样式表单]。是用于(增强)控制网页样式并允许将样式信息与网页内容分离的一种**标记性语言**。

## 基本语法

- 语法规则

1. 选择器: 浏览器根据“选择器”决定受 CSS 样式影响的 HTML 元素(标签)
2. 属性 (property)是你要改变的样式名，并且每个属性都有一个值。属性和值被冒号分开，并由花括号包围，这样就组成了一个完整的样式声明(declaration)，例如: pcolor: blue)
3. 多个声明:如果要定义不止一个声明，则需要用分号将每个声明分开。虽然最后一条声明的最后可以不加分号(但尽量在每条声明的末尾都加上分号)

```css
p{
    color: red;
    font-size:30px;
}
```

4. 注释：Java的多行注释

![CSS语法规则](.\JavaWeb_Markdown笔记图片\CSS语法规则.png)

- CSS和HTML的结合使用方式

1. 基本用法

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title> </title>
</head>
<body>
<div style="border: 3px solid #2067a1; ">标签</div>
<span style="border: 3px solid #2067a1; ">span标签</span>
<p style="border: 3px solid #2067a1; ">p标签</p>
</body>
</html>

<!---
缺点：
1.样式多->代码量大
2.可读性差
3.复用性差
->
```

2. 第二种方法：在 head标签中，使用style标签来定义各种自己需要的 css 样式。

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>02</title>
<!--  style代码专门用来定义css代码-->
  <style type="text/css">
    /*
    css的注释
    */
    div {
      border: 1px solid red;
    }
    span {
      border: 1px solid red;
    }
  </style>
</head>
<body>
<div>标签</div>
<span>span标签</span>
<p>p标签</p>
</body>
</html>
<!--
缺点：
1.不适合多个页面的复用
2.修改维护比较麻烦
-->
```

3. 第三种：把css样式写成一个单独的 css文件，再通过 link标签引入即可复用。

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>css03</title>
<!--link标签用于引入css标签-->
  <LINK REL="stylesheet" type="text/css" href="CSS01TEST.css">
</head>
<body>
  <div>标签</div>
  <span>span标签</span>
  <p>p标签</p>
</body>
</html>
```

```css
div {
  border: 1px solid red;
}
span {
  border: 1px solid red;
}
```

- 标签名选择器

1. 基本格式

```css
标签名 {
    属性：值
}
标签名选择器：可以决定哪些标签被动的使用这个样式。
```

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>标签名选择器</title>
  <style type="text/css">
    div{
      border: 1px solid yellow;
      color: blue;
      font-size: 30px;
    }
    span{
      border: 3px dashed blue;
      color: red;
      font-size: 20px;
    }
  </style>
</head>
<body>
  <div>标签</div>
  <span>span标签</span>
  <p>p标签</p>
</body>
</html>
```

- id选择器

1. 基本格式

```html
#id 属性值{
	属性: 值;
}
```

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>ID选择器</title>
  <style>
    /* 必须有id开头 */
    #id01 {
      color: red;
      font-size: 20px;
      border: 2px yellow solid;
    }
    #id002{
      color: #2067a1;
      font-size: 15px;
      border: 3px #b3d4fc dotted;
    }
  </style>
</head>
<body>
  <div id="id01">标签</div>
  <div id="id002">标签</div>
</body>
</html>
```

- class选择器

1. 基本语法

```html
class 属性值{
	属性: 值;
}
```

2. class类型选择器，可以通过 class 属性有效的选择性地去使用这个样式。

```htm
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>class选择器</title>
  <style type="text/css">
    .class01{
      color: #b3d4fc;
      font-size: 30px;
      border: 2px solid yellow;
    }
    .class02{
      color: gray;
      font-size: 29px;
      border: red;
    }
  </style>
</head>
<body>
  <div class="class01">标签</div>
  <div class="class02">标签</div>
</body>
</html>
```

- 组合选择器

1. 基本语法

```html
选择器 1, 选择器 2, 选择器n {
	属性: 值;
}
```

2. 组合选择器可以让多个选择器共用同一个 cs5样式代码。

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>组合选择器</title>
  <style type="text/css">
    .class01, #id01 {
      color: #b3d4fc;
      font-size: 20px;
      border: #222222 1px solid;
    }
  </style>
</head>
<body>
<div class="class01">标签1</div>
<div id="id01">标签2</div>
</body>
</html>
```

- 常用样式

1. 颜色
2. 边框：高度、宽度
3. 背景颜色
4. 字体样式
5. div居中：边框相对于网页居中
6. 文本居中
7. 超链接去下划线
8. 表格细线
9. 有序列表去除修饰

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>css常用样式</title>
  <style>
    div{
      color: #b3d4fc;
      border: 2px red solid;
      width: 200px;
      height: 300px;
      background-color: aquamarine;
      font-size: 20px;
      margin-left: auto;
      margin-right: auto;
      text-align: center;
    }
    a{
      text-decoration: none;
    }
    table{
      border: #222222 2px solid;
      border-collapse: collapse;/* 合并边框 */

    }
    td{
      border: moccasin 2px solid;
    }
    ul{
      list-style: none;
    }
  </style>
</head>
<body>
  <ul>
    <li>111</li>
    <li>222</li>
    <li>333</li>
  </ul>
  <table>
    <tr>
      <td>1.1</td>
      <td>1.2</td>
    </tr>
  </table>
  <a href="https://www.baidu.com">百度</a>
  <div>这是一个标签</div>
</body>
</html>
```

# JavaScript

- 基本结束

1. Javascript 语言诞生主要是完成页面的数据验证。因此它运行在客户端，需要运行浏览器来解析执行 JavaScript代码。
2. JavaScript的特点：
   - 交互性(它可以做的就是信息的动态交互)
   - 安全性(不允许直接访问本地硬盘)
   - 跨平台性(只要是可以解释 Js 的浏览器都可以执行，和平台无关)

- JavaScript 和 html代码的结合方式

1. 第一种：只需要在 head 标签中，或者在 body 标签中，使用script 标签来书写 JavaScript 代码

```html
<!--第一种使用方式-->
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
  <script type="text/javascript">
    // alert是JavaScript语言提供的一个警告框函数
    // 它可以接收任意类型的参数，这个参数就是警告框的提示信息
    alert("hello");
  </script>
</head>
<body>
</body>
</html>
```

2. 第二种：使用 script 标签入 单独的JavaScript 代码文件

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
<!--  src路径引入外部的js文件(相对路径/绝对路径)
注意：script标签可以用来定义js代码，也可以用来引入js文件
  但是，一个标签两个功能二选一使用。不能同时使用两个功能
-->
  <script type="text/javascript" src="1.js">
  alert("你好");
  </script>
  <script type="text/javascript">
    alert("你好");
  </script>
</head>
<body>
</body>
</html>
```

## 变量

- 基本概念

变量是可以存放某些值的内存的命名。

- JS的变量类型

1. 数值类型: number  -> int short long float double
2. 字符串类型:string
3. 对象类型:object
4. 布尔类型:boolean
5. 函数类型:function

- JS的特殊值

1. undefined 未定义，所有js 变量未赋于初始值的时候，默认值都是undefined.
2. null 空
3. NAN 全称：nut a number。非数字，非数值。

- JS顶一把变量的格式

```javascript
var 变量名;
var 变量名 = 值;
```

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
  <script type="text/javascript">
    var i;
    alert(i);
    i = 12;
    alert(i);
    alert(typeof (i));
    i = "abc"
    alert(i);
    alert(typeof (i))
    var b = 12;
    alert(i * b); // 非数值
  </script>
</head>
<body>
</body>
</html>
```

- 关系(比较)运算符

1. 常见的关系运算符与Java一致
2. 等于 == ：只比较字面值
3. 全等于 === ：除了做字面值的比较之外，还会比较两个变量的数据类型

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
  <script type="text/javascript">
    var a = "12";
    var b = 12;
    alert(a == b);
    alert(a === b);
  </script>
</head>
<body>
</body>
</html>
```

- 逻辑运算符

1. 基本的逻辑运算符与Java一致
2. 且运算: && 两种情况
   - 第一种:当表达式全为真的时候。返回最后一个表达式的值。
   - 第二种:当表达式中，有一个为假的时候。返回第一个为假的表达式的值
3. 或运算: || 两种情况
   - 第一种情况:当表达式全为假时，返回最后一个表达式的值
   - 第二种情况:只要有一个表达式为真。就会把回第一个为真的表达式的值
4. 取反运算: ！
5. 在 JavaScript 语言中，所有的变量，都可以做为一个 boolean 类型的量去使用。
   - 0 、null、 undefined、""(空串) 都认为是 false;
6. 并且 && 与运算和||或运算有短路。
   短路就是说，当这个&&或||运算有结果了之后 。后面的表达式不再执行。

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
  <script type="text/javascript" >
    // var a = 0;
    // var a = null;
    // var a = undefined;
    var a = "";
    if (a) {
      alert("0为真");
    } else {
      alert("0为假");
    }
  </script>
</head>
<body>

</body>
</html>
```

## **数组**(重点)

- JS定义方式

```javascript
var 数组名 = []; // 空数组
var 数组名 = [1, "abc", true];
```

1. 数组的大小可以动态变化

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
  <script type="text/javascript">
    var arr = [];
    alert(arr.length);
    arr[0] = 12;
    alert(arr.length);
    // JavaScript语言中的数组，只要我们通过数组下标赋值，那么最大的下标值，就会自动的给数组做扩容操作。
    arr[2] = "abc";
    alert(arr.length);
    alert(arr[1]); // 未赋值就是未定义
    for (var i = 0; i < arr.length; i++) {
      alert(arr[i]);
    }
  </script>
</head>
<body>

</body>
</html>
```

## 函数(重点)

- 两种定义方式

1. 第一种，可以使用 function 关键字来定义函数。
   - 若有返回值：只需要在函数体内直接使用 return 语句返回值即可

```javascript
function 函数名(形参列表) {
    函数体;
}
```

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
  <script type="text/javascript" >
    function fun() {
      alert("无参函数");
    }
    fun();
    function fun2(a, b) {
      alert("有参函数fun2() a=" + a + "b=" + b);
    }
    fun2(123, "abc");
    // 定义带有返回值的函数
    function sum(a, b) {
      return a+b;
    }
    alert(sum(5, 100));
  </script>
</head>
<body>

</body>
</html>
```

2. 第二种定义方式

```html
<script type="text/javascript">
    var fun = function () {
      alert("无参函数")
    }
    var fun2 = function (a, b) {
      alert("有参函数fun2() a=" + a + "b=" + b);
    }
    var sum = function (a, b) {
      return a+b;
    }
    fun();
    fun2(12, 'ab');
    alert(12, 17);
  </script>
```

3. 注意：在 Java 中团数允许重载，JS不允许重载。但是在 Js 中数的重会直接覆盖掉上一次的定义。

```html
  <script type="text/javascript">
    var fun = function () {
      alert("无参函数")
    }
    var fun = function (a, b) {
      alert("有参函数fun2() a=" + a + "b=" + b);
    }
    fun(); // 有参函数fun2() a=undefinedb=undefined
    fun(12, 'ab'); // 有参函数fun2() a=12b=ab
  </script>
```

- 函数的 arguments 隐形参数 (只在 function 函数内)

1. 隐形参数：在 function函数中不需要定义，但却可以直接用来获取所有参数的变量。
2. 隐形参数特别像 java 基础的可变长参数一样。操作方法也类似。

```html
 <script type="text/javascript">
    function fun() {
      alert(arguments.length);
      alert("无参函数")
      for (var i = 0; i < arguments.length; i++) {
        alert(arguments[i])
      }

    }
    fun(1, "a");
    function sum(a, b) { // 函数有无参数都不影响arguments的使用
      alert(a);
      alert(arguments.length);
      alert("有参函数")
      var all = 0;
      for (var i = 0; i < arguments.length; i++) {
        if (typeof(arguments[i]) == "number") {
          all += arguments[i];
        }
      }
      return all;
    }
    alert(sum(10, 1, 2, 3, "abc"));
  </script>
```

## 自定义对象

- object 形式的自定义对象

```javascript
// 对象的定义
var 变量名 = new Object(); // 对象实例(空对象)
变量名.属性名 = 值; // 定义一个属性
变量名.函数名 = function(){}; //定义一个函数
// 对象访问
变量名.属性/函数名();
```

```html
  <script type="text/javascript">
    var obj = new Object();
    obj.name = "华仔";
    obj.age = 18;
    obj.info = function () {
      alert("姓名：" + this.name + "\t年龄：" + obj.age);
    }
    obj.info();
    alert(obj.name);
  </script>
```

- 花括号{}形式的自定义对象

```javascript
var 变量名 = {};
var 变量名 = {
    属性名:值,
    属性名: 值, // 最后一个属性/函数不加,
    函数名: function(){}
};
```

```html
  <script type="text/javascript">
    var obj = {
      name : "华仔",
      age : 18,
      info : function () {
        alert("姓名：" + this.name + "\t年龄：" + obj.age + "班级：" + this.class);
      },
      class : 1
    };
    obj.info();
    alert(obj.name);
  </script>
```

## 事件

- 事件：事件是电脑输入设备与页面进行交互的响应。
- 常用事件：

1. onload 加载完成事件:页面加载完成之后，常用于做页面js 代码初始化操作
2. onclick 单击事件:常用于按钮的点击响应操作。
3. onblur 失去焦点事件:常用用于输入框失去焦点后验证其输入内容是否合法。
4. onchange 内容发生改变事件:常用车下拉列表和输入框内容发生改变后操作
5. onsubmit 表单提交事件:常用于表单提交前，验证所有表单项是否合法。


### 事件的注册

- 事件的注册(绑定)：当事件响应后为浏览器提供要执行操作的代码。

- 事件的注册的分类：

1. 静态注册/静态绑定：通过 html 标签的事件属性直接赋于事件响应后的代码
2. 动态注册事件：是指先通过 js代码得到标签的 dom 对象，然后再通过 dm 对象.事件名 =f unction(){}，这种形式赋于事件
   响应后的代码,。
   - 动态注册的基本步骤
   - 1. 获取标签对象
   - 2. 标签对象事件名 =fucntion(){}

### onload

- 静态注册

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
  <script type="text/javascript">
    function onloadFun() {
      alert('静态注册onload事件的所有代码')
    }

  </script>
</head>
<!--静态注册onload事件：代码量大可读性很差
代码多：可以写在外面的标签种
-->
<!--<body onload="alert('静态注册onload事件')">-->
<body onload="onloadFun()">

</body>
</html>
```

- 动态注册

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
  <script type="text/javascript">
  //   动态注册onload事件
    window.onload = function () {
      alert("动态注册onload事件的所有代码")
    }
  </script>
</head>
<body>
    
</body>
</html>
```

### onclick

- 静态注册

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
  <script type="text/javascript">

    function clickF() {
      alert('静态注册onclick事件');
    }
  </script>
</head>
<body>
<!--静态注册onclick事件-->
<button onclick="clickF();">按钮1</button>
<button>按钮2</button>
</body>
</html>
```

- 动态注册

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
  <script type="text/javascript">
    window.onload = function () {
    // 动态注册
    // 1.获取标签对象(文档) document
      var btnObj = document.getElementById("btn01"); // Element 指标签
      alert(btnObj);
      // 2. 通过标签对象.事件名 = function(){}
      btnObj.onclick = function () {
        alert("动态注册的click事件");
      }
    }
  </script>
</head>
<body>
<!--静态注册onclick事件-->
<button id="btn01">按钮1</button>
<button >按钮2</button>
</body>
</html>
```

### onblur：失去焦点事件

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
  <script type="text/javascript">
    // 静态注册失去焦点事件
    function onblurFun() {
      // console是控制台对象，JS语言提供，专门用来向浏览解的控制器打印输出，用于测试使用
      // log()是打印方法
      console.log("静态注册失去焦点");
      // 动态注册
    }
    window.onload = function () {
      // 1. 获取标签对象
      var pwdObj = document.getElementById("password");
      alert(pwdObj);
      // 2. 通过标签对象.事件名 = function() {};
      pwdObj.onblur = function () {
        console.log("动态注册失去焦点");
      }
    }
  </script>
</head>
<body>
  用户名：<input type="text" onblur="onblurFun();"> <br/>
  密码：<input id="password" type="text"> <br/>
</body>
</html>
```

### onchange：内容发生改变

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
  <script type="text/javascript">
    function onchangeFun() {
      // alert("选项改变");
    }
    window.onload = function () {
      var changeObj = document.getElementById("s1");
      alert(changeObj);
      changeObj.onchange = function () {
        alert("男神选项改变");
      }
    }
  </script>
</head>
<body>
  请选择你的女idol：
<!--  静态注册onchange事件-->
  <select onchange="onchangeFun();">
    <option>--女神1--</option>
    <option>--女神2--</option>
    <option>--女神3--</option>
    <option>--女神4--</option>
  </select>
  请选择你的男idol：
  <!--  动态注册onchange事件-->
  <select id="s1" onchange="onchangeFun();">
    <option>--男神1--</option>
    <option>--男神2--</option>
    <option>--男神3--</option>
    <option>--男神4--</option>
  </select>

</body>
</html>
```

### onsubmit:表单提交

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
  <script type="text/javascript">
    // 静态注册表单提交
    function onsubmitFunc() {
      // 要验证所有表单项是否合法，如果，有一个不合法就阻止表单提交
      // return false 可以阻止表单提交
      alert("静态注册表单提交");
      return false;
    }
    window.onload = function () {
      var formObj1 = document.getElementById("form01");
      formObj1.onsubmit = function () {
        alert("动态注册表单提交");
        return true;
      }
    }
  </script>
</head>
<body>
<!--return false 可以阻止表单提交-->
<form action="http://localhost:8080" method="get" onsubmit="return onsubmitFunc()">
  <input type="submit" value="静态注册"/>
</form>
<form id="form01" action="http://localhost:8080">
  <input type="submit" value="动态注册"/>
</form>
</body>
</html>
```

## DOM模型

- 基本概念

1. DOM 全称是 Document object Model 文档对象模型
2. 把文档中的标签，属性，文本，转换成为对象来管理。

- Document对象(重点)：指整个html页面->有树形结构和层级关系

![document页面对象树形结构图](.\JavaWeb_Markdown笔记图片\document页面对象树形结构图.png)

1. Document对象：管理了所有的 HTML 文档内容
2. document 它是一种树结构的文档。有层级关系。
3. 它把所有的标签 都 对象化
4. 可以通过 document 访问所有的标签对象。

### Document 对象中的(常用)方法介绍 (**重点**)

1. document.getElementById(elementId)：返回对拥有指定 id 的**第一个**对象的引用
   通过标签的 id 属性查找标签 dom 对象，elementId 是标签的 id 属性值

```java
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
  <script type="text/javascript">
    /*
    需求：当用户点击了较验按钮，要获取输出框中的内容。然后验证其是否合法
    验证规则：必须由字母，戴字。下划线组成。并且长度是5到12位。
     */
    function onclickFunc() {
      // 操作一个标签先获取这个标签对象
      var userObj = document.getElementById("username");
      // alert(userObj.value); // 获取输入内容
      var userText = userObj.value;
      // 验证字符串是否符合规则->正则表达式
      var pat = /^\w{5,12}$/;
      // test方法用于匹配
      // 获取标签对象
      var spanObj = document.getElementById("usernameSpan");
      // innerHTML 表示起始标签和结束标签中的内容 可读可写
      alert(spanObj.innerHTML);
      spanObj.innerHTML = "修改之后";
      if (!pat.test(userText)) {
        spanObj.innerHTML = "用户名不合法"; // 标签可以改为对应的图片
      } else {
        spanObj.innerHTML = "用户名合法";
      }
    }
  </script>
</head>
<body>
用户名：<input type="text" id="username">
<span id="usernameSpan" style="color: red;">1234</span>
<button onclick="onclickFunc()">校验</button>

</body>
</html>
```

2. document .getElementsByName(elementName)
   通过标签的 name 属性查找标签 dom 对象，elementName 标签的 name 属性值

```java
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
  <script type="text/javascript">
    // 全选
    function checkAll() {
      // 让所有复选框都选中
      // document,getElementsByName();是根据 指定的name属性询返回多个标签对象集台
      // 这个集合的操作跟数组 一样
      // 在html页面的顺序就是访问顺序
      var hobbies = document.getElementsByName("hobby");
      // checked表示复选框的进中状态。如果选中是true，不选中是false
      // checked 这个属性可读，可写
      // alert(hobbies[0].checked);
      for (var i=0; i<hobbies.length; i++) {
        hobbies[i].checked = true;
      }
    }
    function checkNo() {
      var hobbies = document.getElementsByName("hobby");
      for (var i=0; i<hobbies.length; i++) {
        hobbies[i].checked = false;
      }
    }
    function checkReverse() {
      var hobbies = document.getElementsByName("hobby");
      for (var i=0; i<hobbies.length; i++) {
        hobbies[i].checked = !hobbies[i].checked;
      }
    }
  </script>
</head>
<body>
  兴趣爱好：
  <input type="checkbox" name="hobby" value="cpp">C++
  <input type="checkbox" name="hobby" value="java">Java
  <input type="checkbox" name="hobby" value=js">JavaScript
<br/>
  <button onclick="checkAll()">全选</button>
  <button onclick="checkNo()">全不选</button>
  <button onclick="checkReverse()">反转</button>
</body>
</html>
```

3. document.getElementsByTagName(tagname)
   通过标签名查找标签 dom 对象。tagname 是**标签名**

```java
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
  <script type="text/javascript">
    // 全选
    function checkAll() {
      // 让所有复选框都选中
      // document,getElementsByTagName();是按照指定标签名来进行查询井返回集合
      // 这个集合的操作跟数组 一样
      // 在html页面的顺序就是访问顺序
      var inputs = document.getElementsByTagName("input");
      for (var i=0; i<inputs.length; i++) {
        inputs[i].checked = true;
      }
    }
  </script>
</head>
<body>
  兴趣爱好：
  <input type="checkbox" name="hobby" value="cpp">C++
  <input type="checkbox" name="hobby" value="java">Java
  <input type="checkbox" name="hobby" value=js">JavaScript
<br/>
  <button onclick="checkAll()">全选</button>
</body>
</html>
```

注意：

a. 查询方法优先使用document.getElementById

b. 如果没有 id 属性，则优先使用 getElementsByName 方法来进行查询

c. 如果id 属性和 name属性都没有最后再按标签名查getElementsByTagName

d. html逐行执行，遇到标签创建代码时才执行创建，整个页面加载完成才执行window.onload

4. document .createElement( tagName)
   方法，通过给定的标签名，创建一个标签对象。tagName 是要创建的标签名

### 节点的常用属性和方法

- 节点就是标签对象/文本-空白也是文本对象

- 方法:

1. 通过具体的元素节点调用
   getElementsByTagName()
   方法，获取当前节点的指定标签名孩子节点
2. appendChild( oChildNode )
   方法，可以添加一个子节点，oChildNode 是要添加的孩子节点

- 属性:

1. childNodes
   属性，获取当前节点的所有子节点
2. firstChild
   属性，获取当前节点的第一个子节点
3. lastChild
   属性，获取当前节点的最后一个子节点
4. parentNode
   属性，获取当前节点的父节点
5. nextSibling
   属性，获取当前节点的下一个节点
6. previousSibling
   属性，获取当前节点的上一个节点
7. className
   用于获取或设置标签的 class 属性值
8. innerHTML
   属性，表示获取/设置起始标签和结束标签中的**内容** -- 包括标签名
9. innerText
   属性，表示获取/设置起始标签和结束标签中的**文本** -- 不包括标签名

## JQuery

- 基本介绍

iQuery顾名思义也就是JavaScript 和查询(Query)，就是辅助JavaScript 开发的js 类库。

- 演示

1. JavaScript原生的单击事件的实现

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
  <script type="text/javascript">
    window.onload = function () {
      var  btnObj = document.getElementById("btnId");
      btnObj.onclick = function () {
        alert("原生单击事件");
      }
    }
  </script>
</head>
<body>
<button id="btnId">SayHello</button>

</body>
</html>
```

2. JQuery实现

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
  <script src="http://code.jquery.com/jquery-1.7.2.min.js"></script>
  <script type="text/javascript">
    $(function () {// 页面加载完成的实现函数，相当于window.onload = function(){}
        var $btnObj = $("#btnId");
        $btnObj.click(function () {
            alert("JQuery单击事件");
        })
    })

  </script>
</head>
<body>
<button id="btnId">SayHello</button>

</body>
</html>
```

- 常见问题

1. 使用jQuery一定要引入 jQuery 库吗?	必须
2. jQuery中的$到底是什么?	是一个函数
3. 怎么为按钮添加点击响应函数的?
   - 使用jQuery 查询到标签对象
   - 使用标签对象.dick( function()]

### 核心函数

- 核心函数

1. 传入参数为[函数] 时
   表示页面加载完成之后。相当于 window.onload =function()
2. 传入参数为 [HTML 字符串]时:
   会对我们创建这个 html 标签对象
3. 传入参数为 [ 选择器字符串 ] 时
   S(“#id 属性值");id 选择器，根据id查询标签对象
   S(“名”);标签名选择器，根据指定的标签名查询标签对象
   S(“.class 属性值”);类型选择器，可以根据 class 属性查询标签对象
4. 传入参数为 [DOM 对象 ] 时:
   会把这个 dom 对象转换为 jQuery 对象

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>核心函数</title>
    <script src="http://code.jquery.com/jquery-1.7.2.min.js"></script>
    <script type="text/javascript">
        // 核心函数的4 个作用
        // 1.
        $(function () {
            alert("页面加载完自动调用");
            // 2.
            $("<div>\n" +
                "    <span>标签1</span>\n" +
                "    <span>标签2</span>\n" +
                "</div>").appendTo("body");
            // 3.
            var $button = $("button");
            alert($button.length);
            // 4.
            var btn1 = document.getElementById("btn01");
            alert(btn1);
            alert($(btn1));

        })
    </script>
</head>
<body>
<!--<div>-->
<!--    <span>标签1</span>-->
<!--    <span>标签2</span>-->
<!--</div>-->
<button id="btn01">1</button>
<button>2</button>
<button>3</button>
</body>
</html>
```



### jQuery对象和dom 对象区分

- Dom对象的获取

1. 通过 getElementByld() ：查询出来的标签对象是Dom 对象
2. 通过 getElementsByName()：查询出来的标签对象是 Dom 对象
3. 通过 getElementsByTagName()：查询出来的标签对象是 Dom 对象
4. 通过 createElement() ：方法创建的对象，是Dom 对象

alert显示[ object HTML标签名Element ]

- jQuery 对象

1. 通过JQuery 提供的API创建的对象，是JQuery 对象
2. 通过JQuery 包装的Dom 对象，也是JQuery 对象
3. 通过Query 提供的API查询到的对象，是JQuery 对象

alert显示[ object Object ]

### jQuery对象的本质

- Query 对象是 dom 对象的数组+jQuery 提供的一系列功能函数

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
  <script src="http://code.jquery.com/jquery-1.7.2.min.js"></script>
  <script type="text/javascript">
    $(function () {
      var $btns = $("button");
      alert($btns);
      for (var i=0; i < $btns.length; i++) {
        alert($btns[i]);
      }
    })
  </script>
</head>
<body>
<button id="btn01">按钮1</button>
<button id="btn02">按钮2</button>
<button id="btn03">按钮3</button>
<button id="btn04">按钮4</button>
</body>
</html>
```

### jQuery 对象和 Dom 对象使用区别

jQuery 对象和 Dom 对象不能互相使用对方的属性和方法

### jQuery 对象和 Dom 对象相互转换

- dom 对象转化为jQuery 对象(*重点)
  1. 先有 DOM 对象
  2. $(DOM 对象 ) 就可以转换成为 jQuery 对象
- jQuery 对象转为 dom 对象 (*重点)
  1. 先有 jQuery 对象
  2. jQuery 对象[下标]

![Jquery和Dom对象的转换](.\JavaWeb_Markdown笔记图片\Jquery和Dom对象的转换.png)

### jQuery 选择器(重点)

#### 基本选择器(重点)

- 基本选择器

1. id选择器： #id
2. 元素选择器: element 根据标签名查找对象
3. 类型选择器：.class 根据 class 查找标签对象
4. 所有元素选择器： * 查找所有元素
5. 组合选择器： $("div, span, p.myClass") -- 结果的顺序和html的顺序一样

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
  <script src="http://code.jquery.com/jquery-1.7.2.min.js"></script>
  <script type="text/javascript">
    $(function () {
        $("#btn1").click(function () {
            $("#one").css("background-color", "red");
        });
        $("#btn2").click(function () {
            $(".mini").css("background-color", "blue");
        });
        $("#btn3").click(function () {
            $("div").css("background-color", "yellow");
        });
        $("#btn4").click(function () {
            $("*").css("background-color", "black");
        });
        $("#btn5").click(function () {
            $("span, #two").css("background-color", "green");
        });
    });
  </script>
</head>
<body>
<input type="button" value="选择id为one的元素" id="btn1">
<input type="button" value="选择class 为 mini的所有元素" id="btn2">
<input type="button" value="元素名为div的所有元素" id="btn3">
<input type="button" value="选择所有元素" id="btn4">
<input type="button" value="组合选择" id="btn5">
<button id="one">按钮1</button>
<button class="mini" id="two">按钮2</button>
<button class="mini">按钮3</button>
<div>
    hehe
</div>
<span>
    aaa
</span>
</body>
</html>
```

#### 层级选择器

1. $("form input")：在给定的祖先元素下匹配所有的后代元素。找到form表单中的所有input元素
2. $("form > input")：在给定的父元素下匹配所有的子元素
3. $("form + input")：匹配所有紧接在 prev 元素后的 next 元素
4. $("form ~ input")：匹配 prev 无素之后的所有 siblings 元素
5. +和~都是选择同级的元素

```html
<script type="text/javascript">
	$(document).ready(function(){
        //1.选 body 内的所有 div 元素
        $("#btn1").click(function(){
        $("body div").css("background", "#bbffaa");
        });
        //2.在 body 内,选择div子元素
        $("#btn2").click(function(){
        $("body > div").css("background", "#bbffaa");
        });
        //3.选 id 为 one 的下一个 div 元囊
        $("#btn3").click(function(){
        $("#one + div").css("background", "#bbffaa");
        });
        //4.选 id 为 two 的元后面的所有 div 兄弟元素
        $("#btn4").click(function(){
        $("#two + div").css("background", "#bbffaa");
            });
    });
</script>
```

#### 基本过滤选择器

1. :first	获取第一个元素
2. :last	 获取最后个元素
3. :not(selector)	去除所有与给定选择器匹配的元素
4. :even	匹配所有索引值为偶数的元素，从 0开始计数
5. :odd	匹配所有索引值为奇数的元素，从 0开始计数
6. :eq(index)	匹配一个给定索引值的元素
7. :gtindex)	匹配所有大于给定索引值的元素
8. :lt(index)	匹配所有小于给定索引值的元素
9. :header	给页面内所有标题加上背景色

```html
<script type="text/javascript">
	$(document).ready(function(){
        //1.选第一个 div 元素
        $("#btn1").click(function(){
        	$("div:first").css("background", "#bbffaa");
        });
		//2.选择最后一个 div 元素
        $("#btn2").click(function(){
        	$("div:last").css("background", "#bbffaa");
        });
        //3.选class不为 one 的所有 div 元素
        $("#btn3").click(function(){
        $("div:not(.one)").css("background","#bbffaa");
         });
		//4.选择索引值为偶数的 div 元素
		$("#btn4").click(function(){
        $("div:even").css("background","#bbffaa");
         });
        //5.选择索引值为奇数的 div 元素
        $("#btn5").click(function(){
        $("div:odd").css("background","#bbffaa");
         });
        //6.选择索引值为大于3的 div 元素
        $("#btn6").click(function(){
        $("div:gt(3)").css("background","#bbffaa");
         });
        //7.选索引值为等于 3 div 元素
        $("#btn7").click(function(){
        $("div:eq(3)").css("background","#bbffaa");
         });
        //8.选索引值为小于 3 div 元素
        $("#btn8").click(function(){
        $("div:lt(3)").css("background","#bbffaa");
         });
        //9.选择所有的标题元素
        $("#btn9").click(function(){
        $(":header").css("background","#bbffaa");
         });
        //10.选择当前正在执行动画的所有元素
        $("#btn10").click(function(){
        $(":animated").css("background","#bbffaa");
         });
        //11.选择没有执行动画的最后一个div
        $("#btn11").click(function(){
        $("div:not(:animated):last").css("background","#bbffaa");
         });
    });
</script>
```

#### 内容过滤器

1. :contains(text)	匹配包含给定文本的元素
2. :empty	匹配所有不包含子元素或者文本的空元素
3.  :parent	匹配含有子元素或者文本(非空)的元素
4.  :has(selector)	匹配**含有选择器所匹配的元素的元素**

```html
<div><p>Hello</p></div>
<div>Hello again!</div>

<script type="text/javascript">
    $("div:has(p)").addClass ("test"); // 返回含有p的div
</script>
```

```html
<script type="text/javascript">
	$(document).ready(function(){
        //1.选含有文本di 的 div 元素
        $("#btn1").click(function(){
        	$("div:contains('di')").css("background", "#bbffaa");
        });
        //2.选不包合子元素(或文本元素) 的 div 元素
		$("#btn2").click(function(){
        	$("div:empty").css("background", "#bbffaa");
        });
        //3.选择含有 class 为 mini 元素 的 div 元素
        $("#btn3").click(function(){
        	$("div:has(.mini)").css("background", "#bbffaa");
        });
        //4.选择合有子元(或者文本元)的div元素
        $("#btn4").click(function(){
        	$("div:parent").css("background", "#bbffaa");
        });
    });
</script>
```

#### 属性过滤器

1. [attribute]匹配包含给定属性的元素

   ```javascript
   // 包含id属性的div
   $("div[id]")
   ```

2. [attribute=value]匹配给定的属性是某个特定值的元素

3. [attribute!=value]匹配所有**不含**有指定的属性，或者属性**不等于特定值**的元素。

4. [attribute^=value]匹配给定的属性是以某些值开始的元素

5. [attributes$=value]匹配给定的属性是以某些值结尾的元素

6. [attribute*=value]匹配给定的属性是以包含某些值的元素

7. [ attrSel1 ] [ attrSel2] [ attrSelN ]复合属性选择器，需要同时满足多个条件时使用。

```html
<script type="text/javascript">
	$(document).ready(function(){
        //1.选取含有属性 title 的div元亲
        $("#btn1").click(function(){
        	$("div[title]").css("background", "#bbffaa");
        });
        //2.选取属title值等于'test' 的div元素
		$("#btn2").click(function(){
        	$("div[title='test']").css("background", "#bbffaa");
        });
        //3.选取 属性title值不等于test的div元素(*没有属性title的也将被选中)
        $("#btn3").click(function(){
        	$("div[title!='test']").css("background", "#bbffaa");
        });
        //4.选取 属性title值 以 te 开始 的div元素
        $("#btn4").click(function(){
        	$("div[title^='te']").css("background", "#bbffaa");
        });
        //5.选取 属性title值 以est 结束 的div元素
        $("#btn5").click(function(){
        	$("div[title$='est']").css("background", "#bbffaa");
        });
        //6.选取 属性tile值 含有es 的div元素
        $("#btn6").click(function(){
        	$("div[title*='es']").css("background", "#bbffaa");
        });
        //7.首先选取有属性id的div元素，然后在结果中 选取属性title值 含有es的 div 元素
        $("#btn7").click(function(){
        	$("div[id][title*='es']").css("background", "#bbffaa");
        });
        //8.选取 含有 title 属性值，且title 属性值不等于 test 的 div 元素
        $("#btn8").click(function(){
        	$("div[title][title!='test']").css("background", "#bbffaa");
        });
    });
</script>
```

#### 表单过滤器

- 查找type == 下面字段的内容

1. :input	匹配所有 input, textarea, select 和 button 元素

2. :text	匹配所有文本输入框
3. :password	匹配所有的密码输入框
4. :radio	匹配所有的单选框
5. :checkbox	匹配所有的复选框
6. :submit	匹配所有提交按钮
7. :image	
8. :reset	
9. :button	
10. :file	
11. :hidden	匹配所有不可见元素，或者type为hidden的元素

- 表单对象属性

1. :enabled	
2. :disabled	不可用的
3. :checked	匹配所有选中的被选中元素(复选框、单选框等，不包括select中的option) 
4. :selected	匹配所有选中的option元素

```html
<script type="text/javascript">
	$(document).ready(function(){
        //1.对表单内 可用input 值操作
        $("#btn1").click(function(){
            // val()可以操作表单项的vaLue属性值
            // 可以设置和获取 -- 传参数设置 不传参数获取
        	$(":text:enabled").val("赋值123");
        });
        //2.对表单内 不可用input 值操作
		$("#btn2").click(function(){
        	$(":text:disabled").val("不可以的表单");
        });
        //3.获取多选框选中的个数 使用size()方法获取进取到的元集合的元个数
        $("#btn3").click(function(){
        	alert($(":checkbox:checked").length);
        });
        //4.获取多选框，每个选中的value值
        $("#btn4").click(function(){
        	var $checkBoies = $(":checkbox:checked");
            // 传统遍历方法
            for (var i=0; i < $checkBoies.length; i++) {
                alert($checkBoies[i].value);
            }
            // each万方法是jQuery对象提供用来遍历元素的方法
            // 在遍历的function函数中，有一个this对象，这个this对象，就是当前遍历到的dom对象
            $checkBoies.each(function() {
                alert(this.value);
            })
        });
        //5.获取下拉框选中的内容
        $("#btn5").click(function(){
        	$("div[title$='est']").css("background", "#bbffaa");
            //获取选中的option标签对象
            var $option = $("select option:selected");
            //遍历，获取option标签中的文本内容
            $option.each(function () {
                // 在each遍历function函数中有一个this对象。这个this对象是当前正在遍历到的dom对象
                alert(this.innerHTML);
            })

        });
    });
</script>
```

### JQuery元素筛选

1. eq()：获取给定索引的元素	功能跟 :eq() 一样

   ```html
   $("p").eq(1);
   ```

2. first()：获取第一个元素	功能跟 :first一样

3. last()：获取最后一个元素

4. filter(exp)：留下匹配的元素

   ```java
   $("p").filter(".selected");
   ```

5. is()：判断是否匹配给定的选择器，只要有一个匹配就返回，true

6. has(exp)：返回包含有匹配选择器的元素的元素	功能跟 :has 一样

7. not(exp)：删除匹配选择器的元素	功能跟 :not 一样

8. children(exp)：返回匹配给定选择器的子元素	功能跟 parent>child 一样

9. find(exp)：返回匹配给定选择器的后代元素	功能跟 ancestor descendant 一样

10. next()：返回当前元素的下一个兄弟元素	功能跟 prev +next 功能一样

11. nextAll()：返回当前元素后面所有的兄弟元素	功能跟 prev~siblings 功能一样

12. nextUntil()：返回当前元素到指定匹配的元素为止的后面元素

    ```html
    <script type="text/javascript">
    	$(document).ready(function(){
            $("#btn1").click(function(){
                // val()可以操作表单项的vaLue属性值
                // 可以设置和获取 -- 传参数设置 不传参数获取
            	$(":div:first").nextUntil("span").addClass("after");
            });
        });
    </script>
    ```

13. parent()：返回父元素

14. prev(exp)：返回当前元素的上一个兄弟元素

15. prevAll()：返回当前元素前面所有的兄弟元素

16. prevUnit(exp)：返回当前元素到指定匹配的元素为止的前面元素

17. siblings(exp)：返回所有兄弟(同级)元素

18. add()：把 add 匹配的选择器的元素添加到当前 jquery 对象中

    ```html
    alert($("div").add("span").length)
    ```

- 练习

```html
<script type="text/javascript">
	$(document).ready(function(){
        //(1)eq()选择索引值 为等于王的 div 元素
        $("#btn1").click(function(){
        	$("div").eq(3).css("background", "#bbffaa");
        });
        //(2)first()选择第一个 div 元素
		$("#btn2").click(function(){
        	$("div").first().css("background", "#bbffaa");
        });
		//(3)last()选择最后一个 div 元素
        $("#btn3").click(function(){
        	$("div").last().css("background", "#bbffaa");
        });
        //(4)filter()在div中选择索引为偶数
        $("#btn4").click(function(){
        	$("div").filter(":even").css("background", "#bbffaa");
        });
        //(5)is()判断#one是否为:empty或:parent
		//is用来检测q对象是否符合指定的选择器
        $("#btn5").click(function(){
        	alert($("#one").is(":empty"));
        });
        //(6)has()选择div中包含class .mini的
        $("#btn6").click(function(){
        	$("div").has(".mini").css("background", "#bbffaa");
        });
        //(7)not()选耀div中class不为one的
        $("#btn7").click(function(){
        	$("div").not(".one").css("background", "#bbffaa");
        });
        //(8)children()在body 中选择所有cLass为one的div子元素
        $("#btn8").click(function(){
        	$("body").children("div.one").css("background", "#bbffaa");
        });
        //(9)find()在body 中选择所有cLass为mini的div元素
        $("#btn9").click(function(){
        	$("body").find("div.mini").css("background", "#bbffaa");
        });
        //(10)next() ]one的下一div
        $("#btn10").click(function(){
        	$("#one").next("div").css("background", "#bbffaa");
        });
        //(11)nextALL() #one后面所有的span元素
        $("#btn11").click(function(){
        	$("#one").nextAll("span").css("background", "#bbffaa");
        });
        //(12)nextUntil() #one和span之间的元素
         $("#btn12").click(function(){
        	$("#one").nextUntil("span").css("background", "#bbffaa");
        });
        //(13)parent() .mini的父元素
         $("#btn13").click(function(){
        	$(".mini").find("div.mini").css("background", "#bbffaa");
        });
        //(14)prev() #two的上一个div
         $("#btn14").click(function(){
        	$("#two").prev("div").css("background", "#bbffaa");
        });
        //(15)prevALL() span前面所有的div
        $("#btn15").click(function(){
        	$("span").prevAll("div").css("background", "#bbffaa");
        });
        //(16)prevUntil() span向前直到#one的元素
        $("#btn16").click(function(){
        	$("span").prevUntil("#one").css("background", "#bbffaa");
        });
        //(17)siblings() #two的所有兄弟元素
        $("#btn17").click(function(){
        	$("#two").siblings().css("background", "#bbffaa");
        });
        //(18)add()选所有的 span 元和d为tio的元案
        $("#btn18").click(function(){
        	$("span").add($("#two")).css("background", "#bbffaa");
        });
    });
</script>
```

### jQuery 的属性操作

- 基本属性

1. html()：它可以设置和获取起始标签和结束标签中的内容，跟 dom 属性 innerHTML 一样。
2. text()：它可以设置和获取起始标签和结束标签中的文本，跟 dom 属性 innerText 一样。
3. val()：它可以设置和获取表单项的 value 属性值，跟 dom 属性 value 一样。
   - val 方法同时设置多个表单项的选中状态

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
  <script type="text/javascript" src="http://code.jquery.com/jquery-1.7.2.min.js"></script>
  <script type="text/javascript">
     $(function () {
       // 无参获取传参设置
       // 1.html()
       // alert($("div").html());
       // $("div").html("<h1>我是div中的标题1</h1>");
       // 2.text()
       // alert($("div").text());
       // $("div").text("<h1>修改内容</h1>"); // 内容都会当作文本
       // 3.val()
       $("button").click(function () {
         alert($("#username").val());
         $("#username").val("超级程序员");
       })
     })
  </script>
</head>
<body>
<div>我是div<span>我是div中的span</span></div>
<input type="text" name="username" id="username">
<button>操作输入框</button>
</body>
</html>
```

```html
<!-- 批量操作属性1 -->
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
  <script type="text/javascript" src="http://code.jquery.com/jquery-1.7.2.min.js"></script>
  <script type="text/javascript">
    $(function () {
      // // 1.操作单选
      // $(":radio").val(["radio1"]);
      // // 2.操作多选
      // $(":checkbox").val(["checkbox1", "checkbox2"]);
      // // 3.操作下拉多选
      // $("#multiple").val(["mul1", "mul3"]);
      // // 4.操作下拉单选
      // $("#single").val(["sin3"]);
      // 5.一次性批量操作
      $("#single, :radio").val(["radio1", "sin3"]);
    });
  </script>
</head>
<body>
单选：
  <input name="radio" type="radio" value="radio1" />radio1
  <input name="radio" type="radio" value="radio2" />radio2
  <br/>
多选：
  <input name="checkbox" type="checkbox" value="checkbox1" /> checkbox1
  <input name="checkbox" type="checkbox" value="checkbox2" /> checkbox2
  <input name="checkbox" type="checkbox" value="checkbox3" /> checkbox3
  <br/>
下拉多选：
  <select id="multiple" multiple="multiple" size="4">
    <option value="mul1">mul1</option>
    <option value="mul2">mul2</option>
    <option value="mul3">mul3</option>
    <option value="mul4">mul4</option>
  </select>
  <br/>
单选下拉：
<select id="single">
  <option value="sin1">sin1</option>
  <option value="sin2">sin2</option>
  <option value="sin3">sin3</option>
  <option value="sin4">sin4</option>
</select>
<br/>
</body>
</html>
```

- 其他属性

1. attr()：可以设置和获取属性的值，不推荐操作 checked、readonly、selected、disabled 等等
2. prop()：可以设置和获取属性的值，推荐操作 checked、readonly、selected、disabled 等等。attr()不能使用的场景使用prop()。
   - 避免出现undefined

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
  <script type="text/javascript" src="http://code.jquery.com/jquery-1.7.2.min.js"></script>
  <script type="text/javascript">
    $(function () {
      // 一个参数获取内容
      // 两个参数设置内容
      // alert($(":checkbox:first").attr("name"));
      $(":checkbox:first").attr("name", "adc");
      alert($(":checkbox:first").attr("name"));
      alert($(":checkbox:first").attr("checked"));// attr查看的属性不存在 会返回undefined
      alert($(":checkbox:last").prop("checked"));
      // 设置自定义属性
      $(":checkbox:first").attr("abc","abcValue");
      alert( $(":checkbox:first").attr("abc") );
    });
  </script>
</head>
<body>
多选：
  <input name="checkbox" type="checkbox" checked="checked" value="checkbox1" /> checkbox1
  <input name="checkbox" type="checkbox" value="checkbox2" /> checkbox2
  <input name="checkbox" type="checkbox" value="checkbox3" /> checkbox3
  <br/>
</body>
</html>
```

- 练习：全选/全不选

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
  <script type="text/javascript" src="http://code.jquery.com/jquery-1.7.2.min.js"></script>
  <script type="text/javascript">
    $(function () {
      // 全选
      $("#checkedAllBtn").click(function () {
        $(":checkbox").prop("checked", true);
      });
      // 全不选
      $("#checkedNoBtn").click(function () {
        $(":checkbox").prop("checked", false);
      });
      // 反选
      $("#checkedRevBtn").click(function () {

        $(":checkbox[name='items']").each(function () {
          this.checked = !this.checked;
        });
        var allCnt = $(":checkbox[name='items']").length;
        var checkedCnt = $(":checkbox[name='items']:checked").length;
        $("#checkedAllBox").prop("checked", allCnt === checkedCnt);
      });
      // 提交
      $("#sendBtn").click(function () {
        $(":checkbox:checked").each(function () {
          alert(this.value);
        })
      })
      // 绑定全选/全不选
      $("#checkedAllBox").click(function () {
        $(":checkbox[name='items']").prop("checked", this.checked);
      })
      // 绑定全部球类
      $(":checkbox[name='items']").click(function () {
        var allCnt = $(":checkbox[name='items']").length;
        var checkedCnt = $(":checkbox[name='items']:checked").length;
        $("#checkedAllBox").prop("checked", allCnt === checkedCnt);
      })
    });
  </script>
</head>
<body>
<form method="post" action="">
  你爱好的运动是？<input type="checkbox" id="checkedAllBox" /> 全选/全不选
  <br />
  <input type="checkbox" name="items" value="足球" />足球
  <input type="checkbox" name="items" value="篮球" />篮球
  <input type="checkbox" name="items" value="羽毛球" />羽毛球
  <input type="checkbox" name="items" value="乒乓球" />乒乓球
  <br />
  <input type="button" id="checkedAllBtn" value="全 选" />
  <input type="button" id="checkedNoBtn" value="全 不 选" />
  <input type="button" id="checkedRevBtn" value="反 选" />
  <input type="button" id="sendBtn" value="提 交" />
</form>
</body>
</html>
```

### DOM的增删改

- 内部插入

1. appendTo()	a.appendTo(b)	把a插入到 b子元素末尾，成为最后一个子元素
2. prependTo()	a.prependTo(b)	把 a 插到 b所有子元素前面，成为第一个子元素

- 外部插入:

1. insertAfter()	a.insertAfter(b)	得到 ba
2. insertBefore()	a.insertBefore(b)	得到 ab


- 替换:

1. replaceWith()	a.replaceWith(b)	用b替换掉a 替换一个
2. replaceAll()	a.replaceAll(b)	用a替换掉b 替换全部

- 删除:

1. remove()	a.remove();	删除 a 标签
2. empty()	a.empty();	清空 a 标签内的内容

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
  <script type="text/javascript" src="http://code.jquery.com/jquery-1.7.2.min.js"></script>
  <script type="text/javascript">
    $(function () {
      // 内部插入
      $("<h1>标题1</h1>").prependTo("div");
      $("<h2>标题2</h2>").appendTo("div");
      // 外部插入
      $("<h3>标题3</h3>").insertAfter("div");
      $("<h4>标题4</h4>").insertBefore("div");
      // 替换
      // $("div").replaceWith($("<h5>标题5</h5>"));
      // $("<h6>标题6</h6>").replaceAll($("div"));
      // 删除
      $("div").empty();
      $("div").remove();
    });
  </script>
</head>
<body>
<form method="post" action="">
  <div>1234</div>
  <div>4321</div>
</form>
</body>
</html>
```

- 练习：从左到右，从右到左

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
  <script type="text/javascript" src="http://code.jquery.com/jquery-1.7.2.min.js"></script>
  <script type="text/javascript">
    $(function () {
      // 1.选中移动到右边
      $("button:eq(0)").click(function () {
        $("select:eq(0) option:selected").appendTo($("select:eq(1)"));
      })
      // 2.全部移动到右边
      $("button:eq(1)").click(function () {
        $("select:eq(0) option").appendTo($("select:eq(1)"));
      })
      // 3.选中移动到左边
      $("button:eq(2)").click(function () {
        $("select:eq(1) option:selected").appendTo($("select:eq(0)"));
      })
      // 4.全部移动到左边
      $("button:eq(3)").click(function () {
        $("select:eq(1) option").appendTo($("select:eq(0)"));
      })
    });
  </script>
</head>
<body>
  <div id="left">
    <select multiple="multiple" name="sel01">
      <option value="opt01">选项1</option>
      <option value="opt02">选项2</option>
      <option value="opt03">选项3</option>
      <option value="opt04">选项4</option>
      <option value="opt05">选项5</option>
      <option value="opt06">选项6</option>
      <option value="opt07">选项7</option>
      <option value="opt08">选项8</option>
      <option value="opt09">选项9</option>
    </select>
    <button>选中移动到右边</button>
    <button>全部移动到右边</button>
  </div>
  <div id="right">
    <select multiple="multiple" name="sel02">

    </select>
    <button>选中移动到左边</button>
    <button>全部移动到左边</button>
  </div>
</body>
</html>
```

- 练习：动态添加/删除行信息

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
  <script type="text/javascript" src="http://code.jquery.com/jquery-1.7.2.min.js"></script>
  <script type="text/javascript">
    $(function () {
      // 创建一个用于复用的删除function函数
      var deleteFun = function () {
        alert(this);
        // 在事件响应的function函数中，有一个this 对象。这个this 对象是当前正在响应事件的dom对象
        // 获取行对象
        var $trObj = $(this).parent().parent();
        var name = $trObj.find("td:first").text();

        // confirm 是JavaScript语言提供的一个确认提示函数。你给它传什么，它就提示什么<br/>
        // 当用户点击了确定，就返回true。当用户点击了取消，就返回false
        if (confirm("是否确定删除[" + name + "]吗?")) {
          $trObj.remove();
        }
      }
        $("#addEmpButton").click(function () {
          // 获取输入框的内容
          var name = $("#empName").val();
          var email = $("#email").val();
          var salary = $("#salary").val();
          var $trObj = $("<tr>" +
            "<td>" + name + "</td>" +
            "<td>" + email + "</td>" +
            "<td>" + salary + "</td>" +
            "<td><a href=\"deleteEmp?id=002\">Delete</a></td>" +
            "</tr>");
          $trObj.appendTo($("#employeeTable"));
          $trObj.find("a").click(deleteFun);
        });
        // 给submit绑定事件
        $("a").click(deleteFun);
      });
  </script>
</head>
<body>
 <table id="employeeTable">
   <tr>
     <th>name</th>
     <th>email</th>
     <th>salary</th>
   </tr>
   <tr>
     <td>Tom</td>
     <td>tom@edu.com</td>
     <td>28000</td>
     <td><a href="deleteEmp?id=001">Delete</a></td>
   </tr>
   <tr>
     <td>Jerry</td>
     <td>Jerry@edu.com</td>
     <td>32000</td>
     <td><a href="deleteEmp?id=002">Delete</a></td>
   </tr>
   <div id="formDiv">
     <h4>添加新员工</h4>
     <table>
       <tr>
        <td class="word">name:</td>
        <td class="inp">
          <input type="text" name="empName" id="empName" />
        </td>
       </tr>
       <tr>
         <td class="word">email:</td>
         <td class="inp">
           <input type="text" name="email" id="email" />
         </td>
       </tr>
       <tr>
         <td class="word">salary:</td>
         <td class="inp">
           <input type="text" name="salary" id="salary" />
         </td>
       </tr>
       <tr>
         <td colspan="2" align="center">
           <button id="addEmpButton" value="abc">
             Submit
           </button>
         </td>
       </tr>
     </table>
   </div>
 </table>
</form>
</body>
</html>
```

### css样式操作

1. addClass()	添加样式
2. removeClass()	删除样式
3. toggleClass()	有就删除，没有就添加样式
4. offset()	获取和设置元素的坐标

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
  <style type="text/css">
    div{
      width:100px;
      height:260px;
    }
    div.whiteborder { /* div限制作用类型 */
      border: 2px white solid;
    }
    div.redDiv {
      background-color: red;
    }
    div.blueBorder {
      border: 5px blue solid;
    }
  </style>
  <script type="text/javascript" src="http://code.jquery.com/jquery-1.7.2.min.js"></script>
  <script type="text/javascript">
    $(function () {
      var $divEle = $("div:first");
      $("#btn01").click(function () {
        $divEle.addClass('redDiv blueBorder'); // 可以同时操作多个
      });
      $("#btn02").click(function () {
        $divEle.removeClass("blueBorder") // 不传参数 -- 全部删除
      });
      $("#btn03").click(function () {
        $divEle.toggle('blueBorder'); // 可以同时操作多个
      });
      $("#btn04").click(function () {
        //offset() - 返回第一个匹配元素相对于文档的位置。
        var pos = $divEle.offset(); // 获取
        console.log(pos); // 控制台显示
        // 设置
        $divEle.offset({
          top:100,
          left:20
        })
      });

    })
  </script>
</head>
<body>
<table align="center">
  <div class="blueBorder">1</div>
  <tr>
    <td>
      <div class="border">
      </div>
    </td>
    <td>
      <div class="btn">
        <input type="button" value="addClass()" id="btn01" />
        <input type="button" value="removeClass()" id="btn02" />
        <input type="button" value="toggleClass()" id="btn03" />
        <input type="button" value="offset()" id="btn04" />
      </div>
    </td>
  </tr>
</table>

</body>
</html>
```

### jQuery动画

- 基本动画	

1. show()	将隐藏的元素显示。
2. hide()	将可见的元素隐藏。
3. toggle()	可见/隐藏相互转换
4. 注意：
   - 以上动画方法都可以添加参数。
   - 1、第一个参数是动画 执行的时长，以毫秒为单位
   - 2、第二个参数是动画的回调函数

- 淡入淡出动画

1. fadeln()	淡入(慢慢可见)
2. fadeOut()	淡出(慢慢消失)
3. fadeTo()	在指定时长内慢慢的将透明度修改到指定的值。
4. fadeToggle()	转换
5. 注意：

   - 以上动画方法都可以添加参数。
   - 1、第一个参数是动画 执行的时长，以毫秒为单位
   - 2、第二个参数是动画的回调函数

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
  <style type="text/css">
    div{
      width:100px;
      height:260px;
    }
    div.redDiv {
      background-color: red;
    }
    div.blueBorder {
      border: 5px blue solid;
    }
  </style>
  <script type="text/javascript" src="http://code.jquery.com/jquery-1.7.2.min.js"></script>
  <script type="text/javascript">
    $(function () {
      $("#btn01").click(function () {
        $("#div1").show(1000, function () {
          alert("动画完成");
        });
      });
      $("#btn02").click(function () {
        $("#div1").hide();
      });
      $("#btn03").click(function () {
        $("#div1").toggle();
      });
      var func = function () {
        $("#div2").toggle(1000, func);
      }
      // func();
      $("#btn04").click(function () {
        $("#div1").fadeIn(1000);
      });
      $("#btn05").click(function () {
        $("#div1").fadeOut(1000);
      });
      $("#btn06").click(function () {
        $("#div1").fadeTo(1000, 0.1); // 1秒内，变为0.1的透明度
      });
      $("#btn07").click(function () {
        $("#div1").fadeToggle(1000);
      });
    });
  </script>
</head>
<body>
<table align="center">
  <tr>
    <td>

    </td>
    <td>
      <div class="btn">
        <input type="button" value="show" id="btn01" />
        <input type="button" value="hide" id="btn02" />
        <input type="button" value="toggle" id="btn03" />
        <input type="button" value="fadeIn" id="btn04" />
        <input type="button" value="fadeOut" id="btn05" />
        <input type="button" value="fadeTo" id="btn06" />
        <input type="button" value="fadeToggle" id="btn07" />
      </div>
      <div class="border">
      </div>
    </td>
  </tr>
</table>
<div class="blueBorder" id="div1">1</div>
<div class="redDiv" id="div2">2</div>
</body>
</html>

```

- 练习:名牌显示

```html
<!-- $("div div") 的 显示有bug-->
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
  <style type="text/css">
    .showmore a span { /* 后代选择器*/
      padding-left: 100px;
      background: aqua;
    }
    .showless a span { /* 后代选择器*/
      padding-left: 100px;
      background: yellow;
    }
    .promoted a {
      color: red;
    }
  </style>
  <script src="http://code.jquery.com/jquery-1.7.2.min.js"></script>
  <script type="text/javascript">
    $(function () {
      // 基本初始状态
      $("li:gt(5):not(:last)").hide();
      // 给功能的按纽绑定单击事件
      $("div div a").click(function () {
        // 切换显示/隐藏
        $("li:gt(5):not(:last)").toggle();
        // 品牌隐藏的状态 : 1 显示全部品牌 ^
        if ($("li:gt(5):not(:last)").is(":hidden")) {
          $("div div a").text("显示全部品牌");
          // 删除向下样式 添加向上样式
          $("div div").removeClass("showmore");
          $("div div").addClass("showmore");

          // 添加高亮
          $("li:contains('索尼')").removeClass("promoted");
        } else {// 品牌显示的状态 : 2 显示精品品牌 ~^
          $("div div a").text("显示精品品牌");
          // 删除向上样式 添加向下样式
          // $("div div").removeClass();
          $("div div").addClass("showless");
          // 去掉高亮
          $("li:contains('索尼')").addClass("promoted");
        }


        return false;
      });
      // 修改按钮文本和角标方向
    });
  </script>
</head>
<body>
<div class="SubCategoryBos">
  <div class="showmore"><!-- 使用showmore/showless图片样式控制图标向上/向下 这里忽略了 -->
    <a href="more.html"><span>显示全部品牌</span></a>
  </div>
  <ul>
    <li><a href="#">佳能</a><i>(3040120)</i> </li>
    <li><a href="#">索尼</a><i>(304030)</i> </li>
    <li><a href="#">三星</a><i>(123123)</i> </li>
    <li><a href="#">尼康</a><i>(304123)</i> </li>
    <li><a href="#">松下</a><i>(3041230)</i> </li>
    <li><a href="#">其他1</a><i>(301230)</i> </li>
    <li><a href="#">其他2</a><i>(304100)</i> </li>
    <li><a href="#">其他3</a><i>(304030)</i> </li>
    <li><a href="#">其他4</a><i>(304020)</i> </li>
    <li><a href="#">其他5</a><i>(304400)</i> </li>
    <li><a href="#">其他所有</a><i>(350400)</i> </li>
  </ul>

</div>
<div class="showmore"><a><span>1</span></a></div>
<div class="showless"><a><span>2</span></a></div>
</body>
</html>
```

### jQuery 事件操作

- 文档加载：$(function(){});和window.onload = function(){}的区别?

1. 触发的顺序
   - jQuery 页面加载 先执行
   - 原生js的页面加载 后执行
2. 触发时机
   - jQuery 的页面加载 是浏览器的内核解析完页面的标签创建DOM对象之后就会马上执行
   - 原生JS的页面加载，除了要等浏览器内核解析完标签创建好 DOM 对象，还要等**标签显示时**需要的**内容加载**完成。
3. 执行次数
   - 原生JS加载只会执行最后一次的内容
   - jQuery 的页面加载 会全部按顺序执行

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
  <script src="http://code.jquery.com/jquery-1.7.2.min.js"></script>
  <script type="text/javascript">
    window.onload = function () {
      alert("原生加载1")
    };
    window.onload = function () {
      alert("原生加载2")
    };
    // 只会执行原生加载3
    window.onload = function () {
      alert("原生加载3")
    };
    // 全部执行
    $(function () {
      alert("Jquery加载1")
    });
    $(function () {
      alert("Jquery加载2")
    });
    $(function () {
      alert("Jquery加载3")
    });

  </script>
</head>
<body>

</body>
</html>
```

#### jQuery 中其他的事件处理方法

- jQuery 事件处理方法 就是JS原生事件方法去掉on	

1. click()	它可以绑定单击事件，以及触发单击事件
2. mouseover()	鼠标移入事件
3. mouseout()	鼠标移出事件
4. bind()	可以给元素一次性绑定一个或多个事件
5. one()	使用方法跟 bind 一样。但是 one 方法绑定的事件只会响应一次。
6. unbind()	跟 bind 方法相反的操作，解除事件的绑定
7. live()	用来绑定事件。可以用来绑定选择器匹配的所有元素的事件。哪怕这个元素是后面动态创建出来的也有效。
   - 不使用live()绑定，后面创建的元素不会绑定前面的事件

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
  <script src="http://code.jquery.com/jquery-1.7.2.min.js"></script>
  <script type="text/javascript">
    $(function () {

      // $("h5").click(function () { // 传入function是绑定
      //   alert("h5单击事件 -- click方法绑定")
      // });
      // $("button").click(function () {
      //   $("h5").click(); // 不传入是调用
      // });
      // 鼠标移入移出
      // $("h5").mouseover(function () {
      //   console.log("鼠标进入");
      // })
      // $("h5").mouseout(function () {
      //   console.log("鼠标出去");
      // })
      // bind 绑定事件
      $("h5").bind("click mouseover mouseout", function () {
        console.log("点击");
      })
      // one 绑定事件
      // $("h5").one("click mouseover mouseout", function () {
      //   console.log("点击");
      // })
      // live 绑定事件
      $("h5").live("click", function () { // 传入function是绑定
        alert("h5单击事件 -- click方法绑定")
      });
      $("h5").unbind("mouseover");
      $('<h5 class="head">什么是JQuery</h5>').appendTo($("#panel"));
    });
  </script>
</head>
<body>
<div id="panel">
  <h5 class="head">什么是JQuery</h5>
  <div class="content">
    内容
  </div>
  <button>触发h5</button>
</div>
</body>
</html>
```

#### 事件的冒泡

- 基本概念：事件的冒泡是指，父子元素同时监听同一个事件。当触发子元素的事件的时候，同一个事件也被传递到了父元素的事件里去响应。
- 阻止冒泡：子元素中返回return false

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
  <script src="http://code.jquery.com/jquery-1.7.2.min.js"></script>
  <script type="text/javascript">
    $(function () {
      $("#content").click(function () {
        alert("div");
      });
      $("span").click(function () {
        alert("span");
        return false;
      });

    })

  </script>
</head>
<body>
<div id="content">
  外层div元素
  <span>
    内层span元素
  </span>
</div>

</body>
</html>
```

#### 获取javaScript 事件对象

- 基本概念：事件对象，是封装有触发的事件信息的一个javascript 对象。重点关心怎么获取和使用。

- 获取

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
  <style type="text/css">
    #aDiv{
      width: 1000px;
      height: 100px;
      background-color: #b3d4fc;
    }
  </style>
  <script src="http://code.jquery.com/jquery-1.7.2.min.js"></script>
  <script type="text/javascript">
      // 1.原生javascript获取 事件对象
      // window.onload = function () {
      //   document.getElementById("aDiv").onclick = function (event) {
      //     console.log(event);
      //   }
      // }
      // 2.JQuery代码获取 事件对象
      $(function () {
        $("#aDiv").click(function (event) {
          console.log(event);
        });
        // 使用bind同时对多个事件绑定同一个函数。怎么获取当前操作是什么事件。
        $("#aDiv").bind("click mouseover mouseout", function (event) {
          if (event.type == "click") {
            console.log("点击");
          } else if (event.type == "mouseover") {
            console.log("移入");
          } else if (event.type == "mouseout") {
            console.log("移出");
          }
        })
      });

  </script>
</head>
<body>
<div id="aDiv">Div1</div>
<div id="content">Div2</div>
</body>
</html>
```

- 练习：图片跟随

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
  <script src="http://code.jquery.com/jquery-1.7.2.min.js"></script>
  <script type="text/javascript">
    $(function () {
      $("#small").bind("mouseover mouseout mousemove", function (event) {
        if (event.type == "mouseover") {
          $("#showBig").show();
        } else if (event.type == "mouseout") {
          $("#showBig").hide();
        } else if (event.type == "mousemove") {
          $("#showBig").offset({
            left: event.pageX + 10, // + 10 避免出现频闪，浏览器误以为鼠标出去
              top:event.pageY + 10,
          })
        }
      })
    })

  </script>
</head>
<body>
<img id="small" src="偏振振幅图像.jpg"/>
<div id="showBig">
  <img src="偏振振幅图像.jpg"/>
</div>

</body>
</html>
```



### 补充：正则表达式(RegExp)

- 具体规则可以查询菜鸟教程：JavaScript RegExp -- [JavaScript 正则表达式 | 菜鸟教程 (runoob.com)](https://www.runoob.com/js/js-regexp.html)

- 中括号

1. 查找括号内的任何字符的一个

- 元字符：[正则表达式 – 元字符 | 菜鸟教程 (runoob.com)](https://www.runoob.com/regexp/regexp-metachar.html)

1. \w： 匹配字母、数字、下划线。等价于/A-Za-z0-9_/。
2. \W：匹配非字母、数字、下划线。等价于 / ^A-Za-z0-9_ /。
3. +：匹配前面的子表达式一次或多次。例如，'zo+' 能匹配 "zo" 以及 "zoo"，但不能匹配 "z"。+ 等价于 {1,}。
4. ' * '：匹配前面的子表达式零次或多次。例如，zo* 能匹配 "z" 以及 "zoo"。* 等价于{0,}。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>正则表达式</title>
    <script type="text/javascript">
        // 1.创建RegExp对象
        var re1 = new RegExp("[abc]");
        // alert(re1);
        // alert(re2);
        // 2. 快捷创建
        var re2 = /[a-d]/; // a-d
        var re3 = /[a-z]/; // 小写字母
        // alert(re1.test(str));
        // alert(re2.test(str));
        // 元字符
        // var patt = /a+/;
        // 表示要求 字符串中是否 *包舍* 零个 或 多个a
        // var patt = /a*/;
        // 表示要求 字符串是否包舍一个或零个a
        // var patt = /a?/;
        // 表示要术 字符串是否包含连续三个a
        // var patt = /a{3}/;
        // 表示要求 字符串是否包至少3个连续的，最多5个连续的a
        // var patt = /a{3,5}/;
        // 表示要 字符事是否包 至少3个连续的a，最多5个连续的a
        // var patt /a{3,5}/;
        // 表示要求 字符串是否包 至少3个连续的a
        // var patt = /a{3,}/;
        // 表示要求 字符事必须以a结尾
        // var patt = /a$/;
        // 表示要 字符串必须以开头
        // var patt = /^a/;
        // 要求字符串，从头到尾都必须完全匹配
        var patt = /^a{3,5}$/;
        var str = "aaaa";
        alert(patt.test(str));

    </script>
</head>
<body>
</body>
</html>
```

# 书城项目：相关技术

## XML

- 什么是 xml

xml是**可扩展**的标记性语言

- xmI 的作用

1. 用来保存数据，而且这些数据具有自我描述性
2. 它还可以做为项目或者模块的配置文件
3. 还可以做为网络传输数据的格式(现在主要是JSON)。

<img src=".\JavaWeb_Markdown笔记图片\xml.png" alt="xml" style="zoom: 80%;" />

### XML的语法

- 基本内容

1. 文档声明

```xml
<?xml version="1.0" encoding="utf-8" ?>
<!--
xml的声明文件
version 版本
encoding 编码-->
<books>
  <book sn="SN123123123123123">
    <name>西游记</name>
    <auther>吴承恩</auther>
    <price>99</price>
  </book>
  <book sn="SN123123123123124">
    <name>三国演义</name>
    <auther>罗贯中</auther>
    <price>99</price>
  </book>
<!--支持单标签和双标签-->
  <book sn="SN123123123123125" name="红楼梦" auther="曹雪芹" price="99"/>
</books>

```

2. XML属性
   - xml 的标签属性和 html 的标签属性是非常类似的，**属性以提供元素的额外信息**
   - 在标签上可以书写属性:一个标签上可以书写多个属性。每个属性的值必须使用 **引号** 引起来的**规则和标签的书写规则一致**。

3. 元素(标签)
   - html标签:
     - 格式：<标签名>封装的数据</标签名>
     - 单标签：<标签名 /> < br /> 行 < hr />水平线
     - 双标签：<标签名>封装的数据</标签名>
     - 标签名大小写不敏感
     - 标签有属性，有基本属性和事件属性
     - 标签要闭合(不闭合 ，html 中不报错。但我们要养成良好的书写习惯，闭合标签。)
   - XML 元素：
     - XML元素指的是从(且包括)开始标签直到(且包括)结束标签的部分。
     - 元素可包含其他元素、文本或者两者的混合物。元素也可以拥有属性。
   - XML 命名规则
     - 名称可以含字母、数字以及其他的字符
     - 名称不能以数字或者标点符号开始
     - 名称不能以字符"xml"(或者 XML、Xml)开始(可以通过语法检验)
     - 名称不能包含空格

4. XML注释：和HTML一样

5. 文本区域(CDATA区)

   - CDATA 格式：

     ```xml
     <![CDATA[这里可以把你输入的字符原样显示,不会解析xml]]>
     ```


6. 其他规则：

   - 所有 XML 元素都须有关闭标签 (也就是闭合)

   - XML：标签对大小写敏感

   - XML：必须正确地套

   - XML：文档必须有根元素（根元素就是顶级元素，没有父标签/唯一一个）

   - XML：中的特殊字符

     ```xml
     <name>&lt;三国演义&gt;</name>
     ```

- xml 解析技术

1. xml 可扩展的标记语言。不管是 html 文件还是 xml 文件它们都是标记型文档，都可以使用 w3c 组织制定的 **dom 技术**来解析。
2. document 对象表示的是整个文档(可以是 htm 文档，也可以是 xml 文档)

![xml解析技术](.\JavaWeb_Markdown笔记图片\xml解析技术.png)

## dom4j解析技术(重点)

- dom4j安装

1. 官网下载
2. 在Java项目中添加jar包：创建lib目录--拷贝jar包--右键--add as Lib

- 案例

```java
import org.dom4j.Document;
import org.dom4j.DocumentException;
import org.dom4j.Element;
import org.dom4j.io.SAXReader;

import java.util.List;

public class Dom4jTest {
  public static void main(String[] args) throws DocumentException {
    test2();
  }
  public static void test() throws DocumentException {
    // 创建一个saxReader输入流，去读取 xml配置文件，生成Document对象
    SAXReader saxReader = new SAXReader();
    Document document = saxReader.read("_05_book_static/src/books.xml");
    System.out.println(document);
  }
  public static void test2() throws  DocumentException {
    //1 读取books.xml文件
    //2 通过Document对象获取根元素
    //3 通过根元事获取book标签对象
    //4 遍历，处理每个book标签转换为Book类
    SAXReader saxReader = new SAXReader();
    Document document = saxReader.read("_05_book_static/src/books.xml");
    Element rootElement = document.getRootElement();
    // element()和elements()都是通过标签名查找子元素
    List books = rootElement.elements("book");
    for (Object book: books) {
      Element bookEle = (Element) book;
      // asXML()把标签对象。转换为标签字符串
      Element nameElement = bookEle.element("name");
      // getText();可以获取标签中的文本内容
      System.out.println(nameElement.getText());
      // 直接 获取指定标标签的文本内容
      String price = bookEle.elementText("price");
      System.out.println(price);
      // 获取属性内容
      String sn = bookEle.attributeValue("sn");
      System.out.println(sn);
    }
  }
}
```

## Tomcat

### JavaWeb

- 基本概念：

1. Javaweb 是指，所有通过Java语言编写可以通过浏览器访问的程序的总称，叫JavaWeb。
2. Javaweb 是基于请求和响应来开发的。

- 请求：请求是指客户端给服务器发送数据，叫请求 Request。
- 响应：响应是指服务器给客户端回传数据，叫响应 Response。

- 请求和响应的关系：成对出现。

### Web资源的分类

- web 资源按实现的技术和呈现的效果的不同，又分为静态资源和动态资源两种。

1. 静态资源：html、css、js、txt、mp4视频，jpg 图片

2. 动态资源：jsp 页面、Servlet 程序

### 常用的 web服务器

1. Tomcat:由 Apache 组织提供的一种 Web服务器，提供对jsp和 servet 的支持。它是一种轻量级的 javaweb容器(服务
   器)也是当前应用最广的 Javaweb服务器(免费)。
2. Jboss
3. GlassFish
4. Resin
5. WebLogic

### Tomcat 服务器和Servlet 版本的对应关系

- Servlet 程序从2.5版本是现在世面使用最多的版本(xml配置)
- 到了 servet3.0 之后。就是注解版本的 servlet 使用。

![Tomcat和Servlet的版本关系](C:\Users\97359\Desktop\Java学习_24_3_28\JavaWeb\JavaWeb_Markdown笔记\JavaWeb_Markdown笔记图片\Tomcat和Servlet的版本关系.png)

### Tomcat 的使用

- 安装：下载直接解压即可
- 目录介绍

1. bin	专门用来存放 Tomcat 服务器的可执行程序
2. conf	专门用来存放 Tocmat 服务器的配置文件
3. lib	专门用来存放 Tomcat 服务器的jar 包
4. logs	专门用来存放 Tomcat 服务器运行时输出的日记信息
5. temp	专门用来存放 Tomcdat 运行时产生的临时数据
6. webapps	专门用来存放部署的 web 工程。
7. work	是 Tomcat 工作时的目录，用来存放 Tomcat 运行时 jsp 翻译为 servlet 的源码，和 session 钝化的目录。

- 如何启动 Tomcat 服务器:

1. 找到 Tomcat 目录下的 bin 目录下的 startup.bat文件，双击，就可以启动 Tomcat服务器
2. 如何测试 Tomcat 服务器启动成功
   - 打开浏览器，在浏览器地址栏中输入以下地址测试:
     - http://localhost:8080
     - http://127.0.0.1:8080
     - http://真实ip地址:8080
   - 出现公猫界面则启动成功

- 常见的启动失败的情况有：

1. 双击 startup.bat文件，出现一个小黑窗口一闪而过。原因：JAVA_HOME环境变量配置出错
   - JAVA_HOME全部大写
   - 中间必须下划线_
   - 路径到JDK的安装目标，不用到bin目录

- 命令行启动 Tomcat 服务器

1. 打开命令行窗口
2. cd 到Tomcat的安装目录
3. catalina run

- 停止Tomcat服务

1. bin目录下的shutdown.bat运行
2. 关闭命令行启动的窗口(ctrl + c)

- 如何修改 Tomcat 的端口号

1. Mysql默认的端口号是:3306

2. Tomcat默认的端口号是:8080

   - 找到 Tomcat 目录下的 conf目录，找到 server.xml配置文件。

   - server.xml文件中，Connector标签下的 port属性
   - 修改完端口号需要重启服务
   - http协议的默认端口号是80

- 如何部暑 web 工程到 Tomcat 中

1. 方法一：只需要把 web 工程的目录拷贝到 Tomcat 的 webapps 目录下即可。
   - 在 webapps 目录下创建一个 book 工程:
   - 把web内容放在 book 的工程文件下
   - 访问

2. 方法二：创建配置文件

   - 找到tomcat安装目录下/conf/catalina/localhost

   - 创建.xml配置文件

     ```xml
     <!-- Context表示一个工程上下文
     path表示工程的访问路径:/abc
     docBase表示你的工程目录在哪里
     -->
     ```

   - 此时访问地址：[注册页面](http://localhost:8080/abc/pages/registry.html)

- 文件打开网页(网页文件拖入浏览器)和访问地址打开网页的区别

1. 文件打开网页：使用的协议是file://协议。
   - file协议表示告诉浏览器直接读取file:协议后面的路径，解析展示在浏览器上即可。
2. 浏览器打开：使用http协议解析

![http解析原理示意](.\JavaWeb_Markdown笔记图片\http解析原理示意.png)

- Root工程访问/index.html页面的访问

1. 网页的默认页面就是：Root工程的页面
   - http://ip:port/ 没有工程名默认是root工程
2. 访问的工程页面：默认是index.html页面
   - http://ip:port/工程名/

### IDEA整合Tomcat服务器

- IDEA添加服务：setting-BED-Application Servers
- IDEA创建服务器工程

1. 创建一个新模块-new-Module-Java Enterprise 或者 手动添加 Java EE的支持
2. web项目目录

![web工程目录](.\JavaWeb_Markdown笔记图片\web工程目录.png)

- 给Tomcat添加Jar包

1. 方法1：直接复制到lib目录下添加Lib
2. 方法2：Project Structure --  project setting -- Modules -- 选择项目 -- dependencies 添加Lib

3. 方法3：Project Structure --  project setting -- Libraries 创建类库 -- 浏览选择需要的jar包 -- 选择需要添加到的模块 -- 在Artifacts中 fix

- 在IDEA中运行Tomcat服务

1. Edit configuration中添加Tomcat的运行环境
2. url设置默认地址
3. deployment设置工程
4. 选择Tomcat配置以后，调试和运行方法和Java程序一样

- IDEA创建Tomcat项目：参考教程

[IDEA创建Web项目配置Tomcat(详细版)_idea web工程 tmocat-CSDN博客](https://blog.csdn.net/QAZJOU/article/details/121097745)

- 修改配置

1. 修改工程访问路径：Application context 通常保持和文件名一致
2. 修改运行的端口号
3. 修改运行使用的浏览器
4. 配置资源热部署
   - 文件修改网页马上就跟着变化：选择 On frame deactivation:Update classes and resources

## Servlet技术

- 基本概念

1. Servlet 是 JavaEE规范之一。规范就是接口
2. Servlet 就 JavaWeb 三大组件之一。三大组件分别是:servet 程序、Filter 过滤器、Listener 监听器。
3. Servet 是运行在服务器上的一个 Java小程序，它**可以接收客户端发送过来的请求，并响应数据给客户端**。

- 创建Servlet程序

```java
package com.uestc.servlet;


import javax.servlet.*;
import java.io.IOException;

public class HelloServlet implements Servlet {
  @Override
  public void init(ServletConfig servletConfig) throws ServletException {

  }

  @Override
  public ServletConfig getServletConfig() {
    return null;
  }

  /**
   * service方法
   * @param servletRequest
   * @param servletResponse
   * @throws ServletException
   * @throws IOException
   */
  @Override
  public void service(ServletRequest servletRequest, ServletResponse servletResponse) throws ServletException, IOException {
    System.out.println("Hello Servlet 被访问");
  }

  @Override
  public String getServletInfo() {
    return null;
  }

  @Override
  public void destroy() {

  }
}
```

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0">

  <servlet>
<!--servlet-name 标签 起别名 一般是类名-->
    <servlet-name>HelloServlet</servlet-name>
    <!--servlet-class 是全类名-->
    <servlet-class>com.uestc.servlet.HelloServlet</servlet-class>
  </servlet>
<!--servlet-mapping  给servlet程序配置访问地址-->
  <servlet-mapping>
<!--  servlet-name  使用该地址的servlet程序名  -->
    <servlet-name>HelloServlet</servlet-name>
<!--  url-pattern标签  配置访问地址
  /斜杠在服务器解析的时候，表示地址为:http://ip:port/工程路径
  /hello 表示地址为:http://ip:port/工程路径/hello
  -->
    <url-pattern>/hello</url-pattern><!--不以斜杠开头会报错-->
  </servlet-mapping>


</web-app>
```

常见错误：

1. url-pattern 内容没有以 / 开头
2. servlet-name 对应的内容不存在/不对应
3. servlet-class 类名出错

解析流程：

![Servlet工程的解析流程](.\JavaWeb_Markdown笔记图片\Servlet工程的解析流程.png)

- Servlet 的生命周期

1. 执行 servlet 构造器方法
2. 执行 init 初始化方法
3. 执行 service 方法
4. 执行 destroy 销毁方法

注意：

1. 第1、2步，是在第一次访问的时候创建 servet 程序会调用。
2. 第3步，每次访问都会调用
3. web程序终止时，执行第4步

- 请求的分发处理

1. service方法需要分别处理post和get请求

```java
package com.uestc.servlet;


import javax.servlet.*;
import javax.servlet.http.HttpServletRequest;
import java.io.IOException;

public class HelloServlet implements Servlet {
  public HelloServlet() {
    System.out.println("1 构造器方法");
  }

  @Override
  public void init(ServletConfig servletConfig) throws ServletException {
    System.out.println("2 初始化方法");
  }

  @Override
  public ServletConfig getServletConfig() {
    return null;
  }

  /**
   * service方法
   * @param servletRequest
   * @param servletResponse
   * @throws ServletException
   * @throws IOException
   */
  @Override
  public void service(ServletRequest servletRequest, ServletResponse servletResponse) throws ServletException, IOException {
    System.out.println("3 Hello Servlet 被访问");
    // 类型转换(因为子接口有getNethod()方法)
    HttpServletRequest httpServletRequest = (HttpServletRequest) servletRequest;
    if ("POST".equals(httpServletRequest.getMethod())) {
      doPost();
    } else if ("GET".equals(httpServletRequest.getMethod())) {
      doGet();
    }
  }
  public void doGet() {
    System.out.println("POST 请求");
  }
  public void doPost() {
    System.out.println("GET 请求");
  }

  @Override
  public String getServletInfo() {
    return null;
  }

  @Override
  public void destroy() {
    System.out.println("4 销毁方法");
  }
}
```

- 实际的开发过程通常不继承servlet，通常使用servlet的子接口或者子类(参考开发说明)

1. 一般在实际项目开发中，都是使用继承 **Httpservlet 类**的方式去实现 servlet 程序。
   - 编写一个类去继承 Httpservlet 类
   - 根据业务需要重写 doGet或 doPost 方法
   - 到 web.xml中的配置 servet 程序的访问地址

- 使用IDEA创建servlet工程

new -- module -- creat servlet (idea里没有怎么解决？？？)

- servlet的继承体系

![servlet继承体系](.\JavaWeb_Markdown笔记图片\servlet继承体系.png)

### ServletConfig 类

- 基本内容：

1. Servlet 程序的配置信息类
2. Servlet 程序和 servletconfg 对象都是由 Tomcat 负责创建，我们负责使用。
3. Servlet 程序默认是第一次访问的时候创建，servletconfig是每个 servlet 程序创建时，就创建一个对应的 servletconfig对象
   - 每个Servlet 程序都有独立的servletconfig -- 关联自己的Servlet 程序

- ServletConfig 类的三大作用

1. 可以获取 servlet 程序的别名 servlet-name 的值
2. 获取初始化参数 init-param
3. 获取 ServletContext 对象

```java
System.out.println("程序别名" + servletConfig.getServletName());
System.out.println("初始化参数" + servletConfig.getInitParameter("username"));
System.out.println("ServletContext 对象" + servletConfig.getServletContext());
```

- 注意事项

1. 通过继承HttpServlet(或相关类)实现的servlet 程序，重写init方法一定要调用父类的init方法

### ServletContext 类

- 基本概念

1. Servetcontext是一个接口，它表示 servet 上下文对象
2. 一个 web工程，只有一个 ServletContext 对象实例(打印地址查看)。
3. servetContext 对象是一个**域对象**。
4. servletContext是在 web工程部署启动时创建。在 web 工程停止时销毁。
   - 不同的servlet均可以操作servletContext

- 什么是域对象

1. 域对象，是可以像 Map 一样存职数据的对象，叫域对象。
2. 这里的域指的是存取数据的操作范围。**操作范围：整个web工程**。

![域对象和Map](.\JavaWeb_Markdown笔记图片\域对象和Map.png)

- Servletcontext类的四个作用

1. 获取web.xml中配置的上下文参数 context-param
2. 获取当前的工程路径，格式:/工程路径
3. 获取工程部署后在服务器硬盘上的绝对路径
4. 像 Map一样存取数据

```xml
<!--web.xml 文件下的内容-->  
<!--context-param是上下文参数(它属于整个veb工程)-->
  <context-param>
    <param-name>username</param-name>
    <param-value>context</param-value>
  </context-param>
  <context-param>
    <param-name>password</param-name>
    <param-value>a123456</param-value>
  </context-param>
<servlet>
    <servlet-name>ContextServlet1</servlet-name>
    <servlet-class>com.uestc.servlet.ContextServlet1</servlet-class>
  </servlet>
  <servlet-mapping>
    <servlet-name>ContextServlet1</servlet-name>
    <url-pattern>/contextServlet1</url-pattern>
  </servlet-mapping>
```

```java
/**
1. 获取web.xml中配置的上下文参数 context-param
2. 获取当前的工程路径，格式:/工程路径
3. 获取工程部署后在服务器硬盘上的绝对路径
*/
package com.uestc.servlet;

import javax.servlet.ServletContext;
import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

public class ContextServlet extends HttpServlet {
  @Override
  protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    super.doGet(req, resp);
    // 获取上下文参数
    ServletContext context = getServletConfig().getServletContext();
    System.out.println("配置信息 1："+context.getInitParameter("username"));
    System.out.println("配置信息 2："+context.getInitParameter("password"));
    // 获取工程路径
    System.out.println("当前工程路径：" + context.getContextPath());
    // 获取服务部署的绝对路径
    // "/" 被服务器解析为 http://ip:port/工程名
    // web目录下的 文件都会被拷贝都绝对路径下
    System.out.println("绝对路径：" + context.getRealPath("/"));
  }

  @Override
  protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    super.doPost(req, resp);
  }
}
```

```java
package com.uestc.servlet;

import javax.servlet.ServletContext;
import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

public class ContextServlet1 extends HttpServlet {
  @Override
  protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    super.doGet(req, resp);
    // 底层就是ServletContext context = getServletConfig().getServletContext();
    ServletContext context = getServletContext();
    // 增加数据
    context.setAttribute("key1", "value1");
    // 获取数据
    System.out.println("key1的数据为：" + context.getAttribute("key1"));
  }
}
```

### HTTP协议

- 什么是协议：协议是指双方，或多方，相互约定好，大家都需要遵守的规则，叫协议。
- HTTP协议：

1. 客户端和服务器之间通信时，发送的数据，需要遵守的规则，叫HTTP 协议。
2. HTTP协议中的数据又叫报文。

- 请求的 HTTP 协议格式

1. 客户端给服务器发送数据叫请求。
   - 请求又分为 GET请求，和 POST 请求两种
2. 服务器给客户端回传数据叫响应。

- GET请求

1. 请求行
   - (1) 请求的方式	GET
   - (2)请求的资源路径[+?+请求参数]	
   - (3)请求的协议的版本号	HTTP/1.1

2. 请求头
   - key : value组成	不同的键值对，表示不同的含义。

![HTTP协议的GET请求](.\JavaWeb_Markdown笔记图片\HTTP协议的GET请求.png)

- POST请求

1. 请求行
   - (1)请求的方式	POST
   - (2)请求的资源路径[+?+请求参数]	
   - (3)请求的协议的版本号	HTTP/1.1
2. 请求头
   - key : value组成	不同的键值对，表示不同的含义。
3. 请求体===>>>就是发送给服务器的数据

![HTTP协议的POST请求](.\JavaWeb_Markdown笔记图片\HTTP协议的POST请求.png)

- 常用请求头	

1. Accept:	表示客户端可以接收的数据类型
2. Accpet-Languege:	表示客户端可以接收的语言类型
3. User-Agent:	表示客户端浏览器的信息
4. Host:	表示请求时的服务器ip 和端口号

- 区分GET请求和POST请求

1. GET请求
   - 1、form标签 method=get
   - 2、a标签
   - 3、link 标签引入 css
   - 4、script 标签引入js文件
   - 5、img标签引入图片
   - 6、iframe引入 html页面
   - 7、在浏览器地址栏中输入地址后敲回车
2. POST请求
   - form标签 method=post

- 响应的 HTTP 协议格式

1. 响应行
   - (1)响应的协议和版本号
   - (2)响应状态码
   - (3)响应状态描述符
2. 响应头
   - (1) key : value	不同的响应头，有其不同含义
     **空行**
3. 响应体	回传给客户端的数据

![HTTP响应](.\JavaWeb_Markdown笔记图片\HTTP响应.png)

- 常见的响应码

1. 200	表示请求成功
2. 302	表示请求重定向
3. 404	表示请求服务器已经收到，但是需要的数据不存在(请求地址错误)
4. 500	表示服务器已经收到请求，但是服务器内部错误(代码错误)

- MIME 类型说明

1. MIME是 HTTP 协议中数据类型。
2. MIME的英文全称是"Multipurpose Internet Mail Extensions"多功能 Internet 邮件扩充服务。
3. MIME类型的格式是“大类型/小类型”，并与某一种文件的扩展名相对应。
4. 常见的MIME类型

![MIME常见的类型](.\JavaWeb_Markdown笔记图片\MIME常见的类型.png)

- EDGE浏览器查看HTTP协议

1. F12打开开发者界面
2. 标头查看：响应标头 请求头 相关参数
3. 响应：查看响应体

### HttpServletRequest类

- 作用

1. 每次只要有请求进入 Tomcat 服务器，Tomcat 服务器就会把请求过来的 HTTP 协议信息解析好封装到 Request 对象中。
2. 然后传递到 service方法(doGet和 doPost)中给我们使用。我们可以通过 HttpServetRequest 对象，获取到所有请求的信息。

- 常用方法

1. getRequestURI()	获取请求的资源路径
2. getRequestURL()	获取请求的统一资源定位符(绝对路径)
3. getRemoteHost()	获取客户端的 ip 地址
4. getHeader()	获取请求头
5. getParameter()	获取请求的参数
6.  getParameterValues()	获取请求的参数(多个值的时候使用)
7. getMethod()	获取请求的方式 GET 或 POST
8. setAttribute(key,value);	设置域数据
9. getAttribute(key);	获取域数据
10. getRequestDispatcher()	获取请求转发对象


- 案例

```java
package com.uestc.servlet;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

public class RequestAPIServlet extends HttpServlet {
  @Override
  protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    super.doGet(req, resp);
    System.out.println("URI:" + req.getRequestURI());
    System.out.println("URL:" + req.getRequestURL());
    // localhost访问 http://localhost:8080/_07_servlet/requestAPIServlet
    // 127.0.0.1访问 http://127.0.0.1:8080/_07_servlet/requestAPIServlet
    // 真实ip访问 http://113.54.206.237:8080/_07_servlet/requestAPIServlet
    System.out.println("Host ip:" + req.getRemoteHost());
    System.out.println("请求头:" + req.getHeader("user-Agent"));
    System.out.println("请求方式:" + req.getMethod());

  }
}
```

```java
package com.uestc.servlet;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;
import java.util.Arrays;

public class ParameterServlet extends HttpServlet {
  @Override
  protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    super.doGet(req, resp);
    String username = req.getParameter("username");
    String password = req.getParameter("password");
    String[] hobby = req.getParameterValues("hobby"); // 多个参数时使用
    System.out.println("用户名" + username);
    System.out.println("密码" + password);
    System.out.println("hobby" + Arrays.toString(hobby));
  }

  @Override
  protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    super.doPost(req, resp);
    System.out.println("-----------------------------------------Post");
      // 在获取请求参数前调用才可以生效
    req.setCharacterEncoding("UTF-8"); // 防止post请求中文乱码
    String username = req.getParameter("username");
    String password = req.getParameter("password");
    String[] hobby = req.getParameterValues("hobby"); // 多个参数时使用
    System.out.println("用户名" + username);
    System.out.println("密码" + password);
    System.out.println("hobby" + Arrays.toString(hobby));

  }
}
```

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0">
  <servlet>
    <servlet-name>RequestAPIServlet</servlet-name>
    <servlet-class>com.uestc.servlet.RequestAPIServlet</servlet-class>
  </servlet>
  <servlet-mapping>
    <servlet-name>RequestAPIServlet</servlet-name>
    <url-pattern>/requestAPIServlet</url-pattern>
  </servlet-mapping>
  <servlet>
    <servlet-name>ParameterServlet</servlet-name>
    <servlet-class>com.uestc.servlet.ParameterServlet</servlet-class>
  </servlet>
  <servlet-mapping>
    <servlet-name>ParameterServlet</servlet-name>
    <url-pattern>/parameterServlet</url-pattern>
  </servlet-mapping>
</web-app>
```

#### 请求转发

- 什么是请求的转发?

1. 请求转发是指，服务器收到请求后，从一次资源跳转到另一个资源的操作叫请求转发。
2. 请求转发，图示

![请求转发](.\JavaWeb_Markdown笔记图片\请求转发.png)

- 请求转发的特点

1. 浏览器地址栏没有变化
2. 他们是同一次请求
3. 他们共享Request域中的数据
4. 可以转发到WEB-INF目录下
5. 不能访问工程以外的资源

```java
package com.uestc.servlet;

import javax.servlet.RequestDispatcher;
import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

public class Servlet1 extends HttpServlet {
  @Override
  protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    String username = req.getParameter("username");
    System.out.println("servlet1中的参数:" + username);
    req.setAttribute("key1", "servlet1 标签");
    // 转发请求要以/ 开头, / 表示地址: http://ip:port/工程名/ 映射为web目录
    RequestDispatcher requestDispatcher = req.getRequestDispatcher("/servlet2");
    requestDispatcher.forward(req, resp);
    return;
  }
}
```

```java
package com.uestc.servlet;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

public class Servlet2 extends HttpServlet {
  @Override
  protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    String username = req.getParameter("username");
    System.out.println("Servlet2中的参数" + username);
    Object key1 = req.getAttribute("key1");
    System.out.println("Servlet2中查看servlet1中的参数" + key1);
    // 添加自己的业务
    System.out.println("servlet2的业务");
    return;
  }
}
```

```xml
  <servlet>
    <servlet-name>Servlet1</servlet-name>
    <servlet-class>com.uestc.servlet.Servlet1</servlet-class>
  </servlet>
  <servlet-mapping>
    <servlet-name>Servlet1</servlet-name>
    <url-pattern>/servlet1</url-pattern>
  </servlet-mapping>

  <servlet>
    <servlet-name>Servlet2</servlet-name>
    <servlet-class>com.uestc.servlet.Servlet2</servlet-class>
  </servlet>
  <servlet-mapping>
    <servlet-name>Servlet2</servlet-name>
    <url-pattern>/servlet2</url-pattern>
  </servlet-mapping>
```

- base标签的作用

1. 引出base标签

<img src=".\JavaWeb_Markdown笔记图片\Base标签讲解1.png" alt="Base标签讲解1" style="zoom:67%;" />

2. 案例

```java
package com.uestc.servlet;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

public class ForwardC extends HttpServlet {
  @Override
  protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    System.out.println("抵达ForwardC程序");
    req.getRequestDispatcher("/a/b/c.html").forward(req, resp);

  }
}
```

```html
<!--index.html-->
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
</head>
<body>
这是Web下的index.html<br/>
<a href="a/b/c.html">a/b/c.html</a>
<a href="http://localhost:8080/_07_servlet/forwardC">转发请求</a>
</body>
</html>
```

```html
<!--a/b/c.html-->
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
<!--  base 标签设置 相对路径-->
<!-- 最后的资源名可以省略 http://localhost:8080/_07_servlet/a/b/  '/'不能省略 -->
  <base href="http://localhost:8080/_07_servlet/a/b/c.html">
</head>
<body>
  这是a下的b下的c.html页面<br/>
<a href="../../index.html">跳回首页</a><br/>
</body>
</html>
```

- Web 中的相对路径和绝对路径

1. 相对路径:
   - .	表示当前目录
   - ..	表示上一级目录
   - 资源名	表示当前目录/资源名
2. 绝对路径
   - http://ip:port/工程名/资源名

- web中/斜杠的不同意义

1. 在 web 中 /斜杠 是一种绝对路径。

   - 斜杠/ 如果被浏览器解析，得到的地址是:http://ip:port/

     ```html
     <a href="/">斜杠</a>
     ```

   - 斜杠/ 如果被服务器解析，得到的地址是:http://ip:port/工程路径

     ```xml
     <url-pattern>/servlet1</url-pattern>
     ```

     ```java
     servletContext.getRealPath("/");
     request.getRequestDispatcher("/");
     ```

     特殊情况：response.sendRediect("/");

     发给浏览器解析得到：http://ip:port/


### HttpServletResponse类

- 基本概念

1. HttpservletResponse 类和 HttpservletRequest类一样。每次请求进来，Tomcat服务器都会创建一个 Response 对象传递给 servet程序去使用。
2. HttpsenvletRequest表示请求过来的信息，HttpservletResponse表示所有响应的信息，如果需要设置返回给客户端的信息，都可以通过 HttpservletResponse 对象来进行设置。

- 两个输出流

1. 字节流：getoutputstream();常用于下载(传递二进制数据)
2. 字符流：getwrter();常用于回传字符串(常用)
3. 两个流同时只能使用一个。

- 客户端回传数据

1. 案例演示

2. 乱码

```java
package com.uestc.servlet;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;
import java.io.PrintWriter;

public class ResponseIOServlet extends HttpServlet {
  @Override
  protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    System.out.println(resp.getCharacterEncoding()); // ISO-8859-1 默认编码
    // 设置服务器字符集
    resp.setCharacterEncoding("UTF-8");
    // 通过响应头设置浏览器使用UTF-8
    resp.setHeader("Content-type", "text/html; charset=UTF-8");

    PrintWriter writer = resp.getWriter();
//    writer.write("response's content!!!");
    writer.write("广岛核弹");
  }
}
```

```java
// 同时设置服务器和客户端都使用UTF-8字符集，还设置了响应头
// 必须在获取流对象前使用
resp.setContentType("text/html; charset=UTF-8");
```

#### 请求重定向

- 基本概念

1. 请求重定向，是指客户端给服务器发请求，然后服务器告诉客户端去新地址访问(因为之前的地址可能已经被废弃)。
2. 重新定向，逻辑解析

![请求重定向](.\JavaWeb_Markdown笔记图片\请求重定向.png)

- 实现案例1

```java
package com.uestc.servlet;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

public class Response1 extends HttpServlet {
  @Override
  protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    System.out.println("Response1 抵达");
    // 设置响应状态码 302, 表示重定向
    resp.setStatus(302);
    // 设置响应头
    resp.setHeader("Location", "http://localhost:8080/_07_servlet/response2");
  }
}
```

```java
package com.uestc.servlet;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;
import java.io.PrintWriter;

public class Response2 extends HttpServlet {
  @Override
  protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    PrintWriter writer = resp.getWriter();
    writer.write("response2's result!!!");
  }
}
```

- 实现案例2(推荐方法)

```java
resp.sendRedirect("http://localhost:8080/_07_servlet/response2");
```

- 请求重定向的特点

1. 浏览器地址栏会发生变化
2. 两次情求，不共享Request域中数据
3. 不能访问WEB-INF下的资源
4. 可以访问工程外的资源

## JavaEE的结构

- JavaEE的三层架构

![JavaEE的三层架构](.\JavaWeb_Markdown笔记图片\JavaEE的三层架构.png)

分层的目的是为了解耦。解耦就是为了降低代码的耦合度。方便项目后期的维护和升级。

- 通常的包分层结构

1. web 层	com.atguigu.web/servlet/controller

2. service 层	com.atguigu.serviceService	接口包

   ​						com.atguigu.service.impl	Service 接口实现类

3. dao 持久层	com.atguigu.dao	Dao接口包

   ​						com.atguigu.dao.impl	Dao接口实现类

4. 实体 bean 对象	com.atguigu.pojo/entity/domain/beanJava	Bean 类

5. 测试包	com.atguigu.test/junit

6. 工具类	com.atguigu.utils

## 书城：开发

- 代码编写过程--思路

1. 创建数据库和表

```mysql
CREATE TABLE t_uesr(
`id` INT AUTO_INCREMENT PRIMARY KEY ,
`username` VARCHAR(20) NOT NULL UNIQUE,
`password` VARCHAR(32) NOT NULL,
`email` VARCHAR(100)
);

INSERT INTO t_uesr(`username`, `password`, `email`) VALUES('admin', 'admin', 'admin@uestc.com');

SELECT * FROM t_uesr
```

2. 编写数据库表对应的 JavaBean 对象

```java
package com.uestc.pojo;

public class user {
  private Integer id;
  private String username;
  private String password;
  private String email;

  @Override
  public String toString() {
    return "user{" +
      "id=" + id +
      ", username='" + username + '\'' +
      ", password='" + password + '\'' +
      ", email='" + email + '\'' +
      '}';
  }

  public user(Integer id, String username, String password, String email) {
    this.id = id;
    this.username = username;
    this.password = password;
    this.email = email;
  }

  public user() {
  }

  public Integer getId() {
    return id;
  }

  public void setId(Integer id) {
    this.id = id;
  }

  public String getUsername() {
    return username;
  }

  public void setUsername(String username) {
    this.username = username;
  }

  public String getPassword() {
    return password;
  }

  public void setPassword(String password) {
    this.password = password;
  }

  public String getEmail() {
    return email;
  }

  public void setEmail(String email) {
    this.email = email;
  }
}
```

3. 编写 工具类 JDBCUtils
   - 下载添加相应的Jar包，配置连接池文件

```java
package com.uestc.utils;
import com.alibaba.druid.pool.DruidDataSource;
import com.alibaba.druid.pool.DruidDataSourceFactory;

import javax.sql.DataSource;
import java.io.InputStream;
import java.sql.Connection;
import java.sql.SQLException;
import java.util.Properties;

public class JDBCUtils {
  private static DruidDataSource dataSource;
  static {
      try {

        Properties properties = new Properties();
        // 读取配置文件
        InputStream resourceAsStream = JDBCUtils.class.getClassLoader().getResourceAsStream("jdbc.properties");
        // 从输入流中加载数据
        properties.load(resourceAsStream);
        dataSource = (DruidDataSource) DruidDataSourceFactory.createDataSource(properties);
      } catch (Exception e) {
          throw new RuntimeException(e);
      }
  }
  // 返回null 获取连接失败
  public static Connection getConnection() {
    Connection connection = null;
    try {
      connection = dataSource.getConnection();
    } catch (SQLException e) {
      throw new RuntimeException(e);
    }
    return  connection;
  }
  public static void close(Connection connection) {
    if (connection != null) {
      try {
        connection.close();
      } catch (SQLException e) {
        throw new RuntimeException(e);
      }
    }
  }

}
```

```java
package com.uestc.test;

import com.uestc.utils.JDBCUtils;
import org.junit.Test;

import java.sql.Connection;

public class JdbcUtilsTest {
  @Test
  public void testJdbcUtils() {
    // 数据库的连接使用过后需要及时的释放
    for (int i=0; i < 100; i++) {
      Connection connection = JDBCUtils.getConnection();
      System.out.println(connection);
      JDBCUtils.close(connection);
    }
  }
}
```

4. 编写 BaseDAO

```java
package com.uestc.dao.impl;

import com.uestc.utils.JDBCUtils;
import org.apache.commons.dbutils.QueryRunner;
import org.apache.commons.dbutils.handlers.BeanHandler;
import org.apache.commons.dbutils.handlers.BeanListHandler;
import org.apache.commons.dbutils.handlers.ScalarHandler;

import java.sql.Connection;
import java.sql.SQLException;
import java.util.List;

public abstract class BaseDao {
  // 使用 DbUtils
  private QueryRunner queryRunner = new QueryRunner();
  // update 方法用来执行Insert/Update/Delete语句
  // 返回-1表示执行失败
  public int update(String sql, Object ...args){
    Connection connection = JDBCUtils.getConnection();
    try {
      queryRunner.update(connection, sql, args);
    } catch (SQLException e) {
      throw new RuntimeException(e);
    } finally {
      JDBCUtils.close(connection);
    }
    return -1;
  }
  public <T> T queryForOne(Class<T> type, String sql, Object ...args) {
    Connection connection = JDBCUtils.getConnection();
    try {
      return queryRunner.query(connection, sql, new BeanHandler<T>(type), args);
    } catch (SQLException e) {
      throw new RuntimeException(e);
    } finally {
      JDBCUtils.close(connection);
    }
  }
  public <T> List<T>  queryForList(Class<T> type, String sql, Object ...args) {
    Connection connection = JDBCUtils.getConnection();
    try {
      return queryRunner.query(connection, sql, new BeanListHandler<T>(type), args);
    } catch (SQLException e) {
      throw new RuntimeException(e);
    } finally {
      JDBCUtils.close(connection);
    }
  }
  // 返回一行一列的语句
  public Object queryForSingleValue(String sql, Object ...args) {
    Connection connection = JDBCUtils.getConnection();
    try {
      return queryRunner.query(connection, sql, new ScalarHandler<>(), args);
    } catch (Exception e) {
      throw new RuntimeException(e);
    } finally {
      JDBCUtils.close(connection);
    }
  }
}
```

- 编写UserDao和测试

```java
package com.uestc.dao.impl;

import com.uestc.dao.UserDao;
import com.uestc.pojo.User;

public class UserDaoImpl extends BaseDao implements UserDao {
  @Override
  public User queryUserByUsername(String username) {
    String sql = "select `id`,`username`, `password`, `email` from t_user where username = ?";
    return queryForOne(User.class, sql, username);
  }

  @Override
  public User queryUserByUsernameAndPassword(String username, String password) {
    String sql = "select `id`,`username`, `password`, `email` from t_user where username = ? and password = ?";
    return queryForOne(User.class, sql, username, password);
  }

  @Override
  public int saveUser(User user) {
    String sql = "INSERT INTO t_user(`username`, `password`, `email`) VALUES(?, ?, ?)";
    return update(sql,user.getUsername(), user.getUsername(), user.getEmail());
  }
}
```

```java
package com.uestc.test;

import com.uestc.dao.UserDao;
import com.uestc.dao.impl.UserDaoImpl;
import com.uestc.pojo.User;
import org.junit.Test;

import static org.junit.Assert.*;

public class UserDaoTest {
  UserDao userDao = new UserDaoImpl();
  @Test
  public void queryUserByUsername() {

    if (userDao.queryUserByUsername("admin") == null) {
      System.out.println("用户名可用/不存在");
    } else {
      System.out.println("用户名存在");
    }
  }

  @Test
  public void queryUserByUsernameAndPassword() {

    if (userDao.queryUserByUsernameAndPassword("admin", "admin") == null) {
      System.out.println("密码与用户名不符合");
    } else {
      System.out.println("查询成功");
    }
  }

  @Test
  public void saveUser() {
    System.out.println(userDao.saveUser(new User(null, "abc123", "abc111", "abc@uestc.com")));
  }
}
```

```java
package com.uestc.test;

import com.uestc.pojo.User;
import com.uestc.service.UserService;
import com.uestc.service.impl.UserServiceImpl;
import org.junit.Test;

import static org.junit.Assert.*;

public class UserServiceTest {
  UserService userService = new UserServiceImpl();

  @Test
  public void registUser() {
    userService.registUser(new User(null, "yh74112", "yh123", "yh74112@uestc.com"));
  }

  @Test
  public void login() {
    User testUser = new User(null, "abc123", "abc123", null);
    if (userService.login(testUser) == null) {
      System.out.println("用户名和密码不匹配");
    } else {
      System.out.println("用户名和密码匹配");
    }
  }

  @Test
  public void existUsername() {
    if (userService.existUsername("abc123")) {
      System.out.println("用户名存在/不可使用");
    } else {
      System.out.println("用户名不存在/可使用");
    }
  }
}
```

5. web编写

   - 编写的基本思路

     ![书城项目_web开发思路](.\JavaWeb_Markdown笔记图片\书城项目_web开发思路.png)

   - web开发阶段，使用base+相对路径

   - 框架开发阶段，使用绝对路径



- IDEA调试

1. 两个元素：断点和debug启动
2. 设置断点
3. debug启动

![idea调试1](.\JavaWeb_Markdown笔记图片\idea调试1.png)

![idea调试2](.\JavaWeb_Markdown笔记图片\idea调试2.png)

4. 变量窗口

![idea调试3](.\JavaWeb_Markdown笔记图片\idea调试3.png)

5. 方法栈窗口
   - 查看方法调用信息
   - 下面一行得方法调用上面一行得方法

![idea调试4](.\JavaWeb_Markdown笔记图片\idea调试4.png)

6. 其他调试按钮

![idea调试5](.\JavaWeb_Markdown笔记图片\idea调试5.png)

- 会员登录

1. 基本开发思路

![登录界面的开发](.\JavaWeb_Markdown笔记图片\登录界面的开发.png)



- 项目整体 -- 见项目工程

## JSP

- 基本概念：JSP的全称是 java serverpages(Java 的服务器页面)。

1. jsp的主要作用是代替 servlet 程序回传 html 页面的数据。
2. 因为 servlet 程序回传 html页面数据是一件非常繁锁的事情。开发成本和维护成本都极高。

![Servlet传输html页面](.\JavaWeb_Markdown笔记图片\Servlet传输html页面.png)

- 小结

1. 创建
2. 访问：访问方式和html页面一样，同样保存在web目录下面
   - a.html页面	访问地址是	http://ip:port/工程路径/a.html
   - b.jsp页面	访问地址是	http://ip:port/工程路径/b.jsp

- JSP的本质

1. jsp 页面本质上是一个 servlet 程序。
2. 当我们第一次访问 jp页面的时候。Tomcat服务器会帮我们把jp 页面翻译成为一个java 源文件。并且对它进行编译成为.class 字节码程序。打开 java 源文件:

![JSP源码](.\JavaWeb_Markdown笔记图片\JSP源码.png)

3. HttpJspBase 继承 HttpServlet

![JSP源码2](.\JavaWeb_Markdown笔记图片\JSP源码2.png)

4. JSP的底层Servlet源代码也是使用输出流把html页面传给客户端。

### JSP的语法

- JSP的头部page指令：jsp 的 page 指令可以修改jsp 页面中一些重要的属性，或者行为。

1. language 属性	表示jsp 翻译后是什么语言文件。暂时只支持java。
2. contentType 属性	表示jsp 返回的数据类型。对应源码中 response.setcontentType()。
   - contentType="text/html;charset=utf-8"
3. pageEncoding 属性	表示当前 jsp 页面文件本身的字符集。
4. import 属性	跟 java 源代码中一样。用于导包，导类。
5. autoFlush 属性	out输出流：设置当 out 输出流缓冲区满了之后,是否自动刷新冲级区。默认值是 true。
   - 不设置刷新，JSP文件内容过多，会导致缓冲区溢出。
6. buffer 属性	out输出流：设置 out 缓冲区的大小。默认是 8kb。
7. errorPage 属性	设置当 jsp 页面运行时出错，自动跳转去的错误页面路径。
8. isErrorPage 属性	设置当前 jsp 页面是否是错误信息页面。默认是 false。如果是 true 可以获取异常信息。
9. session 属性	设置访问当前 jsp 页面，是否会创建HttpSession 对象。默认是 true。
10. extends 属性	设置 jsp 翻译出来的 java 类默认继承的类。 // 通常不会修改

#### JSP中的常用脚本

- 声明脚本

1. 格式：<%! 声明Java代码 %>
2. 作用：可以给 jsp 翻译出来的java 类定义属性和方法甚至是静态代码块/内部类等

3. 案例演示：编译之后相应的class文件内部会添加对应的代码

```jsp
<%@ page import="java.util.Map" %>
<%@ page import="java.util.HashMap" %><%--
  Created by IntelliJ IDEA.
  User: 97359
  Date: 2024/4/26
  Time: 10:31
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
  <title>Title</title>
</head>
<body>
  html数据页面
<%--1. 声明类属性--%>
<%!
  private Integer id;
  private String name;
  private static Map<String, Object> map;
%>
  <%--2. 声明静态代码块--%>
<%! static {
  map = new HashMap<>();
  map.put("kay1", "value1");
  map.put("kay2", "value2");
}
%>
  <%--3. 声明类方法 --%>
  <%! public int sum(int i1, int i2){
    return i1+i2;
  }
  %>
  <%--4. 声明内部类 --%>
  <%! public static class A1{
    private String username;
  }
  %>
</body>
</html>
```

- 表达式脚本

1. 表达式脚本格式：<%= 表达式 %>

2. 表达式脚本的作用是:在jsp页面上输出数据。

3. 案例演示：

```jsp
<%@ page import="java.util.HashMap" %>
<%@ page import="java.util.Map" %><%--
  Created by IntelliJ IDEA.
  User: 97359
  Date: 2024/4/26
  Time: 15:24
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
  <title>Title</title>
</head>
<body>
<%!
  private static Map<String, Object> map = map = new HashMap<>();;
%>
<%--练习:
1.输出整型
2.输出浮点型
3.输出字符串
4.输出对象
--%>
<%=1%%>
<%=12.12%>
<%="字符串"%>
<%=map%>

</body>
</html>
```

- 表达式脚本的特点

1. 所有的表达式脚本都会被翻译到_jspservice()方法中
2. 表达式脚本都会被翻译成为 out.print() 输出到页面上
3. 由于表达式脚本翻译的内容都在 _jspservice() 方法中,所以 _jspservice()方法中的对象都可以直接使用。
4. 表达式脚本中的表达式不能以分号结束

```jsp
<%@ page import="java.util.HashMap" %>
<%@ page import="java.util.Map" %><%--
  Created by IntelliJ IDEA.
  User: 97359
  Date: 2024/4/26
  Time: 15:24
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
  <title>Title</title>
</head>
<body>
<%!
  private static Map<String, Object> map = map = new HashMap<>();;
%>
<%--练习:
1.输出整型
2.输出浮点型
3.输出字符串
4.输出对象
--%>
<%=12%>
<%=12.12%>
<%="字符串"%>
<%=map%>

<%=request.getParameter("username")%>

</body>
</html>
```

- 代码脚本

1. 代码脚本格式：<%Java语句%>

2. 案例演示

```jsp
<%--
  Created by IntelliJ IDEA.
  User: 97359
  Date: 2024/4/26
  Time: 15:57
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
  <title>Title</title>
</head>
<body>
<%--续习:--%)
<%--1.代码脚本----if 语句--%>
<%
int x=10;
if (x == 10) {
  System.out.println("正确的");
}
%>
<%--2.代码脚本----for 循环语句--%>
<%
for (int i=0; i < 10; i++) {
  System.out.println(i);
}
%>
<%--3.翻译后javdp文件中 jspservice方法内的代码都可以写/使用--%>
<% String username = request.getParameter("username");
  System.out.println(username);
%>
<%--4.多个代码脚本组合输出--%>
<table border="1" cellspacing="0">
  <%
    for (int j=0; j<10;j++) {
  %>
    <tr>
      <td>第 <%=j%> 行</td>
    </tr>
  <%
    }
  %>
</table>
</body>
</html>
```

- 代码脚本的特点是:

1. 代码脚本翻译之后都在_jspservice 方法中
2. 代码脚本由于翻译到 _ jspservice()方法中，所以在_jspservice()方法中的现有对象都可以直接使用。
3. 还可以由多个代码脚本块组合完成一个完整的java 语句。
4. 代码脚本还可以和表达式脚本一起组合使用，在jsp页面上输出数据

#### Jsp 中的三种注释

- html注释

1. <!-- 这是html 注释-->

2. html 注释会被翻译到 java 源代码中。在_spservice 方法里，以 out.writer输出到客户端。

- Java注释

1. // 单行注释
2. /* 多行注释 */
3. Java 注释会被翻译到 java 源代码中

- JSP注释

1. <%-- JSP注释 -->
2. jsp 注释可以注掉，jsp 页面中所有代码。

### JSP九大内置对象

- 基本概念

1. JSP中的内置对象，是指Tomcat在翻译 jsp 页面成为 servlet 源代码后，内部提供的九大对象，叫内置对象。

- 九大内置对象

1. request	请求对象
2. response	响应对象
3. pageContext	JSP的上下文对象
4. session	会话对象
5. application	ServletContext对象
6. config	ServletConfig对象
7. out	JSP输出流对象
8. page	指向当前jsp的对象
9. exception	异常对象

### JSP四大域对象

- 四个域对象：

1. pageContext	(PageContextImpl类)	当前jsp 页面范围内有效
2. request	(HttpServletRequest类)	一次请求内有效
3. session	(HttpSession类)	一个会话范围内有效(打开浏览器访问服务器会话开始，直到关闭浏览器会话结束)
4. application	(ServletContext类)	整个 web 工程范围内都有效(只要 web 工程不停止，数据都在)

5. 域对象是可以像 Map一样存取数据的对象。四个域对象功能一样。不同的是它们对数据的存取范围。


- 案例演示

```jsp
<%--
scope1
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
  <title>Title</title>
</head>
<body>
<h1>scope.jsp页面</h1>
 <%
 pageContext.setAttribute("key", "pageContent");
 request.setAttribute("key", "request");
 session.setAttribute("key", "session");
 application.setAttribute("key", "application");
 %>
pageContext是否有值：<%=pageContext.getAttribute("key")%>
request是否有值：<%=request.getAttribute("key")%>
session是否有值：<%=session.getAttribute("key")%>
application是否有值：<%=application.getAttribute("key")%>
<%
  request.getRequestDispatcher("/scope2.jsp").forward(request, response);
%>
<%--转发到scope2 pageContext无法查询--%>
<%--直接访问scope2 pageContext/request无法查询--%>
<%--关闭浏览器再访问scope2 pageContext/request/session无法查询--%>
    <%--重启服务器再访问scope2 pageContext/request/session/application无法查询--%>
</body>
</html>
```

```jsp
<%--
scope2
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
  <title>Title</title>
</head>
<body>
pageContext是否有值：<%=pageContext.getAttribute("key")%>
request是否有值：<%=request.getAttribute("key")%>
session是否有值：<%=session.getAttribute("key")%>
application是否有值：<%=application.getAttribute("key")%>
</body>
</html>
```

- 使用原则

1. 四个域对象都可以存取数据。在使用上它们有优先顺序。
2. 四个域在使用的时候，优先顺序分别是，他们从小到大的范围的顺序。
   - pageContext -> request -> session -> application



### JSP中的out输出和 response.getWriter 输出的区别

- response 表示响应，我们经常用于设置返回给客户端的内容(输出)。out 也是给用户做输出使用。
- 区别解析

1. 图示解析

<img src=".\JavaWeb_Markdown笔记图片\JSP_response和out的区别.png" alt="JSP_response和out的区别" style="zoom:50%;" />

2. 当jsp页面中所有代码执行完成后会做以下两个操作:

- 执行out.flushO操作，会把out缓冲区中的数据追加写入到response缓冲区末尾
- 会执行response的刷新操作。把全部数据写给客户端

3. JSP 底层使用out输出，在实际编程中通常使用out输出
   - out.write()	只适合**输出字符串**
     - **看源码**：直接输出整型，会转化成整型数字对应的ascll码的符号
   - out.print()	将**各类型的数据**转化为字符串再进行输出
   - 开发中通常使用out.print()显示数据

### JSP的常用标签

- 需求

![JSP_包含关系](.\JavaWeb_Markdown笔记图片\JSP_包含关系.png)

- jsp 静态包含

静态包含的特点：

1. 静态包含不会翻译被包含的jsp页面
2. 静态包含其实是把被包含的jsp页面的**代码拷贝**到包含的位置执行输出

```jsp
<%--
  Created by IntelliJ IDEA.
  User: 97359
  Date: 2024/4/28
  Time: 10:45
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
  <title>Title</title>
</head>
<body>
  头部信息 <br>
  主体内容 <br>
<%-- 静态包含
  地址中第一个斜杠 / 表示为 http://ip:port/工程路径/ 映射到代码的web目录
 --%>
  <%@ include file="/include/footer.jsp"%>

</body>
</html>
```

```jsp
<%--
  Created by IntelliJ IDEA.
  User: 97359
  Date: 2024/4/28
  Time: 10:47
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
  <title>Title</title>
</head>
<body>
  尾部信息 <br>

</body>
</html>
```

- jsp 动态包含

动态包含的特点：

1. 动态包含会把包含的jsp页面也翻译成为java代码
2. 动态包含底层代码使用如下代码去调用被包含的jsp页面执行输出。
   - JspRuntimeLibrary.include(request, response, "/include/footer.jsp", out, false);
3. 动态包含可以传递参数

<img src=".\JavaWeb_Markdown笔记图片\JSP_动态包含_图示解析.png" alt="JSP_动态包含_图示解析" style="zoom: 67%;" />

```jsp
<%--
  Created by IntelliJ IDEA.
  User: 97359
  Date: 2024/4/28
  Time: 10:45
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
  <title>Title</title>
</head>
<body>
  头部信息 <br>
  主体内容 <br>
<%-- 动态包含
 --%>
  <jsp:include page="/include/footer.jsp"></jsp:include>

</body>
</html>
```

```jsp
<%--
  Created by IntelliJ IDEA.
  User: 97359
  Date: 2024/4/28
  Time: 10:47
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
  <title>Title</title>
</head>
<body>
  尾部信息 <br>
  尾部信息 <br>
</body>
</html>
```

- 静态包含和动态包含的使用选择：随着JavaEE开发技术的迭代，JSP通常只用来输出页面，所以通常使用静态方法。

- jsp 标签-转发：通过JSP实现请求转发

```jsp
<jsp:forward page="footer.jsp"></jsp:forward>
```

### JSP练习

- 输出乘法口诀表

```jsp
<%--
  Created by IntelliJ IDEA.
  User: 97359
  Date: 2024/4/28
  Time: 11:18
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
  <title>Title</title>
</head>
<body>
<table>
  <% for (int i = 1; i <= 9; i++) { %>
  <tr>
  <%
    for (int j = 1; j <= i; j++) {
  %>

  <td><%= j + "*" + i + "=" + (i*j) %></td>
  <%
    }
  %>
  </tr>
  <%
    }
  %>
</table>
</body>
</html>
```

- jsp 输出一个表格，里面有 10 个学生信息。

```java
package com.uestc.pojo;

public class Student {
  private Integer id;

  public Student(Integer id, String name, Integer age, String phoneNumber) {
    this.id = id;
    this.name = name;
    this.age = age;
    this.phoneNumber = phoneNumber;
  }

  @Override
  public String toString() {
    return "Student{" +
      "id=" + id +
      ", name='" + name + '\'' +
      ", age=" + age +
      ", phoneNumber='" + phoneNumber + '\'' +
      '}';
  }

  public Integer getId() {
    return id;
  }

  public void setId(Integer id) {
    this.id = id;
  }

  public String getName() {
    return name;
  }

  public void setName(String name) {
    this.name = name;
  }

  public Integer getAge() {
    return age;
  }

  public void setAge(Integer age) {
    this.age = age;
  }

  public String getPhoneNumber() {
    return phoneNumber;
  }

  public void setPhoneNumber(String phoneNumber) {
    this.phoneNumber = phoneNumber;
  }

  private String name;
  private Integer age;
  private String phoneNumber;

  public Student() {
  }
}
```

```jsp
<%@ page import="com.uestc.pojo.Student" %>
<%@ page import="java.util.ArrayList" %>
<%@ page import="java.util.List" %><%--
  Created by IntelliJ IDEA.
  User: 97359
  Date: 2024/4/28
  Time: 14:51
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
  <title>Title</title>
  <style>
    table{
      border: 1px red solid;
    }
    td,th{
      border: 1px red solid;
    }
  </style>
</head>
<body>
<%
  List<Student> studentList = new ArrayList<>();
  for (int i=0; i < 10; i++) {
    int id = i+1;
    studentList.add(new Student(id, "name" + id, 18+id, "phoneNum" + id));
  }
%>
<table>
  <tr>
    <td>ID</td>
    <td>姓名</td>
    <td>年龄</td>
    <td>电话</td>
  </tr>
  <% for (Student stu: studentList) { %>
    <tr>
      <td> <%= stu.getId()%></td>
      <td> <%= stu.getName()%></td>
      <td> <%= stu.getAge()%></td>
      <td> <%= stu.getPhoneNumber()%></td>
    </tr>
<% } %>
</table>
</body>
</html>
```

- 练习2提升：请求转发的实际应用

![JSP_练习2_提升内容](.\JavaWeb_Markdown笔记图片\JSP_练习2_提升内容.png)

```java
// Servlet 服务
package com.uestc.servlet;

import com.uestc.pojo.Student;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;
import java.util.ArrayList;
import java.util.List;

public class SearchStudentServlet extends HttpServlet {
  @Override
  protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    // 获取请求的参数
    // 发sql语句查询学生的信息
    // 使用for循环生成查询到的数据做模拟
    List<Student> studentList = new ArrayList<>();
    for (int i=0; i < 10; i++) {
      int id = i+1;
      studentList.add(new Student(id, "name" + id, 18+id, "phoneNum" + id));
    }
    // 保存查询到的结果(学生信息)到request域中
    req.setAttribute("stuList", studentList);
    // 请求转发到showstudent.jsp页面
    req.getRequestDispatcher("/test/showStudent.jsp").forward(req, resp);

  }
}
```

```jsp
<%@ page import="com.uestc.pojo.Student" %>
<%@ page import="java.util.ArrayList" %>
<%@ page import="java.util.List" %><%--
  Created by IntelliJ IDEA.
  User: 97359
  Date: 2024/4/28
  Time: 14:51
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
  <title>Title</title>
  <style>
    table{
      border: 1px red solid;
    }
    td,th{
      border: 1px red solid;
    }
  </style>
</head>
<body>
<%--需要客户端发送请求才能获取List，直接访问request是不存在"stuList"
会空指针
--%>
<%
  List<Student> stuList = (List<Student>) request.getAttribute("stuList");
%>
<table>
  <tr>
    <td>ID</td>
    <td>姓名</td>
    <td>年龄</td>
    <td>电话</td>
  </tr>
  <% for (Student stu: stuList) { %>
    <tr>
      <td> <%= stu.getId()%></td>
      <td> <%= stu.getName()%></td>
      <td> <%= stu.getAge()%></td>
      <td> <%= stu.getPhoneNumber()%></td>
    </tr>
<% } %>
</table>

</body>
</html>
```

### Listener 监听器

- 基本概念

1. Listener 监听器它是JavaWeb的三大组件之一。JavaWeb 的**三大组件**分别是:serlvet 程序、Filter 过滤器、Listener 监听器。
2. Listener它是 JavaEE的规范，就是**接口**。
3. 监听器的作用是，监听某种事物的变化。然后通过回调函数，反馈给客户(程序)去做一些相应的处理。

#### ServletContextListener监听器

- 基本内容

1. ServletContextlistener 它可以监听 servletcontext 对象的创建和销毁。
2. Servletcontext 对象在 web 工程启动的时候创建，在 web 工程停止的时候销毁。
3. 监听到创建和销毁之后都会分别调用 servletcontextListener 监听器的方法反馈。
4. 两个方法：

```java
public interface ServletContextlistener extends EventListener {
	// 在ServletContext对象创建之后马上调用，做初始化
public void contextInitialized(ServletContextEvent sce){};
    // 在SeretContext 对象销毁之后调用
public void contextDestroyed(servletContextEvent sce){};
}
```

- 使用步骤

1. 编写一个类去实现 ServletContextListener
2. 实现其两个回调方法
3. 到 web.xml 中去配置监听器

```java
package com.uestc.listener;

import javax.servlet.ServletContextEvent;
import javax.servlet.ServletContextListener;

public class MyServletContextListennerImpl implements ServletContextListener {
    // 工程启动时调用
  @Override
  public void contextInitialized(ServletContextEvent servletContextEvent) {
    System.out.println("ServletContext 对象创建");
  }
	// 工程终止时调用
  @Override
  public void contextDestroyed(ServletContextEvent servletContextEvent) {
    System.out.println("ServletContext 对象销毁");
  }
}
```

```xml
<listener>
    <listener-class>com.uestc.listener.MyServletContextListennerImpl</listener-class>
  </listener>
```

## EL 表达式

- 基本概念

1. EL表达式的全称是:Expression Language。是表达式语言。
2. EL表达式的作用:EL 表达式主要是代替jsp 页面中的表达式脚本在**jsp页面中进行数据的输出**。
3. 因为 EL 表达式在输出数据的时候，要比jsp的表达式脚本要简洁很多。

- 区别

1. 当输出内容为空时，EL表达式输出" "，表达式脚本输出null

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
  <title>Title</title>
</head>
<body>
<%
request.setAttribute("key", "value");
%>
表达式脚本输出key的值是:<%=request.getAttribute("key") %><br/>
EL表达式输出key的值是:${key}<br/>
不存在时：
表达式脚本输出key的值是:<%=request.getAttribute("key1") %><br/>
EL表达式输出key的值是:${key1}<br/>
</body>
</html>
```

2. 四个域中都保存了相同的key的数据。EL表达式会从小到大访问，pageContext->requset->session->application,和代码的顺序无关。
3. 输出对象属性的方法

```jsp
<%@ page import="com.uestc.pojo.Person" %>
<%@ page import="java.util.List" %>
<%@ page import="java.util.ArrayList" %>
<%@ page import="java.util.Map" %>
<%@ page import="java.util.HashMap" %><%--
  Created by IntelliJ IDEA.
  User: 97359
  Date: 2024/4/29
  Time: 10:24
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
  <title>Title</title>
</head>
<body>
<%
  Person person = new Person();
  person.setId(123);
  person.setPhones(new String[]{"13511112222", "13433332222"});
  List<String> cities = new ArrayList<String>();
  cities.add("北京");
  cities.add("上海");
  cities.add("深圳");
  person.setCities(cities);

  Map<String, Object> map= new HashMap<>();
  map.put("key1", "value1");
  map.put("key2", "value2");
  map.put("key3", "value3");
  map.put("key4", "value4");
  person.setMap(map);
  pageContext.setAttribute("p", person);
%>
输出person对象：${p}<br/>
输出person对象的属性：${p.id}
输出person对象的phones${p.phones[0]}
输出person对象的cities集合${p.cities}
输出person对象的List集合${p.cities}
输出person对象的List集合中的元素${p.cities[0]}
输出person对象的map${p.map}
输出person对象的map中的元素${p.map.key1}

</body>
</html>
```

4. EL表达式是通过对象的getXXX方法获取对象的属性，即使类中不存在该属性但是存在属性的get方法也可以访问

### EL 表达式的运算

- 关系运算

![EL表达式_关系运算](.\JavaWeb_Markdown笔记图片\EL表达式_关系运算.png)

- 逻辑运算

![EL表达式_逻辑运算](.\JavaWeb_Markdown笔记图片\EL表达式_逻辑运算.png)

- 算数运算

![EL表达式_算数运算符](.\JavaWeb_Markdown笔记图片\EL表达式_算数运算符.png)

- empty 运算：

1. empty运算可以判断一个数据是否为空，如果为空，则输出 true,不为空输出 false。
2. 以下几种情况为空:
   - 值为 null 值的时候，为空
   - 值为空串的时候，为空
   - 值是 Object 类型数组，长度为零的时候
   - list 集合，元素个数为零
   - map 集合，元素个数为零

```jsp
<%@ page import="java.util.List" %>
<%@ page import="java.util.ArrayList" %>
<%@ page import="java.util.Map" %>
<%@ page import="java.util.HashMap" %>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
  <title>Title</title>
</head>
<body>
<%
  // 值为 null 值的时候，为空
  request.setAttribute("emptyNull", null);
  // 值为空串的时候，为空
  request.setAttribute("emptyStr", "");
  // 值是 Object 类型数组，长度为零的时候
  request.setAttribute("emptyArr", new Object[]{});
  // list 集合，元素个数为零
  List<String> list = new ArrayList<>();
  request.setAttribute("emptyList", list);
  // map 集合，元素个数为零
  Map<String, Object> map = new HashMap<>();
  request.setAttribute("emptyMap", map);
%>
  ${empty emptyNull} <br/>
  ${empty emptyStr} <br/>
  ${empty emptyArr} <br/>
  ${empty emptyList} <br/>
  ${empty emptyMap} <br/>
</body>
</html>
```

- 三元运算：  表达式1 ？ 表达式2 ： 表达式3

```jsp
${12 != 12 ? "不相等" : "相等"}
```

- "."点运算 和 []中括号运算符

1. "."点运算，可以输出 Bean 对象中某个属性的值。
2. []中括号运算，可以输出有序集合中某个元素的值。

3. 并且[]中括号运算，还可以输出 map 集合中 key 里含有特殊字符的 key 的值。

```jsp
<%
  Map<String, Object> spMap = new HashMap<String, Object>();
  map.put("a.a.a", "aaaValue");
  map.put("b+b+b", "aaaValue");
  map.put("c-c-c", "aaaValue");
  request.setAttribute("spMap", spMap);
%>
${spMap.a.a.a} 中括号： ${spMap['a.a.a']}
${spMap.b+b+b} 中括号： ${spMap['b+b+b']} 
${spMap.c-c-c} 中括号： ${spMap['c-c-c']}
<%--找不到的值默认为 0--%>
```

### EL表达式的 11个隐含对象

- EL表达式中 11 个隐含对象，是EL表达式中自己定义的，可以**直接使用**。

1. pageContext	PageContextlmpl	它可以获取 jsp 中的九大内置对象
2. pageScope	Map<String,Object>	它可以获取 pagecontext 域中的数据
3. requestScope	Map<String,Object>	它可以获取 Request 域中的数据
4. sessionScope	Map<String,Object>	它可以获取 session 域中的数据
5. applicationScope	Map<String,Object>	它可以获取 servletcontext 域中的数据
6. param	Map<String,String>	它可以获取请求参数的值
7. paramValues	Map<String,String[]>	它也可以获取请求参数的值，获取多个值的时候使用。
8. header	Map<String,String>	它可以获取请求头的信息
9. headerValues	Map<String,String[]>	它可以获取请求头的信息，它可以获取多个值的情况
10. cookie	Map<String,Cookie>	它可以获取当前请求的 cookie 信息
11. InitParam	Map<String,String>	它可以获取在 web.xml 中配置的< context-param >上下文参数

- EL获取四个特定域中的属性

1. pagescope	pageContext 域
2. requestScope	Request 域
3. sessionscope	Session 域
4. applicationscope	ServletContext 域

```jsp
<%
  pageContext.setAttribute("key1", "pageContext1");
  pageContext.setAttribute("key2", "pageContext2");
  request.setAttribute("key2", "request");
  session.setAttribute("key2", "session");
  application.setAttribute("key2", "application");
%>
${requestScope.key2}
```

- pageContext 对象的使用

1. 协议:
2. 服务器ip:
3. 服务器端口:
4. 获取工程路径:
5. 获取请求方法:
6. 获取客户端ip 地址:
7. 获取会话的id 编号:

```jsp
<%--
request.getscheme()它可以获取请求的协议
request.getServerName()获取请求的服务器ip或域名
request.getServerPort()获取请求的服务器端口号
request.getContextPath()获取当前工程路径
request.getMethod()获取请求的方式(GET或POST)
request.getRemoteHost()获取客户端的ip地址
session.getId()获取会话的唯一标识
--%>
<%--实际开发缩写--%>
<%
pageContext.setAttribute("req", request);
%>
1. 协议: ${req.scheme}<br>${pageContext.request.scheme}<br>
2. 服务器ip:${pageContext.request.serverName}<br>
3. 服务器端口:${pageContext.request.serverPort}<br>
4. 获取工程路径:${pageContext.request.contextPath}<br>
5. 获取请求方法:${pageContext.request.method}<br>
6. 获取客户端ip 地址:${pageContext.request.remoteHost}<br>
7. 获取会话的id 编号:${pageContext.session.id}<br>
```

- 其他隐藏对象的使用

1. param/paramValues

```jsp
<%--param显示参数 ？ 输入参数--%>
${param}
输出参数name:${param.name}
<%--paramValues显示多个输入参数 ？ 输入参数--%>
${paramValues.hobby[1]}
```

2. head/headValues

```jsp
输出请求头【User-Agent】的值:${header['User-Agent']}<br>
输出请求头【Connection】的值:${header.connection}<br>
<%--多请求头的情况比较少--%>
输出请求头【User-Agent】的值:${headerValues['User-Agent'][0]}<br>
```

3. cookie/InitParam

```xml
// 配置xml文件
<context-param>
    <param-name>username</param-name>
    <param-value>zyp123</param-value>
  </context-param>
  <context-param>
    <param-name>password</param-name>
    <param-value>z123456</param-value>
  </context-param>
```

```jsp
获取Cookie名称：${cookie.JSESSIONID.name}<br>
获取Cookie值：${cookie.JSESSIONID.value}<br>
输出Context-param的值${initParam.username}<br>
```

## JSTL 标签库

- 基本概念

1. JSTL标签库 全称是指 (JSP Standard Tag Librany) JSP 标准标签库，是一个不断完善的开放源代码的JSP 标签库。
2. EL表达式主要是为了替换jsp 中的**表达式脚本**，而标签库则是为了**替换代码脚本**。这样使得整个jsp 页面变得更佳简洁。

- JSTL 由五个不同功能的标签库组成

![JSTL标签库](.\JavaWeb_Markdown笔记图片\JSTL标签库.png)

- 在JSP标签库中使用 taglib 指令引入标签库

1. CORE 标签库
   - <%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core” %>
2. XML 标签库
   - <%@ taglib prefix="x" uri="http://java.sun.com/jsp/jstl/xml" %>
3. FMT 标签库
   - <%@ taglib prefix="fmt" uri="http://javy.sun.com/jsp/jstl/fmt" %>
4. SQL 标签库
   - <%@ taglib prefix="sql" uri="http://java.sun.com/jsp/jstl/sql" %>
5. FUNCTIONS 标签库
   - <%@ taglib prefix="fn" uri="http://java.sun.com/jsp/jstl/functions" %>

- 使用步骤

1. 先导入 jstl 标签库的jar 包。
2. 第二步，使用 taglib 指令引入标签库。

```jsp
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
```

- core核心库的使用

1. scope 属性设置保存的域
   - page表示PageContext域(默认值)
   - request表示Request域
   - session表示Session域
   - application表示Servletcontext域

2. set标签

```jsp
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
  <title>Title</title>
</head>
<body>
    <%--set 标签--%>
保存之前：${requestScope.abc}<br>
    <%--scope 选择域 var表示key value表示value--%>
<c:set scope="request" var="abc" value="abcValue"/>
保存之后：${requestScope.abc}<br>
</body>
</html>
```

3. if标签

```jsp
<%--if 标签
没有 if else 判断
--%>
<c:if test="${12 == 12}">
  <h1>12等于12</h1>
</c:if>
<c:if test="${12 != 12}">
  <h1>12等于12</h1>
</c:if>
```

4. < c:choose > < c:when >< c:otherwise >标签：类似switch-case-default
   - 标签内部只能使用jsp注释，不能使用html注释
   - when标签的父标签只能是choose标签

```jsp
<% request.setAttribute("height", 179); %>
<c:choose>
  <c:when test="${requestScope.height > 190}">
    <h2>很高</h2>
  </c:when>
  <c:when test="${requestScope.height > 170}">
    <h2>还行</h2>
  </c:when>
  <c:otherwise>
    <h2>很矮</h2>
  </c:otherwise>
```

5. <c:forEach />：遍历输出

   - 遍历数字:1-10

     ```jsp
     <table>
       <c:forEach begin="1" end="10" var="i">
         <tr>
           <td>第${i}行</td>
         </tr>
     
       </c:forEach>
     </table>
     ```

   - 遍历 Object 数组

     ```jsp
     <%--
     items 表示遍历的数据源(遍历的集合)
     var 表示当前遍历到的数据
     --%>
     <%
     request.setAttribute("arr", new String[]{"13699998888", "13688889999"});
     %>
     <c:forEach items="${requestScope.arr}" var="item">
       ${item} <br>
     </c:forEach>
     ```

   - 遍历Map 集合

     ```jsp
     <c:forEach items="${requestScope.map}" var="entry">
       ${entry}<br>
       ${entry.key}<br>
       ${entry.value}<br>
     </c:forEach>
     ```

   - 遍历 List 集合：ist 中存放 Person 类，有属性:编号，用户名，密码，年龄，电话信息

     ```jsp
     <%@ page import="java.util.List" %>
     <%@ page import="com.uestc.pojo.Student" %>
     <%@ page import="java.util.ArrayList" %>
     <%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
     <%@ page contentType="text/html;charset=UTF-8" language="java" %>
     <html>
     <head>
       <title>Title</title>
     </head>
     <body>
     <%
       List<Student> studentList = new ArrayList<>();
       for (int i = 1; i <= 10; i++) {
         studentList.add(new Student(i, "username"+i, "pwd"+i, 18, "136" + i));
       }
       request.setAttribute("stus", studentList);
     %>
     <table>
       <tr>
         <th>编号</th>
         <th>用户名</th>
         <th>密码</th>
         <th>年龄</th>
         <th>电话</th>
         <th>操作</th>
       </tr>
     <c:forEach begin="1" end="9" step="2" items="${requestScope.stus}" var="stu" varStatus="status">
       <tr>
         <td>${stu.id} <br></td>
         <td>${stu.username} <br></td>
         <td>${stu.password} <br></td>
         <td>${stu.age} <br></td>
         <td>${stu.phone} <br></td>
         <td>修改/删除</td>
     <%--  通过varStatus查看参数  --%>
         <td>status.current</td>
       </tr>
     </c:forEach>
     </table>
     </body>
     </html>
     ```

   - varStatus

![JSTL标签库_core_循环1](.\JavaWeb_Markdown笔记图片\JSTL标签库_core_循环1.png)

## 文件的上传和下载

- 基本介绍：文件的上传和下载，是非常常见的功能。

### 文件上传

- 文件的上传

1. 要有一个form 标签，method=post 请求
2. form标签的 encType 属性值必频为 multipart/form-data 值
   - Content-Type 表示提交的数据类型
   - encType=multipart/form-data 表示提交的数据，以多段(每一个表单项一个数据段)的形式进行拼接，然后以二进制流的形式发送给服务器
   - boundary表示每段数据的分隔符，随机生成

3. 在 form 标签中使用 input type=file添加上传的文件

4. 编写服务器代码接收，处理上传的数据。

![文件上传_HTTP协议内容](.\JavaWeb_Markdown笔记图片\文件上传_HTTP协议内容.png)

```java
package com.uestc.servlet;

import javax.servlet.ServletException;
import javax.servlet.ServletInputStream;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;
import java.util.Arrays;

public class UploadServlet extends HttpServlet {

  @Override
  protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
  //  文件必须以流的形式接收
    System.out.println("doPost");
    ServletInputStream inputStream = req.getInputStream();
    byte[] buffer = new byte[10240];
    int read = inputStream.read(buffer);
    System.out.println(new String(buffer, 0, read));
  }
}
```



- 文件的读取

1. 使用封装的JAR包API
   - commons-fileupload-1.5.jar
   - commons-io-2.16.1.jar
2. 常见类/方法：
   - ServletFileUpload类，用于解析上传的数据
   - Fileltem类，表示每一个表单项。
   - boolean ServletFileUpload,isMultipartcontent(HttpServletRequest request);
     判断当前上传的数据格式是否是多段的格式。
   - public List< Fileltem > parseRequest(HttpServletRequest request)
     解析上传的数据
   - boolean FileItem.isFormField()
     判断当前这个表单项，是否是普通的表单项。还是上传的文件类型。
     true 表示普通类型的表单项
     falsq表示上传的文件类型
   - String FileItem.getFieldName( )
     获取表单项的 name属性值
   - String FileItem.getstring()
     获取当前表单项的值。
   - String FileItem.getName();
     获取上传的文件名
   - void Fileltem.write( file );
     将上传的文件写到 参数 file 所指向抽硬盘位置。

### 文件下载

- 基本思路

![文件下载_基本思路](.\JavaWeb_Markdown笔记图片\文件下载_基本思路.png)

# 书城：第三阶段

- 页面JSP化：把原本的html页面改写为JSP页面

1. 在 html 页面顶行添加 page 指令,
2. 修改文件后缀名为:.jsp
3. 使用 IDEA 搜索替换.html为.jsp(Ctrl+Shift+R/Ctrl+R)

- BaseServlet 的抽取1：在实际的项目开发中，一个模块，一般只使用一个Servlet程序。

<img src=".\JavaWeb_Markdown笔记图片\BaseServlet抽取.png" alt="BaseServlet抽取" style="zoom: 50%;" />

- 通过反射处理多种任务请求

1. 获取action参数值
2. 通过反射获取action对应的业务方法
3. 通过反射调用业务方法

```java
package com.uestc.web;

import javax.servlet.http.HttpServlet;
import java.lang.reflect.Method;

public class UserServletTest extends HttpServlet {
  public void login() {
    System.out.println("login()方法调用");
  }
  public void registry() {
    System.out.println("registry()方法调用");
  }
  public void updateUser() {
    System.out.println("updateUser()方法调用");
  }
  public void updateUserPassword() {
    System.out.println("updateUserPassword()方法调用");
  }

  public static void main(String[] args) {
    String action = "login";
    try {
      // 避免业务过多，无限使用if else
      // 反射获取业务方法
      Method method = UserServletTest.class.getDeclaredMethod(action);
      System.out.println(method);
      // 反射调用业务方法
      method.invoke(new UserServlet());
    } catch (Exception e) {
        throw new RuntimeException(e);
    }

  }
}
```

```java
package com.uestc.web;

import com.uestc.pojo.User;
import com.uestc.service.UserService;
import com.uestc.service.impl.UserServiceImpl;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;
import java.lang.reflect.Method;

public class UserServlet extends HttpServlet {
  private UserService userService = new UserServiceImpl();
  protected void login(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    // 处理登录
    // 获取请求参数 userService.login
    String username = req.getParameter("username");
    String password = req.getParameter("password");
    // 登录业务
    User loginUser = userService.login(new User(null, username, password, null));
    if (loginUser == null) {
      System.out.println("用户名为：" + username + "登录失败");
      req.setAttribute("msg", "用户名与密码不匹配");
      req.setAttribute("username", username);
      req.getRequestDispatcher("/pages/user/login.jsp").forward(req, resp);
    } else {
      req.getRequestDispatcher("/pages/user/login_success.jsp").forward(req, resp);
    }
  }
  protected void registry(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    // 处理注册
    // 1. 获取请求参数
    String username = req.getParameter("username");
    String password = req.getParameter("pwd");
    String email = req.getParameter("email");
    String code = req.getParameter("code");
    // 2. 检验验证码是否正确
    if ("7364".equals(code)) {
      // 检测用户名
      if (userService.existUsername(username)) {
        System.out.println("用户名[" + username + "]已存在！");
        req.setAttribute("msg", "用户名已存在");
        req.setAttribute("username", username);
        req.setAttribute("email", email);
        req.getRequestDispatcher("/pages/user/registry.jsp").forward(req, resp);
      } else {
        userService.registUser(new User(null, username, password, email));
        req.getRequestDispatcher("/pages/user/registry_success.jsp").forward(req, resp);
      }
    } else {
      System.out.println("验证码：" + code + "错误");
      req.setAttribute("msg", "验证码错误");
      req.setAttribute("username", username);
      req.setAttribute("email", email);
      req.getRequestDispatcher("/pages/user/registry.jsp").forward(req, resp);
    }
  }

  protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    String action = req.getParameter("action");
    try {
      // 避免业务过多，无限使用if else
      // 反射获取业务方法
      System.out.println(action);
      Method method = this.getClass().getDeclaredMethod(action, HttpServletRequest.class, HttpServletResponse.class);
      // 反射调用业务方法
      method.invoke(this, req, resp);
    } catch (Exception e) {
      throw new RuntimeException(e);
    }
  }
}
```

- BaseServlet 的抽取2：构建BaseServlet基类

<img src=".\JavaWeb_Markdown笔记图片\BaseServlet抽取2.png" alt="BaseServlet抽取2" style="zoom: 67%;" />

```java
package com.uestc.web;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;
import java.lang.reflect.Method;

public abstract class BaseServlet extends HttpServlet {
  protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    String action = req.getParameter("action");
    try {
      // 避免业务过多，无限使用if else
      // 反射获取业务方法
      System.out.println(action);
      Method method = this.getClass().getDeclaredMethod(action, HttpServletRequest.class, HttpServletResponse.class);
      // 反射调用业务方法
      method.invoke(this, req, resp);
    } catch (Exception e) {
      throw new RuntimeException(e);
    }
  }
}
```

```java
package com.uestc.web;

import com.uestc.pojo.User;
import com.uestc.service.UserService;
import com.uestc.service.impl.UserServiceImpl;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;
import java.lang.reflect.Method;

public class UserServlet extends BaseServlet {
  private UserService userService = new UserServiceImpl();
  protected void login(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    // 处理登录
    // 获取请求参数 userService.login
    String username = req.getParameter("username");
    String password = req.getParameter("password");
    // 登录业务
    User loginUser = userService.login(new User(null, username, password, null));
    if (loginUser == null) {
      System.out.println("用户名为：" + username + "登录失败");
      req.setAttribute("msg", "用户名与密码不匹配");
      req.setAttribute("username", username);
      req.getRequestDispatcher("/pages/user/login.jsp").forward(req, resp);
    } else {
      req.getRequestDispatcher("/pages/user/login_success.jsp").forward(req, resp);
    }
  }
  protected void registry(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    // 处理注册
    // 1. 获取请求参数
    String username = req.getParameter("username");
    String password = req.getParameter("pwd");
    String email = req.getParameter("email");
    String code = req.getParameter("code");
    // 2. 检验验证码是否正确
    if ("7364".equals(code)) {
      // 检测用户名
      if (userService.existUsername(username)) {
        System.out.println("用户名[" + username + "]已存在！");
        req.setAttribute("msg", "用户名已存在");
        req.setAttribute("username", username);
        req.setAttribute("email", email);
        req.getRequestDispatcher("/pages/user/registry.jsp").forward(req, resp);
      } else {
        userService.registUser(new User(null, username, password, email));
        req.getRequestDispatcher("/pages/user/registry_success.jsp").forward(req, resp);
      }
    } else {
      System.out.println("验证码：" + code + "错误");
      req.setAttribute("msg", "验证码错误");
      req.setAttribute("username", username);
      req.setAttribute("email", email);
      req.getRequestDispatcher("/pages/user/registry.jsp").forward(req, resp);
    }
  }
}
```

- 数据的封装和抽取 BeanUtils的使用

1. Beanutils工具类(第三方工具类)，它可以一次性的把所有请求的参数注入到JavaBean 中
   - commons-beanutils-1.9.4.jar
   - commons-logging-1.3.1.jar
   - commons-collections-3.2.2.jar
2. 使用beanutils类实现注入
   - Map/req.getParameterMap() 提供的key和Bean的get/set方法的名字必须相同

# 书城：第四阶段

- 使用EL 表达式修改表单回显(EL 表达式 替换表达式脚本)

```jsp
<%--            <%=request.getAttribute("msg")==null? "请输入用户名和密码": request.getAttribute("msg")%>--%>
            ${ empty requestScope.msg ? "请输入用户名和密码": requestScope.msg}
<%--                 value="<%=request.getAttribute("username")==null?"":request.getAttribute("username")%>"--%>
            value="${requestScope.username}"

```

# 书城：第五阶段

## MVC 概念

- 基本概念

1. MVC 全称:Model模型、View 视图、 Controller 控制器。
2. MVC最早出现在JavaEE 三层中的 Web层，它可以有效的指导 web 层的代码如何有效分离，单独工作。
   - 单独开发，组合使用。目的是：解耦。
3. View视图:只负责数据和界面的显示，不接受任何与显示数据无关的代码，便于程序员和美工的分工合作--**JSP/HTML** 。
4. Controler 控制器:只负责接收请求,调用业务层的代码处理请求,然后派发页面,是一个“调度者”的角色--**servlet**。转到某个页面。或者是重定向到某个页面。
5. Model模型:将与业务逻辑相关的数据封装为具体的JavaBean 类，其中不掺杂任何与数据处理相关的代码--JavaBean/domain/entity/pojo。

## 图书模块

- 编写图书模块的数据库表

```mysql
CREATE TABLE t_book(
	`id` INT PRIMARY KEY AUTO_INCREMENT,
	`name` VARCHAR(100),
	`price` DECIMAL(11, 2),
	`author` VARCHAR(100),
	`sales` INT,
	`stock` INT,
	`img_path` VARCHAR(200)
);

TRUNCATE TABLE t_book;

INSERT INTO t_book (`name`, `price`, `author`, `sales`, `stock`, `img_path`)
VALUES
('三体', 28.50, '刘慈欣', 1000, 500, 'img/default.jpg'),
('平凡的世界', 36.99, '路遥', 800, 300, 'img/default.jpg'),
('活着', 25.75, '余华', 1200, 600, 'img/default.jpg'),
('白夜行', 29.00, '东野圭吾', 1500, 400, 'img/default.jpg'),
('围城', 21.49, '钱钟书', 900, 200, 'img/default.jpg'),
('人间失格', 20.80, '太宰治', 700, 700, 'img/default.jpg'),
('挪威的森林', 26.20, '村上春树', 1100, 550, 'img/default.jpg'),
('飘', 32.99, '玛格丽特·米切尔', 1300, 650, 'img/default.jpg'),
('百年孤独', 30.45, '加西亚·马尔克斯', 1400, 450, 'img/default.jpg'),
('追风筝的人', 28.70, '卡勒德·胡赛尼', 1600, 850, 'img/default.jpg');

SELECT * FROM t_book
```

- 编写图书模块的 JavaBean

```java
package com.uestc.pojo;

import java.math.BigDecimal;

public class Book {
  private Integer id;
  private String name;
  private String author;
  private BigDecimal price;
  private Integer sales;
  private Integer stock;
  private String imgPath = "img/default.jpg";

  public Integer getId() {
    return id;
  }

  @Override
  public String toString() {
    return "Book{" +
      "id=" + id +
      ", name='" + name + '\'' +
      ", author='" + author + '\'' +
      ", price=" + price +
      ", sales=" + sales +
      ", stock=" + stock +
      ", imgPath='" + imgPath + '\'' +
      '}';
  }

  public void setId(Integer id) {
    this.id = id;
  }

  public String getName() {
    return name;
  }

  public void setName(String name) {
    this.name = name;
  }

  public String getAuthor() {
    return author;
  }

  public void setAuthor(String author) {
    this.author = author;
  }

  public BigDecimal getPrice() {
    return price;
  }

  public void setPrice(BigDecimal price) {
    this.price = price;
  }

  public Integer getSales() {
    return sales;
  }

  public void setSales(Integer sales) {
    this.sales = sales;
  }

  public Integer getStock() {
    return stock;
  }

  public void setStock(Integer stock) {
    this.stock = stock;
  }

  public String getImgPath() {
    return imgPath;
  }

  public void setImgPath(String imgPath) {
    if (!"".equals(imgPath) && imgPath != null) {
      this.imgPath = imgPath;
    }
  }

  public Book() {
  }

  public Book(Integer id, String name, String author, BigDecimal price, Integer sales, Integer stock, String imgPath) {
    this.id = id;
    this.name = name;
    this.author = author;
    this.price = price;
    this.sales = sales;
    this.stock = stock;
    if (!"".equals(imgPath) && imgPath != null) {
      this.imgPath = imgPath;
    }

  }

}
```

- 编写图书模块的 Dao 和测试Dao

```java
package com.uestc.dao.impl;

import com.uestc.dao.BookDao;
import com.uestc.pojo.Book;

import java.util.List;

public class BookDaoImpl extends BaseDao implements BookDao {
  @Override
  public int addBook(Book book) {
    String sql = "INSERT INTO t_book (`name`, `price`, `author`, `sales`, `stock`, `img_path`) values (?,?,?,?,?,?);";
    return update(sql, book.getName(), book.getPrice(), book.getAuthor(), book.getSales(), book.getStock(), book.getImgPath());
  }

  @Override
  public int deleteBookById(Integer id) {
    String sql = "delete from t_book where id=?";
    return update(sql, id);
  }

  @Override
  public int updateBook(Book book) {
    String sql = "update t_book set `name`=?, `author`=?, `price`=?, `sales`=?, `stock`=?, `img_path`=? where id=?";
    return update(sql, book.getName(), book.getAuthor(), book.getPrice(), book.getSales(), book.getStock(), book.getImgPath(), book.getId());
  }

  @Override
  public Book queryBookById(Integer id) {
    String sql = "select `id`, `name`, `price`, `author`, `sales`, `stock`, `img_path` from t_book where id=?";
    return queryForOne(Book.class, sql, id);
  }

  @Override
  public List<Book> queryBooks() {
    String sql = "select `id`, `name`, `price`, `author`, `sales`, `stock`, `img_path` from t_book";
    return queryForList(Book.class, sql);
  }
}
```

```java
package com.uestc.test;

import com.uestc.dao.BookDao;
import com.uestc.dao.impl.BookDaoImpl;
import com.uestc.pojo.Book;
import org.junit.Test;

import java.math.BigDecimal;

import static org.junit.Assert.*;

public class BookDaoTest {
  private BookDao bookDao = new BookDaoImpl();

  @Test
  public void addBook() {
    bookDao.addBook(new Book(null, "name1", "author1", new BigDecimal("99.99"), 1000, 500, "img/default.jpg"));
  }

  @Test
  public void deleteBookById() {
    bookDao.deleteBookById(11);
  }

  @Test
  public void updateBook() {
    bookDao.updateBook(new Book(11, "成都", "author1", new BigDecimal("99.99"), 1000, 500, "img/default.jpg"));
  }

  @Test
  public void queryBookById() {
    System.out.println(bookDao.queryBookById(11));
  }

  @Test
  public void queryBooks() {
    for (Book book: bookDao.queryBooks()) {
      System.out.println(book);
    }
  }
}
```

- 编写图书模块的Service和测试Service

```java
package com.uestc.service;

import com.uestc.pojo.Book;

import java.util.List;

public interface BookService {
  public void addBook(Book book);
  public void deleteBookById(Integer id);
  public void updateBook(Book book);
  public Book queryBookById(Integer id);
  public List<Book> queryBooks();
}
```

```java
package com.uestc.service.impl;

import com.uestc.dao.BookDao;
import com.uestc.dao.impl.BookDaoImpl;
import com.uestc.pojo.Book;
import com.uestc.service.BookService;

import java.util.List;

public class BookServiceImpl implements BookService {
  private BookDao bookDao = new BookDaoImpl();
  @Override
  public void addBook(Book book) {
    bookDao.addBook(book);
  }

  @Override
  public void deleteBookById(Integer id) {
    bookDao.deleteBookById(id);
  }

  @Override
  public void updateBook(Book book) {
    bookDao.updateBook(book);
  }

  @Override
  public Book queryBookById(Integer id) {
    return bookDao.queryBookById(id);
  }

  @Override
  public List<Book> queryBooks() {
    return bookDao.queryBooks();
  }
}
```

- 编写图书模块的 Web 层，和页面联调测试

![book_web](.\JavaWeb_Markdown笔记图片\book_web.png)

- 区分前后台：便于权限的管理

<img src=".\JavaWeb_Markdown笔记图片\前后台管理.png" alt="前后台管理" style="zoom: 67%;" />

- 图书列表的添加

<img src=".\JavaWeb_Markdown笔记图片\图书_添加.png" alt="图书_添加" style="zoom:67%;" />

1. 表单重复提交:
   - 当用户提交完请求，浏览器会记录下最后一次请求的全部信息。当用户按下功能键F5，就会发起浏览器记录的最后一次请求。
   - 使用重定向--两次请求

- 图书列表的删除

![图书_删除](.\JavaWeb_Markdown笔记图片\图书_删除.png)

- 修改图书信息

![图书_修改](.\JavaWeb_Markdown笔记图片\图书_修改.png)

1. 通到的问题:book_edit.jsp页面，即要做添加操作。又要做修改操作。而到底是添加，还是修改是由一个隐藏域来决定的。如何动态修改隐藏域<input type="hidden" name="action" value="xxx”/>让它的值即可以实现添加，又可以修改？

2. 解决方案一:可以发请求发起时，附带上当前要操作的值。并注入到隐藏域中。

3. 解决方案二:判断有无id参数来区分

   - ```html
     <input type="hidden" name="action" value="${empty param.id? "add": "update"}" />
     ```

4. 解决方案三:判断域中是否存在book对象

- 图书显示页面的分页

![图书_显示分页](.\JavaWeb_Markdown笔记图片\图书_显示分页.png)

- 页码的显示：显示连续5个页面

1. 如果总页码小于等于5 的情况，页码的范围是:1-总页码
2. 总页码大于5的情况。假设一共 10 页
   - 页码小于等于ceil[5/2] -- 都显示1-5页
   - 页码为最后ceil[5/2]页 -- 都显示最后5页
   - 其他：当前页码附近的5个页面

- 首页分页内容

![图书_首页分页](.\JavaWeb_Markdown笔记图片\图书_首页分页.png)

- 通过价钱查询

![图书_价格区间查询分页](.\JavaWeb_Markdown笔记图片\图书_价格区间查询分页.png)

# Cookie

- 基本概念：

1. Cookie 是 servlet发送到 Web 浏览器的少量信息，这些信息由**浏览器保存**，然后发送回服务器。
2. Cookie 是服务器通知客户端保存键值对的一种技术。
3. 客户端有了 Cookie 后，每次请求都发送给服务器
4. 每个 cookie 的大小不能超过 4kb

- 解决乱码

```java
// 在BaseServlet中添加
// 解决请求中的乱码
req.setCharacterEncoding("UTF-8");
// 解决响应乱码
resp.setContentType("text/html;charset=UTF-8");
```

- Cookie创建

1. 首次创建/获取，CookieID存在请求报文中
2. 之后使用，CookieID存在响应报文中

<img src=".\JavaWeb_Markdown笔记图片\Cookie_创建.png" alt="Cookie_创建" style="zoom:67%;" />

```java
public class CookieServlet extends BaseServlet{

  protected void createCookie(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    Cookie cookie = new Cookie("key1", "value1");
    // 添加 -- 通知客户端
    resp.addCookie(cookie);
    resp.getWriter().write("Cookie创建成功");
  }
}
```

- 服务器获取Cookie：服务器获取客户端的 Cookie 只需要一行代码:req.getCookies() Cookie[]

```java
 protected void getCookie(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    Cookie[] cookies = req.getCookies();
    // 只能遍历获取需要的Cookie
    for (Cookie cookie: cookies) {
      resp.getWriter().write("遍历结果：key=" + cookie.getName() + ",value=" + cookie.getValue() + "<br />");
    }
    // 通常用工具类实现
    Cookie neededCookie = CookieUtils.findCookie("key1", cookies);
    resp.getWriter().write("查找结果：key=" + neededCookie.getName() + ",value=" + neededCookie.getValue() + "<br />");
  }
}
```

- Cookie 值的修改

注意：

对于 Version 0cookie，值不应包含空格、方括号、圆括号、等号、逗号、双引号、斜杠、问号、at 符号、冒号和分号（中文）。空值在所有浏览器上的行为不一定相同。

如果需要上述字符，可以使用Base64处理后传输。

1. 方案一:
   - 先创建一个要修改的同名的 Cookie 对象
   - 在构造器，同时赋于新的 Cookie 值。
   - 调用 response.addCookie( Cookie );
2. 方案二:
   - 先查找到需要修改的 Cookie 对象
   - 调用 setValue()方法赋于新的 Cookie 值。
   - 调用 response.addCookie()通知客户端保存修改

- 浏览器查看/删除 Cookie

- Cookie 生命控制

1. Cookie 的生命控制指的是如何管理 cookie 什么时候被销毁(删除)
2. cookie.setMaxAge()
   - 正数，表示在指定的秒数后过期 -- 过期时间是参考格林时间
   - 负数，表示浏览器关闭，cookie 就会被删除(默认值是-1)
   - 零，表示马上删除 Cookie

- Cookie有效路径 Path 的设置

1. Cookie 的 path 属性可以有效的过滤哪些 Cookie 可以发送给服务器。哪些不发。path 属性是通过请求的地址来进行有效的过滤。
2. 请求地址为http://ip:port/工程路径/a.html 时
   - CookieA：path=/工程路径  会发送
   - CookieB：path=/工程路径/abc  不会发送
3. 请求地址为http://ip:port/工程路径/abc/a.html 时
   - CookieA：path=/工程路径  会发送
   - CookieB：path=/工程路径/abc  会发送
4. 服务器只会发送满足工程路径的Cookie

- 免用户名登录的实现

<img src=".\JavaWeb_Markdown笔记图片\Cookie_免用户名登录.png" alt="Cookie_免用户名登录" style="zoom:67%;" />

- CookieServlet

```java
package com.uestc.servlet;

import com.uestc.utils.CookieUtils;

import javax.servlet.ServletException;
import javax.servlet.http.Cookie;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

public class CookieServlet extends BaseServlet{
  protected void testPath(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    Cookie cookie = new Cookie("path1", "path1");
    cookie.setPath(req.getContextPath() + "/abc");
    resp.addCookie(cookie);
    resp.getWriter().write("创建带有path的Cookie");
  }

  protected void testAge(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    Cookie cookie = new Cookie("ageName", "ageValue");
    cookie.setMaxAge(0);
    resp.addCookie(cookie);
    resp.getWriter().write("查看Cookie");
  }

  protected void createCookie(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    Cookie cookie = new Cookie("key2", "value2");
    // 添加 -- 通知客户端
    resp.addCookie(cookie);
    resp.getWriter().write("Cookie创建成功");
  }
  protected void getCookie(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    Cookie[] cookies = req.getCookies();
    // 只能遍历获取需要的Cookie
    for (Cookie cookie: cookies) {
      resp.getWriter().write("遍历结果：key=" + cookie.getName() + ",value=" + cookie.getValue() + "<br />");
    }
    // 通常用工具类实现
    Cookie neededCookie = CookieUtils.findCookie("key1", cookies);
    resp.getWriter().write("查找结果：key=" + neededCookie.getName() + ",value=" + neededCookie.getValue() + "<br />");
  }
  protected void updateCookie(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    //- 先创建一个要修改的同名的 Cookie 对象
    //- 在构造器，同时赋于新的 Cookie 值。
    Cookie cookieNew = new Cookie("key1", "newValue1");
    //- 调用 response.addCookie( Cookie );
    resp.addCookie(cookieNew);
    resp.getWriter().write("key1 -- Cookie已经修改");
  }
  protected void updateCookie2(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    //- 先查找到需要修改的 Cookie 对象
    //- 调用 setValue()方法赋于新的 Cookie 值。
    //- 调用 response.addCookie()通知客户端保存修改
    Cookie[] cookies = req.getCookies();
    Cookie neededCookie = CookieUtils.findCookie("key1", cookies);
    neededCookie.setValue("setNewValue");
    resp.addCookie(neededCookie);
  }
}
```



# Session：会话

- 基本概念

1. Session 就一个接口(Httpsession)。
2. Session 就是会话。它是用来维护一个客户端和服务器之间关联的一种种技术。
3. 每个客户端都有自己的一个 session 会话 。
4. session 会话中，我们经常用来**保存用户登录之后**的信息，信息**保存在服务器端**。

- 如何创建 Session 和获取：request.getSession()

1. 第一次调用是:创建 session 会话。
2. 之后调用都是:获取前面创建好的session 会话对象。
3. 判断是不是才创建的Session：isNew()
   - true 表示才创建
   - fasle 表示之前已经创建
4. 每个Session都有一个唯一的ID值。

- Session 生命周期控制

1. public void setMaxlnactivelnterval(int interval) 设置Session的超时时长，超过指定的时长，session 就会被销毁。

   - 修改指定Session的超时时长

2. public int getMaxlnactivelnterval() 获取 Session的超时时间

   - Session 默认的超时时间长为 30 分钟。

   - 因为在 Tomcat 服务器的配置文件 web.xm中默认有以下的配置,它就表示配置了当前Tomcat服务器下所有的session
     超时配置默认时长为:30 分钟。

     ```xml
     <session-config>
     <session-timeout>30</session-timeout>
     </session-config>
     ```

   - 在工程内的web.xml设置上述配置就可以修改默认时长

     ```xml
     <session-config>
         <session-timeout>15</session-timeout>
       </session-config>
     ```

- Session超时的概念：客户端两次请求的最大间隔时长。

![Session_超时时长](.\JavaWeb_Markdown笔记图片\Session_超时时长.png)

- 设置对话立即超时：public void invalidate()

```java
  protected void deleteNow(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    HttpSession session = req.getSession();
    session.invalidate();
    resp.getWriter().write("当前Session立即超时");
  }
  protected void life3(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    HttpSession session = req.getSession();
    session.setMaxInactiveInterval(3);
    resp.getWriter().write("当前Session设置为3秒后超时");

  }
  protected void defaultLife(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    int time = req.getSession().getMaxInactiveInterval();
    resp.getWriter().write("默认Session超时时长：" + time);
  }
```

- **浏览器和Session** 之间关联的技术

1. session 技术，底层其实是基于 cookie 技术来实现的。

<img src=".\JavaWeb_Markdown笔记图片\Session_和浏览器的关联.png" alt="Session_和浏览器的关联" style="zoom:67%;" />

# 书城：第六阶段

- 登陆---显示用户名
- 登出---注销用户

1. 销毁 session 中用户登录的信息(或者销毁 session)
2. 重定向到首页或登录页面

- 表单重复提交有三种常见的情况:

1. 提交完表单：服务器使用请求转发进行页面跳转。此时，用户按下功能键F5，就会发起最后一次的请求。造成表单重复提交问题。
   - 解决方法:**使用重定向来进行跳转**
2. 网络延迟/服务器忙，服务器未响应，用户手动重复提交。
3. 用户回退浏览器重新提交。
   - 后面两种解决方法：使用**验证码**

- 表单重复提：验证码

![验证码_重复提交](.\JavaWeb_Markdown笔记图片\验证码_重复提交.png)

- 使用谷歌 kaptcha 图片验证码

1. 添加Jar包
   - kaptcha-2.3.jar
2. 在 web.xml 中去配置用于生成验证码的 servlet 程序

```xml
<servlet>
    <servlet-name>KaptchaServlet</servlet-name>
    <servlet-class>com.google.code.kaptcha.servlet.KaptchaServlet</servlet-class>
  </servlet>
  <servlet-mapping>
    <servlet-name>KaptchaServlet</servlet-name>
    <url-pattern>/kaptchaServlet.jpg</url-pattern>
  </servlet-mapping>
```

3. 在表单中使用img标签去显示验证码图片并使用它

```jsp
<form action="http://localhost:8080/_13_cookie_session/loginServlet" method="get">
    用户名：<input type="text" name="username" value="${cookie.username.value}" /> <br />
    密码： <input type="password" name="password" /> <br />
    验证码： <input type="text" name="code">
    <img src="http://localhost:8080/_13_cookie_session/kaptchaServlet.jpg" alt="" style="width: 100px; height: 22px"> <br />
    <input type="submit" value="登录" />
  </form>
```

4. 在服务器获取谷歌生成的猃证码和客户端发送过来的验证码比较使用。

```java
public class RegistServlet extends HttpServlet {
  @Override
  protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    // 获取
    String token = (String) req.getSession().getAttribute("KAPTCHA_SESSION_KEY");
    // 删除
    req.getSession().removeAttribute("KAPTCHA_SESSION_KEY");
    // 获取表单的code
    String code = req.getParameter("code");
    String username = req.getParameter("username");
    if (token != null && token.equalsIgnoreCase(code)) {
      System.out.println("保存到数据库:[" + username + "]");
      resp.sendRedirect(req.getContextPath() + "/ok.jsp");
    } else {
      System.out.println("请勿重复提交");
    }
  }
}
```

- 在书城项目中使用验证码
- 实现切换验证码

1. 部分浏览器存在缓存机制可能无法刷新

![验证码_使用](.\JavaWeb_Markdown笔记图片\验证码_使用.png)

2. js

```javascript
// 给验证码图片绑定单击事件
$("#code_img").click(function () {
    // src属性表示验证码img标签的 图片路径。它可读，可写
    this.src = "${basePath}/kaptcha.jpg?d=" + new Date();
})
```

# 书城：第七阶段

## 购物车模块

- 购物车模块需求分析

![购物车_实现思路](.\JavaWeb_Markdown笔记图片\购物车_实现思路.png)

- 购物车实现
- 首页，购物车回显

```java
// Referer 请求头
System.out.println("Referer:" + req.getHeader("Referer"));
```

![购物车_回显](.\JavaWeb_Markdown笔记图片\购物车_回显.png)

- 修改购物车商品数量

<img src=".\JavaWeb_Markdown笔记图片\购物车_修改商品数量.png" alt="购物车_修改商品数量" style="zoom: 67%;" />

## 订单模块

- 订单模块：需求分析

![购物车_订单](.\JavaWeb_Markdown笔记图片\购物车_订单.png)

- 创建对应的数据表

```mysql
CREATE TABLE t_order(
`order_id` VARCHAR(50) PRIMARY KEY,
`create_time` DATETIME,
`price` DECIMAL(11, 2),
`status` INT,
`user_id` INT,
FOREIGN KEY(`user_id`) REFERENCES t_user(`id`)
);

CREATE TABLE t_order_item(
`id` INT PRIMARY KEY AUTO_INCREMENT,
`name` VARCHAR(100),
`count` INT,
`price` DECIMAL(11, 2),
`total_price` DECIMAL(11, 2),
`order_id` VARCHAR(50),
FOREIGN KEY(`order_id`) REFERENCES t_order(`order_id`)
);
```

- Order和OrderItem的pojo类

- 编写订单模块的 Dao 程序和测试

# Filter：过滤器

- Filter 什么是过滤器

1. Filter 过滤器它是 JavaWeb 的三大组件之一。三大组件分别是:Servlet程序、Listener 监听器、filter 过滤器
2. Filter 过滤器它是 JavaEE的规范。也就是接口
3. Filter 过滤器它的作用是:**拦截请求**，过滤响应。
   - 拦截请求常见的应用场景有:
     - 1、权限检查
     - 2、日记操作
     - 3、事务管理
     - ……等等

- Filter 的初体验

1. 要求:在你的 web 工程下，有一个admin 目录。这个 admin目录下的所有资源(html页面、jpg图片、jsp 文件、等等)都必
   须是用户登录之后才允许访问。
2. 思考:根据之前我们学过内容。我们知道，用户登录之后都会把用户登录的信息保存到 session 域中。所以要检查用户是否
   登录，可以判断 Session 中否包含有用户登录的信息即可。

```jsp
// 初级判断方法 -- 有局限性 -> 使用filter实现 -- 高级
<%
  Object user = session.getAttribute("user");
  if (user == null) {
    request.getRequestDispatcher("/login.jsp").forward(request, response);
    return;
  }
%>
```

- Filter实现 :使用步骤

![Filter_使用分析](.\JavaWeb_Markdown笔记图片\Filter_使用分析.png)

1. 实现javax.servlet.filter 接口

2. 重写对应方法：doFilter等

   ```java
   public class AdminFilter implements Filter {
     @Override
     public void init(FilterConfig filterConfig) throws ServletException {
   
     }
   /*
   doFilter方法，专门用于拦截请求。可以做权限检查
    */
     @Override
     public void doFilter(ServletRequest servletRequest, ServletResponse servletResponse, FilterChain filterChain) throws IOException, ServletException {
       HttpServletRequest httpServletRequest = (HttpServletRequest) servletRequest;
       HttpSession session = httpServletRequest.getSession();
       Object user = session.getAttribute("user");
       if (user == null) {
         servletRequest.getRequestDispatcher("/login.jsp").forward(servletRequest, servletResponse);
         return;
       } else {
         // 让程序继续往下访问用户的目标资源 -- 非常重要 -- 没有该语句无法正确访问资源
         filterChain.doFilter(servletRequest, servletResponse);
       }
     }
     @Override
     public void destroy() {
   
     }
   }
   ```

3. 在web.xml文件配置filter

   ```xml
   <!-- 配置filter过滤器 -->
     <filter>
   <!--  别名  -->
       <filter-name>AdminFilter</filter-name>
   <!--  全类名  -->
       <filter-class>com.uestc.filter.AdminFilter</filter-class>
     </filter>
     <filter-mapping>
   <!--  需要使用的filter  -->
       <filter-name>AdminFilter</filter-name>
   <!--  需要拦截的路径  -->
   <!--  / 表示 http://ip:port/工程名/  -->
   <!--  /admin/* 映射到 http://ip:port/工程名/admin/*  -->
       <url-pattern>/admin/*</url-pattern>
     </filter-mapping>
   ```

- filter的声明周期：Filter 的生命周期包含几个方法：

1. 构造器方法
2. init 初始化方法
   - 第1，2步，在web 工程启动的时候执行(Filter 已经创建)
3. doFiter 过滤方法
   - 第3步，每次拦截到请求，就会执行
4. destroy 销毁
   - 第4步，停止 web 工程的时候，就会执行(停止 web 工程，也会销毁 Filter 过滤器)

- FilterConfig类

1. Filterconfig 类见名知义，它是 Filter 过滤器的配置文件类。
   Tomcat 每次创建 Filter 的时候，也会同时创建一个 FilterConfig 类，这里包含了 Filter 配置文件的配置信息。

2. FilterConfig 类的作用是获取 filter 过滤器的配置内容：

   - 获取 Filter 的名称 filter-name 的内容

   - 获取在 Filter 中配置的 init-param 初始化参数

     ```xml
       <filter>
         <filter-name>AdminFilter</filter-name>
         <filter-class>com.uestc.filter.AdminFilter</filter-class>
         <init-param>
           <param-name>username</param-name>
           <param-value>root</param-value>
         </init-param>
         <init-param>
           <param-name>url</param-name>
           <param-value>jdbc:mysql://localhost3306/test</param-value>
         </init-param>
       </filter>
     ```

     ```java
     // 获取Filter的名称 filter-name的内容
         // 获取在web.xml中配置的init-param初始化参数
         // 获取servletcontext对象
         System.out.println("filter-name的值" + filterConfig.getFilterName());
         System.out.println("初始化参数：" + filterConfig.getInitParameter("url"));
         System.out.println(filterConfig.getServletContext());
     ```

   - 获取 ServletContext 对象

- FilterChain 过滤器链：多个过滤器配合工作

![FilterChain_使用分析](.\JavaWeb_Markdown笔记图片\FilterChain_使用分析.png)

1. 在web.xml文件中的配置顺序决定多个filter的执行顺序
2. 多个filter执行的特点
   - 所有filter和目标资源默认都执行在同一个线程中
   - 多个Filter共同执行的时候，它们都使用同一个Request对象。

- Filter 的拦截路径

1. 精确匹配
   - <url-pattern>/target.jsp</url-pattern>
   - 以上配置的路径，表示请求地址必须为:http://ip:port/工程名/target.jsp
2. 目录匹配
   - <url-pattern>/admin/*</url-pattern>
   - 以上配置的路径，表示请求地址必须为:http://ip:port/工程名/target.jsp/admin/* 该目录下的资源
3. 后缀名匹配
   - <url-pattern>*.html</url-pattern>
   - 以上配置的路径，表示请求必须以.html结尾才会执行拦截
   - 不一定是类型，字符串结尾同样可以

# 书城：第八阶段

- 添加图书管理的Filter过滤器

```xml
<filter>
    <filter-name>ManagerFilter</filter-name>
    <filter-class>com.uestc.filter.ManagerFilter</filter-class>
</filter>
<filter-mapping>
    <filter-name>ManagerFilter</filter-name>
    <!-- 同时拦截资源访问和servlet的访问 -->
    <url-pattern>/pages/manager/*</url-pattern>
    <url-pattern>/manager/bookServlet</url-pattern>
</filter-mapping>
```

## Filter和ThreadLocal组合管理事务

- ThreadLocal的使用

1. ThreadLocal 的作用，它可以解决多线程的数据安全问题。
2. ThreadLocal 的特点:
   - ThreadLocal 可以为当前线程关联一个数据。(它可以像 Map 一样存取数据，**key为当前线程**)。
   - 每一个 ThreadLocal 对象，只能为当前线程**关联一个数据**，如果要为当前线程关联**多个数据**，就需要使用**多个ThreadLocal 对象实例**。
   - 每个 ThreadLocal 对象实例定义的时候，一般都是 static 类型(API推荐 private static)。
   - ThreadLocal 中保存数据，在线程销毁后。会由JVM虚拟自动释放。

- Filter和ThreadLocal组合管理事务

1. 需要相关联的操作都执行成功
2. 否则就都不执行

- Jdbc的数据库事务管理

![JDBC_数据库事务管理](.\JavaWeb_Markdown笔记图片\JDBC_数据库事务管理.png)

1. 要确保所有操作都在一个事务内，就必须要确保，所有操作都使用同-个Connection连接对象。
   - ThreadLocal要确保所有操作都使用同一个Connection连接对象。
   - 那么操作的前提条件是所有操作都必须在同一个线程中完成。



- 使用 Filter 过滤器统一给所有的 Service 方法都加上 try-catch。来进行实现的管理。

![FilterChain_使用分析](.\JavaWeb_Markdown笔记图片\FilterChain_使用分析.png)

- 将所有异常都统一交给 Tomcat，让 Tomcat 展示友好的错误信息页面

1. 在 web.xml 中我们可以通过错误页面配置来管理。

   ```xml
   <!-- error-page标签配置，服务器出错之后，自动跳转的页面  -->
     <error-page>
   <!--  error-code是错误类型  -->
       <error-code>500</error-code>
       <location>/pages/error/error500.jsp</location>
     </error-page>
   ```

2. 添加对应的友好界面





# JSON、AJAX、i18n

## JSON

- 什么是Json

1. JSON (JavaScript 0bject Notation)是一种轻量级的数据交换格式。易于人阅读和编写。同时也易于机器解析和生成。JSON
   采用完全独立于语言的文本格式，而且很多语言都提供了对 json的支持(包括C，c+t，C#,Java，JavaScript,Perl,Python
   等)。这样就使得 JSON 成为**理想的数据交换格式**。

2. 轻量级指的是跟 xml做比较。
3. 数据交换指的是客户端和服务器之间业务数据的传递格式。

### JSON 在 JavaScript 中的使用

- JSON的定义

json是由键值对组成，并且由花括号(大括号)包围。每个键由引号引起来，键和值之间使用冒号进行分隔，多组键值对之间进行逗号进行分隔。

```javascript
var jsonObj = {
      "key1":12,
      "key2":"anc12",
      "key3":true,
      "key4":[11, "arr", false],
      "key5": {
        "inkey1":511,
        "inkey2":"value2",
      },
      "key6": [{
        "inkey1":111,
        "inkey2":"value2",
      },
        {"inkey1":222,
          "inkey2":"value22",}
      ]
    }
    alert(typeof jsonObj); // object 类型
```

- JSON的访问

1. json 本身是一个对象。
2. json 中的 key 我们可以理解为是对象中的一个属性。
3. json 中的 key访问就跟访问对象的属性一样: json对象.key

```javascript
    alert(jsonObj.key1); // object 类型
// 遍历元素
for (var i = 0; i < jsonObj.key4.length; i++) {
  alert(jsonObj.key4[i]);
}
alert(jsonObj.key5.inkey1);
```

- json的两个常用形式

1. json 的存在有两种形式。
   - 一种是:对象的形式存在，我们叫它json 对象。
   - 一种是:字符串的形式存在，我们叫它json字符串。
2. JSON.stringify()：把 json 对象转换成为 json 字符串
3. JSON.parse()：把json 字符串转换成为 json 对象

```js
var jsonObjString = JSON.stringify(jsonObj);
alert(jsonObjString); // 类似Java的toString()
var jsonObj2 = JSON.parse(jsonObjString);
alert(jsonObj2)
```

- JSON在java 中的使用

0. 导入gson的jar包

1. javaBean和json 的互转

   ```java
   @Test
     public void test1(){
     Person person = new Person(1, "name1");
     // 创建Gson对象
     Gson gson = new Gson();
     // 转化为json的String形式
     String json = gson.toJson(person);
     System.out.println(json);
     // String形式转化为Java对象
     Person jsonToPerson = gson.fromJson(json, Person.class);
     System.out.println(jsonToPerson);
   }
   ```

2. List 和 json 的互转

   ````java
   @Test
     public void test2(){
       List<Person> list = new ArrayList<>();
       list.add(new Person(1, "name1"));
       list.add(new Person(2, "name2"));
       list.add(new Person(3, "name3"));
       Gson gson = new Gson();
       String personList = gson.toJson(list);
       System.out.println(personList);
       // String形式转化为Java对象
       List<Person> reList = gson.fromJson(personList, new PersonListType());
       System.out.println(reList);
     }
   ````

   ```java
   public class PersonListType extends TypeToken<List<Person>> {
   }
   ```

3. map 和json 的互转

   ```java
   Map<Integer, Person> map = new HashMap<>();
       map.put(1, new Person(1, "name1"));
       map.put(2, new Person(2, "name2"));
       map.put(3, new Person(3, "name3"));
       Gson gson = new Gson();
       String personList = gson.toJson(map);
       System.out.println(personList);
       // String形式转化为Java对象
       Map<Integer, Person> reMap = gson.fromJson(personList, new PersonMapList());
       System.out.println(reMap);
   ```

   ```java
   public class PersonListType extends TypeToken<List<Person>> {
   }
   ```

4. 可以把这些类写成匿名内部类

```java
Map<Integer, Person> reMap = gson.fromJson(personList, new TypeToken<HashMap<Integer, Person>>(){});
```

## AJAX

- 基本概念

1. AJAK 即“Asynchronous Javascript And XML”(异步 JavaScrpt和 XML)，是指一种创建交互式网页应用的网页开发技术。
2. AJAK  是一种浏览器通过**js 异步发起请求**。**局部更新页面**的技术。
   - 局部更新页面：地址栏不会发生变化;不会舍弃原来的页面内容。
   - 异步发起请求：服务器什么时候响应什么时候运行程序。不会等待服务器的响应。提升用户体验(避免服务器响应时整个页面卡顿等待)。

- 演示案例

1. JS发起Ajax请求

```jsp
<%--
  Created by IntelliJ IDEA.
  User: 97359
  Date: 2024/5/16
  Time: 9:49
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
  <title>Title</title>
  <script type="text/javascript">
    // 在这里使用javascript语言发起Ajax请求，访问服务器AjaxServlet中javascriptAjax
    // 1 我们首先要创建XMLHttpRequest
    // 2 调用open方法设置请求参数
    // 3 调用send方法发送请求
    // 4 在send方法前绑定onreadystatechange事件，处理请求完成后的操作。
    function ajaxRequest() {
      var xmlHttpRequest = new XMLHttpRequest();
      xmlHttpRequest.open("GET", "http://localhost:8080/_15_filter/ajaxServlet?action=javaScriptAjax", true);
      xmlHttpRequest.send();
      xmlHttpRequest.onreadystatechange = function () {
        if (xmlHttpRequest.readyState == 4 && xmlHttpRequest.status == 200) {
          var parse = JSON.parse(xmlHttpRequest.responseText);
          document.getElementById("div01").innerHTML = "编号：+" + parse.id + "姓名：" + parse.name;
        }
      }
    }

  </script>
</head>
<body>
<button onclick="ajaxRequest()">ajax request</button>
<div id="div01">

</div>

</body>
</html>
```

2. 服务器返回数据

```java
public class AjaxServlet extends BaseServlet{

  protected void javaScriptAjax(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    System.out.println("收到Ajax请求");
    Person person = new Person(1, "name1嘻嘻嘻");
    Gson gson = new Gson();
    String json = gson.toJson(person);
    resp.getWriter().write(json);
  }
}
```



- XMLHttpRequest 对象的三个重要的属性:

![AJAX_htttpRequest对象](.\JavaWeb_Markdown笔记图片\AJAX_htttpRequest对象.png)

- 通常使用框架(Jquery)中的Ajax请求 :一般不使用原生

## jQuery 中的AJAX请求

- $.ajax方法

1. url	表示请求的地址
2. type	表示请求的类型 GET 或 POST请求
3. data	表示发送给服务器的数据
   - 格式有两种:
   - name=value&name=value
   - {key:value}
4. success	请求成功，响应的回调函数
5. dataType	响应的数据类型
   - 常用的数据类型有:
   - text 表示纯文本
   - xml 表示 xml数据
   - json 表示json 对象

- $.get 方法和$.post 方法

1. url	请求的 url 地址
2. data	发送的数据
3. callback	成功的回调函数
4. type	返回的数据类型

- $.getJSON 方法

1. url	请求的 url 地址
2. data	发送给服务器的数据
3. callback	成功的回调函数

- 表单序列化 serialize()

serialize()可以把表单中所有表单项的内容都获取到，并以name=value&name=value 的形式进行拼接。

```jsp
<%--
  Created by IntelliJ IDEA.
  User: 97359
  Date: 2024/5/16
  Time: 11:19
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
  <title>Title</title>
  <script src="static/script/jquery.js"></script>
  <script type="text/javascript">
    $(function () {
      $("#ajaxBtn").click(function () {
        $.ajax({
          url:"http://localhost:8080/_15_filter/ajaxServlet",
          // data:"action=jqueryAjax",
          data:{action:"jqueryAjax"},
          type:"GET",
          success: function (reData) {
            // alert("服务器返回的数据：" + reData);
            // var parse = JSON.parse(reData);
            // $("#msg").html("编号：" + parse.id + ",姓名：" + parse.name);
            $("#msg").html("编号：" + reData.id + ",姓名：" + reData.name);
          },
          // dataType:"text" // 文本需要自己转换为json对象
          dataType:"json"
        });
      });
      $("#getBtn").click(function () {
        $.get("http://localhost:8080/_15_filter/ajaxServlet","action=jqueryGet", function (reData) {
            $("#msg").html("GET编号：" + reData.id + ",姓名：" + reData.name);
        },
      "json")});
      $("#postBtn").click(function () {
        $.get("http://localhost:8080/_15_filter/ajaxServlet","action=jqueryPost", function (reData) {
            $("#msg").html("Post编号：" + reData.id + ",姓名：" + reData.name);
          },
          "json")});
      $("#getJSONBtn").click(function () {
        $.getJSON("http://localhost:8080/_15_filter/ajaxServlet","action=jqueryGetJSON", function (reData) {
            $("#msg").html("getJSON编号：" + reData.id + ",姓名：" + reData.name);
          })
      });
      $("#submit").click(function () {
        // alert($("#form01").serialize());
        $.getJSON("http://localhost:8080/_15_filter/ajaxServlet","action=jquerySerialize&" + $("#form01").serialize(), function (reData) {
          $("#msg").html("Serialize 编号" + reData.id + "姓名" + reData.name);
        })
      })

    });
  </script>
</head>
<body>

<button id="ajaxBtn">ajaxRequest</button>
<button id="getBtn">get请求</button>
<button id="postBtn">post请求</button>
<button id="getJSONBtn">getJSON</button>
<div id="msg">

</div>

<form id="form01">
  用户名：<input name="username" type="text" /><br />
  密码：<input name="password" type="password" /><br />
  下拉单选：<select name="Single">Single
  <option value="Single">Single</option>
  <option value="Single2">Single2</option>
</select>
  下拉多选：
  <select name="multiple" multiple="multiple">
    <option selected="selected" value="Multiple">Multiple</option>
    <option value="Multiple2">Multiple2</option>
    <option selected="selected" value="Multiple3">Multiple3</option>
  </select>
  复选：
  <input type="checkbox" name="check" value="check1" /> check1
  <input type="checkbox" name="check" value="check2" checked="checked" /> check2 <br/>
  单选：
  <input type="radio" name="radio" value="radio1" checked="checked" /> radio1
  <input type="radio" name="radio" value="radio2" /> radio2<br/>
</form>
<button id="submit">提交--serialize</button>

</body>
</html>
```

```java
package com.uestc.servlet;

import com.google.gson.Gson;
import com.uestc.pojo.Person;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

public class AjaxServlet extends BaseServlet{

  protected void javaScriptAjax(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    System.out.println("收到Ajax请求");
    Person person = new Person(1, "name1嘻嘻嘻");
    Gson gson = new Gson();
    String json = gson.toJson(person);
    resp.getWriter().write(json);
  }
  protected void jqueryAjax(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    System.out.println("jqueryAjax方法");
    Person person = new Person(1, "ZYP");
    Gson gson = new Gson();
    String json = gson.toJson(person);
    resp.getWriter().write(json);
  }
  protected void jqueryGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    System.out.println("Get方法");
    Person person = new Person(1, "ZYP");
    Gson gson = new Gson();
    String json = gson.toJson(person);
    resp.getWriter().write(json);
  }
  protected void jqueryPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    System.out.println("Post方法");
    Person person = new Person(1, "ZYP");
    Gson gson = new Gson();
    String json = gson.toJson(person);
    resp.getWriter().write(json);
  }
  protected void jqueryGetJSON(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    System.out.println("GetJSON方法");
    Person person = new Person(1, "ZYP");
    Gson gson = new Gson();
    String json = gson.toJson(person);
    resp.getWriter().write(json);
  }
  protected void jquerySerialize(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    System.out.println("jquerySerialize方法");
    System.out.println("用户名：" + req.getParameter("username"));
    System.out.println("密码：" + req.getParameter("password"));
    Person person = new Person(1, "ZYP");
    Gson gson = new Gson();
    String json = gson.toJson(person);
    resp.getWriter().write(json);
  }
}
```



## 书城：第九阶段

- ajax_验证用户名

![ajax_验证用户](.\JavaWeb_Markdown笔记图片\ajax_验证用户.png)



- 使用AJAX请求修改添加商品到购物车的实现
  ![ajax_购物车](.\JavaWeb_Markdown笔记图片\ajax_购物车.png)

## i18n国际化(了解)

- Internationalization -> i18n
- 国际化三要素

![i18n_国际化三要素](.\JavaWeb_Markdown笔记\JavaWeb_Markdown笔记图片\i18n_国际化三要素.png)

- 获取locale

```java
package com.uestc.i18n;
import org.junit.Test;
import java.util.Locale;
public class I18nTest {
  @Test
  public void testLocale() {
//    Locale locale = Locale.getDefault();
//    System.out.println(locale);
//    for (Locale available: Locale.getAvailableLocales()) {
//      System.out.println(available);
//    }
    // 获取常量对象
    System.out.println(Locale.CHINESE);
    System.out.println(Locale.US);
  }
}
```

- 设置配置文件和获取配置参数

```properties
// i18n_en_US.properties
username=用户名
password=密码
sex=性别
age=年龄
```

```properties
// i18n_en_US.properties
username=username_EN
password=password_EN
sex=sex_EN
age=age_EN
```

```java
@Test
  public void testI18n() {
    // 获取locale对象
    Locale locale = Locale.CHINA;
    // 通过指定的basename和Locale对象，读取相应的配置文件
    // i18n 是文件的前缀 可以修改 abc 也可以
    ResourceBundle bundle = ResourceBundle.getBundle("i18n", locale);
    System.out.println(bundle.getString("username"));
    System.out.println(bundle.getString("password"));
    System.out.println(bundle.getString("sex"));
    System.out.println(bundle.getString("age"));
  }
```

- 网页国际化

1. js脚本

```jsp
<%@ page import="java.util.Locale" %>
<%@ page import="java.util.ResourceBundle" %><%--
  Created by IntelliJ IDEA.
  User: 97359
  Date: 2024/5/20
  Time: 10:44
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
  <title>Title</title>
</head>
<body>
<%
  Locale locale = null;
  String country = request.getParameter("country");
  if ("cn".equals(country)) {
    locale = Locale.CHINA;
  } else if ("usa".equals(country)){
    locale = Locale.US;
  } else {
    locale = request.getLocale();
  }
  // 获取读取包(根据 指定的baseName和Locale读取 语言信息)
  ResourceBundle i18n = ResourceBundle.getBundle("i18n", locale);
%>
<a href="i18n.jsp?country=cn">中文</a>
<a href="i18n.jsp?country=usa">English</a>
<center>
  <h1><%=i18n.getString("regist")%> </h1>
  <table>
    <form>
      <tr>
        <td><%=i18n.getString("username")%></td>
        <td><input name="username" type="text"></td>
      </tr>
      <tr>
        <td><%=i18n.getString("password")%></td>
        <td><input name="password" type="password"></td>
      </tr>
      <tr>
        <td><%=i18n.getString("sex")%></td>
        <td><input type="radio" /><%=i18n.getString("boy")%>
          <input type="radio" /><%=i18n.getString("girl")%>
        </td>
      </tr>
      <tr>
        <td><%=i18n.getString("email")%></td>
        <td><input type="text" /></td>
      </tr>
      <tr>
        <td colspan="2" align="center">
          <input type="reset" value="<%=i18n.getString("reset")%>">
          <input type="submit" value="<%=i18n.getString("submit")%>">
        </td>

      </tr>
    </form>
  </table>
</center>
</body>
</html>

```

2. 使用el脚本

```jsp
<%@ page import="java.util.Locale" %>
<%@taglib prefix="fmt" uri="http://java.sun.com/jsp/jstl/fmt" %>
<%@ page import="java.util.ResourceBundle" %><%--
  Created by IntelliJ IDEA.
  User: 97359
  Date: 2024/5/20
  Time: 10:44
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
  <title>Title</title>
</head>
<body>
<%--
使用el标签实现
1 使用标签设置Locale信息
2 使用标签设置baseName
3 使用标签输出国际化信息
--%>
<%--使用标签设置Locale信息--%>
<fmt:setLocale value="${param.locale}" />
<%--使用标签设置baseName--%>
<fmt:setBundle basename="i18n"/>
<%--使用标签输出国际化信息--%>
<fmt:message key="username"/>

<a href="i18n_fmt.jsp?locale=zh_CN">中文</a>
<a href="i18n_fmt.jsp?locale=en_US">English</a>
<center>
<h1><fmt:message key="regist"/></h1>
<table>
<form>
<tr>
  <td><fmt:message key="username"/></td>
  <td><input name="username" type="text"></td>
</tr>
<tr>
  <td><fmt:message key="password"/></td>
  <td><input name="password" type="password"></td>
</tr>
<tr>
<td><fmt:message key="sex" /></td>
  <td><input type="radio" /><fmt:message key="boy"/>
  <input type="radio" /><fmt:message key="girl"/>
  </td>
  </tr>
  <tr>
    <td><fmt:message key="email"/></td>
    <td><input type="text" /></td>
  </tr>
  <tr>
    <td colspan="2" align="center">
      <input type="reset" value="<fmt:message key="reset"/>"/>
      <input type="submit" value="<fmt:message key="submit"/>"/>
    </td>
  </tr>
  </form>
  </table>
</center>
</body>
</html>
```

