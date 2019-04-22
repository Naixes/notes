
# 常见浏览器介绍

```
浏览器是网页运行的平台，五大浏览器：IE、火狐（Firefox）、谷歌（Chrome）、Safari和Opera。
```

## 浏览器内核（理解）             

```
浏览器内核又可以分成两部分：渲染引擎(layout engineer 或者 Rendering Engine)和 JS 引擎。

渲染引擎 它负责取得网页的内容（HTML、XML、图像等等）、整理讯息（例如加入 CSS 等），以及计算网页的显示方式，然后会输出至显示器或打印机。浏览器的内核的不同对于网页的语法解释会有不同，所以渲染的效果也不相同。

JS 引擎 则是解析 Javascript 语言，执行 javascript语言来实现网页的动态效果。

最开始渲染引擎和 JS 引擎并没有区分的很明确，后来 JS 引擎越来越独立，内核就倾向于只指渲染引擎。有一个网页标准计划小组制作了一个 ACID 来测试引擎的兼容性和性能。内核的种类很多，但是常见的浏览器内核可以分这四种：Trident、Gecko、Blink、Webkit。
五大浏览器采用的都是单内核，而随着浏览器的发展现在也出现了双内核。像360浏览器、QQ浏览器都是采用双内核。

四大内核分别是：Trident（也称IE内核）、webkit、Blink、Gecko
```

+ IE浏览器内核：Trident内核，也是俗称的IE内核；
+ Chrome浏览器内核：统称为Chromium内核或Chrome内核，以前是Webkit内核，现在是Blink内核；
+ Firefox浏览器内核：Gecko内核，俗称Firefox内核；
+ Safari浏览器内核：Webkit内核；
+ Opera浏览器内核：最初是自己的Presto内核，后来是Webkit，现在是Blink内核；

##移动端的浏览器内核

主要说的是系统内置浏览器的内核。

iPhone 和 iPad 等苹果 iOS 平台主要是 WebKit

Android 4.4 之前的 Android 系统浏览器内核是 WebKit，Android4.4 系统浏览器切换到了Chromium，内核是 Webkit 的分支 Blink

Windows Phone 8 系统浏览器内核是 Trident。

# Web标准（重点）

##  Web 标准构成

 Web标准不是某一个标准，而是由W3C和其他标准化组织制定的一系列标准的集合。主要包括结构（Structure）、表现（Presentation）和行为（Behavior）三个方面。

~~~
结构标准：结构用于对网页元素进行整理和分类，主要包括XML和XHTML两个部分。
样式标准：表现用于设置网页元素的版式、颜色、大小等外观样式，主要指的是CSS。
行为标准：行为是指网页模型的定义及交互的编写，主要包括DOM和ECMAScript两个部分
~~~

理想状态我们的源码： .HTML    .css   .js 

# HTML

HTML（英文Hyper Text Markup Language的缩写）中文译为“超文本标签语言”，主要是通过HTML标签对网页中的文本、图片、声音等内容进行描述。

## HTML骨架格式

```html
<HTML>   
    <head>     
        <title></title>
    </head>
    <body>
    </body>
</HTML>
```

1.  HTML标签：所有HTML中标签的一个根节点。

2. head标签：用于存放：title,meta,base,style,script,link

注意：在head标签中我们必须要设置的标签是title

3. title标签：让页面拥有一个属于自己的标题。

4. body标签：页面在的主体部分，用于存放所有的HTML标签：

## HTML标签分类

1. 双标签
2. 单标签 单标签也称空标签，是指用一个标签符号即可完整地描述某个功能的标签。


## HTML标签关系

1. 嵌套关系
2. 并列关系

# 工具

HTML骨架快捷键：

1.  html: 5   
2.  !

~~~
<!doctype html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport"
        content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
</head>
<body>

</body>
</html>
~~~

# 文档类型声明<!DOCTYPE>

~~~html
<!DOCTYPE html>
~~~

<!DOCTYPE> 标签位于文档的最前面，用于向浏览器说明当前文档使用哪种 HTML 或 XHTML 标准规范，必需在开头处使用<!DOCTYPE>标签为所有的XHTML文档指定XHTML版本和类型，只有这样浏览器才能按指定的文档类型进行解析，这里使用的是 html 5 的版本。

DTD文档类型定义：浏览器会使用它来判断文档类型，从而决定使用何种协议来解析 

# 字符集

<meta charset="UTF-8">

utf-8是目前最常用的字符集编码方式，常用的字符集编码方式还有gbk和gb2312。

gb2312 简单中文  包括6763个汉字

BIG5   繁体中文 港澳台等用

GBK包含全部中文字符    是GB2312的扩展，加入对繁体字的支持，兼容GB2312

UTF-8则包含全世界所有国家需要用到的字符

# HTML标签的语义化

## 为什么要有语义化标签

1. 方便代码的阅读和维护

2. 同时让浏览器或是网络爬虫可以很好地解析，从而更好分析其中的内容 

3. 使用语义化标签会具有更好地搜索引擎优化 


核心：合适的地方给一个最为合理的标签。

语义是否良好： 当我们去掉CSS之后，网页结构依然组织有序，并且有良好的可读性。

遵循的原则：先确定语义的HTML ，再选合适的CSS。

# HTML标签

## 排版标签

排版标签主要和css搭配使用，显示网页结构的标签，是网页布局最常用的标签。

### 标题标签 (熟记)

 单词缩写：  head   标题

HTML提供了6个等级的标题，即 <h1>、<h2>、<h3>、<h4>、<h5>和<h6>

> 注意： 
>
>  h1 标签因为重要，尽量少用， 一般h1 都是给logo使用。
>
> 默认情况下，HTML 会自动地在块级元素前后添加一个额外的空行，比如段落、标题元素前后。

### 段落标签( 熟记)

块级元素，单词缩写：  paragraph  段落 

~~~html
<p>  文本内容  </p>
~~~

默认情况下，文本在一个段落中会根据浏览器窗口的大小自动换行。

### 水平线标签(认识)

单词缩写：  horizontal  横线

```html
<hr />是单标签
```

 在网页中显示默认样式的水平线。

### 换行标签(熟记)

单词缩写：  break   打断 ,换行

```html
<br />
```

### div span标签(重点)

div  span    是没有语义的     是我们网页布局主要的2个容器，如果与 CSS 一同使用，可用于对大的内容块设置样式属性。 

div（分类块级元素），division  的缩写   分割， 分区的意思  其实有很多div 来组合网页。

span（分类行内元素），跨度，跨距；范围  

语法格式：

~~~html
<div> 这是头部 </div>    <span>今日价格</span>
~~~

## 文本格式化标签(熟记)

在网页中，有时需要为文字设置粗体、斜体或下划线效果，这时就需要用到HTML中的文本格式化标签，使文字以特殊的方式显示。

b（粗体）  i（斜体）  s（删除线）  u （下划线）  没有 强调的意思建议使用：

strong   em  del   ins  语义更强烈

## 标签属性

使用HTML制作网页时，如果想让HTML标签提供更多的信息，可以使用HTML标签的属性加以设置。其基本语法格式如下：

```html
<标签名 属性1="属性值1" 属性2="属性值2" …> 内容 </标签名>
```

## 图像标签img (重点)

单词缩写：   image  图像

其基本语法格式如下：

该语法中src属性用于指定图像文件的路径和文件名，他是img标签的必需属性。

```html
<img src="图像URL" />
```

| 属性  | 值                        | 说明           |
| ----- | ------------------------- | -------------- |
| src   | url                       | 路径           |
| alt   | 文本                      | 不显示时的替换 |
| title | 文本                      | 悬停内容       |
| align | bottom（默认）;middle;top | 文本对齐方式   |

结合map实现图像映射

``````html
<img src="1.jpg" usemap="#Map" />
<map name="Map">
	<area shape="热点形状" coords="坐标" href="链接" alt="替代文字" />
	<area shape="circle" coords="180,139,14" href ="/example/html/venus.html" target ="_blank" alt="Venus" />
	<area shape="rect" coords="0,0,110,260" href ="/example/html/sun.html"  target ="_blank" alt="Sun" />
</map>
``````

## 链接标签

单词缩写：  anchor 的缩写 

基本语法格式如下：

```html
<a href="跳转目标" target="目标窗口的弹出方式">文本或图像</a>
```

**href**：用于指定链接目标的**url**地址，当为标签应用href属性时，它就具有了超链接的功能。  Hypertext Reference的缩写。意思是超文本引用

**target**：用于指定链接页面的打开方式，其取值有**\_self**和**\_blank**两种，其中\_self为默认值，\_blank为在新窗口中打开方式。

注意：

1. 外部链接 需要添加 http:// www.baidu.com
2. 内部链接 直接链接内部页面名称即可 比如 < a href="index.html"> 首页 </a >
3. 如果当时没有确定链接目标时，通常将链接标签的href属性值定义为“#”(即href="#")，表示该链接暂时为一个空链接。
4. 不仅可以创建文本超链接，在网页中各种网页元素，如图像、表格、音频、视频等都可以添加超链接。

### 锚点定位 

通过创建锚点链接，用户能够快速定位到目标内容。
创建锚点链接分为两步：

~~~html
1.使用<a href="#id名">"链接文本"</a>创建链接文本。
2.使用相应的id名标注跳转目标的位置。
~~~

### base 标签

base 可以设置整体链接的打开状态   

base 写到  <head>  </head>  之间

`<base target='_blank' />`

##  特殊字符标签 （理解）

| 特殊字符 | 描述     | 代码    |
| -------- | -------- | ------- |
| <        |          | &lt     |
| >        |          | &gt     |
| &        |          | &amp    |
| ￥       |          | &yen    |
| &copy;   | 版权     | &copy   |
| &reg;    | 注册商标 | &reg    |
| &deg;    |          | &deg    |
| &plusmn; |          | &plusmn |
| &times;  |          | &times  |
| &divide; |          | &divide |
| ²        | 平方     | &sup2   |
| &nbsp;   | 空格     | &nbsp   |

## 注释标签

```html
    <!-- 注释语句 -->
```

# 路径

## 相对路径

1. 图像文件和HTML文件位于同一文件夹：只需输入图像文件的名称即可，如&lt;img src="logo.gif" /&gt;。
2. 图像文件位于HTML文件的下一级文件夹：输入文件夹名和文件名，之间用“/”隔开，如&lt;img src="img/img01/logo.gif" /&gt;。
3. 图像文件位于HTML文件的上一级文件夹：在文件名之前加入“../” ，如果是上两级，则需要使用 “../ ../”，以此类推，如&lt;img src="../logo.gif" /&gt;。

## 绝对路径

绝对路径

“D:\web\img\logo.gif”，或完整的网络地址，例如“http://www.itcast.cn/images/logo.gif”。

# 列表标签

## 无序列表 ul （重点）

无序列表的各个列表项之间没有顺序级别之分，是并列的。其基本语法格式如下：

```html
<ul>
  <li>列表项1</li>
  <li>列表项2</li>
  <li>列表项3</li>
  ......
</ul>
```

脚下留心：

```
 1. <ul></ul>中只能嵌套<li></li>，直接在<ul></ul>标签中输入其他标签或者文字的做法是不被允许的。
 2. <li>与</li>之间相当于一个容器，可以容纳所有元素。
```

## 有序列表 ol

有序列表即为有排列顺序的列表，其各个列表项按照一定的顺序排列定义，有序列表的基本语法格式如下：

```html
<ol type="A">
  <li>列表项1</li>
  <li>列表项2</li>
  <li>列表项3</li>
  ......
</ol>
```

type：A，a，I，i

## 自定义列表

定义列表常用于对术语或名词进行解释和描述，定义列表的列表项前没有任何项目符号。其基本语法如下：

```html
<dl>
  <dt>名词1</dt>
  <dd>名词1解释1</dd>
  <dd>名词1解释2</dd>
  ...
  <dt>名词2</dt>
  <dd>名词2解释1</dd>
  <dd>名词2解释2</dd>
  ...
</dl>
```

# 表格 table(会使用)

## 创建表格

在HTML网页中，要想创建表格，就需要使用表格相关的标签。创建表格的基本语法格式如下：

```html
<table>
  <tr>
    <td>单元格内的文字</td>
    ...
  </tr>
  ...
</table>
```

在上面的语法中包含三对HTML标签，分别为 &lt;table&gt;&lt;/table&gt;、&lt;tr&gt;&lt;/tr&gt;、&lt;td&gt;&lt;/td&gt;，他们是创建表格的基本标签，缺一不可，下面对他们进行具体地解释。

~~~
1.table用于定义一个表格。
2.tr 用于定义表格中的一行，必须嵌套在 table /table标签中，在 table /table中包含几对 tr /tr，就有几行表格。
3.td /td：用于定义表格中的单元格，必须嵌套在<tr></tr>标签中，一对 <tr> </tr>中包含几对<td></td>，就表示该行中有多少列（或多少个单元格）。
~~~

注意：

```
1. <tr></tr>中只能嵌套<td></td>
```

```
2. <td></td>标签，他就像一个容器，可以容纳所有的元素
```

## 表格属性

|    属性     |               描述               | 常用值                       |
| :---------: | :------------------------------: | ---------------------------- |
|   border    |               边框               |                              |
| cellspacing |   单元格与单元格边框之间的空隙   | 2（默认）                    |
| cellpadding | 单元格内容与单元格边框之间的空隙 | 1（默认）                    |
|    width    |                                  |                              |
|   height    |                                  |                              |
|    align    |           水平对齐方式           | left,center,right            |
|    frame    |     边框显示的样式，ie不兼容     | box,above,below,hsides,vside |

## 表头标签

表头一般位于表格的**第一行或第一列**，其文本加粗居中，如下图所示，即为设置了表头的表格。设置表头非常简单，只需用表头标签**&lt;th&gt;&lt;/th&gt;**替代相应的单元格标签&lt;td&gt;&lt;/td&gt;即可。

## 表格结构

```<caption></caption>```:表格标题,必须紧跟<table></table>标签后

在使用表格进行布局时，可以将表格划分为头部、主体和页脚（页脚因为有兼容性问题，我们不在赘述），具体 如下所示：

```<thead></thead>```：用于定义表格的头部。
必须位于<table></table> 标签中，一般包含网页的logo和导航等头部信息。

```<tbody></tbody>```：用于定义表格的主体。
位于<table></table>标签中，一般包含网页中除头部和底部之外的其他内容。

```
<table border="1">
  <thead>
    <tr>
      <th>Month</th>
      <th>Savings</th>
    </tr>
  </thead>

  <tfoot>
    <tr>
      <td>Sum</td>
      <td>$180</td>
    </tr>
  </tfoot>

  <tbody>
    <tr>
      <td>January</td>
      <td>$100</td>
    </tr>
    <tr>
      <td>February</td>
      <td>$80</td>
    </tr>
  </tbody>
</table>
```

## 合并单元格

跨行合并：rowspan（合并列）    跨列合并：colspan（合并行）

合并单元格的思想：

​     将多个内容合并的时候，就会有多余的东西，把它删除。

​     合并顺序：从上到下，从左到右

# 表单标签

在HTML中，一个完整的表单通常由表单控件（也称为表单元素）、提示信息和表单域3个部分构成。

1. 表单控件：包含了具体的表单功能项，如单行文本输入框、密码输入框、复选框、提交按钮、重置按钮等。

2. 提示信息：一个表单中通常还需要包含一些说明性的文字，提示用户进行填写和操作。

3. 表单域：  他相当于一个容器，用来容纳所有的表单控件和提示信息，可以通过他定义处理表单数据所用程序的url地址，以及数据提交到服务器的方法。如果不定义表单域，表单中的数据就无法传送到后台服务器。

## input 控件

在上面的语法中，&lt;input /&gt;标签为单标签，type属性为其最基本的属性，其取值有多种，用于指定不同的控件类型。除了type属性之外，&lt;input /&gt;标签还可以定义很多其他的属性，其常用属性如下表所示。

| 属性      | 值/描述                                                      |
| --------- | ------------------------------------------------------------ |
| type      | text,password,radio,checkbox,button,submit,reset,image(图像形式的提交按钮，结合src属性使用),file |
| name      | 同一组radio或checkbox的name相同                              |
| value     | 默认文本值                                                   |
| size      | 显示宽度                                                     |
| checked   | checked（radio或checkbox结合使用）                           |
| maxlength |                                                              |

##  label标签

label 标签为 input 元素定义标注（标签）。

作用：  用于绑定一个表单元素, 当点击label标签的时候, 被绑定的表单元素就会获得输入焦点

**for** 属性规定 label 与哪个表单元素绑定（id）。

```html
<label for="male">Male</label>
<input type="radio" name="sex" id="male" value="male">
```

## textarea控件(文本域)

如果需要输入大量的信息，就需要用到&lt;textarea&gt;&lt;/textarea&gt;标签。通过textarea控件可以轻松地创建多行文本输入框，其基本语法格式如下：

```html
<textarea cols="每行中的字符数" rows="显示的行数">
  文本内容
</textarea>
```

## 下拉菜单

使用select控件定义下拉菜单的基本语法格式如下

```html
<select>
  <option>选项1</option>
  <option>选项2</option>
  <option>选项3</option>
  ...
</select>
```

注意：

1. &lt;select&gt;</select&gt;中至少应包含一对&lt;option></option&gt;。
2. 在option 中定义selected =" selected "时，当前项即为默认选中项。

## 表单域

在HTML中，form标签被用于定义表单域，即创建一个表单，以实现用户信息的收集和传递，form中的所有有**name**属性的内容都会被提交给服务器。创建表单的基本语法格式如下：

```html
<form action="url地址" method="提交方式" name="表单名称">
  各种表单控件
</form>
```

常用属性：

1. Action在表单收集到信息后，需要将信息传递给服务器进行处理，action属性用于指定接收并处理表单数据的服务器程序的url地址。
2. method用于设置表单数据的提交方式，其取值为get或post。
3. name用于指定表单的名称，以区分同一个页面中的多个表单。

注意：  每个表单都应该有自己表单域。

#浏览器缓存机制

缓存可以说是性能优化中**简单高效**的一种优化方式了，它可以**显著减少网络传输所带来的损耗**。

对于一个数据请求来说，可以分为发起网络请求、后端处理、浏览器响应三个步骤。浏览器缓存可以帮助我们在第一和第三步骤中优化性能。比如说直接使用缓存而不发起请求，或者发起了请求但后端存储的数据和前端一致，那么就没有必要再将数据回传回来，这样就减少了响应数据。

##缓存位置

从缓存位置上来说分为四种，并且各自有**优先级**，当依次查找缓存且都没有命中的时候，才会去请求网络

1. Service Worker
2. Memory Cache
3. Disk Cache
4. Push Cache
5. 网络请求

###Service Worker

Service Worker 的缓存与浏览器其他内建的缓存机制不同，它可以让我们**自由控制**缓存哪些文件、如何匹配缓存、如何读取缓存，并且**缓存是持续性的**。

当 Service Worker 没有命中缓存的时候，我们需要去调用 `fetch` 函数获取数据。也就是说，如果我们没有在 Service Worker 命中缓存的话，会根据缓存查找优先级去查找数据。**但是不管我们是从 Memory Cache 中还是从网络请求中获取的数据，浏览器都会显示我们是从 Service Worker 中获取的内容。**

###Memory Cache

Memory Cache 也就是内存中的缓存，读取内存中的数据肯定比磁盘快。**但是内存缓存虽然读取高效，可是缓存持续性很短，会随着进程的释放而释放。** 一旦我们关闭 Tab 页面，内存中的缓存也就被释放了。

当我们访问过页面以后，再次刷新页面，可以发现很多数据都来自于内存缓存

![img](https://user-gold-cdn.xitu.io/2018/12/5/1677db8003dc8311?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)从内存中读取缓存

那么既然内存缓存这么高效，我们是不是能让数据都存放在内存中呢？

先说结论，这是**不可能**的。首先计算机中的内存一定比硬盘容量小得多，操作系统需要精打细算内存的使用，所以能让我们使用的内存必然不多。内存中其实可以存储大部分的文件，比如说 JSS、HTML、CSS、图片等等。但是浏览器会把哪些文件丢进内存这个过程就很**玄学**了，我查阅了很多资料都没有一个定论。

当然，我通过一些实践和猜测也得出了一些结论：

- 对于大文件来说，大概率是不存储在内存中的，反之优先
- 当前系统内存使用率高的话，文件优先存储进硬盘

###Disk Cache

Disk Cache 也就是存储在硬盘中的缓存，读取速度慢点，但是什么都能存储到磁盘中，比之 Memory Cache **胜在容量和存储时效性上。**

在所有浏览器缓存中，Disk Cache 覆盖面基本是最大的。它会**根据 HTTP Herder 中的字段判断**哪些资源需要缓存，哪些资源可以不请求直接使用，哪些资源已经过期需要重新请求。**并且即使在跨站点的情况下，相同地址的资源一旦被硬盘缓存下来，就不会再次去请求数据。**

###Push Cache

Push Cache 是 HTTP/2 中的内容，当以上三种缓存都没有命中时，它才会被使用。**并且缓存时间也很短暂，只在会话（Session）中存在，一旦会话结束就被释放。**

Push Cache 在国内能够查到的资料很少，也是因为 HTTP/2 在国内不够普及，但是 HTTP/2 将会是日后的一个趋势。这里推荐阅读 [HTTP/2 push is tougher than I thought](https://link.juejin.im/?target=https%3A%2F%2Fjakearchibald.com%2F2017%2Fh2-push-tougher-than-i-thought%2F) 这篇文章，但是内容是英文的，我翻译一下文章中的几个结论，有能力的同学还是推荐自己阅读

- 所有的资源都能被推送，但是 Edge 和 Safari 浏览器兼容性不怎么好
- 可以推送 `no-cache` 和 `no-store` 的资源
- 一旦连接被关闭，Push Cache 就被释放
- 多个页面可以使用相同的 HTTP/2 连接，也就是说能使用同样的缓存
- Push Cache 中的缓存只能被使用一次
- 浏览器可以拒绝接受已经存在的资源推送
- 你可以给其他域名推送资源

###网络请求

如果所有缓存都没有命中的话，那么只能发起请求来获取资源了。

那么为了性能上的考虑，大部分的接口都应该选择好缓存策略，接下来我们就来学习缓存策略这部分的内容。

##缓存策略

通常浏览器缓存策略分为两种：**强缓存**和**协商缓存**，并且缓存策略都是通过设置 HTTP Header 来实现的。

###强缓存

强缓存可以通过设置两种 HTTP Header 实现：`Expires` 和 `Cache-Control` 。**强缓存表示在缓存期间不需要请求**，`state code` 为 200。

####Expires

```
Expires: Wed, 22 Oct 2018 08:41:00 GMT
```

`Expires` 是 HTTP/1 的产物，表示资源会在 `Wed, 22 Oct 2018 08:41:00 GMT` 后过期，需要再次请求。并且 `Expires` **受限于本地时间**，如果修改了本地时间，可能会造成缓存失效。

####Cache-control

```
Cache-control: max-age=30
```

`Cache-Control` 出现于 HTTP/1.1，**优先级高于 Expires** 。该属性值表示资源会在 30 秒后过期，需要再次请求。

`Cache-Control` **可以在请求头或者响应头中设置**，并且可以组合使用多种指令

![img](https://user-gold-cdn.xitu.io/2018/12/6/1678234a1ed20487?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)多种指令配合流程图

从图中我们可以看到，我们可以将**多个指令配合起来一起使用**，达到多个目的。比如说我们希望资源能被缓存下来，并且是客户端和代理服务器都能缓存，还能设置缓存失效时间等等。

接下来我们就来学习一些常见指令的作用

![img](https://user-gold-cdn.xitu.io/2018/12/5/1677ef2cd7bf1bba?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)常见指令作用

###协商缓存

如果缓存过期了，就需要发起请求验证资源是否有更新。协商缓存可以通过设置两种 HTTP Header 实现：`Last-Modified` 和 `ETag` 。

当浏览器发起请求验证资源时，如果资源没有做改变，那么服务端就会返回 304 状态码，并且更新浏览器缓存有效期。

![img](https://user-gold-cdn.xitu.io/2018/12/6/16782357baddf1c6?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)协商缓存

1. **Last-Modified 和 If-Modified-Since**

`Last-Modified` 表示本地文件最后修改日期，`If-Modified-Since` 会将 `Last-Modified` 的值发送给服务器，询问服务器在该日期后资源是否有更新，有更新的话就会将新的资源发送回来，否则返回 304 状态码。

但是 `Last-Modified` 存在一些**弊端**：

- 如果本地**打开**缓存文件，即使没有对文件进行修改，但还是会造成 `Last-Modified` 被修改，服务端不能命中缓存导致发送相同的资源
- 因为 `Last-Modified` 只能**以秒计时**，如果在不可感知的时间内修改完成文件，那么服务端会认为资源还是命中了，不会返回正确的资源

因为以上这些弊端，所以在 HTTP / 1.1 出现了 `ETag` 。

2. **ETag 和 If-None-Match**

`ETag` 类似于文件指纹，`If-None-Match` 会将当前 `ETag` 发送给服务器，询问该资源 `ETag` 是否变动，有变动的话就将新的资源发送回来。并且 `ETag` **优先级**比 `Last-Modified` **高**。

以上就是缓存策略的所有内容了，看到这里，不知道你是否存在这样一个疑问。**如果什么缓存策略都没设置，那么浏览器会怎么处理？**

对于这种情况，浏览器会采用一个**启发式的算法**，通常会取响应头中的 `Date` 减去 `Last-Modified` 值的 10% 作为缓存时间。

##实际场景应用缓存策略

单纯了解理论而不付诸于实践是没有意义的，接下来我们来通过几个场景学习下如何使用这些理论。

###频繁变动的资源

对于频繁变动的资源，首先需要使用 `Cache-Control: no-cache` 使浏览器每次都请求服务器，然后配合 `ETag` 或者 `Last-Modified` 来验证资源是否有效。这样的做法虽然不能节省请求数量，但是能显著减少响应数据大小。

###代码文件

这里特指除了 HTML 外的代码文件，因为 HTML 文件一般不缓存或者缓存时间很短。

一般来说，现在都会使用工具来打包代码，那么我们就可以对文件名进行哈希处理，只有当代码修改后才会生成新的文件名。基于此，我们就可以给代码文件设置缓存有效期一年 `Cache-Control: max-age=31536000`，这样只有当 HTML 文件中引入的文件名发生了改变才会去下载最新的代码文件，否则就一直使用缓存。

#浏览器渲染原理

学习浏览器渲染原理更多的是为了解决性能的问题，如果不了解这部分的知识，你就不知道什么情况下会对性能造成损伤。

我们知道执行 JS 有一个 JS 引擎，那么执行渲染也有一个渲染引擎。同样，渲染引擎在不同的浏览器中也不是都相同的。比如在 Firefox 中叫做 **Gecko**，在 Chrome 和 Safari 中都是基于 **WebKit** 开发的。在这节中，主要学习关于 **WebKit** 的这部分渲染引擎内容。

## 浏览器接收到 HTML 文件并转换为 DOM 树

当我们打开一个网页时，浏览器都会去请求对应的 HTML 文件。虽然平时我们写代码时都会分为 JS、CSS、HTML 文件，也就是字符串，但是计算机硬件是不理解这些字符串的，所以在网络中传输的内容其实都是 `0` 和 `1` 这些**字节数据**。当浏览器接收到这些字节数据以后，它会将这些**字节数据转换为字符串**，也就是我们写的代码。

![img](https://user-gold-cdn.xitu.io/2018/11/27/16754281e59587f3?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

当数据转换为字符串以后，浏览器会先将这些字符串通过词法分析转换为**标记**（token），这一过程在词法分析中叫做**标记化**（tokenization）。

![img](https://user-gold-cdn.xitu.io/2018/11/27/16754288f37a5347?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

那么什么是标记呢？这其实属于编译原理这一块的内容了。简单来说，标记还是字符串，是构成代码的**最小单位**。这一过程会将代码分拆成一块块，并给这些内容打上标记，便于理解这些最小单位的代码是什么意思。

![img](https://user-gold-cdn.xitu.io/2018/11/27/167540a7b5cef612?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

当结束标记化后，这些标记会紧接着**转换为 Node**，最后这些 Node 会根据不同 Node 之前的联系构建为一颗 DOM 树。

![img](https://user-gold-cdn.xitu.io/2018/11/27/1675416cbea98c3c?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

以上就是浏览器从网络中接收到 HTML 文件然后一系列的转换过程。

![img](https://user-gold-cdn.xitu.io/2018/11/27/167542b09875a74a?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

当然，在解析 HTML 文件的时候，浏览器还会遇到 CSS 和 JS 文件，这时候浏览器也会去下载并解析这些文件，接下来就让我们先来学习浏览器如何解析 CSS 文件。

## 将 CSS 文件转换为 CSSOM 树

其实转换 CSS 到 CSSOM 树的过程和上一小节的过程是极其类似的

![img](https://user-gold-cdn.xitu.io/2018/11/27/167542a9af5f193f?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

在这一过程中，浏览器会确定下每一个节点的**样式**到底是什么，并且这一过程其实是**很消耗资源**的。因为样式你可以自行设置给某个节点，也可以通过继承获得。在这一过程中，浏览器得**递归** CSSOM 树，然后确定具体的元素到底是什么样式。

如果你有点不理解为什么会消耗资源的话，我这里举个例子

```html
<div>
  <a> <span></span> </a>
</div>
<style>
  span {
    color: red;
  }
  div > a > span {
    color: red;
  }
</style>
```

对于第一种设置样式的方式来说，浏览器只需要找到页面中所有的 `span` 标签然后设置颜色，但是对于第二种设置样式的方式来说，浏览器首先需要找到所有的 `span` 标签，然后找到 `span` 标签上的 `a` 标签，最后再去找到 `div` 标签，然后给符合这种条件的 `span` 标签设置颜色，这样的递归过程就很复杂。所以我们**应该尽可能的避免写过于具体的 CSS 选择器**，然后对于 HTML 来说也**尽量少的添加无意义标签**，保证**层级扁平**。

## 生成渲染树

当我们生成 DOM 树和 CSSOM 树以后，就需要将这两棵树**组合为渲染树**。

![img](https://user-gold-cdn.xitu.io/2018/11/27/16754488529c48bd?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

在这一过程中，不是简单的将两者合并就行了。渲染树只会包括**需要显示的节点**和这些节点的样式信息，如果某个节点是 `display: none` 的，那么就不会在渲染树中显示。

当浏览器生成渲染树以后，就会根据渲染树来进行**布局**（也可以叫做回流），然后调用 GPU 绘制，合成图层，显示在屏幕上。对于这一部分的内容因为过于底层，还涉及到了硬件相关的知识，这里就不再继续展开内容了。

那么通过以上内容，我们已经详细了解到了浏览器从接收文件到将内容渲染在屏幕上的这一过程。接下来，我们将会来学习上半部分遗留下来的一些知识点。

## 为什么操作 DOM 慢

想必大家都听过操作 DOM 性能很差，但是这其中的原因是什么呢？

因为 DOM 是属于渲染引擎中的东西，而 JS 又是 JS 引擎中的东西。当我们**通过 JS 操作 DOM 的时候，其实这个操作涉及到了两个线程之间的通信，那么势必会带来一些性能上的损耗。**操作 DOM 次数一多，也就等同于一直在进行线程之间的通信，并且操作 DOM 可能还会带来重绘回流的情况，所以也就导致了性能上的问题。

> 经典面试题：插入几万个 DOM，如何实现页面不卡顿？

对于这道题目来说，首先我们肯定不能一次性把几万个 DOM 全部插入，这样肯定会造成卡顿，所以解决问题的重点应该是如何分批次部分渲染 DOM。大部分人应该可以想到通过 `requestAnimationFrame`（计时器）的方式去循环的插入 DOM，其实还有种方式去解决这个问题：**虚拟滚动**（virtualized scroller）。

**这种技术的原理就是只渲染可视区域内的内容，非可见区域的那就完全不渲染了，当用户在滚动的时候就实时去替换渲染的内容。**

![img](https://user-gold-cdn.xitu.io/2018/12/15/167b1c6887ecbba7?imageslim)

从上图中我们可以发现，即使列表很长，但是渲染的 DOM 元素永远只有那么几个，当我们滚动页面的时候就会实时去更新 DOM，这个技术就能顺利解决这道经典面试题。如果你想了解更多的内容可以了解下这个 [react-virtualized](https://link.juejin.im/?target=https%3A%2F%2Fgithub.com%2Fbvaughn%2Freact-virtualized)。

## 什么情况阻塞渲染

首先渲染的前提是生成渲染树，所以 **HTML 和 CSS 肯定会阻塞渲染**。如果你想渲染的越快，你越应该降低一开始需要渲染的文件**大小**，并且**扁平层级，优化选择器**。

然后当浏览器在**解析到 `script` 标签时，会暂停构建 DOM**，完成后才会从暂停的地方重新开始。也就是说，如果你想首屏渲染的越快，就越**不应该在首屏就加载 JS 文件，这也是都建议将 `script` 标签放在 `body` 标签底部的原因。**

当然在当下，并不是说 `script` 标签必须放在底部，因为你可以给 `script` 标签添加 `defer` 或者 `async` 属性。

当 `script` 标签加上 `defer` 属性以后，表示该 JS 文件会并行下载，但是会放到 HTML 解析完成后顺序执行，所以对于这种情况你可以把 `script` 标签放在任意位置。

对于没有任何依赖的 JS 文件可以加上 `async` 属性，表示 JS 文件下载和解析不会阻塞渲染。

## 重绘（Repaint）和回流（Reflow）

重绘和回流会在我们设置节点样式时频繁出现，同时也会很大程度上影响性能。

- 重绘是当节点需要更改外观而不会影响布局的，比如改变 `color` 就叫称为重绘
- 回流是布局或者几何属性需要改变就称为回流。

回流**必定**会发生重绘，重绘**不一定**会引发回流。回流所需的成本比重绘高的多，改变父节点里的子节点很可能会导致父节点的一系列回流。

以下几个动作可能会导致性能问题：

- 改变 `window` 大小
- 改变字体
- 添加或删除样式
- 文字改变
- 定位或者浮动
- 盒模型

并且很多人不知道的是，重绘和回流其实也和 Eventloop 有关。

1. 当 Eventloop 执行完 Microtasks 后，会判断 `document` 是否需要更新，因为浏览器是 60Hz 的刷新率，每 16.6ms 才会更新一次。
2. 然后判断是否有 `resize` 或者 `scroll` 事件，有的话会去触发事件，所以 `resize` 和 `scroll` 事件也是至少 16ms 才会触发一次，并且自带节流功能。
3. 判断是否触发了 media query
4. 更新动画并且发送事件
5. 判断是否有全屏操作事件
6. 执行 `requestAnimationFrame` 回调
7. 执行 `IntersectionObserver` 回调，该方法用于判断元素是否可见，可以用于懒加载上，但是兼容性不好
8. 更新界面
9. 以上就是一帧中可能会做的事情。如果在一帧中有空闲时间，就会去执行 `requestIdleCallback`回调。

以上内容来自于 [HTML 文档](https://link.juejin.im/?target=https%3A%2F%2Fhtml.spec.whatwg.org%2Fmultipage%2Fwebappapis.html%23event-loop-processing-model)。

### 减少重绘和回流

- 使用 `transform` 替代 `top`

```js
<div class="test"></div>
<style>
  .test {
    position: absolute;
    top: 10px;
    width: 100px;
    height: 100px;
    background: red;
  }
</style>
<script>
  setTimeout(() => {
    // 引起回流
    document.querySelector('.test').style.top = '100px'
  }, 1000)
</script>
```

- 使用 `visibility` 替换 `display: none` ，因为前者只会引起重绘，后者会引发回流（改变了布局）

- 不要把节点的属性值放在一个循环里当成循环里的变量

  ```js
  for(let i = 0; i < 1000; i++) {
      // 获取 offsetTop 会导致回流，因为需要去获取正确的值
      console.log(document.querySelector('.test').style.offsetTop)
  }
  ```

- 不要使用 `table` 布局，可能很小的一个小改动会造成整个 `table` 的重新布局

- 动画实现的速度的选择，动画速度越快，回流次数越多，也可以选择使用 `requestAnimationFrame`

- CSS 选择符**从右往左**匹配查找，避免节点层级过多

- 将频繁重绘或者回流的节点设置为图层，图层能够阻止该节点的渲染行为影响别的节点。比如对于 `video` 标签来说，浏览器会自动将该节点变为图层。

  

  ![img](https://user-gold-cdn.xitu.io/2018/3/29/1626fb6f33a6f9d7?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

  

  设置节点为图层的方式有很多，我们可以通过以下几个常用属性可以生成新图层

  - `will-change`
  - `video`、`iframe` 标签

## 思考题

> 思考题：在不考虑缓存和优化网络协议的前提下，考虑可以通过哪些方式来最快的渲染页面，也就是常说的关键渲染路径，这部分也是性能优化中的一块内容。

首先你可能会疑问，那怎么测量到底有没有加快渲染速度呢

![img](https://user-gold-cdn.xitu.io/2018/11/27/16754b5a3511198f?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

当发生 `DOMContentLoaded` 事件后，就会生成渲染树，生成渲染树就可以进行渲染了，这一过程更大程度上和硬件有关系了。

**提示如何加速：**

1. 从文件大小考虑
2. 从 `script` 标签使用上来考虑
3. 从 CSS、HTML 的代码书写上来考虑
4. 从需要下载的内容是否需要在首屏使用上来考虑

# 前端优化

## 图片优化

### 计算图片大小

对于一张 100 * 100 像素的图片来说，图像上有 10000 个像素点，如果每个像素的值是 **RGBA** 存储的话，那么也就是说每个像素有 4 个通道，每个通道 1 个字节（8 位 = 1个字节），所以该图片大小大概为 39KB（10000 * 1 * 4 / 1024）。

但是在实际项目中，一张图片可能并不需要使用那么多颜色去显示，我们可以通过减少每个像素的调色板来相应缩小图片的大小。

了解了如何计算图片大小的知识，那么对于如何优化图片，想必大家已经有 2 个思路了：

- **减少像素点**
- **减少每个像素点能够显示的颜色**

### 图片加载优化

1. 不用图片。很多时候会使用到很多修饰类图片，其实这**类修饰图片**完全可以用 **CSS 去代替**。
2. 对于**移动端**来说，屏幕宽度就那么点，完全没有必要去加载原图浪费带宽。**一般图片都用 CDN 加载**，可以计算出适配屏幕的宽度，然后去请求相应裁剪好的图片。
3. **小图使用 base64 格式**
4. 将多个图标文件整合到一张图片中（**雪碧图**）
5. 选择正确的图片格式：
   - 对于能够显示 WebP 格式的浏览器尽量使用 WebP 格式。因为 WebP 格式具有更好的图像数据压缩算法，能带来更小的图片体积，而且拥有肉眼识别无差异的图像质量，缺点就是兼容性并不好
   - 小图使用 PNG，其实对于大部分图标这类图片，完全可以使用 SVG 代替
   - 照片使用 JPEG

## DNS 预解析

DNS 解析也是需要时间的，可以通过预解析的方式来预先获得域名所对应的 IP。

```html
<link rel="dns-prefetch" href="//yuchengkai.cn">
```

## 节流

考虑一个场景，滚动事件中会发起网络请求，但是我们并**不希望用户在滚动过程中一直发起请求，而是隔一段时间发起一次**，对于这种情况我们就可以使用节流。

理解了节流的用途，我们就来实现下这个函数

```js
// func是用户传入需要防抖的函数
// wait是等待时间
const throttle = (func, wait = 50) => {
  // 上一次执行该函数的时间
  let lastTime = 0
  return function(...args) {
    // 当前时间
    let now = +new Date()
    // 将当前时间和上一次执行函数时间对比
    // 如果差值大于设置的等待时间就执行函数
    if (now - lastTime > wait) {
      lastTime = now
      func.apply(this, args)
    }
  }
}

setInterval(
  throttle(() => {
    console.log(1)
  }, 500),
  1
)
```

## 防抖

考虑一个场景，有一个按钮点击会触发网络请求，但是我们并不希望每次点击都发起网络请求，而是**当用户点击按钮一段时间后没有再次点击的情况才去发起网络请求**，对于这种情况我们就可以使用防抖。

理解了防抖的用途，我们就来实现下这个函数

```js
// func是用户传入需要防抖的函数
// wait是等待时间
const debounce = (func, wait = 50) => {
  // 缓存一个定时器id
  let timer = 0
  // 这里返回的函数是每次用户实际调用的防抖函数
  // 如果已经设定过定时器了就清空上一次的定时器
  // 开始一个新的定时器，延迟执行用户传入的方法
  return function(...args) {
    if (timer) clearTimeout(timer)
    timer = setTimeout(() => {
      func.apply(this, args)
    }, wait)
  }
}
```

## 预加载

在开发中，可能会遇到这样的情况。**有些资源不需要马上用到，但是希望尽早获取，这时候就可以使用预加载。**

预加载其实是声明式的 `fetch` ，强制浏览器请求资源，并且不会阻塞 `onload` 事件，可以使用以下代码开启预加载

```html
<link rel="preload" href="http://example.com">
```

预加载可以一定程度上降低首屏的加载时间，因为可以将一些不影响首屏但重要的文件延后加载，唯一缺点就是兼容性不好。

## 预渲染

可以通过预渲染将下载的文件预先在后台渲染，可以使用以下代码开启预渲染

```html
<link rel="prerender" href="http://example.com"> 
```

预渲染虽然可以提高页面的加载速度，但是要确保该页面大概率会被用户在之后打开，否则就是白白浪费资源去渲染。

## 懒执行

懒执行就是将**某些逻辑延迟到使用时再计算**。该技术可以用于首屏优化，对于某些耗时逻辑并不需要在首屏就使用的，就可以使用懒执行。懒执行需要唤醒，一般可以通过定时器或者事件的调用来唤醒。

## 懒加载

懒加载就是**将不关键的资源延后加载**。

懒加载的原理就是只加载自定义区域（通常是可视区域，但也可以是即将进入可视区域）内需要加载的东西。对于图片来说，先设置图片标签的 `src` 属性为一张占位图，将真实的图片资源放入一个自定义属性中，当进入自定义区域时，就将自定义属性替换为 `src` 属性，这样图片就会去下载资源，实现了图片懒加载。

懒加载不仅可以用于图片，也可以使用在别的资源上。比如进入可视区域才开始播放视频等等。

## CDN

CDN 的原理是尽可能的在各个地方分布机房缓存数据，这样即使我们的根服务器远在国外，在国内的用户也可以通过国内的机房迅速加载资源。

因此，我们可以将静态资源尽量使用 CDN 加载，由于浏览器对于单个域名有并发请求上限，可以考虑使用多个 CDN 域名。并且对于 CDN 加载静态资源需要注意 CDN 域名要与主站不同，否则每次请求都会带上主站的 Cookie，平白消耗流量。

 

- 减少重绘避免重排，本质是合并修改

  1. css操作合并到一个类中，一次性修改
  2. 将Dom操作合并，一次性插入

- 减少DNS查找

  网页的呈现过程：域名解析 --> 发起TCP的3次握手 --> 建立TCP连接后发起http请求 --> 服务器响应http请求，浏览器得到html代码 --> 浏览器解析html代码，并请求html代码中的资源（如js、css、图片等） --> 浏览器对页面进行渲染呈现给用户 

  域名解析过程：浏览器DNS缓存-->系统DNS缓存-->host文件-->向DNS服务器发起域名解析请求...

  减少主机名的数量就可以减少DNS查找的数量。 

- 使用DNS预解析DNS（Domain Name System 域名系统）

  - DNS解析：通过主机名，最终得到该主机名对应的IP地址的过程。 DNS解析时间可能导致大量用户感知延迟，DNS解析所需的时间差异非常大，延迟范围可以从1ms（本地缓存结果）到普遍的几秒钟时间。所以利用DNS预解析是有意义的。 

  - DNS预解析是浏览器试图在用户访问链接之前解析域名，域名解析后，如果用户确实访问该域名，那么DNS解析时间将不会有延迟。 

  - DNS预解析在某个页面中包含非常多的域名非常有效，如搜索结果页。 

  - 遇到网页中的超链接，`DNS prefetching`从中提取域名并将其解析为IP地址，这些工作在用户浏览网页时，使用最少的CPU和网络在后台进行解析。

    当用户点击这些已经预解析的域名，可以平均减少200毫秒耗时（假设用户最近还未访问过该域名），更重要的是用户不会遇到DNS解析最坏的情况（往往超过1秒）。

    https://www.xuanfengge.com/dns-prefetching-analysis.html

- 压缩合并资源，减少请求

- 使用浏览器缓存

  Cache-Control 用于控制文件在本地缓存有效时长。最常见的，比如服务器回包：Cache-Control:max-age=600 表示文件在本地应该缓存，且有效时长是600秒（从发出请求算起）。在接下来600秒内，如果有请求这个资源，浏览器不会发出 HTTP 请求，而是直接使用本地缓存的文件。

  Last-Modified 是标识文件在服务器上的最新更新时间。下次请求时，如果文件缓存过期，浏览器通过 If-Modified-Since 字段带上这个时间，发送给服务器，由服务器比较时间戳来判断文件是否有修改。如果没有修改，服务器返回304告诉浏览器继续使用缓存；如果有修改，则返回200，同时返回最新的文件。

  Expires 是 HTTP1.0 标准中的字段，Cache-Control 是 HTTP1.1 标准中新加的字段，功能一样，都是控制缓存的有效时间。Expires 的值一个绝对的时间点，如：Expires: Thu, 10 Nov 2015 08:45:11 GMT，表示在这个时间点之前，缓存都是有效的。 当这两个字段同时出现时，Cache-Control 是高优化级的。

  Etag 也是和 Last-Modified 一样，对文件进行标识的字段。不同的是，Etag 的取值是一个对文件进行标识的特征字串。在向服务器查询文件是否有更新时，浏览器通过 If-None-Match 字段把特征字串发送给服务器，由服务器和文件最新特征字串进行匹配，来判断文件是否有更新。没有更新回包304，有更新回包200。Etag 和 Last-Modified 可根据需求使用一个或两个同时使用。两个同时使用时，只要满足基中一个条件，就认为文件没有更新。

  还有一些应用层的缓存机制比如：DOMStorage和appstorage等

- 非核心代码异步加载

- 使用CDN

  内容分发网络（Content delivery network或Content distribution network，缩写：CDN）。简单来说它主要的工作是把我们需要被分发的内容分发到世界各地的各个节点上，让世界各地的人都可以在距离最近的网络节点拿到想要拿到的内容，减少网络传输距离从而达到加速的目的。

  CDN的本质仍然是一个缓存，而且将数据缓存在里用户最近的地方，使用户以最快的速度获取数据，即网络访问第一跳。 

  适用于静态资源

- 减少DOM嵌套

- 将样式表放在头部，脚本放在底部

# 安全防范知识点

## XSS

> 涉及面试题：什么是 XSS 攻击？如何防范 XSS 攻击？什么是 CSP？

XSS 简单点来说，就是攻击者想尽一切办法将**可以执行的代码注入到网页中**。

XSS 可以分为多种类型，但是总体上我认为分为两类：**持久型和非持久型**。

持久型也就是攻击的代码被服务端写入进**数据库**中，这种攻击危害性很大，因为如果网站访问量很大的话，就会导致大量正常访问页面的用户都受到攻击。

举个例子，对于评论功能来说，就得防范持久型 XSS 攻击，因为我可以在评论中输入以下内容

![img](https://user-gold-cdn.xitu.io/2018/12/2/1676a843648d488c?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

这种情况如果前后端没有做好防御的话，这段评论就会被存储到数据库中，这样每个打开该页面的用户都会被攻击到。

非持久型相比于前者危害就小的多了，一般通过**修改 URL 参数**的方式加入攻击代码，诱导用户访问链接从而进行攻击。

举个例子，如果页面需要从 URL 中获取某些参数作为内容的话，不经过过滤就会导致攻击代码被执行

```html
<!-- http://www.domain.com?name=<script>alert(1)</script> -->
<div>{{name}}</div>                                                  
```

但是对于这种攻击方式来说，如果用户使用 Chrome 这类浏览器的话，浏览器就能自动帮助用户防御攻击。但是我们不能因此就不防御此类攻击了，因为我不能确保用户都使用了该类浏览器。

![img](https://user-gold-cdn.xitu.io/2018/12/2/1676d5e1a09c8367?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

对于 XSS 攻击来说，通常有两种方式可以用来防御。

### 转义字符

首先，**对于用户的输入应该是永远不信任的**。最普遍的做法就是转义输入输出的内容，对于引号、尖括号、斜杠进行转义

```js
function escape(str) {
  str = str.replace(/&/g, '&amp;')
  str = str.replace(/</g, '&lt;')
  str = str.replace(/>/g, '&gt;')
  str = str.replace(/"/g, '&quto;')
  str = str.replace(/'/g, '&#39;')
  str = str.replace(/`/g, '&#96;')
  str = str.replace(/\//g, '&#x2F;')
  return str
}
```

通过转义可以将攻击代码 `<script>alert(1)</script>` 变成

```js
// -> &lt;script&gt;alert(1)&lt;&#x2F;script&gt;
escape('<script>alert(1)</script>')
```

但是对于显示富文本来说，显然不能通过上面的办法来转义所有字符，因为这样会把需要的格式也过滤掉。对于这种情况，通常采用**白名单过滤**的办法，当然也可以通过黑名单过滤，但是考虑到需要过滤的标签和标签属性实在太多，更加推荐使用白名单的方式。

```js
const xss = require('xss')
let html = xss('<h1 id="title">XSS Demo</h1><script>alert("xss");</script>')
// -> <h1>XSS Demo</h1>&lt;script&gt;alert("xss");&lt;/script&gt;
console.log(html)
```

以上示例使用了 `js-xss` 来实现，可以看到在输出中保留了 `h1` 标签且过滤了 `script` 标签。

### CSP

CSP **本质上就是建立白名单**，开发者明确告诉浏览器哪些外部资源可以加载和执行。我们只需要配置规则，如何拦截是由浏览器自己实现的。我们可以通过这种方式来尽量减少 XSS 攻击。

通常可以通过两种方式来开启 CSP：

1. 设置 HTTP Header 中的 `Content-Security-Policy`
2. 设置 `meta` 标签的方式 `<meta http-equiv="Content-Security-Policy">`

这里以设置 HTTP Header 来举例

- 只允许加载本站资源

  ```
  Content-Security-Policy: default-src ‘self’
  ```

- 只允许加载 HTTPS 协议图片

  ```
  Content-Security-Policy: img-src https://*
  ```

- 允许加载任何来源框架

  ```
  Content-Security-Policy: child-src 'none'
  ```

当然可以设置的属性远不止这些，你可以通过查阅 [文档](https://link.juejin.im/?target=https%3A%2F%2Fdeveloper.mozilla.org%2Fen-US%2Fdocs%2FWeb%2FHTTP%2FHeaders%2FContent-Security-Policy) 的方式来学习，这里就不过多赘述其他的属性了。

对于这种方式来说，只要开发者配置了正确的规则，那么即使网站存在漏洞，攻击者也不能执行它的攻击代码，并且 CSP 的兼容性也不错。

![img](https://user-gold-cdn.xitu.io/2018/12/2/1676d8215a3d1f5b?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

## CSRF

> 涉及面试题：什么是 CSRF 攻击？如何防范 CSRF 攻击？

CSRF 中文名为**跨站请求伪造**。原理就是攻击者构造出一个后端请求地址，诱导用户点击或者通过某些途径自动发起请求。如果用户是在登录状态下的话，后端就以为是用户在操作，从而进行相应的逻辑。

举个例子，假设网站中有一个通过 `GET` 请求提交用户评论的接口，那么攻击者就可以在钓鱼网站中加入一个图片，图片的地址就是评论接口

```
<img src="http://www.domain.com/xxx?comment='attack'"/>
```

那么你是否会想到使用 `POST` 方式提交请求是不是就没有这个问题了呢？其实并不是，使用这种方式也不是百分百安全的，攻击者同样可以诱导用户进入某个页面，在页面中通过表单提交 `POST` 请求。

### 如何防御

防范 CSRF 攻击可以遵循以下几种规则：

1. Get 请求不对数据进行修改
2. 不让第三方网站访问到用户 Cookie
3. 阻止第三方网站请求接口
4. 请求时附带验证信息，比如验证码或者 Token

#### SameSite

可以对 Cookie 设置 `SameSite` 属性。该属性表示 **Cookie 不随着跨域请求发送**，可以很大程度减少 CSRF 的攻击，但是该属性目前并不是所有浏览器都兼容。

#### 验证 Referer

对于需要防范 CSRF 的请求，我们可以通过验证 Referer 来判断该请求是否为第三方网站发起的。

#### Token

服务器下发一个随机 Token，每次发起请求时将 Token 携带上，服务器验证 Token 是否有效。

## 点击劫持

> 涉及面试题：什么是点击劫持？如何防范点击劫持？

点击劫持是一种视觉欺骗的攻击手段。攻击者将需要攻击的网站通过 `iframe` 嵌套的方式嵌入自己的网页中，并将 `iframe` 设置为透明，在页面中透出一个按钮诱导用户点击。

![img](https://user-gold-cdn.xitu.io/2018/12/1/16768734d57c5f47?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

对于这种攻击方式，推荐防御的方法有两种。

### X-FRAME-OPTIONS

`X-FRAME-OPTIONS` 是一个 HTTP 响应头，在现代浏览器有一个很好的支持。这个 HTTP 响应头 就是为了防御用 `iframe` 嵌套的点击劫持攻击。

该响应头有三个值可选，分别是

- `DENY`，表示页面不允许通过 `iframe` 的方式展示
- `SAMEORIGIN`，表示页面可以在相同域名下通过 `iframe` 的方式展示
- `ALLOW-FROM`，表示页面可以在指定来源的 `iframe` 中展示

### JS 防御

对于某些远古浏览器来说，并不能支持上面的这种方式，那我们只有通过 JS 的方式来防御点击劫持了。

```html
<head>
  <style id="click-jack">
    html {
      display: none !important;
    }
  </style>
</head>
<body>
  <script>
    if (self == top) {
      var style = document.getElementById('click-jack')
      document.body.removeChild(style)
    } else {
      top.location = self.location
    }
  </script>
</body>
```

以上代码的作用就是当通过 `iframe` 的方式加载页面时，攻击者的网页直接不显示所有内容了。

## 中间人攻击

> 涉及面试题：什么是中间人攻击？如何防范中间人攻击？

中间人攻击是**攻击方同时与服务端和客户端建立起了连接，并让对方认为连接是安全的，但是实际上整个通信过程都被攻击者控制了。攻击者不仅能获得双方的通信信息，还能修改通信信息。**

通常来说不建议使用公共的 Wi-Fi，因为很可能就会发生中间人攻击的情况。如果你在通信的过程中涉及到了某些敏感信息，就完全暴露给攻击方了。

当然防御中间人攻击其实并不难，只需要增加一个安全通道来传输信息。**HTTPS** 就可以用来防御中间人攻击，但是并不是说使用了 HTTPS 就可以高枕无忧了，因为如果你没有完全关闭 HTTP 访问的话，攻击方可以通过某些方式将 HTTPS 降级为 HTTP 从而实现中间人攻击。

# 从 V8 中看 JS 性能优化

> 注意：该知识点属于性能优化领域。

## 测试性能工具

Chrome 已经提供了一个大而全的性能测试工具 **Audits**

![img](https://user-gold-cdn.xitu.io/2018/12/3/16772c479b194d48?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)Audits 所处位置

点我们点击 Audits 后，可以看到如下的界面

![img](https://user-gold-cdn.xitu.io/2018/12/3/16772c52e83d97c7?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)Audits 界面

在这个界面中，我们可以选择想测试的功能然后点击 **Run audits** ，工具就会自动运行帮助我们测试问题并且给出一个完整的报告

![img](https://user-gold-cdn.xitu.io/2018/12/3/16772ca3d13a68ab?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)Audits 工具给出的报告

上图是给掘金首页测试性能后给出的一个报告，可以看到报告中分别为**性能、体验、SEO** 都给出了打分，并且每一个指标都有详细的**评估**

![img](https://user-gold-cdn.xitu.io/2018/12/3/16772cae50f7eb81?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)指标中的详细评估

评估结束后，工具还提供了一些**建议**便于我们提高这个指标的分数

![img](https://user-gold-cdn.xitu.io/2018/12/3/16772cbdcdaccf15?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)优化建议

我们只需要一条条根据建议去优化性能即可。

除了 **Audits** 工具之外，还有一个 **Performance** 工具也可以供我们使用。

![img](https://user-gold-cdn.xitu.io/2018/12/3/16772cf78a4fa18f?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)Performance 工具给出的报告

在这张图中，我们可以详细的看到每个**时间段**中浏览器在处理什么事情，哪个过程最消耗时间，便于我们更加详细的了解性能**瓶颈**。

## JS 性能优化

JS 是编译型还是解释型语言其实并不固定。首先 JS 需要有引擎才能运行起来，无论是浏览器还是在 Node 中，这是解释型语言的特性。但是在 V8 引擎下，又引入了 `TurboFan` 编译器，他会在特定的情况下进行优化，将代码编译成执行效率更高的 **Machine Code**，当然这个编译器并不是 JS 必须需要的，只是为了提高代码执行性能，所以总的来说 JS 更偏向于解释型语言。

那么这一小节的内容主要会针对于 Chrome 的 **V8** 引擎来讲解。

在这一过程中，JS 代码首先会解析为**抽象语法树**（AST），然后会通过解释器或者编译器转化为 **Bytecode** 或者 **Machine Code**

![img](https://user-gold-cdn.xitu.io/2018/12/3/167736409eebe688?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)V8 转化代码的过程

从上图中我们可以发现，JS 会首先被解析为 AST，解析的过程其实是略慢的。代码越多，解析的过程也就耗费越长，这也是我们需要压缩代码的原因之一。另外一种减少解析时间的方式是预解析，会作用于未执行的函数，这个我们下面再谈。

![img](https://user-gold-cdn.xitu.io/2018/12/3/1677468f20b62240?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)2016 年手机解析 JS 代码的速度

这里需要注意一点，对于函数来说，应该**尽可能避免声明嵌套函数**（类也是函数），因为这样会造成函数的重复解析。

```js
function test1() {
  // 会被重复解析
  function test2() {}
}
```

然后 **Ignition** 负责将 AST 转化为 Bytecode，**TurboFan** 负责编译出优化后的 Machine Code，**并且 Machine Code 在执行效率上优于 Bytecode**

![img](https://user-gold-cdn.xitu.io/2018/12/3/16773b904cfb732f?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

那么我们就产生了一个疑问，**什么情况下代码会编译为 Machine Code？**

JS 是一门**动态类型**的语言，并且还有一大堆的规则。简单的加法运算代码，内部就需要考虑好几种规则，比如数字相加、字符串相加、对象和字符串相加等等。这样的情况也就势必导致了内部要增加很多判断逻辑，降低运行效率。

```js
function test(x) {
  return x + x
}

test(1)
test(2)
test(3)
test(4)
```

对于以上代码来说，如果一个函数被**多次调用**并且参数一直传入 `number` 类型，那么 V8 就会认为该段代码可以编译为 Machine Code，因为你**固定了类型**，不需要再执行很多判断逻辑了。

但是如果一旦我们传入的参数**类型改变**，那么 Machine Code 就会被 **DeOptimized** 为 Bytecode，这样就有性能上的一个损耗了。所以如果我们希望代码能多的编译为 Machine Code 并且 DeOptimized 的次数减少，就应该尽可能保证传入的**类型一致**。

那么你可能会有一个疑问，到底优化前后有多少的提升呢，接下来我们就来实践测试一下到底有多少的提升。

```js
const { performance, PerformanceObserver } = require('perf_hooks')

function test(x) {
  return x + x
}
// node 10 中才有 PerformanceObserver
// 在这之前的 node 版本可以直接使用 performance 中的 API
const obs = new PerformanceObserver((list, observer) => {
  console.log(list.getEntries())
  observer.disconnect()
})
obs.observe({ entryTypes: ['measure'], buffered: true })

performance.mark('start')

let number = 10000000
// 不优化代码
%NeverOptimizeFunction(test)

while (number--) {
  test(1)
}

performance.mark('end')
performance.measure('test', 'start', 'end')
```

以上代码中我们使用了 `performance` API，这个 API 在性能测试上十分好用。不仅可以用来测量代码的执行时间，还能用来测量各种网络连接中的时间消耗等等，并且这个 API 也可以在浏览器中使用。

![img](https://user-gold-cdn.xitu.io/2018/12/4/16778338eb8b7130?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)优化与不优化代码之间的巨大差距

从上图中我们可以发现，优化过的代码执行时间只需要 9ms，但是不优化过的代码执行时间却是前者的二十倍，已经接近 200ms 了。在这个案例中，我相信大家已经看到了 V8 的性能优化到底有多强，**只需要我们符合一定的规则书写代码，引擎底层就能帮助我们自动优化代码。**

另外，编译器还有个骚操作 **Lazy-Compile**，当函数没有被执行的时候，会对函数进行一次预解析，直到代码被执行以后才会被解析编译。对于上述代码来说，`test` 函数需要被预解析一次，然后在调用的时候再被解析编译。**但是对于这种函数马上就被调用的情况来说，预解析这个过程其实是多余的**，那么有什么办法能够让代码不被预解析呢？

其实很简单，我们只需要给函数**套上括号**就可以了

```
(function test(obj) {
  return x + x
})
```

但是不可能我们为了性能优化，给所有的函数都去套上括号，并且也不是所有函数都需要这样做。我们可以通过 [optimize-js](https://link.juejin.im/?target=https%3A%2F%2Fgithub.com%2Fnolanlawson%2Foptimize-js) 实现这个功能，这个库会分析一些函数的使用情况，然后给需要的函数添加括号，当然这个库很久没人维护了，如果需要使用的话，还是需要测试过相关内容的。

## 小结

- 可以通过 **Audit** 工具获得网站的多个指标的性能报告
- 可以通过 **Performance** 工具了解网站的性能瓶颈
- 可以通过 **Performance** API 具体测量时间
- 为了减少编译时间，我们可以采用**减少代码文件的大小**或者**减少书写嵌套函数**的方式
- 为了让 V8 优化代码，我们应该尽可能保证传入参数的**类型一致**。这也给我们带来了一个思考，这是不是也是使用 TypeScript 能够带来的好处之一

# HTML5新标签与特性

## 文档类型设定

- document
  - HTML:
  - XHTML:
  - HTML5

## 字符设定

- <meta http-equiv="charset" content="utf-8">：HTML与XHTML中建议这样去写
- <meta charset="utf-8">：HTML5的标签中建议这样去写

## 常用新标签

| 标签         | 描述                                                         |
| ------------ | ------------------------------------------------------------ |
| <article>    | 定义文章。                                                   |
| <aside>      | 定义页面内容以外的内容，内容应该与周围内容相关。             |
| <details>    | 定义用户能够查看或隐藏的额外细节。 目前只有 Chrome 和 Safari 6 支持 <details> 标签。 |
| <figcaption> | 定义 <figure> 元素的标题。                                   |
| <figure>     | 规定自包含内容，比如图示、图表、照片、代码清单等。           |
| <footer>     | 定义文档或节的页脚。                                         |
| <header>     | 规定文档或节的页眉。                                         |
| <main>       | 规定文档的主内容。                                           |
| <mark>       | 定义重要的或强调的文本。                                     |
| <nav>        | 定义导航链接。                                               |
| <section>    | 定义文档中的节。                                             |
| <summary>    | 定义 <details> 元素的可见标题。                              |
| <time>       | 定义日期/时间。                                              |
| <datalist>   | 定义选项列表。请与 input 元素配合使用该元素，来定义 input 可能的值。   input 元素的 list 属性来绑定 datalist。 |
| <fieldset>   | 可将表单内的相关元素分组，浏览器会以特殊方式来显示它们，它们可能有特殊的边界、3D 效果，或者甚至可创建一个子表单来处理这些元素。 <legend>为 fieldset 元素定义标题。 |

### 移除的标签

没有语义化注重样式的标签

### 兼容处理

```
<script src="../js/html5shiv.min.js"></script>
```

### figure 和 figcaption 元素

在书籍和报纸中，与图片搭配的标题很常见。

标题（caption）的作用是为图片添加可见的解释。

```
<figure>
   <img src="pic_mountain.jpg" alt="The Pulpit Rock" width="304" height="228">
   <figcaption>Fig1. - The Pulpit Pock, Norway.</figcaption>
</figure> 
```

## 常用新属性

| **属性**         | **用法**                                       | **含义**                                                   |
| ---------------- | ---------------------------------------------- | ---------------------------------------------------------- |
| **placeholder**  | <input type="text" placeholder="请输入用户名"> | 占位符提供可描述输入字段预期值的提示信息                   |
| **autofocus**    | <input type="text" autofocus>                  | 规定当页面加载时 input 元素应该自动获得焦点                |
| **multiple**     | <input type="file" multiple>                   | 多文件上传                                                 |
| **autocomplete** | <input type="text" autocomplete="off">         | 规定表单是否应该启用自动完成功能，只有提交过的内容才会记录 |
| **required**     | <input type="text" required>                   | 必填项                                                     |
| **accesskey**    | <input type="text" accesskey="s">              | 规定激活（使元素获得焦点）元素的快捷键为alt+‘s’            |

## 新增的type属性值：

| **类型**     | **使用示例**            | **含义**                               |
| ------------ | ----------------------- | -------------------------------------- |
| **email**    | <input type="email">    | 输入邮箱格式，包含校验                 |
| **tel**      | <input type="tel">      | 输入手机号码格式，手机上会弹出数字键盘 |
| **url**      | <input type="url">      | 输入url格式，包含校验                  |
| **number**   | <input type="number">   | 只能输入数字格式                       |
| **search**   | <input type="search">   | 搜索框（体现语义化）                   |
| **range**    | <input type="range">    | 自由拖动滑块，value取值                |
| **time**     | <input type="time">     |                                        |
| **date**     | <input type="date">     |                                        |
| **datetime** | <input type="datetime"> |                                        |
| **month**    | <input type="month">    |                                        |
| **week**     | <input type="week">     |                                        |

## 综合案例

~~~html
<form action="">
  <fieldset>
    <legend>学生档案</legend>
    <label for="userName">姓名:</label>
    <input type="text" name="userName" id="userName" placeholder="请输入用户名"> <br>
    <label for="userPhone">手机号码:</label>
    <input type="tel" name="userPhone" id="userPhone" pattern="^1\d{10}$"><br>
    <label for="email">邮箱地址:</label>
    <input type="email" required name="email" id="email"><br>
    <label for="collage">所属学院:</label>
    <input type="text" name="collage" id="collage" list="cList" placeholder="请选择"><br>
    <datalist id="cList">
      <option value="前端与移动开发学院"></option>
      <option value="java学院"></option>
      <option value="c++学院"></option>
    </datalist><br>
    <label for="score">入学成绩:</label>
    <input type="number" max="100" min="0" value="0" id="score"><br>
    <label for="level">基础水平:</label>
    <meter id="level" max="100" min="0" low="59" high="90"></meter><br>
    <label for="inTime">入学日期:</label>
    <input type="date" id="inTime" name="inTime"><br>
    <label for="leaveTime">毕业日期:</label>
    <input type="date" id="leaveTime" name="leaveTime"><br>
    <input type="submit">
  </fieldset>
</form>
~~~

## 操作类名

```js
div.classList.remove('')
div.classLIst.add('')
div.classList.toggle('')
div.classList.contains('')
```

## Web存储

### cookie，localStorage，sessionStorage，indexDB

我们先来通过表格学习下这几种存储方式的区别

| 特性         | cookie                                     | localStorage             | sessionStorage | indexDB                  |
| ------------ | ------------------------------------------ | ------------------------ | -------------- | ------------------------ |
| 数据生命周期 | 一般由服务器生成，可以设置过期时间         | 除非被清理，否则一直存在 | 页面关闭就清理 | 除非被清理，否则一直存在 |
| 数据存储大小 | 4K                                         | 5M                       | 5M             | 无限                     |
| 与服务端通信 | 每次都会携带在 header 中，对于请求性能影响 | 不参与                   | 不参与         | 不参与                   |

从上表可以看到，`cookie` 已经不建议用于存储。如果没有大量数据存储需求的话，可以使用 `localStorage` 和 `sessionStorage` 。对于不怎么改变的数据尽量使用 `localStorage` 存储，否则可以用 `sessionStorage` 存储。

sessionStorage/localStorage：将数据存储到本地

API：

```js
window.sessionStorage.setItem('name',name)
window.sessionStorage.getItem('name')
window.sessionStorage.removeItem('name')
window.sessionStorage.clear()
```

sessionStorage

1. 存储在当前页面内存中
2. 5M左右

localStorage

1. 同一个浏览器可以共享
2. 永久存储，存储在硬盘
3. 20M左右

对于 `cookie` 来说，我们还需要注意安全性。

| 属性      | 作用                                                         |
| --------- | ------------------------------------------------------------ |
| value     | 如果用于保存用户登录态，应该将该值加密，不能使用明文的用户标识 |
| http-only | 不能通过 JS 访问 Cookie，减少 XSS 攻击                       |
| secure    | 只能在协议为 HTTPS 的请求中携带                              |
| same-site | 规定浏览器不能在跨域请求中携带 Cookie，减少 CSRF 攻击        |

### Service Worker

Service Worker 是运行在浏览器背后的**独立线程**，一般可以用来实现缓存功能。使用 Service Worker的话，传输协议必须为 **HTTPS**。因为 Service Worker 中涉及到请求拦截，所以必须使用 HTTPS 协议来保障安全。

Service Worker 实现缓存功能一般分为三个步骤：首先需要先注册 Service Worker，然后监听到 `install` 事件以后就可以缓存需要的文件，那么在下次用户访问的时候就可以通过拦截请求的方式查询是否存在缓存，存在缓存的话就可以直接读取缓存文件，否则就去请求数据。以下是这个步骤的实现：

```js
// index.js
if (navigator.serviceWorker) {
  navigator.serviceWorker
    .register('sw.js')
    .then(function(registration) {
      console.log('service worker 注册成功')
    })
    .catch(function(err) {
      console.log('servcie worker 注册失败')
    })
}
// sw.js
// 监听 `install` 事件，回调中缓存所需文件
self.addEventListener('install', e => {
  e.waitUntil(
    caches.open('my-cache').then(function(cache) {
      return cache.addAll(['./index.html', './index.js'])
    })
  )
})

// 拦截所有请求事件
// 如果缓存中已经有请求的数据就直接用缓存，否则去请求数据
self.addEventListener('fetch', e => {
  e.respondWith(
    caches.match(e.request).then(function(response) {
      if (response) {
        return response
      }
      console.log('fetch source')
    })
  )
})
```

打开页面，可以在开发者工具中的 `Application` 看到 Service Worker 已经启动了

![img](https://user-gold-cdn.xitu.io/2018/3/28/1626b1e8eba68e1c?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

在 Cache 中也可以发现我们所需的文件已被缓存

![img](https://user-gold-cdn.xitu.io/2018/3/28/1626b20dfc4fcd26?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

当我们重新刷新页面可以发现我们缓存的数据是从 Service Worker 中读取的

![img](https://user-gold-cdn.xitu.io/2018/3/28/1626b20e4f8f3257?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

## 应用缓存ApplicationCache

指定缓存文件，5M左右

```html
<html lang='en' manifest='demo.appcache'>
...
</html>
```

manifest=应用程序缓存清单路径，文件扩展名建议为appcache

appcache文件内容：

```config
#第一句
CACHE MANIFEST
#需要缓存的清单列表
CACHE:
../01.jpg
#*代表所有文件
#每次请求都需要重新获取的清单列表
NETWORK：
../02.jpg
#没找到时的替代文件
FALLBACK:
#被替代文件 替代文件
../03.jpg ../04.jpg
#/代表所有文件
```

不起作用时要配置IIS管理器（服务器）里的的MIME类型：text/cache-manifest

根据官方文档，AppCache 已经不推荐使用了，标准也不会再支持。 

## 多媒体标签

- embed：标签定义嵌入的内容

- audio：播放音频

- video：播放视频


### 多媒体 embed（会使用）

embed可以用来插入各种多媒体，格式可以是 Midi、Wav、AIFF、AU、MP3等等。url为音频或视频文件及其路径，可以是相对路径或绝对路径。

因为兼容性问题，这里只讲解插入网络视频， 后面H5会讲解 audio 和video 视频多媒体。 

```html
<embed src="http://player.youku.com/player.php/sid/XMTI4MzM2MDIwOA==/v.swf" allowFullScreen="true" quality="high" width="480" height="400" align="middle" allowScriptAccess="always" type="application/x-shockwave-flash"></embed>
```

 优酷，土豆，爱奇艺，腾讯、乐视等等

1. 先上传
2. 在分享

### 多媒体 audio

```
<audio controls>
  <source src="horse.ogg" type="audio/ogg">
  <source src="horse.mp3" type="audio/mpeg">
您的浏览器不支持 audio 元素。
</audio>
```

**autoplay**：autoplay自动播放

**controls**：controls是否显示默认播放控件

**loop**：loop循环播放，loop='2'，-1为循环播放

目前<audio>元素支持三种音频格式文件: MP3, Wav, 和 Ogg由于版权等原因，不同的浏览器可支持播放的格式是不一样的

| 浏览器               | MP3  | Wav  | Ogg  |
| -------------------- | ---- | ---- | ---- |
| Internet Explorer 9+ | YES  | NO   | NO   |
| Chrome 6+            | YES  | YES  | YES  |
| Firefox 3.6+         | YES  | YES  | YES  |
| Safari 5+            | YES  | YES  | NO   |
| Opera 10+            | YES  | YES  | YES  |

多浏览器支持的方案，如下图

 ``````
<audio src="" controls autoplay>
  <source src="bgs.mp3" />
  <source src="bgs.wav" />
  <source src="bgs.ogg" />
  你的浏览器不支持该audio音频播放
</audio>
 ``````



### 多媒体 video

``````
<video width="320" height="240" controls>
  <source src="movie.mp4" type="video/mp4">
  <source src="movie.ogg" type="video/ogg">
  您的浏览器不支持Video标签。
</video>
``````

**autoplay** 自动播放

**controls** 是否显示默认播放控件

**loop** 循环播放

**width** 设置播放窗口宽度

**height**设置播放窗口的高度

当前， <video> 元素支持三种视频格式： MP4, WebM, 和 Ogg ，由于版权等原因，不同的浏览器可支持播放的格式是不一样的，如下图供参考

| 浏览器            | MP4                  | WebM | Ogg  |
| ----------------- | -------------------- | ---- | ---- |
| Internet Explorer | YES                  | NO   | NO   |
| Chrome            | YES                  | YES  | YES  |
| Firefox           | YES                  | YES  | YES  |
| Safari            | YES                  | NO   | NO   |
| Opera             | YES (从 Opera 25 起) | YES  | YES  |

**多浏览器支持的方案同音频**

## DOM操作

### 获取元素

document.getElementByClassName('class')类数组

document.getElementByTagName('tag')类数组

document.querySelector('')返回第一个匹配的元素

document.querySelectorAll('')类数组

### 类名操作

Node.classLisht.add('')

Node.classLisht.remove('')

Node.classLisht.toggle('')

Node.classLisht.contains('')

### 自定义属性

1. 在HTML5中我们可以自定义属性，其格式如下`data-*=""`，例如：`data-info="我是自定义属性"`，通过`Node.dataset['info']` 我们便可以获取到自定义的属性值。
2. 当我们如下格式设置时，则需要以驼峰格式才能正确获取：`data-my-name="itcast"`，获取`Node.dataset['myName']`