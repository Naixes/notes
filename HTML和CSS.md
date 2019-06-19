# HTML

HTML（英文Hyper Text Markup Language的缩写）中文译为“超文本标签语言”，主要是通过HTML标签对网页中的文本、图片、声音等内容进行描述。

## HTML骨架格式

```html
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
```

### html标签

`<html></html>`限定了文档的开始点和结束点，在它们之间是文档的头部和主体，所有HTML中标签的一个根节点。

 `<html></html>`标签中可添加的专属属性

| 属性     | 值                           | 描述                                                        |
| :------- | :--------------------------- | :---------------------------------------------------------- |
| manifest | url                          | 定义一个 URL，在这个 URL 上描述了文档的缓存信息。（已废弃） |
| xmlns    | http://www.w3.org/1999/xhtml | 定义 XML namespace 属性。                                   |

**全局属性**

**HTML 属性**赋予元素意义和语境。下面的全局属性可用于任何 **HTML 元素**。

| 属性            | 描述                                                   |
| :-------------- | :----------------------------------------------------- |
| accesskey       | 规定激活元素的快捷键。                                 |
| class           | 规定元素的一个或多个类名（引用样式表中的类）。         |
| contenteditable | 规定元素内容是否可编辑。                               |
| contextmenu     | 规定元素的上下文菜单。上下文菜单在用户点击元素时显示。 |
| data-*          | 用于存储页面或应用程序的私有定制数据。                 |
| dir             | 规定元素中内容的文本方向。                             |
| draggable       | 规定元素是否可拖动。                                   |
| dropzone        | 规定在拖动被拖动数据时是否进行复制、移动或链接。       |
| hidden          | 规定元素仍未或不再相关。                               |
| id              | 规定元素的唯一 id。                                    |
| lang            | 规定元素内容的语言。                                   |
| spellcheck      | 规定是否对元素进行拼写和语法检查。                     |
| style           | 规定元素的行内 CSS 样式。                              |
| tabindex        | 规定元素的 tab 键次序。                                |
| title           | 规定有关元素的额外信息。                               |
| translate       | 规定是否应该翻译元素内容。                             |

### head标签

用于存放：title,meta,base,style,script,link

`<head>`标签用于定义文档的头部，它是所有头部元素的容器。描述了文档的各种属性和信息，包括文档的标题、在 Web 中的位置以及和其他文档的关系等。

head 标签规定了自身必须是 html 标签中的第一个标签，它的内容必须包含一个 title，并且最多只能包含一个 base。如果文档作为 iframe，或者有其他方式指定了文档标题时，可以允许不包含 title 标签。

#### base标签

`<base>` 标签为页面上的所有链接规定默认地址或默认目标。base 标签最多只有一个，它改变全局的链接地址，它是一个非常危险的标签，容易造成跟JavaScript 的配合问题，所以在实际开发中，我比较建议你使用 JavaScript 来代替 base标签。

通常情况下，浏览器会从当前文档的 URL 中提取相应的元素来填写相对 URL 中的空白。使用 `<base>` 标签可以改变这一点。浏览器随后将不再使用当前文档的 URL，而使用指定的基本 URL 来解析所有的相对 URL。这其中包括 `<a>`、 `<img>`、 `<link>`、 `<form>` 标签中的 URL。

| 属性   | 值                                  | 描述                                       |
| :----- | :---------------------------------- | :----------------------------------------- |
| href   | URL                                 | 规定页面中所有相对链接的基准 URL。（必选） |
| target | blank  parent  _self _top framename | 在何处打开页面中所有的链接。（可选）       |

#### link标签

主要用于**style文件**引入

| 属性     | 值                                                           | 描述                                        |
| :------- | :----------------------------------------------------------- | :------------------------------------------ |
| charset  | char_encoding                                                | HTML5 中不支持。                            |
| href     | URL                                                          | 规定被链接文档的位置。                      |
| hreflang | language_code                                                | 规定被链接文档中文本的语言。                |
| media    | media_query                                                  | 规定被链接文档将被显示在什么设备上。        |
| rel      | alternate author help icon licence next pingback prefetch prev search sidebar stylesheet tag | 规定当前文档与被链接文档之间的关系。        |
| rev      | reversed relationship                                        | HTML5 中不支持。                            |
| sizes    | height xwidth any                                            | 规定被链接资源的尺寸。仅适用于 rel="icon"。 |
| target   | blank self top parent frame_name                             | HTML5 中不支持。                            |
| type     | MIME_type                                                    | 规定被链接文档的 MIME 类型。                |

#### style标签

| 属性  | 值                                                        | 描述                                 |
| :---- | :-------------------------------------------------------- | :----------------------------------- |
| type  | text/css                                                  | 规定样式表的 MIME 类型。（必选）     |
| media | screen tty tv projection handheld print braille aural all | 为样式表规定不同的媒介类型。（可选） |

#### title标签

让页面拥有一个属于自己的标题。

heading（h1-6） 和 title 两个英文单词意义区分十分微妙，在中文中更是找不到对应的词汇来区分。但是实际使用中，两者确实有一定区别。

title 作为元信息，可能会被用在浏览器收藏夹、微信推送卡片、微博等各种场景，这时侯往往是上下文缺失的，所以 title 应该是完整地概括整个网页内容的。而 h1 则仅仅用于页面展示，它可以默认具有上下文，并且有链接辅助，所以可以简写，即便无法概括全文，也不会有很大的影响。

#### meta标签

是一组键值对，它是一种通用的元信息表示标签。提供了有关当前**HTML**元素的**元信息 (meta-information)**，比如描述、针对搜索引擎的关键词以及刷新频率。

在 head 中可以出现任意多个 meta 标签。一般的 meta 标签由 name 和 content 两个属性来定义。name 表示元信息的名，content 则用于表示元信息的值。

<meta> 的属性对象如下：

| 属性       | 描述                                        |
| :--------- | :------------------------------------------ |
| content    | 设置或返回元素的 content 属性的值。         |
| http-equiv | 把 content 属性连接到一个 HTTP 头部。       |
| name       | 把 content 属性连接到某个名称。             |
| scheme     | 设置或返回用于解释 content 属性的值的格式。 |

**content**，此属性包含 `http-equiv` 或 `name` 属性的值，具体取决于所使用的值。

<meta name="keywords" content="WEB,CSS,鱼头" />

**scheme**，此属性是用来设置或返回用于解释 content 属性的值的格式。例子如下：

<meta name="revised" content="2019-04-03" scheme="YYYY-MM-DD" />

MDN：不要用这属性，因为这属性并没什么用处。: )

**name**，此属性定义文档级元数据的名称。值得注意的是，如果定义的元数据设置了 `itemprop`, `http-equiv` or `charset` ，就不能再设置**name**了。

| 值               | 描述                                                         |
| :--------------- | :----------------------------------------------------------- |
| application-name | 定义正运行在该网页上的网络应用名称                           |
| author           | 文档作者                                                     |
| description      | 其中包含页面内容的简短和精确的描述。一些浏览器，如Firefox和Opera，将其用作书签页面的默认描述。 |
| generator        | 包含生成页面的软件的标识符。                                 |
| keywords         | 包含与逗号分隔的页面内容相关的单词。                         |
| referrer         | 控制所有从该文档发出的 HTTP 请求中HTTP `Referer` 首部的内容。 |
| others           | 其他的内容。                                                 |

**http-equiv**，此属性把**content**属性连接到**HTTP**头部。

| 值                      | 描述                                                         |
| :---------------------- | :----------------------------------------------------------- |
| content-security-policy | 允许站点管理者在指定的页面控制用户代理的资源。除了少数例外，这条政策将极大地指定服务源 以及脚本端点。这将帮助防止跨站脚本攻击。 |
| content-type            | 相当于添加了 content-type 这个 http 头，值为content指定的内容 |
| default-style           | 这个属性指定了在页面上使用的首选样式表. `content`属性必须包含 `<link>` 元素的标题, `href`属性链接到CSS样式表或包含CSS样式表的 `<style>`元素的标题。 |
| refresh                 | 刷新，这个属性指定如果 `<content>`只包含一个正整数，则是重新载入页面的时间间隔(秒)，包含一个正整数并且跟着一个字符串,则是重定向到指定链接的时间间隔(秒)。 |

除了基本用法，meta 标签还有一些变体，主要用于简化书写方式或者声明自动化行为。下面是几种重点的内容：

**具有 charset 属性的 meta**：从 HTML5 开始，为了简化写法，meta 标签新增了 charset 属性。添加了 charset 属性的 meta 标签无需再有 name 和 content。它描述了 HTML 文档自身的编码形式。因此建议这个标签放在 head 的第一个。

`<mete charset='utf-8'>`

**具有 http-equiv 属性的 meta**：具有 http-equiv 属性的 meta 标签，表示执行一个命令

`<meta http-equiv='content-type', content='text/html'>`

content-language 指定内容的语言；
default-style 指定默认样式表；
refresh 刷新；
set-cookie 模拟 http 头 set-cookie，设置 cookie；
x-ua-compatible 模拟 http 头 x-ua-compatible，声明 ua 兼容性；
content-security-policy 模拟 http 头 content-security-policy，声明内容安全策略。

**name 为 viewport 的 meta**：实际上，meta 标签可以被自由定义，只要写入和读取的双方约定好 name 和 content 的格式就可以了。name 为 viewport 的 meta，它没有在 HTML 标准中定义，却是移动端开发的事实标准：这类 meta 的 name 属性为 viewport，它的 content 是一个复杂结构，是用逗号分隔的
键值对，键值对的格式是 key=value。

width：页面宽度，可以取值具体的数字，也可以是 device-width，表示跟设备宽度相等。
height：页面高度，可以取值具体的数字，也可以是 device-height，表示跟设备高度相等。
initial-scale：初始缩放比例。
minimum-scale：最小缩放比例。
maximum-scale：最大缩放比例。
user-scalable：是否允许用户缩放。

**其它预定义的 meta**：在 HTML 标准中，还定义了一批 meta 标签的 name，可以视为一种有约定的 meta

application-name：如果页面是 Web application，用这个标签表示应用名称。
author: 页面作者。
description：页面描述，这个属性可能被用于搜索引擎或者其它场合。
generator: 生成页面所使用的工具，主要用于可视化编辑器，如果是手写 HTML 的网页，不需要加这个 meta。
keywords: 页面关键字，对于 SEO 场景非常关键。
referrer: 跳转策略，是一种安全考量。  控制所有从该文档发出的 HTTP 请求中HTTP `Referer` 首部的内容。                                                                                                                                                         theme-color: 页面风格颜色，实际并不会影响页面，但是浏览器可能据此调整页面之外的 UI（如窗口边框或者 tab 的颜色）。

**常用meta**：

```html
　　搜索引擎索引方式
　　<meta name="robots" content="index,follow" />
　　<!--
　　all：文件将被检索，且页面上的链接可以被查询；
　　none：文件将不被检索，且页面上的链接不可以被查询；
　　index：文件将被检索；
　　follow：页面上的链接可以被查询；
　　noindex：文件将不被检索；
　　nofollow：页面上的链接不可以被查询。
　　-->
　　页面重定向和刷新
　　<meta http-equiv="refresh" content="0;url=" />
　　移动设备
　　<meta name="viewport" content="width=device-width, initial-scale=1.0,maximum-scale=1.0, user-scalable=no"/>
　　<!-- `width=device-width` 会导致 iPhone 5 添加到主屏后以 WebApp 全屏模式打开页面时出现黑边  -->
　　优先使用 IE 最新版本和 Chrome
　　<meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1" />
　　<!-- 关于X-UA-Compatible -->
　　禁止浏览器从本地计算机的缓存中访问页面内容
　　<meta http-equiv="Pragma" content="no-cache">
    浏览器不会自动调整文件的大小,也就是说是固定大小,不会随着浏览器拉伸缩放。
   <meta name="MobileOptimized" content="240"/> 
```

<https://blog.csdn.net/weixin_42133469/article/details/81588097>

<https://github.com/joshbuchea/HEAD>

### body标签

页面在的主体部分，用于存放所有的HTML标签

` <html>`内可使用的标签大概有**357**个，其中**MDN**给 **<body>**内的元素分了11类。

**1. 内容分区：**

> 内容分区元素允许你将文档内容从逻辑上进行组织划分。

**2. 文本内容**

> 使用 HTML 文本内容元素来组织在开标签和闭标签里的块或章节的内容。这些元素能标识内容的宗旨或结构，而这对于 accessibility 和 SEO 很重要。

**3. 内联文本语义**

> 使用 HTML 内联文本语义（Inline text semantics）定义一个单词、一行内容，或任意文字的语义、结构或样式。

**4. 图片和多媒体**

> HTML 支持各种多媒体资源，例如图像，音频和视频。

**5. 内嵌内容**

> 除了常规的多媒体内容，HTML 可以包括各种其他的内容，即使它并不容易交互。

**6. 脚本**

> 为了创建动态内容和 Web 应用程序，HTML 支持使用脚本语言，最突出的就是 JavaScript。某些元素支持此功能。

**7. 编辑标识**

> 这些元素能标示出某个文本被更改过的部分。

**8. 表格内容**

> 这里的元素用于创建和处理表格数据。

**9. 表单**

> HTML 提供了许多可一起使用的元素，这些元素能用来创建一个用户可以填写并提交到网站或应用程序的表单。

**10. 交互元素**

> HTML 提供了一系列有助于创建交互式用户界面对象的元素。

**11. Web组件**

> Web 组件是一种与 HTML 相关联（HTML-related）的技术，简单来说，它允许创建自定义元素，并如同普通的 HTML 一样使用它们。此外，你甚至可以创建经过自定义的标准 HTML 元素。

## 文档类型声明<!DOCTYPE>

~~~html
<!DOCTYPE html>

<!DOCTYPE> 标签位于文档的最前面，用于向浏览器说明当前文档使用哪种 HTML 或 XHTML 标准规范，这里使用的是 html 5 的版本。
~~~

DTD文档类型定义：浏览器会使用它来判断文档类型，从而决定使用何种协议来解析 

# 路径

## 相对路径

## 绝对路径

# 元素

## 元素属性

使用HTML制作网页时，如果想让HTML标签提供更多的信息，可以使用HTML标签的属性加以设置。其基本语法格式如下：

```html
<标签名 属性1="属性值1" 属性2="属性值2" …> 内容 </标签名>
```

## 文档元信息

所谓元信息，是指描述自身的信息，元信息类标签，就是 HTML 用于描述文档自身的一类标签，它们通常出现在 head 标签中，一般都不会在页面被显示出来（与此相对，其它标签，如语义类标签，描述的是业务）。

元信息多数情况下是给浏览器、搜索引擎等机器阅读的，有时候这些信息会在页面之外显示给用户，有时候则不会。

### meta 标签

#### 字符集

<meta charset="UTF-8">

utf-8是目前最常用的字符集编码方式，常用的字符集编码方式还有gbk和gb2312。

gb2312 简单中文  包括6763个汉字

BIG5   繁体中文 港澳台等用

GBK包含全部中文字符    是GB2312的扩展，加入对繁体字的支持，兼容GB2312

UTF-8则包含全世界所有国家需要用到的字符

#### 视口

https://www.cnblogs.com/chunyangji/p/5795487.html

视口是html的包含块，移动端浏览器厂商为了让窄屏幕下友好展示，会将视口的宽度不与屏幕关联，就会远大于屏幕宽度。可以用meta viewport手动设置视口宽度

`<meta name="viewport" content="width=device-width, initial-scale=1, user-scalable=0">`

将浏览器中虚拟的页面容器缩放到屏幕大小然后展示出来

HEAD仓库有一些视口的常见写法

## 注释标签

```html
    <!-- 注释语句 -->
```

## 语义化标签

### 为什么要有语义化标签

1. 样式丢失时候能让页面呈现**清晰的结构**，语义化更具**可读性**，有利于**开发和维护**，与CSS3关系更和谐。
2. 适宜机器阅读，具有更好地搜索引擎优化（**SEO**），方便**浏览器或网络爬虫及其他设备解析**，如盲人阅读器根据语义渲染网页，读屏软件自动生成目录等

不恰当的使用语义会造成负面作用

遵循的原则：先确定语义的HTML ，再选合适的CSS。

- 使用场景：
- **作为自然语言的延伸**：用来**表达一定的结构**或**消除歧义**

比如：ruby表示注解（html5：ruby，rt，rp）、em表示重音（strong表示重要的内容）

- **作为标题摘要**

可以生成目录结构

hgroup中的h1-h6被视为同一标题的不同部分

section可以使h下降一级

- **作为整体结构**

适合**机器阅读**的特性，提出明确的主次关系，让浏览器很好地支持**阅读视图**功能；提高**搜索引擎命中**；对视障用户的读屏软件更友好

比如 body，header，nav，aside，artical，section，footer，address 组成的结构

```html
<body>
    <header><nav>...</nav></header>
    <aside><nav>...</nav></aside>
    <section></section>
    <section></section>...
    <footer><address></address></footer>
</body>
```

```html
<body>
    <header></header>
    <artical>
        <header></header>
        <section></section>
        <footer></footer>
    </artical>
    <artical></artical>...
    <footer><address></address></footer>
</body>
```

### 标题标签-h

**块级元素**

HTML提供了6个等级的标题，即 <h1>、<h2>、<h3>、<h4>、<h5>和<h6>

> 注意： 
>
>  h1 标签因为重要，尽量少用， 一般h1 都是给logo使用。
>
> 默认情况下，HTML 会自动地在块级元素前后添加一个额外的空行，比如段落、标题元素前后。

### 段落标签-p

**块级元素**

~~~html
<p>  文本内容  </p>
~~~

默认情况下，文本在一个段落中会根据浏览器窗口的大小自动换行。

### 水平线标签-hr

**块级元素**

```html
<hr />是单标签
```

 表示**故事的走向和话题的转变**，在网页中显示默认样式的水平线。

### 换行标签-br

**行内元素**

```html
<br />
```

### div span标签

div（分类**块级元素**）  span（分类**行内元素**）    

是没有语义的，是我们网页布局主要的2个容器，可用于对大的内容块设置样式属性。 

~~~html
<div> 这是头部 </div>    <span>今日价格</span>
~~~

### 文本格式化标签

使文字以特殊的方式显示：

b（粗体）=>关键字

i（斜体）=>变调

s（删除线）=>错误内容

u （下划线）=>避免歧义的标注

strong：重要内容

em：重音

del：删除文本

ins：插入文本

### 列表标签

#### 无序列表-ul

**块级元素**

无序列表的各个列表项之间没有顺序级别之分，是并列的。其基本语法格式如下：

```html
<ul>
  <li>列表项1</li>
  <li>列表项2</li>
  <li>列表项3</li>
  ......
</ul>
```

```
 1. <ul></ul>中只能嵌套<li></li>，直接在<ul></ul>标签中输入其他标签或者文字的做法是不被允许的。
 2. <li>与</li>之间相当于一个容器，可以容纳所有元素。
```

#### 有序列表-ol

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

#### 自定义列表-dl

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

### 其他

| 标签        | 描述                                               |
| ----------- | -------------------------------------------------- |
| <data>      | 与time类似，给机器阅读的内容，意义广泛，可自由定义 |
| <var>       | 变量，计算机、数学领域                             |
| <kbd>       | 用户输入，多表示键盘按键                           |
| <sub>       | 下标                                               |
| <sup>       | 上标                                               |
| <bdi>/<bdo> | bdi（html5）多语言混合时指定语言或书写方向         |
| <wbr>       | 表示可以换行的位置，把多个单词粘成很长时使用       |
| <menu>      | ul的变体，功能菜单                                 |

### HTML5语义化标签

| 标签         | 描述                                                         |
| ------------ | ------------------------------------------------------------ |
| <article>    | 定义文章。                                                   |
| <aside>      | 定义主体内容以外的内容，内容应该与周围内容相关，导航、广告等工具性质内容。 |
| <details>    | 定义用户能够查看或隐藏的额外细节。 目前只有 Chrome 和 Safari 6 |
| <figcaption> | 定义 <figure> 元素的标题。                                   |
| <figure>     | 规定自包含内容，比如图示、图表、照片、代码清单等。           |
| <footer>     | 定义文档或节的页脚。一般是body或artical的直接子元素，可以和aside、nav、section相关联 |
| <address>    | 文章（作者）的联系方式，关联到artical和body                  |
| <header>     | 规定文档或节的页眉。一般是body或artical的直接子元素          |
| <main>       | 规定文档的主内容。                                           |
| <mark>       | 定义高亮文本。                                               |
| <nav>        | 定义导航链接。header中多为文章目录，aside中多为关联页面或整站地图 |
| <section>    | 定义文档中的节。                                             |
| <summary>    | 定义 <details> 元素的可见标题。                              |
| <time>       | 定义日期/时间。                                              |
| <datalist>   | 定义选项列表。请与 input 元素配合使用该元素，来定义 input 可能的值。   input 元素的 list 属性来绑定 datalist。 |
| <fieldset>   | 可将表单内的相关元素分组，浏览器会以特殊方式来显示它们，它们可能有特殊的边界、3D 效果，或者甚至可创建一个子表单来处理这些元素。 <legend>为 fieldset 元素定义标题。 |

修改之前没有语义化注重样式的标签

| 标签    | 描述                         |
| ------- | ---------------------------- |
| <small> | 补充评论                     |
| <s>     | 错误内容，多用于打折前价格   |
| <i>     | 变调                         |
| <b>     | 关键字                       |
| <u>     | 之前是下划线，避免歧义的标注 |

#### 兼容处理

```html
<script src="../js/html5shiv.min.js"></script>
```

#### figure 和 figcaption 元素

在书籍和报纸中，与图片搭配的标题很常见。

标题（caption）的作用是为图片添加可见的解释。

```html
<figure>
   <img src="pic_mountain.jpg" alt="The Pulpit Rock" width="304" height="228">
   <figcaption>Fig1. - The Pulpit Pock, Norway.</figcaption>
</figure> 
```

### 语义化标签呈现Wiki百科

开这个页面：https://en.wikipedia.org/wiki/World_Wide_Web
副本：<http://static001.geekbang.org/static/time/quote/World_Wide_Web-Wikipedia.html>

```html
<aside></aside>
<artical>
    <!-- 标题组：中间的横线使用样式，hr表示故事的走向和话题的转变 -->
	<hgroup><h1></h1><h2></h2></hgroup>
    <!-- 缩写 -->
    <abbr title="World Wide Web">www</abbr>
    <!-- note：注记 -->
    <p class="note"></p>
    <p>...
        <!-- 重要的内容 -->
        <strong></strong>
        <!-- 引述 -->
        <blockquote>段落引述</blockquote>
        <q>行内引述</q>
    	<cite>作品名</cite>
    	<time datetime="2019-05-06">时间</time>
    	<figure>
            具有一定自包含性的内容
            <img src=""/>
            <figcaption>独立内容的标题</figcaption>
    	</figure>
    	<!-- 定义 -->
    	The <dfn>Internet</dfn> is ...
    	<!-- 目录 -->
    	<nav>
    		<h2>Contents</h2>
            <ol>
                <li>
                	<ol>
                        ...
                    </ol>
                </li>
                <li></li>
                ...
            </ol>
    	</nav>
    	<!-- pre：预先排版的内容不需要浏览器排版 -->
    	<pre>
    		<samp>计算机输出标签：定义样本文本</samp>
    		<code>计算机输出标签：代码文本</code>
    	</pre>
    </p>
</artical>
```

## 链接标签

链接是 HTML 中的一种机制，它是 HTML 文档和其它文档或者资源的连接关系，在 HTML 中，链接有两种类型。一种是超链接型标签，一种是外部资源链接。

![链接标签](E:\Jennifer\other\notes\media\链接标签.png)

### a标签

**行内元素**

a 标签是“anchor”的缩写，它是锚点的意思，所谓锚点，实际上也是一种比喻的用法。

基本语法格式如下：

```html
<a href="跳转目标" target="目标窗口的弹出方式">文本或图像</a>
```

**href**：用于指定链接目标的**url**地址，当为标签应用href属性时，它就具有了超链接的功能。 Hypertext Reference的缩写。意思是超文本引用

**target**：用于指定链接页面的打开方式，其取值有**\_self**和**\_blank**两种，其中\_self为默认值，\_blank为在新窗口中打开方式。

注意：

1. 外部链接 需要添加 http://
2. 内部链接 直接链接内部页面名称即可 比如` < a href="index.html"> 首页 </a >`
3. 如果当时没有确定链接目标时，通常将链接标签的href属性值定义为“#”(即href="#")，表示该链接暂时为一个空链接。
4. 不仅可以创建文本超链接，在网页中各种网页元素，如图像、表格、音频、视频等都可以添加超链接。

锚点定位 ：

通过创建锚点链接，用户能够快速定位到目标内容。
创建锚点链接分为两步：

```html
1.使用<a href="#id名">"链接文本"</a>创建链接文本。
2.使用相应的id名标注跳转目标的位置。
```

a 标签其实同时充当了链接和目标点的角色，当 a 标签有 href 属性时，它是链接，当它有 name时，它是链接的目标。具有 href 的 a 标签跟一些 link 一样，会产生超链接，也就是在用户不操作的情况下，它们不会被主动下载的被动型链接。

重点的内容是，a 标签也可以有 rel 属性，首先是跟 link 相同的一些 rel，包括下面的几种。这些跟 link 语义完全一致，不同的是，a 标签产生的链接是会实际显示在网页中的，而 link 标签仅仅是元信息。

alternate
author
help
license
next
prev
search

除了这些之外，a 标签独有的 rel 类型：

tag 表示本网页所属的标签；
bookmark 到上级章节的链接。

a 标签还有一些辅助的 rel 类型，用于提示浏览器或者搜索引擎做一些处理：

nofollow 此链接不会被搜索引擎索引；
noopener 此链接打开的网页无法使用 opener 来获得当前页面的窗口；
noreferrer 此链接打开的网页无法使用 referrer 来获得当前页面的 url；
opener 打开的网页可以使用 window.opener 来访问当前页面的 window 对象，这是 a 标签的默认行为。

### area标签

a 标签基本解决了在页面中插入文字型和整张图片超链接的需要，但是如果我们想要在图片的某个区域产生超链接，那么就要用到另一种标签了——area 标签。

area 标签与 a 标签非常相似，不同的是，它不是文本型的链接，而是区域型的链接。
area 标签支持的 rel 与 a 完全一样，这里就不多说了。
area 是整个 html 规则中唯一支持非矩形热区的标签，它的 shape 属性支持三种类型。

圆形：circle 或者 circ，coords 支持三个值，分别表示中心点的 x,y 坐标和圆形半径 r。
矩形：rect 或者 rectangle，coords 支持两个值，分别表示两个对角顶点 x1，y1 和 x2，y2。
多边形：poly 或者 polygon，coords 至少包括 6 个值，表示多边形的各个顶点。

因为 area 设计的时间较早，所以不支持含有各种曲线的路径，但是它也是唯一一个支持了非矩形触发区域的元素，所以，对于一些效果而言，area 是必不可少的。

area 必须跟 img 和 map 标签配合使用。使用示例如下（例子来自 html 标准）。

```html
<img src="planets.gif" alt="Planets" usemap ="#planetmap" />

<map id="planetmap">
 <area shape ="rect" coords ="0,0,110,260" href ="sun.htm" alt="Sun" />
 <area shape ="circle" coords ="129,161,10" href ="mercur.htm" alt="Mercury" />
 <area shape ="circle" coords ="180,139,14" href ="venus.htm" alt="Venus" />
</map>
```

这个例子展示了在一张图片上画热区并且产生链接，分别使用了矩形、圆形和多边形三种 area。

### link标签

HTML 标准并没有规定浏览器如何使用元信息，我们还讲到了元信息中有不少是被设计成“无需被浏览器识别，而是专门用于搜索引擎看的”。link 标签也是元信息的一种，在很多时候，它也是不会对浏览器产生任何效果的。

link 标签会生成一个链接，它可能生成超链接，也可能生成外部资源链接。一些 link 标签会生成超链接，这些超链接又不会像 a 标签那样显示在网页中。这就是**超链接型的link 标签**。这意味着多数浏览器中，这些 link 标签不产生任何作用。但是，这些 link 标签能够被搜索引擎和一些浏览器插件识别，从而产生关键性作用。比如，到页面 RSS 的 link 标签，能够被浏览器的 RSS 订阅插件识别，提示用户当前页面是可以
RSS 订阅的。
另外一些 link 标签则会把外部的资源链接到文档中，也就是说，会实际下载这些资源，并且做出一些处理，比如我们常见的用 link 标签引入样式表。除了元信息的用法之外，多数**外部资源型的 link 标签**还能够被放在 body 中使用，从而起到把外部资源链接进文档的作用。link 标签的链接类型主要通过 rel 属性来区分，我们提到 xx 型 link 即表示属性rel 为 xx 的 link。

#### 超链接类 link 标签

超链接型 link 标签是一种被动型链接，在用户不操作的情况下，它们不会被主动下载。
link 标签具有特定的 rel 属性，会成为特定类型的 link 标签。产生超链接的 link 标签包括：具有
rel=“canonical” 的 link、具有 rel="alternate"的 link、具有 rel=“prev” rel="next"的link 等等。

**canonical 型 link**

`<link rel='canonical' href='xx'>`

这个标签提示页面它的主 URL，在网站中常常有多个 URL 指向同一页面的情况，搜索引擎访问这类页面时会去掉重复的页面，这个 link 会提示搜索引擎保留哪一个 URL。

**alternate 型 link**

这个标签提示页面它的变形形式，这个所谓的变形可能是当前页面内容的不同格式、不同语言或者为不同的设备设计的版本，这种 link 通常也是提供给搜索引擎来使用的。
alternate 型的 link 的一个典型应用场景是，页面提供 rss 订阅时，可以用这样的 link 来引入：

`<link rel='alternate' type='application/rss+xml' title='RSS' href='xxx'>`

除了搜索引擎外，很多浏览器插件都能识别这样的 link。

**prev 型 link 和 next 型 link**

在互联网应用中，很多网页都属于一个序列，比如分页浏览的场景，或者图片展示的场景，每个网页是序列中的一个项。这种时候，就适合使用 prev 和 next 型的 link 标签，来告诉搜索引擎或者浏览器它的前一项和后一项，这有助于页面的批量展示。因为 next 型 link 告诉浏览器“这是很可能访问的下一个页面”，HTML 标准还建议对 next 型link 做预处理

**其它超链接类的 link**

其它超链接类 link 标签都表示一个跟当前文档相关联的信息，可以把这样的 link 标签视为一种带链接功能的 meta 标签。

rel=“author” 链接到本页面的作者，一般是 mailto: 协议
rel=“help” 链接到本页面的帮助页
rel=“license” 链接到本页面的版权信息页
rel=“search” 链接到本页面的搜索页面（一般是站内提供搜索时使用）

#### 外部资源类 link 标签

外部资源型 link 标签会被主动下载，并且根据 rel 类型做不同的处理。外部资源型的标签包括：具有 icon 型的 link、预处理类 link、modulepreload 型的 link、stylesheet、pingback。

**icon 型 link**

这类链接表示页面的 icon。多数浏览器会读取 icon 型 link，并且把页面的 icon 展示出来。icon 型 link 是**唯一一个外部资源类的元信息 link**，其它元信息类 link 都是超链接，这意味着，icon 型 link 中的图标地址**默认会被浏览器下载和使用**。如果没有指定这样的 link，多数浏览器会使用域名根目录下的 favicon.ico，即使它并不存在，所以从性能的角度考虑，建议一定要保证页面中有 icon 型的 link。**只有 icon 型 link 有有效的 sizes 属性**，HTML 标准允许一个页面出现多个 icon 型 link，并且用sizes 指定它适合的 icon 尺寸。

**预处理类 link** 

我们都知道，导航到一个网站需要经过 dns 查询域名、建立连接、传输数据、加载进内存和渲染等一系列的步骤。预处理类 link 标签就是允许我们控制浏览器，提前针对一些资源去做这些操作，以提高性能（当
然如果你乱用的话，性能反而更差）。下面我来列一下这些 link 类型：

dns-prefetch 型 link 提前对一个域名做 dns 查询，这样的 link 里面的 href 实际上只有域名有意义。
preconnect 型 link 提前对一个服务器建立 tcp 连接。
prefetch 型 link 提前取 href 指定的 url 的内容。
preload 型 link 提前加载 href 指定的 url。
prerender 型 link 提前渲染 href 指定的 url。

**modulepreload 型的 link**

modulepreload 型 link 的作用是预先加载一个 JavaScript 的模块。这可以保证 JS 模块不必等到执行时才加载。这里的所谓加载，是指完成下载并放入内存，并不会执行对应的 JavaScript。

```html
<link rel="modulepreload" href="app.js">
<link rel="modulepreload" href="helpers.js">
<link rel="modulepreload" href="irc.js">
<link rel="modulepreload" href="fog-machine.js">
<script type="module" src="app.js">
```

这个例子来自 HTML 标准，我们假设 app.js 中有 import “irc” 和 import “fog-machine”,而 irc.js 中有 import “helpers”。这段代码使用 moduleload 型 link 来预加载了四个 js 模块。尽管，单独使用 script 标签引用 app.js 也可以正常工作，但是我们通过加入对四个 JS 文件的link 标签，使得四个 JS 文件有机会被并行地下载，这样提高了性能。

**stylesheet 型 link**

基本用法是从一个 CSS 文件创建一个样式表。这里 type 属性可以没有，如果有，必须是"text/css"才会生效。
rel 前可以加上 alternate，成为 rel=“alternate stylesheet”，此时必须再指定 title 属性。这样可以为页面创建一份变体样式，一些浏览器，如 Firefox 3.0，支持从浏览器菜单中切换这些样式，当然了，大部分浏览器不支持这个功能，所以仅仅从语义的角度了解一下这种用法即可。

**pingback 型 link**

这样的 link 表示本网页被引用时，应该使用的 pingback 地址，这个机制是一份独立的标准，遵守 pingback 协议的网站在引用本页面时，会向这个 pingback url 发送一个消息。

## 特殊字符标签

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

## 表格-table

### 创建表格

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

~~~
1.table用于定义一个表格。
2.tr 用于定义表格中的一行，必须嵌套在 table /table标签中，在 table /table中包含几对 tr /tr，就有几行表格。
3.td ：用于定义表格中的单元格，必须嵌套在<tr></tr>标签中，一对 <tr> </tr>中包含几对<td></td>，就表示该行中有多少列（或多少个单元格）。
~~~

注意：

```
1. <tr></tr>中只能嵌套<td></td>
```

```
2. <td></td>标签，他就像一个容器，可以容纳所有的元素
```

### 表格属性

|    属性     |               描述               | 常用值                       |
| :---------: | :------------------------------: | ---------------------------- |
|   border    |               边框               |                              |
| cellspacing |   单元格与单元格边框之间的空隙   | 2（默认）                    |
| cellpadding | 单元格内容与单元格边框之间的空隙 | 1（默认）                    |
|    width    |                                  |                              |
|   height    |                                  |                              |
|    align    |           水平对齐方式           | left,center,right            |
|    frame    |     边框显示的样式，ie不兼容     | box,above,below,hsides,vside |

### 表头标签

表头一般位于表格的**第一行或第一列**，其文本加粗居中，如下图所示，即为设置了表头的表格。设置表头非常简单，只需用表头标签**&lt;th&gt;&lt;/th&gt;**替代相应的单元格标签&lt;td&gt;&lt;/td&gt;即可。

### 表格结构

```<caption></caption>```:表格标题,必须紧跟<table></table>标签后

在使用表格进行布局时，可以将表格划分为头部、主体和页脚（页脚因为有兼容性问题），具体 如下所示：

```<thead></thead>```：用于定义表格的头部。
必须位于<table></table> 标签中，一般包含网页的logo和导航等头部信息。

```<tbody></tbody>```：用于定义表格的主体。
位于<table></table>标签中，一般包含网页中除头部和底部之外的其他内容。

```html
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

### 合并单元格

跨行合并：rowspan（合并列）    跨列合并：colspan（合并行）

## 表单标签

在HTML中，一个完整的表单通常由表单控件（也称为表单元素）、提示信息和表单域3个部分构成。

1. 表单控件：包含了具体的表单功能项，如单行文本输入框、密码输入框、复选框、提交按钮、重置按钮等。

2. 提示信息：一个表单中通常还需要包含一些说明性的文字，提示用户进行填写和操作。

3. 表单域：  他相当于一个容器，用来容纳所有的表单控件和提示信息，可以通过他定义处理表单数据所用程序的url地址，以及数据提交到服务器的方法。如果不定义表单域，表单中的数据就无法传送到后台服务器。

### input 标签

**块级元素**

在上面的语法中，&lt;input /&gt;标签为单标签，type属性为其最基本的属性，其取值有多种，用于指定不同的控件类型。除了type属性之外，&lt;input /&gt;标签还可以定义很多其他的属性，其常用属性如下表所示。

| 属性      | 值/描述                                                      |
| --------- | ------------------------------------------------------------ |
| type      | text,password,radio,checkbox,button,submit,reset,image(图像形式的提交按钮，结合src属性使用),file |
| name      | 同一组radio或checkbox的name相同                              |
| value     | 默认文本值                                                   |
| size      | 显示宽度                                                     |
| checked   | checked（radio或checkbox结合使用）                           |
| maxlength |                                                              |

### label 标签

label 标签为 input 元素定义标注（标签）。

作用：  用于绑定一个表单元素, 当点击label标签的时候, 被绑定的表单元素就会获得输入焦点

**for** 属性规定 label 与哪个表单元素绑定（**id**）。

```html
<label for="male">Male</label>
<input type="radio" name="sex" id="male" value="male">
```

### textarea 标签(文本域)

如果需要输入大量的信息，就需要用到&lt;textarea&gt;&lt;/textarea&gt;标签。通过textarea控件可以轻松地创建多行文本输入框，其基本语法格式如下：

```html
<textarea cols="每行中的字符数" rows="显示的行数">
  文本内容
</textarea>
```

### 下拉菜单

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

### 表单域

在HTML中，form标签被用于定义表单域，即创建一个表单，以实现用户信息的收集和传递，form中的所有有**name**属性的内容都会被提交给服务器。创建表单的基本语法格式如下：

```html
<form action="url地址" method="提交方式" name="表单名称">
  各种表单控件
</form>
```

常用属性：

1. Action在表单收集到信息后，需要将信息传递给服务器进行处理，action属性用于指定接收并处理表单数据的服务器程序的url地址。
2. method用于设置表单数据的提交方式。
3. name用于指定表单的名称，以区分同一个页面中的多个表单。

注意：  每个表单都应该有自己表单域。

### HTML5新增属性

| **属性**         | **用法**                                       | **含义**                                                   |
| ---------------- | ---------------------------------------------- | ---------------------------------------------------------- |
| **placeholder**  | <input type="text" placeholder="请输入用户名"> | 占位符提供可描述输入字段预期值的提示信息                   |
| **autofocus**    | <input type="text" autofocus>                  | 规定当页面加载时 input 元素应该自动获得焦点                |
| **multiple**     | <input type="file" multiple>                   | 多文件上传                                                 |
| **autocomplete** | <input type="text" autocomplete="off">         | 规定表单是否应该启用自动完成功能，只有提交过的内容才会记录 |
| **required**     | <input type="text" required>                   | 必填项                                                     |
| **accesskey**    | <input type="text" accesskey="s">              | 规定激活（使元素获得焦点）元素的快捷键为alt+‘s’            |

### HTML5新增type属性值：

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

### 综合案例

```html
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
```

## 替换型元素

链接外的另一种引入文件的方式了。替换型元素是把文件的内容引入，替换掉自身位置的一类标签。

### script标签

script	标签是为数不多的既可以作为替换型标签，又可以不作为替换型标签的元素。

两种 script 标签的写法，一种是直接把脚本代码写在 script 标签之间，另一种是把代码放到独立的 js 文件中，用 src 属性引入。

凡是替换型元素，都是使用 src 属性来引用文件的，而链接型元素是使用 href 标签的。但是 style 标签并非替换型元素，不能使用 src 属性，这样，我们用 link 标签引入 CSS 文件，当然就是用 href 标签啦。

### img标签

**行内元素**

src属性用于指定图像文件的路径和文件名，他是img标签的必需属性。

```html
<img src="图像URL" />
```

| 属性  | 值                        | 说明           |
| ----- | ------------------------- | -------------- |
| src   | url                       | 路径           |
| alt   | 文本                      | 不显示时的替换 |
| title | 文本                      | 悬停内容       |
| align | bottom（默认）;middle;top | 文本对齐方式   |

**结合map实现图像映射**

```html
<img src="1.jpg" usemap="#Map" />
<map name="Map">
	<area shape="热点形状" coords="坐标" href="链接" alt="替代文字" />
	<area shape="circle" coords="180,139,14" href ="/example/html/venus.html" target ="_blank" alt="Venus" />
	<area shape="rect" coords="0,0,110,260" href ="/example/html/sun.html"  target ="_blank" alt="Sun" />
</map>
```

img没有办法像 script 标签那样作为非替换型标签来使用的，它必须有 src 属性才有意义。如果一定不想要引入独立文件，可以使用 **data uri**。

当我们单独指定宽度或高度后，图片会被**等比例缩放**。这个特性非常重要，适用于那种我们既要限制图片尺寸，又要保持图片比例的场景。如果从性能的角度考虑，建议你同时给出图片的宽高，因为替换型元素加载完文件后，如果尺寸发生变换，会触发重排版。

**alt 属性**，这个属性很难被普通用户感知，对于视障用户非常重要，可以毫不夸张地讲，给 img 加上 alt 属性，已经做完了可访问性的一半。

img 标签还有一组重要的属性，那就是 **srcset 和 sizes**，它们是 src 属性的升级版（标签必须有 src 属性，这是不严谨的说法）。
这两个属性的作用是在不同的屏幕大小和特性下，使用不同的图片源。下面一个例子也来自MDN，它展示了 srcset 和 sizes 的用法

```html
<img srcset="elva-fairy-320w.jpg 320w, 
             elva-fairy-480w.jpg 480w, 
             elva-fairy-800w.jpg 800w" 
     sizes="(max-width:	320px)	280px, 
            (max-width:	480px)	440px,
            800px"
	src="elva-fairy-800w.jpg" alt="Elva	dressed as a fairy">
```

srcset	提供了根据屏幕条件选取图片的能力，但是其实更好的做法，是使用	picture	元素。

#### **Data URL**

参考：[http://verymuch.site/2017/12/14/Data-URL%E7%AE%80%E4%BB%8B%E4%B8%8E%E4%BD%BF%E7%94%A8/](http://verymuch.site/2017/12/14/Data-URL简介与使用/)

`Data URL`，是以`data:`模式为前缀的URL，允许内容的创建者将较小的文件嵌入到文档中，使用场合与常规URL相同。

`Data URL`由**data:前缀、MIME类型（表明数据类型）、base64标志位（如果是文本，则可选）以及数据本身四部分组成**。

语法格式如下：

```js
data:[<mediatype>][;base64],data
```

`mediatype`是一个MIME（Multipurpose Internet Mail Extension）类型字符串，如`image/jpeg`表示一个JPEG图片文件。如果省略，默认值为`text/plain;charset=US-ASCII`。

1. Data URL的优势

   和传统的外部资源引用相比：

   - 当访问外部资源很麻烦或受限时，可以将外部资源转为Data URL引用（鸡肋）
   - 当图片是在服务器端用程序动态生成，每个访问用户显示的都不同时，这是需要返回一个可用的URL（场景较少）
   - 当图片的体积太小，**占用一个HTTP会话**不是很值得时

2. Data URL的缺点

   虽然Data URL允许使用者将文件嵌入到文档中，这在某些场景下较为合适，但是Data URL也有一些缺点：

   - 体积更大：Base64编码的**数据体积通常是原数据的体积4/3**，也就是Data URL形式的图片会比二进制格式的图片体积大1/3
   - 不会缓存：Data URL形式的图片**不会被浏览器缓存**，这意味着每次访问这样的页面时都被下载一次。这是一个使用效率方面的问题——尤其当这个图片被整个网站大量使用的时候。

**获取base64编码**

1. Linux/Mac OS X下可以使用`uuencode`命令

`uuencode -m <源文件> <转码后标识>`

1. Javascript中有两个函数负责编码和解码base64字符串，分别是`atob`和`btoa`。
   - `atob()`: 负责解码已经使用base64编码了的字符串。
   - `btoa()`: 将二进制字符串转为base64编码的ASCII字符串。

两者都只针对Data URL中的data进行处理。

```js
btoa('hello base64') // "aGVsbG8gYmFzZTY0"
atob('aGVsbG8gYmFzZTY0') // "hello base64"
```

3. Canvas提供了`toDataURL`方法，用于获取canvas绘制内容，将其转为base64格式。
4. 使用FileReader API的`readAsDataURL`方法

```html
<div class="demo-area">
  <input type="file" id="testReadAsDataURL">
  <textarea id="testReadAsDataURL-content"></textarea>
</div>
```

```js
var reader = new FileReader()
reader.onload = function(e) {
  var textarea = document.getElementById('testReadAsDataURL-content');
  textarea.value = reader.result
}
document.getElementById('testReadAsDataURL').onchange = function(e) {
  var file = e.target.files[0]
  reader.readAsDataURL(file)
}
```

#### **base64原理**

Data URL是Base64编码的，且Base64编码的数据体积通常是原数据的体积4/3。

1. 为什么Base64编码可以内联到HTML中

我们知道HTTP协议是文本协议，不同于常规的二进制协议那样直接进行二进制传输。Base64编码是**从二进制到字符的过程，可用于在HTTP环境下传递较长的标识信息。**

2. 为什么Base64编码后，体积会增大1/3

首先Base64是一种编码算法，该算法共包含64个字符。包括大小写拉丁字母各26个、数字10个、加号+和斜杠/，共64个字符。此外还有等号=用来作为后缀用途。

首先，ASCII码的范围是0-127，其中0-31和127是控制字符，共33个。其余95个，即32-126是可打印字符，包括数字、大小写字母、常用符号等。早期的一些传输协议，例如邮件传输协议SMTP，只能传输可打印的ASCII字符。这样原本的8bit字节码（0-255）就会超出使用范围，从而导致无法传输。

这时，就产生了Base64编码，它利用**6bit字符来表达原本的8bit字符**。6bit显然不够容纳8bit的数据。6和8的最小公倍数是24，所以我们用4个Base64字符刚好能够表示三个传统的8bit字符，所以体积会大1/3。

![base64-01](E:\Jennifer\other\notes\media\base64-01.jpg)

如果待编码的字符串长度不是三的倍数时需要做一个特殊处理，假设待编码字符串长度为10。这前9个字符可以用12个Base64字符表示。第10个字符的前6bit作为一个Base64字符，**剩下的2bit后面需要先补0，补到6位**作为第二个Base64字符，至于第三个和第四个Base64字符，虽然没有相对应的内容，我们仍需**以=填充**。

![base64-02](E:\Jennifer\other\notes\media\base64-02.jpg)

### picture标签

picture	元素可以根据屏幕的条件为其中的	img	元素提供不同的源，它的基本用法如下：

通过包含零或多个 [`source`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/source) 元素和一个 [`img`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/img) 元素来为不同的显示/设备场景提供图像版本。浏览器会选择最匹配的子 `<source>` 元素，如果没有匹配的，就选择 `<img>` 元素的 `src` 属性中的URL。然后，所选图像呈现在`<img>`元素占据的空间中。

```html
<picture>
		<source	srcset="image-wide.png"	media="(min-width:	600px)">
		<img	src="image-narrow.png">
</picture>
```

这里的 media 属性是 media query，跟 CSS 的 @media	规则一致。

### video标签

```html
<video controls="controls" >
<source src="movie.webm" type="video/webm" >
<source src="movie.ogg" type="video/ogg" >
<source src="movie.mp4" type="video/mp4">
You browser does not support video.
</video>
```

source 标签除了支持 media 之外，还可以使用 type 来区分源文件的使用场景。

video 中还支持一种标签：track。是一种播放时序相关的标签，它最常见的用途就是字幕。track 标签中，必须使用 srclang来指定语言，此外，track 具有 kind 属性，共有五种。

subtitles：就是字幕了，不一定是翻译，也可能是补充性说明
captions：报幕内容，可能包含演职员表等元信息，适合听障人士或者没有打开声音的人了解音频内容
descriptions：视频描述信息，适合视障人士或者没有视频播放功能的终端打开视频时了解视频内容用
chapters：用于浏览器视频内容。
metadata：给代码提供的元信息，对普通用户不可见。

### audio标签

```html
<audio controls>
<source src="song.mp3" type="audio/mpeg">
<source src="song.ogg" type="audio/ogg">
<p>You browser does not support audio.</p>
</audio>
```

### iframe标签

最后我们来讲一下 iframe，这个标签能够嵌入一个完整的网页。不过，在移动端，iframe	受到了相当多的限制，它无法指定大小，里面的内容会被完全平铺到父级页面上。同时很多网页也会通过	http	协议头禁止自己被放入 iframe 中。

iframe 标签也是各种安全问题的重灾区。opener、window.name、甚至 css 的 opacity 都是黑客可以利用的漏洞。因此，在 2019 年，当下这个时间点，任何情况下我都不推荐在实际开发中用以前的 iframe。

# 语言

## 实体

## 命名空间

# 补充标准

# H5

- H5 是一个产品名词
- HTML5 是一个技术名词

不是HTML5，泛指移动端页面，具体的就是在iPhone这类无法播放Flash的移动端上呈现的，可以达到Flash效果（如各种动画，互动）的，用于广告、营销的，具有酷炫效果的网页。可以简略称为「移动端PPT」，H5可能用到HTML5的标准，也可能完全没有用到。

# CSS的发展历程

# 引入CSS样式表

## 内部样式表

内嵌式是将CSS代码集中写在HTML文档的head头部标签中，并且用style标签定义

```html
<head>
    <style type="text/CSS">
        选择器 {属性1:属性值1; 属性2:属性值2; 属性3:属性值3;}
    </style>
</head>
```

语法中，style标签一般位于head标签中**title标签之后**，也可以把他放在HTML文档的任何地方。

type="text/CSS"  在html5中可以省略， 写上也比较符合规范， 所以这个地方可以写也可以省略。

## 行内式（内联样式）

内联样式，又有人称行内样式、行间样式、内嵌样式。是通过标签的style属性来设置元素的样式

```html
<标签名 style="属性1:属性值1; 属性2:属性值2; 属性3:属性值3;"> 内容 </标签名>
```

语法中style是标签的属性，实际上任何HTML标签都拥有style属性，用来设置行内式。其中属性和值的书写规范与CSS样式规则相同，行内式只对其所在的标签及嵌套在其中的子标签起作用。

## 外部样式表（外链式）

链入式是将所有的样式放在一个或多个以.CSS为扩展名的外部样式表文件中，通过link标签将外部样式表文件链接到HTML文档中，其基本语法格式如下：

```html
<head>
  <link href="CSS文件的路径" type="text/CSS" rel="stylesheet" />
</head>
```

注意：  link 是个单标签哦!!!

该语法中，link标签需要放在head头部标签中，并且必须指定link标签的三个属性，具体如下：

```
href：定义所链接外部样式表文件的URL，可以是相对路径，也可以是绝对路径。
type：定义所链接文档的类型，在这里需要指定为“text/CSS”，表示链接的外部文件为CSS样式表。
rel：定义当前文档与被链接文档之间的关系，在这里需要指定为“stylesheet”，表示被链接的文档是一个样式表文件。
```

## 三种样式表总结

| 样式表     | 优点                     | 缺点                     | 使用情况       | 控制范围           |
| ---------- | ------------------------ | ------------------------ | -------------- | ------------------ |
| 行内样式表 | 书写方便，权重高         | 没有实现样式和结构相分离 | 较少           | 控制一个标签（少） |
| 内部样式表 | 部分结构和样式相分离     | 没有彻底分离             | 较多           | 控制一个页面（中） |
| 外部样式表 | 完全实现结构和样式相分离 | 需要引入                 | 最多，强烈推荐 | 控制整个站点（多） |

# CSS书写规范

# CSS注释

```
CSS规则是使用     /*  需要注释的内容  */  进行注释的。
```

# CSS qulified Rule

## 字体样式-font

- font-size:字号大小

font-size属性用于设置字号，该属性的值可以使用相对长度单位，也可以使用绝对长度单位。

- font-family:字体

font-family属性用于设置字体。`p{ font-family:"微软雅黑";}`

可以同时指定多个字体，中间以**逗号**隔开，表示如果浏览器不支持第一个字体，则会尝试下一个，直到找到合适的字体。

```
1. 现在网页中普遍使用12px+。
2. 尽量使用偶数的数字字号。ie6等老式浏览器支持奇数会有bug。
4. 中文字体需要加引号，英文字体一般不需要加引号。如果字体名中包含空格、#、$等符号，则该字体必须引号，例如font-family: "Times New Roman";。
5. 当需要设置英文字体时，英文字体名必须位于中文字体名之前。
6. 尽量使用系统默认字体，保证在任何用户的浏览器中都能正确显示。
```

- CSS Unicode字体

在 CSS 中设置字体名称，直接写中文是可以的。但是在文件编码（GB2312、UTF-8 等）不匹配时会产生乱码的错误。xp 系统不支持 类似微软雅黑的中文。

1. 你可以使用英文来替代。 比如 font-family:"Microsoft Yahei"。 

2. 在 CSS 直接使用 Unicode 编码来写字体名称可以避免这些错误。
`font-family: "\5FAE\8F6F\96C5\9ED1"`，表示设置字体为“微软雅黑”。

| 字体名称    | 英文名称        | Unicode 编码         |
| ----------- | --------------- | -------------------- |
| 宋体        | SimSun          | \5B8B\4F53           |
| 新宋体      | NSimSun         | \65B0\5B8B\4F53      |
| 黑体        | SimHei          | \9ED1\4F53           |
| 微软雅黑    | Microsoft YaHei | \5FAE\8F6F\96C5\9ED1 |
| 楷体_GB2312 | KaiTi_GB2312    | \6977\4F53_GB2312    |
| 隶书        | LiSu            | \96B6\4E66           |
| 幼园        | YouYuan         | \5E7C\5706           |
| 华文细黑    | STXihei         | \534E\6587\7EC6\9ED1 |
| 细明体      | MingLiU         | \7EC6\660E\4F53      |
| 新细明体    | PMingLiU        | \65B0\7EC6\660E\4F53 |

- font-weight:字体粗细

字体加粗除了用 b 和 strong 标签之外，可以使用CSS 来实现，但是CSS 是没有语义的。

```html
font-weight属性用于定义字体的粗细，其可用属性值：normal、bold、bolder、lighter、100~900（100的整数倍）。

数字 400 等价于 normal，而 700 等价于 bold。  但是我们更喜欢用数字来表示。
```

- font-style:字体风格

字体倾斜除了用 i  和 em 标签之外，可以使用CSS 来实现，但是CSS 是没有语义的。

font-style属性用于定义字体风格，其可用属性值如下：

1. normal：默认值，浏览器会显示标准的字体样式。

2. italic：浏览器会显示斜体的字体样式。

```
平时我们很少给文字加斜体，反而喜欢给斜体标签（em，i）改为普通模式。
```

- font:综合设置字体样式

font属性用于对字体样式进行综合设置，其基本语法格式如下：

```css
选择器{font: font-style  font-weight  font-size/line-height  font-family;}
行高不写单位的情况：line-height=n*font-size
```

使用font属性时，必须按上面语法格式中的顺序书写，**不能更换顺序**，各个属性以空格隔开。

注意：其中不需要设置的属性可以省略（取默认值），但**必须保留font-size和font-family属性**，否则font属性将不起作用。

## 文本颜色-color

color属性用于定义文本的颜色，其取值方式有如下3种：

1. 预定义的颜色值，如red，green，blue等。
2. 十六进制，如#FF0000，#FF6600，#29D794等。
3. RGB/RGBA，如红色可以表示为rgb(255,0,0)或rgb(100%,0%,0%)。

需要注意的是，如果使用RGB代码的百分比颜色值，取值为0时也不能省略百分号，必须写为0%。

## 行间距-line-height

行间距就是行与行之间的距离，即字符的垂直间距，一般称为行高。line-height常用的属性值单位有三种，分别为像素px，相对值em和百分比%，实际工作中使用最多的是像素px。

一般情况下，行距比字号大7.8像素左右就可以了。

### 行高的测量

行高可以调整文字在盒子内垂直方向的位置

## 水平对齐方式-text-align

| 值      | 描述             |
| ------- | ---------------- |
| left    | 左对齐（默认值） |
| right   |                  |
| center  |                  |
| justify | 两端对齐         |
| inherit |                  |

## 首行缩进-text-indent

其属性值可为不同单位的数值、em或相对于浏览器窗口宽度的百分比%，允许使用负值, 建议使用em作为设置单位，1em 就是一个字的宽度 。

## 文本装饰-text-decoration 

| 值           | 描述                                          |
| ------------ | --------------------------------------------- |
| none         | 默认。定义标准的文本。                        |
| underline    | 定义文本下的一条线。下划线 也是我们链接自带的 |
| overline     | 定义文本上的一条线。                          |
| line-through | 定义穿过文本下的一条线。                      |

## 字间距-letter-spacing

letter-spacing属性用于定义字间距，所谓字间距就是字符与字符之间的空白。其属性值可为不同单位的数值，允许使用负值，默认为normal。

## 单词间距-word-spacing

word-spacing属性用于定义英文单词之间的间距，对中文字符无效。和letter-spacing一样，其属性值可为不同单位的数值，允许使用负值，默认为normal。

word-spacing和letter-spacing均可对英文进行设置。不同的是letter-spacing定义的为字母之间的间距，而word-spacing定义的为英文单词之间的间距。

## 自动换行-word-break

| 值        | 描述                           |
| --------- | ------------------------------ |
| normal    | 使用浏览器默认的换行规则。     |
| break-all | 允许在单词内换行。             |
| keep-all  | 只能在半角空格或连字符处换行。 |

主要处理英文单词

## 文本显示-white-space

设置或检索对象内文本显示方式。通常我们使用于强制一行显示内容 

```
normal : 默认处理方式
nowrap : 强制在同一行内显示所有文本，直到文本结束或者遭遇br标签对象才换行。可以处理中文
```

## 文本方向-writing-mode

定义了文本水平或垂直排布以及在块级元素中文本的行进方向。

`writing-mode:horizontal-tb` 定义了内容从左到右水平流动，从上到下垂直流动。下一条水平线位于上一条线下方。

`writing-mode:vertical-rl` 定义了内容从上到下垂直流动，从右到左水平流动。下一条垂直线位于上一行的左侧。

`writing-mode:vertical-lr`定义了内容从上到下垂直流动，从左到右水平流动。下一条垂直线位于上一行的右侧。

`writing-mode:sideways-rl`(仅Firefox41+实现)定义了内容从上到下垂直流动，所有字形，甚至是垂直脚本中的字形，都设置在右侧。

`writing-mode:sideways-lr`(仅Firefox41+实现)内容从上到下垂直流动，所有字形，甚至是垂直脚本中的字形，都设置在左侧。

## 文本对齐-direction

`direction: ltr;`

默认值，让文本和其他元素从左到右显示。

`direction: rtl;`

让文本和其他元素从右到左显示。

## 文字溢出-text-overflow

```
clip : 　不显示省略标记（...），而是简单的裁切 
ellipsis : 　当对象内文本溢出时显示省略标记（...）
```

注意：一定要首先强制一行内显示，再和overflow属性  搭配使用

### 溢出的文字隐藏

```
p {
	white-space: nowrap;
	overflow: hidden;
	text-overflow: ellipsis;
}
```

## 颜色透明度(CSS3)

1. RGBA：此色彩模式与RGB相同，只是新增了Alpha透明度(0-1)。 不会影响子代的透明度

```css
color: rgba(r,g,b,a)  
```

2. HSLA(H,S,L,A)：

H：Hue(色调)。0(或360)表示红色，120表示绿色，240表示蓝色。取值为：0 - 360 

S：Saturation(饱和度)。取值为：0.0% - 100.0% 

L：Lightness(亮度)。取值为：0.0% - 100.0% ，一般取50%

A：Alpha（0-1）

## 文字阴影(CSS3)

以后我们可以给我们的文字添加阴影效果了  Shadow  影子  

```css
text-shadow:水平位置 垂直位置 模糊距离 阴影颜色;
```

![1498467502625](./media/1498467502625.png) 

**前两项是必须写的**, 后两项可以选写。

### 凹凸文字 

```css
<head>
        <meta charset="utf-8">
        <style>
        body {
        	background-color: #ccc;
        }
		div {
			color: #ccc;
			font: 700 80px "微软雅黑";
		}
		div:first-child {
			/* text-shadow: 水平位置  垂直位置  模糊距离 阴影颜色; */
			text-shadow: 1px 1px 1px #000, -1px -1px 1px #fff;
		}
		div:last-child {
			/* text-shadow: 水平位置  垂直位置  模糊距离 阴影颜色; */
			text-shadow: -1px -1px 1px #000, 1px 1px 1px #fff;
		}
        </style>
    </head>
    <body>
    <div>我是凸起的文字</div>
    <div>我是凹下的文字</div>
    </body>
```

![1498467533412](./media/1498467533412.png)

## 背景-background

CSS 可以添加背景颜色和背景图片，以及来进行图片设置。

| 属性名称                                                    | 描述             |
| ----------------------------------------------------------- | ---------------- |
| background-color                                            | 背景颜色         |
| background-image                                            | 背景图片地址     |
| background-repeat                                           | 是否平铺         |
| background-position                                         | 背景位置         |
| background-attachment                                       | 背景固定还是滚动 |
| 背景的合写（复合属性）                                      |                  |
| background:背景颜色 背景图片地址 背景平铺 背景滚动 背景位置 |                  |

- 背景图片（image）

```css
background-image : none | url (url) 

none : 　无背景图（默认的）
url : 　使用绝对或相对地址指定背景图像 
```

background-image 属性允许指定一个图片展示在背景中（只有CSS3才可以多背景）可以和background-color 连用。 如果图片不重复地话，图片覆盖不到地地方都会被背景色填充。 如果有背景图片平铺，则会覆盖背景颜色。

提倡背景图片后面的url不要加引号。

- 背景平铺（repeat）

```css
background-repeat : repeat | no-repeat | repeat-x | repeat-y | round | space

repeat : 　背景图像在纵向和横向上平铺（默认的）
no-repeat : 　背景图像不平铺
repeat-x : 　背景图像在横向上平铺
repeat-y : 　背景图像在纵向平铺 
```

- 背景位置（position）

```css
background-position : length || length
background-position : position || position 

length : 　百分数 | 由浮点数字和单位标识符组成的长度值。请参阅长度单位 
position : 　top | center | bottom | left | center | right 
```

设置或检索对象的背景图像位置。必须先指定background-image属性。默认值为：(0% 0%)。
如果只指定了一个值，该值将用于横坐标。纵坐标将默认为50%。第二个值将用于纵坐标。

注意：

1. position 后面是x坐标和y坐标。 可以使用方位名词或者 精确单位。
2. 如果和精确单位和方位名字混合使用，则必须是x坐标在前，y坐标后面。比如 background-position: 15px top;   则 15px 一定是  x坐标   top是 y坐标。

- 背景附着（attachment）

```css
background-attachment : scroll | fixed  

scroll : 　背景图像是随对象内容滚动
fixed : 　背景图像固定 
```

- 背景简写

background属性的值的书写顺序官方并没有强制标准的。为了可读性，建议大家如下写：

background：背景颜色 背景图片地址 背景平铺 背景滚动 背景位置

```css
background: transparent url(image.jpg) repeat-y  scroll 50% 0 ;
```

### 背景透明 CSS3

CSS3支持背景半透明的写法语法格式是:

```css
background: rgba(0,0,0,0.3);
```

 最后一个参数是alpha 透明度  取值范围 0~1之间

 注意：  背景半透明是指盒子背景半透明， 盒子里面的内容不收影响。

### 背景缩放-size CSS3

通过**background-size**设置背景图片的尺寸，就像我们设置img的尺寸一样，在移动Web开发中做屏幕适配应用非常广泛。

其参数设置如下：

```css
number/percentage：可以设置长度单位(px)或百分比（设置百分比时，参照盒子的宽高）当只取一个值时，第二个值相当于auto 。
cover：会自动调整缩放比例，保证图片始终填充满背景区域，如有溢出部分则会被隐藏。我们平时用的cover 最多
contain：会自动调整缩放比例，保证图片始终完整显示在背景区域。
```

```css
background-image: url('images/gyt.jpg');
background-size: 300px 100px;
/* background-size: contain; */
/* background-size: cover; */
```

### 背景参考原点-origin CSS3

1. 作用：background-origin 属性规定 background-position 属性相对于什么位置来定位。默认值是left top左上角（border-box）

   `background-origin: padding-box|border-box|content-box;`

2. 属性值说明：

| padding-box | 背景图像相对于内边距框来定位。 |
| ----------- | ------------------------------ |
| border-box  | 背景图像相对于边框盒来定位。   |
| content-box | 背景图像相对于内容框来定位。   |

### 背景裁剪-clip CSS3

1. background-clip 属性规定背景的绘制区：虽然是设置裁切，但是控制的是显示。就是设置最终显示那些区域

   `background-clip: border-box|padding-box|content-box;`

2. 属性值说明：

| **值**      | **描述**               |
| ----------- | ---------------------- |
| border-box  | 背景被裁剪到边框盒。   |
| padding-box | 背景被裁剪到内边距框。 |
| content-box | 背景被裁剪到内容框。   |

结合background-origin应用：为块设置精灵图背景，以更大的范围响应用户的需要。

### 多背景 CSS3

以逗号分隔可以设置多背景，可用于自适应布局  做法就是 用逗号隔开就好了。

- 一个元素可以设置多重背景图像。 
- 每组属性间使用逗号分隔。 
- 如果设置的多重背景图之间存在着交集（即存在着重叠关系），前面的背景图会覆盖在后面的背景图之上。
- 为了避免背景色将图像盖住，背景色通常都定义在最后一组上，

```css
缩写：background:url(test1.jpg) no-repeat scroll 10px 20px/50px 60px content-box padding-box,
	   url(test1.jpg) no-repeat scroll 10px 20px/70px 90px content-box padding-box,
	   url(test1.jpg) no-repeat scroll 10px 20px/110px 130px content-box padding-box #aaa;
拆分：background-image:url(test1.jpg),url(test2.jpg),url(test3.jpg);
background-repeat:no-repeat,no-repeat,no-repeat;
background-attachment:scroll,scroll,scroll;
background-position:10px 20px,10px 20px,10px 20px;
background-size:50px 60px,70px 90px,110px 130px;
background-origin:content-box,content-box,content-box;
background-clip:padding-box,padding-box,padding-box;
background-color:#aaa;

```

也可以这么写：

```
background-image:url("1.jpg"),url("2.jpg"),url("3.jpg");
background-repeat: no-repeat, no-repeat, no-repeat;  
background-position: 0 0, 200px 0, 400px 201px;  
```

## 用户界面样式

 所谓的界面样式， 就是更改一些用户操作样式， 比如 更改用户的鼠标样式， 表单轮廓，防止表单域拖拽等。但是比如滚动条的样式改动受到了很多浏览器的抵制，因此我们就放弃了。 

### 鼠标样式cursor

 设置或检索在对象上移动的鼠标指针采用何种系统预定义的光标形状。 

```css
cursor :  default  小白 | pointer  小手  | move  移动  |  text  文本
```

```html
<ul>
  <li style="cursor:default">我是小白</li>
  <li style="cursor:pointer">我是小手</li>
  <li style="cursor:move">我是移动</li>
  <li style="cursor:text">我是文本</li>
</ul>
```

 尽量不要用hand  因为 火狐不支持     pointer ie6以上都支持的尽量用

### 轮廓- outline

 是绘制于元素周围的一条线，位于边框边缘的外围，可起到突出元素的作用。

```css
 outline : outline-color ||outline-style || outline-width 
```

我们平时都是去掉的，最直接的写法是 ：  outline: 0;   或者  outline: none;

```html
 <input  type="text"  style="outline: 0;"/>
```

### 防止拖拽文本域-resize

resize：none    这个单词可以防止 火狐 谷歌等浏览器随意的拖动 文本域。

右下角不可以拖拽： 

```html
<textarea  style="resize: none;"></textarea>
```

### 垂直对齐-vertical-align 

以前我们讲过让带有宽度的块级元素居中对齐，是margin: 0 auto;

以前我们还讲过让文字居中对齐，是 text-align: center;

```css
vertical-align : baseline |top |middle |bottom 
```

设置或检索对象内容的垂直对其方式。 

vertical-align 不影响块级元素中的内容对齐，它只针对于 行内元素或者行内块元素，特别是行内块元素， **通常用来控制图片/表单与文字的对齐**。

### 图片、表单和文字对齐

所以我们知道，我们可以通过vertical-align 控制图片和文字的垂直关系了。 默认的图片会和文字基线对齐。

### 去除图片底侧空白缝隙

图片或者表单等行内块元素，他的底线会和父级盒子的基线对齐。这样会造成一个问题，就是图片底侧会有一个空白缝隙。

解决的方法就是：  

1. 给img vertical-align:middle | top等等。  让图片不要和基线对齐；
2. 给img 添加 display：block; 转换为块级元素就不会存在问题了；
3. 给父元素添加font-size： 0；
4. 给父元素添加line-height： 0；

# CSS @-rule

## @charset

`@charset`用于定义样式表中使用的字符编码。它必须写在样式表的**最开头**且前面**不可**有别的字符。

`@charset "UTF-8";`

## @import

`@import`用于导入外部 `CSS样式表`文件。

与link的区别：@import先加载html后加载css

1. link属于XHTML标签，而@import完全是css提供的一种方式。link标签除了可以加载css外，还可以做很多其他的事情，比如定义RSS，定义rel连接属性等，@import只能加载CSS。

2. 加载顺序的差别：当一个页面被加载的时候（就是被浏览者浏览的时候），link引用的CSS会同时被加载，而@import引用的CSS会等到页面全部被下载完再加载。所以有时候浏览@import加载CSS的页面时会没有样式（就是闪烁），网速慢的时候还挺明显。

3. 兼容性的差别。由于@import是CSS2.1提出的只有在IE5以上的才能识别，而link标签无此问题，完全兼容。

4. 使用dom控制样式时的差别。当时用JavaScript控制dom去改变样式的时候，只能使用link标签，因为@import不是dom可以控制的（不支持）。

```css
/* @import url; */
/* @import url list-of-media-queries; */
@importm'custom.css';
@import url("fineprint.css") print ;
```

## @media

`@media`用于定义在一个或多个**设备类型**、**具体特点**和**环境**的媒体查询来应用样式。

```css
@media screen and (min-width: 900px) {
    h1 { color: red; }
}
```

## @page

`@page`用于在打印文档时修改某些CSS属性。 `@page`规则只能修改 `margin`、 `orphans`、 `widow` 和 `page breaks of the document`，对其他属性的修改是无效的。

```css
@page {
    size: 10in 20in;
    margin: 10% 20%;
}
```

## @keyframes

`@keyframs`通过定义动画序列中的**关键帧**来控制 `CSS动画`不同步骤的状态。

```css
@keyframes slidein {
    from { width: 300%; }
    to { width: 100%; }
}
```

## @fontface

`@font-face`用于给网页指定文本字体。

```css
@font-face {
    font-family: "xxx";
    src: url("xxx");
}
body {
    font-family: "xx";
}
```

## @supports

`@supports`用来检测规则组的**规则**是否生效。规则与 `@media`类似

```css
@supports (display: flex) {
    div { display: flex; }
}
```

## @namespace

`@namespace`是用来定义使用在 `CSS样式表`中的 `XML`命名空间的@规则。

```css
/* 默认命名空间 */
@namespace "XML-namespace-URL";
@namespace url(XML-namespace-URL);

/* 命名空间前缀 */
@namespace prefix url(XML-namespace-URL);
@namespace prefix "XML-namespace-URL";

@namespace svg url(http://www.w3.org/2000/svg);

/* 匹配所有的XHTML <a> 元素, 因为 XHTML 是默认无前缀命名空间 */
a {}

/* 匹配所有的 SVG <a> 元素 */
svg|a {}

/* 匹配 XHTML 和 SVG <a> 元素 */
*|a {}
```

## @viewport

```css
@viewport {
    min-width: 640px;
 	/* 初始缩放系数 */   
    zoom: 0.75;
    /* 文档方向 */
 	/* landscape文件应锁定在横向。portrait文档应该锁定在纵向方向上 */ 
    orientation: landscape;
}
```

## @counter-style

`@counter-style`用于自定义 `counter`的样式

```css
/*
 * @counter-style <counter-style-name> {
 *   <group-rule-body>
 * }
 */
@count-style circled-alpha {
    system: fixed;
    symbols: Ⓐ;
	suffix: " ";
}
.items {
    list-style: circled-alpha
}
```

## @doucment

`@document`如果满足条件组的**条件**，则规则生效（推延至 CSS Level 4 规范）

```css
@document url(http://www.w3.org/),
               url-prefix(http://www.w3.org/Style/),
               domain(mozilla.org),
               regexp("https:.*")
{
  /* 该条CSS规则会应用在下面的网页:
     + URL为"http://www.w3.org/"的页面.
     + 任何URL以"http://www.w3.org/Style/"开头的网页
     + 任何主机名为"mozilla.org"或者主机名以".mozilla.org"结尾的网页     
     + 任何URL以"https:"开头的网页 */

  /* make the above-mentioned pages really ugly */
  body { color: purple; background: yellow; }
}
```

# 选择器

## 基础选择器

- 标签选择器（元素选择器）

标签选择器是指用HTML标签名称作为选择器，为页面中某一类标签指定统一的CSS样式。

```
标签名{属性1:属性值1; 属性2:属性值2; 属性3:属性值3; } 
```

- 类选择器

类选择器使用“.”（英文点号）进行标识，后面紧跟类名

```
.类名{属性1:属性值1; 属性2:属性值2; 属性3:属性值3; }
```

小技巧：

```
1.长名称或词组可以使用中横线来为选择器命名。
2.不要纯数字、中文等命名，尽量使用英文字母来表示。
```

命名规范：  见附件（Web前端开发规范手册.doc）

- 多类名选择器

我们可以给标签指定多个类名，从而达到更多的选择目的。

```
1. 样式显示效果跟HTML元素中的类名先后顺序没有关系,受CSS样式书写的上下顺序有关。
2. 各个类名中间用空格隔开。
```

- id选择器

id选择器使用“#”进行标识，后面紧跟id名。

```
#id名{属性1:属性值1; 属性2:属性值2; 属性3:属性值3; }
```

大多数HTML元素都可以定义id属性，元素的id值是唯一的，只能对应于文档中某一个具体的元素。

- 通配符选择器

通配符选择器用“*”号表示，他是所有选择器中作用范围最广的，能匹配页面中所有的元素。

例如下面的代码，使用通配符选择器定义CSS样式，清除所有HTML标记的默认边距。

```css
* {
  margin: 0;                    /* 定义外边距*/
  padding: 0;                   /* 定义内边距*/
}
```

## 伪类选择器

  伪类选择器用于向某些选择器添加特殊的效果。比如给链接添加特殊效果， 比如可以选择 第1个，第n个元素。

### 链接伪类选择器

- E:link      /* 未访问的链接 */

- E:visited   /* 已访问的链接 */

- E:hover     /* 鼠标移动到链接上 */

- E:active    /* 选定的链接 */

  注意写的时候，他们的顺序尽量不要颠倒  按照  lvha 的顺序。   love   hate  爱上了讨厌 记忆法

### 结构(位置)伪类选择器（CSS3)

- E:first-child :选取属于其父元素的首个子元素的指定选择器（CSS2）
- E:last-child :选取属于其父元素的最后一个子元素的指定选择器
- E:nth-child(n) ： 匹配属于其父元素的第 N 个子元素，不论元素的类型
  - -n+5：表示前5个
- E:nth-last-child(n) ：选择器匹配属于其元素的第 N 个子元素的每个元素，不论元素的类型，从最后一个子元素开始计数。  
- E:nth-child(even): 所有的偶数
- E:nth-child(odd): 所有的奇数
- E:nth-of-type(n):指定类型
- E:nth-last-of-type(n):指定类型，从最后一个子元素开始计数。  
- E:empty 选中没有任何子节点的E元素，注意，空格也算子元素

**重点：n遵循线性变化，其取值0、1、2、3、4、... 但是当n<=0时，选取无效 **

## 目标伪类选择器(CSS3)

 E:target目标伪类选择器 :为锚点目标元素添加样式，当E为当前锚链接目标时的样式。

```css
h1:target {
		color: red;
		font-size: 30px;
}
```

## 组合选择器

- 交集选择器

EE：交集选择器由两个选择器构成，选择器之间不能有空格。

- 并集选择器

E，E：并集选择器（CSS选择器分组）是各个选择器通过**逗号**连接而成的。

- 后代选择器

E E：后代选择器又称为包含选择器，用来选择元素或元素组的后代，中间用**空格**分隔。

- 子元素选择器

E > E：子元素选择器只能选择作为某元素子元素的元素。中间跟一个 **&gt;** 进行连接。

- 相邻选择器

E + E：选中符合条件的**相邻**元素

- 兄弟选择器（CSS3）

E ~ E：选中符合条件的兄弟元素

```html
<p>p1</p>
<p>p2</p>
<h3>这是一个标题</h3>
<p>p3</p>
<h3>这是一个标题</h3>
<p>p4</p>
<p>p5</p>

如果使用p + p{color:#f00;}，那么p2, p5将会变成红色
如果使用p ~ p{color:#f00;}，那么p2,p3,p4,p5将会变成红色；
```

- **|**: 命名空间选择器

例如：`.a|.b`。在例子中选中的就是属于 `.a`的 `.b`，跟 `.a.b`一样，属于**Selectors Leve 3**的内容。

- **||**：列选择器

例如：`.a||.b`。在例子中选中的就是由 `.a`表示的列的网格/表中的单元格的 `.b`，属于 `SelectorsLevel4`的内容。

## 属性选择器

选取标签带有某些特殊属性的选择器 我们成为属性选择器

E[attr]：选中带有attr属性的标签

E[attr='val']：选中带有attr属性值等于val的标签

E[attr~='val']：选中带有attr属性值为用空格分隔的字词列表，其中包括val的标签

CSS3：

E[attr^='val']：选中带有attr属性值以val开头的标签

E[attr$='val']：选中带有attr属性值以val结尾的标签

E[attr*='val']：选中带有attr属性值包含val字符的标签

E[attr|='val']：选中带有attr属性值为以val开头并用连接符"-"分隔的字符串的E元素，如果属性值仅为val，也将被选择

```css
/* 获取到 拥有 该属性的元素 */
div[class^=font] { /*  class^=font 表示 font 开始位置 */
	color: pink;
}
div[class$=footer] { /*  class$=footer 表示 footer 结束位置 */
	color: skyblue;
}
div[class*=tao] { /* class*=tao  *=  表示tao 在任意位置都可以 */
	color: green;
}
```

```html
<div class="font12">属性选择器</div>
<div class="font12">属性选择器</div>
<div class="font24">属性选择器</div>
<div class="font24">属性选择器</div>
<div class="font24">属性选择器</div>
<div class="24font">属性选择器123</div>
<div class="sub-footer">属性选择器footer</div>
<div class="jd-footer">属性选择器footer</div>
<div class="news-tao-nav">属性选择器</div>
<div class="news-tao-header">属性选择器</div>
<div class="tao-header">属性选择器</div>
```

## 伪元素选择器（CSS3)

1. E::first-letter文本的第一个单词或字（如中文、日文、韩文等）
2. E::first-line 文本第一行；
3. E::selection 可改变选中文本的样式；

```css
p::first-letter {
  font-size: 20px;
  color: hotpink;
}
/* 首行特殊样式 */
p::first-line {
  color: skyblue;
}
p::selection {
  /* font-size: 50px; */
  color: orange;
}
```

4、E::before和E::after

在E元素内部的开始位置和结束位创建一个元素，该元素为行内元素，且必须要结合content属性使用。

```css
div::befor {
  content:"开始";
}
div::after {
  content:"结束";
}
```

E:after、E:before 在旧版本里是伪元素，CSS3的规范里“:”用来表示伪类，“::”用来表示伪元素，但是在高版本浏览器下E:after、E:before会被自动识别为E::after、E::before，这样做的目的是用来做兼容处理。

## 其他

**:root选择器**用匹配文档的根元素。

在HTML中根元素始终是HTML元素。

# 函数

根据MDN所陈列的关键字索引，**css函数**一共有**86**个。

根据w3cplus中可以划分为以下几类：

- **属性函数**：`attr()`；
- **背景图片函数**：`linear-gradient()`、 `radial-gradient()`、 `conic-gradient()`、 `repeating-linear-gradient()`、 `repeating-radial-gradient()`、 `repeating-conic-gradient()`、 `image-set()`、 `image()`、 `url()`、 `element()`；
- **颜色函数**：`rgb()`、 `rgba()`、 `hsl()`、 `hsla()`、 `hwb()`、 `color-mod()`；
- **图形函数**：`circle()`、 `ellipse()`、 `inset()`、 `polygon()`、 `path()`
- **滤镜函数**：`blur()`、 `brightness()`、 `contrast()`、 `drop-shadow()`、 `grayscale()`、 `hue-rotate()`、 `invert()`、 `opacity()`、 `saturate()`、 `sepia()`；
- **转换函数**：`matrix()`、 `matrix3d()`、 `perspective()`、 `rotate()`、 `rotate3d()`、 `rotateX()`、 `rotateY()`、 `rotateZ()`、 `scale()`、 `scale3d()`、 `scaleX()`、 `scaleY()`、 `scaleZ()`、 `skew()`、 `skewX()`、 `skewY()`、 `translate()`、 `translateX()`、 `translateY()`、 `translateZ()`、 `translate3d()`；
- **数学函数**：`calc()`、 `min()`、 `max()`、 `mixmax()`、 `repeat()`；
- **缓动函数**：`cubic-bezier()`、 `steps()`；
- **其他函数**：`counter()`、 `counters()`、 `toggle()`、 `var()`、 `symbols()`。

这些函数各有各的功能，按需排列组合可以实现很多很酷炫的效果。在这里一定要安利大漠老师的CSS中的函数以及张鑫旭老师在**CSS CONF**中的分享，里面就讲了很多关于**CSS 函数**的应用。

## 背景图片函数

### element()

`element()`是属于CSS Image Value and Replaced Content Module Level 4中的背景函数。

`element()`可以将网站中的部分内容当成图片渲染。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <style>
    .edit,
    .show {
        width: 200px;
        height: 200px;
        margin: 10px;
        border: 1px solid #ccc;
    }
    .show {
      background: -moz-element(#edit);
      background-size: 100% 100%;
    }
    </style>
</head>
<body>
    <h1>限火狐浏览器</h1>
    <div contenteditable class="edit" id="edit"></div>
    <div class="show" id="show"></div>
</body>
</html>
```

### conic-gradient()

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <style>
    .colorful {
        width: 300px;
        height: 300px;
        background: conic-gradient(
            #9ED110,
            #50B517,
            #179067,
            #476EAF,
            #9f49ac,
            #CC42A2,
            #FF3BA7,
            #FF5800,
            #FF8100,
            #FEAC00,
            #FFCC00,
            #EDE604
        );
        border-radius: 50%;
        cursor: pointer;
        transition: all 0.5s ease;
    }
    .colorful:hover {
        /* filter：滤镜 */
        /* blur()：调整模糊度 */
        /* contrast()：调整对比度 */
        /* brightness()：调整亮度 */
        /* drop-shadow()：调整阴影 */
        /* hue-rotate（）：色调旋转 */
        /* grayscale()：转换为灰度 */
        filter: hue-rotate(180deg)
    }
    </style>
</head>
<body>
    <div class="colorful"></div>
</body>
</html>
```

# 其他

## 自定义属性

参考：[http://verymuch.site/2019/04/15/CSS%E8%87%AA%E5%AE%9A%E4%B9%89%E5%B1%9E%E6%80%A7%E5%8F%8A%E5%85%B6%E7%94%A8%E6%B3%95/#more](http://verymuch.site/2019/04/15/CSS自定义属性及其用法/#more)

### 自定义属性名

预处理器的变量也有一些缺点和限制，如下：

1. **不能动态修改变量**：预处理器是在编译时进行变量的处理，编译后变量其实就不存在了。
2. **没有DOM结构，无法级联继承**。
3. **不能用JavaScript进行读写**。

CSS自定义属性的语法格式为`--*`，双横线加上具体的自定义属性名，属性名是一个合法的CSS[标识符](https://www.w3.org/TR/css-syntax-3/#identifier)即可。

自定义属性没有具体的CSS含义，其用途完全由作者和使用者决定。自定义属性可以**应用于任何元素，其可以被继承，并且支持级联，不支持动画**。

注意：与CSS属性不同，自定义属性是**大小写敏感的**。

### 自定义属性值

可以是任何有效的CSS值，如颜色、字符、布局的值、甚至是表达式。

通过`var()`函数，自定义属性的值可以用作另一个属性的值。

`var( <custom-property-name> [, <declaration-value> ]? )`

其中第一个参数为自定义属性名，第二个参数为后备值。当传入的自定义属性无效或者不存在时，会使用后备值。

注意：

1. 自定义属性不能作为一个独立属性值的一部分

2. 会导致动画瑕疵，因为其只会在指定帧影响使用了自定义属性的可动画属性。
3. 如果在计算属性的时候，发现了依赖依赖循环，则**依赖循环中的所有自定义属性值都使用初始值代替**。

### 优势

1. **可以动态修改自定义属性**
2. **有DOM结构的概念，可以级联继承**。
3. **可以用JavaScript进行读写**。

CSS自定义属非常适合用来实现**主题的切换**

# 单位

# 布局

## 正常流

正常流的盒子属于**格式化上下文(FC)**，在**CSS2.2**中可以是**表格**、**块**或**内联**。 在**CSS3**中引入了**flex**跟**grid**，当然以后会引入得更多。

**块级盒子(block-level boxes)** 与创建 **块级格式化上下文(BFC)** 有关；

**行内级盒子(inline-level boxes)** 与创建 **行内级格式化上下文(IFC)** 有关。

### BFC

https://www.cnblogs.com/lhb25/p/inside-block-formatting-ontext.html

BFC(Block formatting context)：直译为"块级格式化上下文"。

创建了 BFC的元素就是一个独立的盒子，它是一个独立的渲染区域，只有Block-level box参与， 它规定了内部的Block-level Box如何布局，并且与这个区域外部毫不相干。

Box是CSS布局的对象和基本单位， 直观点来说，就是一个页面是由很多个Box(即boxes)组成的。元素的类型和display属性，决定了这个Box的类型。 不同类型的Box， 会参与不同的Formatting context(一个决定如何渲染文档的容器)，因此Box内的元素会以不同的方式渲染。

常见的盒子类型：

block-level box: display属性为block, list-item, table的元素，会生成block-level box。并且参与block fomatting context。 

inline-level box: display属性为inline, inline-block, inline-table的元素，会生成inline-level box。并且参与inline formatting context。

#### Formatting context

Formatting context是W3C CSS2.1规范中的一个概念。它是页面中的一块渲染区域，并且有一套渲染规则，它决定了其子元素将如何定位，以及和其他元素的关系和相互作用。  

#### W3C定义

​	浮动元素和绝对定位元素，非块级盒子的块级容器（例如 inline-blocks, table-cells, 和 table-captions），以及overflow值不为“visiable”的块级盒子，都会为他们的内容创建新的块级格式化上下文。 
​	在一个块级格式化上下文里，盒子从包含块的顶端开始垂直地一个接一个地排列，两个盒子之间的垂直的间隙是由他们的margin 值所决定的。两个相邻的块级盒子的垂直外边距会发生叠加。 

​	在块级格式化上下文中，每一个盒子的左外边缘（margin-left）会触碰到容器的左边缘(border-left)（对于从右到左的格式来说，则触碰到右边缘），即使存在浮动也是如此，除非这个盒子创建一个新的块级格式化上下文。 

#### 元素的显示模式

素的显示模式 display，分为 块级元素行内元素行内块元素，其实，它还有很多其他显示模式。

<img src="E:/Jennifer/other/notes/media/dis.png"  style="border: 1px dashed #ccc; padding: 5px;" />

#### 参与BFC的条件

**display 属性为 block, list-item, table 的元素，生成block-level box，可以参与BFC.**

#### 什么情况可以产生BFC

要给这些元素添加如下属性就可以触发BFC。

```
-float属性不为none
-position为absolute或fixed
-display为inline-block, table-cell, table-caption, flex, inline-flex
-overflow不为visible。

```

#### BFC元素所具有的特性

BFC布局规则特性：

1. 在BFC中，盒子从顶端开始垂直地一个接一个地排列。
2. 盒子**垂直**方向的距离由margin决定。**属于同一个BFC**的两个相邻盒子的margin会发生重叠。==》消除margin重叠问题
3. 在BFC中，每一个盒子的左外边缘（margin-left）会触碰到容器的左边缘(border-left)不会压住边框（对于从右到左的格式来说，则触碰到右边缘）。
4. BFC的区域不会与浮动盒子产生交集，而是紧贴浮动边缘。==》两栏右侧自适应效果
5. 计算BFC的高度时，自然也会检测浮动或者定位的盒子高度。==》清除浮动效果

#### BFC的主要用途

(1) 清除元素内部浮动

计算BFC的高度时，自然也会检测浮动或者定位的盒子高度。所以只要把父元素设为BFC就可以清理子元素的浮动了，最常见的用法就是在父元素上设置overflow: hidden样式，对于IE6加上zoom:1就可以了。

主要用到 

```
计算BFC的高度时，自然也会检测浮动或者定位的盒子高度。
```

<img src="E:/Jennifer/other/notes/media/fu.jpg" />
(2) 解决外边距合并问题

外边距合并的问题。

主要用到 

```
盒子垂直方向的距离由margin决定。属于同一个BFC的两个相邻盒子的margin会发生重叠

```

属于同一个BFC的两个相邻盒子的margin会发生重叠，那么我们创建不属于同一个BFC，就不会发生margin重叠了。

<img src="E:/Jennifer/other/notes/media/ma.png" />

(3) 制作右侧自适应的盒子问题

主要用到 

```
普通流体元素BFC后，为了和浮动元素不产生任何交集，顺着浮动边缘形成自己的封闭上下文

```

<img src="E:/Jennifer/other/notes/media/you.png" />

(4) 多列布局中防止最后一列因为浏览器四舍五入了列宽使总宽度会超出容器而掉下来，我们在多列布局中的最后一列里创建一个新的BFC，它将总是占据其他列先占位完毕后剩下的空间。 

```html
<div class="container">
    <div class="column">column 1</div>
    <div class="column">column 2</div>
    <div class="column">column 3</div>
</div>
<style>
.column {
    width: 31.33%;
    background-color: green;
    float: left;
    margin: 0 1%;
}
/*  Establishing a new block formatting 
    context in the last column */
.column:last-child {
    float: none;
	overflow: hidden; 
}
</style>
```

现在尽管盒子的宽度稍有改变，但布局不会打破。当然，对多列布局来说这不一定是个好办法，但能避免最后一列下掉。这个问题上弹性盒或许是个更好的解决方案，但这个办法可以用来说明元素在这些环境下的行为。

### IFC

跟**BFC**不一样，**IFC**内的盒子会从**包含块**的顶部一个接着一个地水平排列。这些盒子会考虑水平 `margin`， `border`跟 `padding`。垂直对齐的方式也略有复杂。然后，包含形成一条线的框的矩形区域称为**线盒（line box）**。 

**线盒（line box）的宽度**：由浮动情况跟它所在的包含块决定。

**线盒（line box）的高度**：由 `line-height`的计算结果决定。

#### 基线（baseline）

**线盒（line box）** 的高度由 `line-height`的计算结果决定。

`line-height`的定义就是**线盒（line box）**内两**基线（baseline）**（W3C原文）的间距。

`vertical-align`的默认值就是基线。

![img](https://mmbiz.qpic.cn/mmbiz_jpg/y0rsINPrlZy47EnPpnuzxFOjUlBytKfD4GPZTqnt4gj0mWhW1fxB0seiagCqHlDxTZ7yl8zpISZN8ls2LGDhRKg/640?wx_fmt=jpeg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

如上图所示，我们看到小写字母**x**的位置，它的上下边缘就是我们的**基线（baseline）**，但下边缘才是我们日常使用的属性值。顺便一提，CSS单位 `ex`便是指的这个**字母x**的高度。

## 层叠上下文与层叠顺序

其他参考：[http://verymuch.site/2019/01/18/CSS%E7%9A%84%E2%80%9C%E5%B1%82%E2%80%9D%E5%B3%A6%E2%80%9C%E5%8F%A0%E2%80%9D%E7%BF%A0/#more](http://verymuch.site/2019/01/18/CSS的"层"峦"叠"翠/#more)

![img](https://mmbiz.qpic.cn/mmbiz_png/y0rsINPrlZy47EnPpnuzxFOjUlBytKfD8PibeV0wAgc8rZLrbic8d8CMSXEDgFr0bzgUQ7lqnJewia0icgsx5L9WHg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

上面便是在同样的上下文中，元素的层叠规则（CSS3以后的除外，那规则会比较复杂）。元素的 **z-index 值**只在父级层叠上下文中有意义。级层叠上下文被自动视为父级层叠上下文的一个独立单元。

文档中的层叠上下文由满足以下任意一个条件的元素形成：

- 根元素 (HTML),
- z-index 值不为 `auto` 的 绝对/相对定位，
- 一个 z-index 值不为 `auto` 的 flex 项目 (flex item)，即：父元素 `display:flex|inline-flex`，
- `opacity` 属性值小于 1 的元素，
- `transform` 属性值不为 `none` 的元素，
- `mix-blend-mode` 属性值不为 "normal"的元素，
- `filter`值不为 `none` 的元素，
- `perspective`值不为 `none` 的元素，
- `isolation` 属性被设置为 `isolate` 的元素，
- `position:fixed`
- 在 `will-change` 中指定了任意 CSS 属性，即便你没有直接指定这些属性的值
- `-webkit-overflow-scrolling` 属性被设置 `touch` 的元素

## 弹性布局

这个是 **CSS** 史上第一个以 **start-end** 来定义方向的属性，这是一个可伸缩的布局模型，使得我们对块级元素的布局排列变得十分灵活，适应性非常强，其强大的伸缩性，在响应式开中可以发挥极大的作用。

一个设有 `display:flex` 或 `display:inline-flex` 的元素是一个伸缩容器，伸缩容器的子元素被称为为伸缩项目，这些子元素使用伸缩布局模型来排版。

主轴：Flex容器的主轴主要用来配置Flex项目，默认是水平方向

侧轴：与主轴垂直的轴称作侧轴，默认是垂直方向的

方向：默认主轴从左向右，侧轴默认从上到下

主轴和侧轴并不是固定不变的，通过flex-direction可以互换。

![1498441839910](E:/Jennifer/other/notes/media/1498441839910.png)

- flex子项目在主轴的缩放比例，不指定flex属性，则不参与伸缩分配

min-width: 280px  最小宽度  不能小于 280

max-width: 1280px  最大宽度  不能大于 1280

### flex-direction

调整主轴方向（默认为水平方向）

flex-direction: column 垂直排列

flex-direction: row  水平排列

http://m.ctrip.com/html5/   携程网手机端地址

### justify-content

调整主轴对齐（水平对齐）

| 值            | 描述                                             | 白话文                                         |
| ------------- | ------------------------------------------------ | ---------------------------------------------- |
| flex-start    | 默认值。项目位于容器的开头。                     | 让子元素从父容器的开头开始排序但是盒子顺序不变 |
| flex-end      | 项目位于容器的结尾。                             | 让子元素从父容器的后面开始排序但是盒子顺序不变 |
| center        | 项目位于容器的中心。                             | 让子元素在父容器中间显示                       |
| space-between | 项目位于各行之间留有空白的容器内。               | 左右的盒子贴近父盒子，中间的平均分布空白间距   |
| space-around  | 项目位于各行之前、之间、之后都留有空白的容器内。 | 相当于给每个盒子添加了左右margin外边距         |

### align-items

调整侧轴对齐（垂直对齐）

子盒子如何在父盒子里面垂直对齐（单行）

| 值         | 描述                           | 白话文                                                |
| ---------- | ------------------------------ | ----------------------------------------------------- |
| stretch    | 默认值。项目被拉伸以适应容器。 | 让子元素的高度拉伸适用父容器（子元素不给高度的前提下) |
| center     | 项目位于容器的中心。           | 垂直居中                                              |
| flex-start | 项目位于容器的开头。           | 垂直对齐开始位置 上对齐                               |
| flex-end   | 项目位于容器的结尾。           | 垂直对齐结束位置 底对齐                               |

### flex-wrap

控制是否换行

当我们子盒子内容宽度多于父盒子的时候如何处理

| 值           | 描述                                                         |
| ------------ | ------------------------------------------------------------ |
| nowrap       | 默认值。规定灵活的项目不拆行或不拆列。  不换行，则 收缩（压缩） 显示  强制一行内显示 |
| wrap         | 规定灵活的项目在必要的时候拆行或拆列。                       |
| wrap-reverse | 规定灵活的项目在必要的时候拆行或拆列，但是以相反的顺序。     |

### flex-flow

是flex-direction、flex-wrap的简写形式

```css
flex-flow: flex-direction  flex-wrap;  
```

例如：

```css
display: flex;
/* flex-direction: row;
flex-wrap: wrap;   这两句话等价于下面的这句话*/
flex-flow: column wrap;  /* 两者的综合 */
```

### flex

flex属性是flex-grow, flex-shrink 和 flex-basis的简写，默认值为0 1 auto。后两个属性可选

- flex-grow：设置子元素所占宽度的比例
- flex-shrink: 宽度不够时收缩的比例
- flex-basis：宽度多余时的比例

`flex` 属性可以指定1个，2个或3个值。

**单值语法**: 值必须为以下其中之一:

- 一个无单位 **数( <number>)** : 它会被当作 `<flex-grow>的值`。
- 一个有效的 **宽度(width)** 值: 它会被当作 `<flex-basis>的值`。
- 关键字 `none`、 `auto`, 或 `initial` 。

**双值语法**: 第一个值必须为一个无单位数，并且它会被当作 `<flex-grow>` 的值。第二个值必须为以下之一：

- 一个无单位数：它会被当作 `<flex-shrink>` 的值。
- 一个有效的宽度值: 它会被当作 `<flex-basis>` 的值。

**三值语法:**

- 第一个值必须为一个无单位数，并且它会被当作 `<flex-grow>` 的值。
- 第二个值必须为一个无单位数，并且它会被当作 `<flex-shrink>` 的值。
- 第三个值必须为一个有效的宽度值， 并且它会被当作 `<flex-basis>` 的值。

### align-content

堆栈（由flex-wrap产生的独立行）多行垂直对齐方式齐

align-content是针对flex容器里面多轴(多行)的情况,align-items是针对一行的情况进行排列。

必须对父元素设置自由盒属性display:flex;，并且设置排列方式为横向排列flex-direction:row;并且设置换行，flex-wrap:wrap;这样这个属性的设置才会起作用。

| 值            | 描述                                             | 测试 |
| ------------- | ------------------------------------------------ | ---- |
| stretch       | 默认值。项目被拉伸以适应容器。                   |      |
| center        | 项目位于容器的中心。                             |      |
| flex-start    | 项目位于容器的开头。                             |      |
| flex-end      | 项目位于容器的结尾。                             |      |
| space-between | 项目位于各行之间留有空白的容器内。               |      |
| space-around  | 项目位于各行之前、之间、之后都留有空白的容器内。 |      |

9、order控制子项目的排列顺序，正序方式排序，从小到大

用css 来控制盒子的前后顺序。  用order 就可以

用整数值来定义排列顺序，数值小的排在前面。可以为负值。 默认值是 0

```css
order: 1;
```

游戏：xxx网址

## Grid布局

**Flex**是一维布局，**Grid**是二维布局。意思就是**Flex**只能同时在一个方向进行作用，而**Grid**却可以在纵横两个方向同时工作。

### 网格轨道

我们通过 **grid-template-columns** 和 **grid-template-rows** 属性来定义网格中的行和列。这些属性定义了网格的轨道。一个网格轨道就是网格中任意两条线之间的空间。

#### fr单位

轨道可以使用任何长度单位进行定义。 网格还引入了一个另外的长度单位来帮助我们创建灵活的网格轨道。新的`fr`单位代表网格容器中可用空间的一等份。下一个网格定义将创建三个相等宽度的轨道，这些轨道会随着可用空间增长和收缩。

#### repeat()

有着多轨道的大型网格可使用 `repeat()` 标记来重复部分或整个轨道列表。

有规律的重复：

`grid-template-columns: repeat(3, 1fr 2fr);`

#### grid-auto-rows

grid-template-rows/columns没有定义时，网格将会在隐式网格中创建行和列。按照默认，这些轨道将自动定义尺寸，所以会根据它里面的内容改变尺寸。 

可以在隐式网格中用 grid-auto-rows 和 grid-auto-columns 属性来定义一个设置大小尺寸的轨道。 

#### minmax()

在设置一个显式的网格或者定义自动创建的行和列的大小的时候，我们也许想给网格一个最小的尺寸，确保他们能扩大到容纳他里面添加的内容。

### 网格线

应该注意的是，当我们定义网格时，我们定义的是网格轨道，而不是网格线。Grid 会为我们创建编号的网格线来让我们来定位每一个网格元素

![Diagram showing numbered grid lines.](https://mdn.mozillademos.org/files/14761/1_diagram_numbered_grid_lines.png)

### 网格单元

一个网格单元是在一个网格元素中最小的单位， 从概念上来讲其实它和表格的一个单元格很像。现在再看回我们前面的一个例子, 一旦一个网格元素被定义在一个父级元素当中，那么他的子级元素将会排列在每个事先定义好的网格单元中。

### 网格区域

网格元素可以向行或着列的方向扩展一个或多个单元，并且会创建一个网格区域。网格区域的形状应该是一个矩形 - 也就是说你不可能创建出一个类似于“L”形的网格区域。

### 网格间距

在两个网格单元之间的 *网格横向间距*  或 *网格纵向间距*  可使用 [`grid-column-gap`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/grid-column-gap) 和 [`grid-row-gap`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/grid-row-gap) 属性来创建，或者直接使用两个合并的缩写形式 [`grid-gap`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/grid-gap)。

# 标签显示模式（display）

HTML标签一般分为块标签和行内标签两种类型，它们也称块元素和行内元素。具体如下：

## 块级元素(block-level)

每个块元素通常都会独自占据一整行或多整行，可以对其设置宽度、高度、对齐等属性，常用于网页布局和网页结构的搭建。

```
常见的块元素有<h1>~<h6>、<p>、<div>、<ul>、<ol>、<li>等，其中<div>标签是最典型的块元素。

```

块级元素的特点：

（1）总是从新行开始

（2）高度，行高、外边距以及内边距都可以控制。

（3）宽度默认是容器的100%

（4）可以容纳内联元素和其他块元素。

## 行内元素(inline-level)

行内元素（内联元素）不占有独立的区域，仅仅靠自身的字体大小和图像尺寸来支撑结构，一般不可以设置宽度、高度、对齐等属性，常用于控制页面中文本的样式。

```
常见的行内元素有<a>、<strong>、<b>、<em>、<i>、<del>、<s>、<ins>、<u>、<span>等，其中<span>标签最典型的行内元素。

```

行内元素的特点：

（1）和相邻行内元素在一行上。

（2）高、宽无效，但水平方向的padding和margin可以设置，垂直方向的无效。

（3）默认宽度就是它本身内容的宽度。

（4）行内元素只能容纳文本或则其他行内元素。（a特殊可以放块级元素）

**注意：**

1. 只有 文字才 能组成段落  因此 p  里面不能放块级元素，同理还有这些标签h1,h2,h3,h4,h5,h6,dt，他们都是**文字类块级标签**，里面不能放其他块级元素。
2. 链接里面不能再放链接。

## 块级元素和行内元素区别

```
块级元素的特点：
（1）总是从新行开始
（2）高度，行高、外边距以及内边距都可以控制。
（3）宽度默认是容器的100%
（4）可以容纳内联元素和其他块元素。

```

```
行内元素的特点：
（1）和相邻行内元素在一行上。
（2）高、宽无效，但水平方向的padding和margin可以设置，垂直方向的无效。
（3）默认宽度就是它本身内容的宽度。
（4）行内元素只能容纳文本或则其他行内元素。

```

## 行内块元素（inline-block）

```
在行内元素中有几个特殊的标签——<img />、<input />、<td>，可以对它们设置宽高和对齐属性，有些资料可能会称它们为行内块元素。

行内块元素的特点：
（1）和相邻行内元素（行内块）在一行上,但是之间会有空白缝隙。
（2）默认宽度就是它本身内容的宽度。
（3）高度，行高、外边距以及内边距都可以控制。

```

**行内元素和行内块元素可以当成文本，可以用text-align居中**

## 标签显示模式转换 display

块转行内：display:inline;

行内转块：display:block;

块、行内元素转换为行内块： display: inline-block;

# CSS 三大特性

层叠 继承  优先级 是我们学习CSS 必须掌握的三个特性。

## CSS层叠性

所谓层叠性是指多种CSS样式的叠加。

是浏览器处理冲突的一个能力,如果一个属性通过两个相同选择器设置到同一个元素上产生了样式冲突，那么这个时候一个属性就会将另一个属性层叠掉

一般情况下，如果出现样式冲突，则会按照CSS书写的顺序，以最后的样式为准。

1. 样式冲突，遵循的原则是就近原则。 那个样式离着结构近，就执行那个样式。
2. 样式不冲突，不会层叠

## CSS继承性

所谓继承性是指书写CSS样式表时，子标签会继承父标签的某些样式，如文本颜色和字号。想要设置一个可继承的属性，只需将它应用于父元素即可。

简单的理解就是：  子承父业。

不可继承的：```display、margin、border、padding、background、height、min-height、max- height、width、min-width、max-width、overflow、position、left、right、top、 bottom、z-index、float、clear、table-layout、vertical-align、page-break-after、 page-bread-before和unicode-bidi```

**所有元素**可继承：```visibility和cursor```

**内联元素**可继承：```letter-spacing、word-spacing、white-space、line-height、color、font、 font-family、font-size、font-style、font-variant、font-weight、text- decoration、text-transform、direction```

**块状元素**可继承：```text-indent和text-align```

**列表元素**可继承：```list-style、list-style-type、list-style-position、list-style-image```

**表格元素**可继承：```border-collapse```

注意：

```
恰当地使用继承可以简化代码，降低CSS样式的复杂性。子元素可以继承父元素的样式（text-，font-，line-这些元素开头的都可以继承，以及color属性）

```

## CSS优先级

定义CSS样式时，经常出现两个或更多规则应用在同一元素上，这时就会出现优先级的问题。

权重：内联>ID>class>标签>通用

在考虑权重时，还需要注意一些特殊的情况，具体如下：

```
继承样式的权重为0。也就是说子元素定义的样式会覆盖继承来的样式。
权重相同时，CSS遵循就近原则。
CSS定义了一个!important命令，该命令被赋予最大的优先级。
```

其实像 `max-width`、 `mix-width`、 `max-height`、 `min-height`等条件属性是可以覆盖 `!important`的。

## CSS特殊性（Specificity）

关于CSS权重，我们需要一套计算公式来去计算，这个就是 CSS Specificity，我们称为CSS 特性或称非凡性，它是一个衡量CSS值优先级的一个标准 具体规范入如下：

specificity用一个四位的数 字串(CSS2是三位)来表示，更像四个级别，值从左到右，左面的最大，一级大于一级，数位之间没有进制，级别之间不可超越。 

| 继承或者* 的贡献值       | 0,0,0,0  |
| ------------------------ | -------- |
| 每个元素（标签）贡献值为 | 0,0,0,1  |
| 每个类，伪类贡献值为     | 0,0,1,0  |
| 每个ID贡献值为           | 0,1,0,0  |
| 每个行内样式贡献值       | 1,0,0,0  |
| 每个!important贡献值     | ∞ 无穷大 |

权重是可以叠加的

 比如的例子：

```
.nav ul li   ------>      0,0,1,2
.nav a       ------>      0,0,1,1   
#nav p       ----->       0,1,0,1
```

```
总结：权重是优先级的算法，层叠是优先级的表现
```

# 盒子模型

CSS就三个大模块：  盒子模型 、 浮动 、 定位，其余的都是细节。

所谓盒子模型就是把HTML页面中的元素看作是一个矩形的盒子，也就是一个盛装内容的容器。每个矩形都由元素的内容、内边距（padding）、边框（border）和外边距（margin）组成。 

## 基础盒模型（Box Model）

当浏览器对一个**render tree**进行渲染时，浏览器的渲染引擎就会根据**基础盒模型(CSS basic box model)**，将所有元素划分为一个个矩形的盒子，这些盒子的外观，属性由 `CSS`来决定。

规定了元素框处理元素内容、内边距、边框 和 外边距 的方式。

### 标准盒模型

**width，height指content的宽高**

**box-sizing: content-box**对应的盒模型

![这里写图片描述](https://img-blog.csdn.net/20180324150509906?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3p3a2trazE=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70) 

### IE盒模型

**width表示content+padding+border这三个部分的宽度** 

**box-sizing: border-box**对应的盒模型

![这里写图片描述](https://img-blog.csdn.net/20180324150533356?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3p3a2trazE=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70) 

## 盒子边框（border）

语法： 

```css
border : border-width || border-style || border-color 
```

边框属性—设置边框样式（border-style）

边框样式用于定义页面中边框的风格，常用属性值如下：

```
none：没有边框即忽略所有边框的宽度（默认值）
solid：边框为单实线(最为常用的)
dashed：边框为虚线  
dotted：边框为点线
double：边框为双实线
```

### 表格的细线边框

以前学过的html表格边框很粗，这里只需要CSS一句话就可以美观起来。

table{ border-collapse:collapse; }  collapse 单词是合并的意思

border-collapse:collapse; 表示边框合并在一起。

### 圆角边框(CSS3)

从此以后，我们的世界不只有矩形。radius 半径（距离）

语法格式：

```css
border-radius: 左上角  右上角  右下角  左下角;
```

## 内边距（padding）

padding属性用于设置内边距。是指边框与内容之间的距离。

padding-top，padding-right，padding-bottom，padding-left

padding: 上右下左/上下  左右 /上  左右  下/上  右  下  左

## 外边距（margin）

margin属性用于设置外边距。  设置外边距会在元素之间创建“空白”， 这段空白通常不能放置其他内容。

margin-top，margin-right，margin-bottom，margin-left

margin:上外边距 右外边距  下外边距  左外边

取值顺序跟内边距相同。

### 外边距实现盒子居中

可以让一个盒子实现水平居中，需要满足以下两个条件：

1. 必须是块级元素。     
2. 盒子必须指定了宽度（width）

然后就给**左右的外边距都设置为auto**，就可使块级元素水平居中。

```css
.header{ width:960px; margin:0 auto;}

```

### 文字盒子居中，图片和背景区别

1. 文字水平居中是  text-align: center
2. 盒子水平居中  左右margin 改为 auto 

```css
text-align: center; /*  文字居中水平 */
margin: 10px auto;  /* 盒子水平居中  左右margin 改为 auto 就阔以了 */

```

3. 插入图片 我们用的最多 比如产品展示类
4. 背景图片我们一般用于小图标背景 或者 超大背景图片

```css
section img {  
		width: 200px;/* 插入图片更改大小 width 和 height */
		height: 210px;
		margin-top: 30px;  /* 插入图片更改位置可以用 margin 或 padding 盒模型 */
		margin-left: 50px; /* 插入图片也是一个盒子 */
	}
aside {
		width: 400px;
		height: 400px;
		border: 1px solid purple;
		background: #fff url(images/sun.jpg) no-repeat;
		background-size: 200px 210px; /*  背景图片更改大小只能用 background-size */
		background-position: 30px 50px; /* 背景图片更该位置用 background-position */
	}

```

### 清除元素的默认内外边距

为了更方便地控制网页中的元素，制作网页时，可使用如下代码清除元素的默认内外边距： 

```css
* {
   padding:0;         /* 清除内边距 */
   margin:0;          /* 清除外边距 */
}

```

注意：  行内元素是只有左右外边距的，是没有上下外边距的。 内边距，在ie6等低版本浏览器也会有问题。

我们尽量不要给行内元素指定上下的内外边距就好了。

## 外边距合并

使用margin定义块元素的垂直外边距时，可能会出现外边距的合并。

解决方案：让这两个元素处于不同的BFC

### 相邻块元素垂直外边距的合并

当上下相邻的两个块元素相遇时，如果上面的元素有下外边距margin-bottom，下面的元素有上外边距margin-top，则他们之间的垂直间距不是margin-bottom与margin-top之和，而是两者中的**较大者**。这种现象被称为相邻块元素垂直外边距的合并（也称外边距塌陷）。

解决方案：  避免就好了。

### 嵌套块元素垂直外边距的合并

对于两个嵌套关系的块元素，如果父元素没有上内边距及边框，则父元素的上外边距会与子元素的上外边距发生合并，合并后的外边距为两者中的较大者，即使父元素的上外边距为0，也会发生合并。

解决方案：

1. 可以为父元素定义1像素的上边框或上内边距。
2. 可以为父元素添加overflow:hidden。（创建不同的BFC）

## content宽度和高度

使用宽度属性width和高度属性height可以对盒子的大小进行控制。

width和height的属性值可以为不同单位的数值或相对于父元素的百分比%，实际工作中最常用的是像素值。

大多数浏览器，如Firefox、IE6及以上版本都采用了W3C规范，符合CSS规范的盒子模型的总宽度和总高度的计算原则是：

```css
  /*外盒尺寸计算（元素空间尺寸）*/
  Element空间高度 = content height + padding + border + margin
  Element 空间宽度 = content width + padding + border + margin
  /*内盒尺寸计算（元素实际大小）*/
  Element Height = content height + padding + border （Height为内容高度）
  Element Width = content width + padding + border （Width为内容宽度）
```

注意：

1、宽度属性width和高度属性height仅适用于块级元素，对行内元素无效（ img 标签和 input除外）。

2、计算盒子模型的总高度时，还应考虑上下两个盒子**垂直外边距合并**的情况。

3、**如果一个盒子没有给定宽度/高度或者占满父亲的宽度/高度，则padding 不会影响本盒子大小**。

## 盒子模型布局稳定性

 分不清内外边距大部分情况下是可以混用的。但是，总有一个最好用的吧，我们根据稳定性来分，建议如下：

按照 优先使用  宽度 （width）  其次 使用内边距（padding）    再次  外边距（margin）。   

```
  width >  padding  >   margin   
```

原因：

1. margin 会有外边距合并 还有 ie6下面浮动后margin 加倍的bug所以最后使用。
2. padding  会影响盒子大小， 需要进行加减计算 其次使用。
3. width   没有问题我们经常使用宽度剩余法 高度剩余法来做。

## 盒子阴影

语法格式：

```css
box-shadow:水平阴影 垂直阴影 模糊距离 阴影尺寸 阴影颜色  内/外阴影；
```

1. 前两个属性是必须写的。其余的可以省略。
2. 外阴影 (outset) 但是不能写    默认   想要内阴影  inset 

```css
div {
	width: 200px;
	height: 200px;
	border: 10px solid red;
	/* box-shadow: 5px 5px 3px 4px rgba(0, 0, 0, .4);  */
	/* box-shadow:水平位置 垂直位置 模糊距离 阴影尺寸（影子大小） 阴影颜色  内/外阴影； */
	box-shadow: 0 15px 30px  rgba(0, 0, 0, .4);	
}
```

## 盒子居中

http://www.cnblogs.com/2050/p/3392803.html

### 水平居中

1. margin：0 auto；
2. （display: table-cell;）text-align:center;
3. flex布局；
4. 定位+transform；

### 垂直居中

1. margin-top+top定位
2. dispaly：table-cell；vertical-align：middle；
3. margin-top

## 视觉格式化模型

> `CSS`的**视觉格式化模型(visual formatting model)** 是根据 **基础盒模型(CSS basic box model)**将 **文档(doucment)** 中的元素转换一个个盒子的**实际算法**。
>
> 官方说法就是：**它规定了用户端在媒介中如何处理文档树( document tree )。**

每个盒子的布局由以下因素决定：

- 盒子的尺寸
- 盒子的类型：**行内盒子 (inline)**、**行内级盒子 (inline-level)**、**原子行内级盒子 (atomic inline-level)**、**块盒子 (block)**
- 定位：**普通流**、**浮动**、**绝对定位**
- 文档树中当前盒子的**子元素** 或 **兄弟元素**
- **视口(viewport)** 的**尺寸** 和**位置**
- 盒子内部图片的**尺寸**
- 其他某些外部因素

**视觉格式化模型(visual formatting model)** 的计算，都取决于一个矩形的边界，这个矩形，被称作是 **包含块( containing block )** 。 一般来说，(元素)生成的框会扮演它子孙元素包含块的角色；我们称之为：一个(元素的)框为它的子孙节点建造了包含块。包含块是一个相对的概念。

例子如下：

```html
<div>
    <table>
        <tr>
        	<td>hi</td>
        </tr>
    </table>
</div>
```

以上代码为例， `div` 和 `table` 都是包含块。 `div` 是 `table` 的包含块，同时 `table` 又是 `td`的包含块，不是绝对的。

![img](https://mmbiz.qpic.cn/mmbiz_png/y0rsINPrlZzAMxWXXgbYLvdQMkloKObC2cvH53RV1acqRcgWP4RaXV77nTbsJlN3DxwfnZTiaSTac9Z7ogUr9fg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

## 盒子的生成

盒子的生成是 **CSS视觉格式化模型** 的一部分，用于从文档元素生成盒子。盒子的类型取决于 `CSS display` 属性。

- **块级元素**

  当元素的 `display` 为 `block`、 `list-item` 或 `table` 时，它就是块级元素。

- **块级盒子**

  块级盒子用于描述它与父、兄弟元素之间的关系。

- 每个块级盒子都会参与**块格式化上下文（block formatting context）**的创建。

- 每个块级元素都会至少生成一个块级盒子，即**主块级盒子（principal block-level box）**，包含由后代元素生成的盒子以及内容，同时它也会参与定位方案。

- 一个同时是块容器盒子的块级盒子称为**块盒子（block box）**。

- **匿名盒子**

- 某些情况下需要进行视觉格式化时，需要添加一些增补性的盒子，这些盒子不能被 `CSS选择器`选中，也就是所有可继承的 CSS 属性值都为 `inherit` ，而所有不可继承的 CSS 属性值都为 `initial`。因此称为**匿名盒子(anonymous boxes)**。

- **行内元素**

- 当元素的 `display` 为 `inline`、 `inline-block` 或 `inline-table` 时，它就是行内级元素。

- 显示时可以与其他行内级内容一起显示为多行。

- **行内盒子**

- 行内级元素会生成行内级盒子，该盒子同时会参与**行内格式化上下文（inlineformatting context）**创建。

- **匿名行内盒子**

- 类似于块盒子，CSS引擎有时候也会自动创建一些行内盒子。这些行内盒子无法被选择符选中，因此是匿名的，它们从父元素那里继承那些可继承的属性，其他属性保持默认值 `initial`。

- **行盒子**

- 行盒子**由行内格式化上下文创建**，用来显示一行文本。在块盒子内部，行盒子总是从块盒子的一边延伸到另一边（译注：即占据整个块盒子的宽度）。当有浮动元素时，行盒子会从向左浮动的元素的右边缘延伸到向右浮动的元素的左边缘。

- **run-in 盒子**（在CSS 2.1的标准中移除了）

- run-in盒子可以通过 `display:run-in`来设置，它既可以是块盒子，又可以是行内盒子，这取决于它后面的盒子的类型。

# 浮动(float)

## 普通流(normal flow)

CSS的定位机制有3种：普通流（标准流）、浮动和定位。

html语言当中另外一个相当重要的概念----------标准流！或者普通流。普通流实际上就是一个网页内标签元素正常从上到下，从左到右排列顺序的意思，比如块级元素会独占一行，行内元素会按顺序依次前后排列；按照这种大前提的布局排列之下绝对不会出现例外的情况叫做普通流布局。

## 浮动(float)

## 什么是浮动？

元素的浮动是指设置了浮动属性的元素会脱离标准普通流的控制，移动到其父元素中指定位置的过程。

在CSS中，通过float属性来定义浮动，其基本语法格式如下：

```
选择器{float:属性值;}
```

| 属性值 | 描述                 |
| ------ | -------------------- |
| left   | 元素向左浮动         |
| right  | 元素向右浮动         |
| none   | 元素不浮动（默认值） |

## 浮动详细内幕特性

1. 浮动脱离标准流，**不占位置，漂浮在后面的标准流盒子上面**，会影响标准流。浮动只有左右浮动。
2. 浮动首先创建包含块的概念（包裹）。就是说， 浮动的元素总是找离它最近的父级元素对齐。但是**不会超出内边距**的范围。 
3. 浮动的盒子需要和标准流的父级搭配使用，如果其中一个子级有浮动的，则其他子级**都需要浮动**。这样才能一行对齐显示。

```
浮动的元素排列位置，跟上一个元素（块级）有关系。如果上一个元素有浮动，则A元素顶部会和上一个元素的顶部对齐；如果上一个元素是标准流，则A元素的顶部会和上一个元素的底部对齐。
因此一个父盒子里面的子盒子，如果其中一个子级有浮动的，则其他子级都需要浮动。这样才能一行对齐显示。
浮动的目的就是为了让多个块级元素同一行上显示。

```

4. 浮动可以使元素显示模式体现为**行内块特性**。
5. 并列的盒子边框重叠的地方会变粗，可以加margin-left：-1结合浮动变细。要使用hover变色时可以用relative或z-index提升层级避免遮盖。

# 版心和布局流程

“版心”(可视区) 是指网页中主体内容所在的区域。一般在浏览器窗口中水平居中显示，常见的宽度值为960px、980px、1000px、1200px等。

## 布局流程

为了提高网页制作的效率，布局时通常需要遵守一定的布局流程，具体如下：

1、确定页面的版心（可视区）。

2、分析页面中的行模块，以及每个行模块中的列模块。

3、制作HTML结构 。

4、CSS初始化，然后开始运用盒子模型的原理，通过DIV+CSS布局来控制网页的各个模块。

## 一列固定宽度且居中

![1541727433019](C:\Users\ADMINI~1\AppData\Local\Temp\1541727433019.png)

最普通的，最为常用的结构

## 两列左窄右宽型

![1541727503478](C:\Users\ADMINI~1\AppData\Local\Temp\1541727503478.png)

比如小米    <a href="http://www.mi.com" target="_blank"> 小米官网 </a>

## 通栏平均分布型

![1541727483113](C:\Users\ADMINI~1\AppData\Local\Temp\1541727483113.png)

比如锤子    <a href="http://www.smartisan.com/" target="_blank"> 锤子官网 </a>

# 清除浮动

## 为什么要清除浮动

由于浮动元素不再占用原文档流的位置，所以它会对后面的元素排版产生影响，为了解决这些问题，此时就需要在该元素中清除浮动。

准确地说，并不是清除浮动，而是**清除浮动后造成的影响**

## 清除浮动本质

清除浮动主要为了解决父级元素因为子级浮动引起内部高度变化的问题。

## 清除浮动的方法

其实本质叫做闭合浮动更好一些, 记住，清除浮动就是把浮动的盒子圈到里面，让父盒子闭合出口和入口不让他们出来影响其他元素。

在CSS中，clear属性用于清除浮动，其基本语法格式如下：

```
选择器{clear:属性值;}

```

| 属性值 | 描述                                       |
| ------ | ------------------------------------------ |
| left   | 不允许左侧有浮动元素（清除左侧浮动的影响） |
| right  | 不允许右侧有浮动元素（清除右侧浮动的影响） |
| both   | 同时清除左右两侧浮动的影响                 |

### 额外标签法

```html
是W3C推荐的做法是通过在浮动元素末尾添加一个空的标签例如 <div style=”clear:both”></div>，或则其他标签br等亦可。

```

优点： 通俗易懂，书写方便

缺点： 添加许多无意义的标签，结构化较差。	

### 父级添加overflow属性方法

可以通过触发BFC的方式，可以实现清除浮动效果。

```css
可以给父级添加： overflow为 hidden|auto|scroll  都可以实现。

```

优点：  代码简洁

缺点：  内容增多时候容易造成不会自动换行导致内容被隐藏掉，无法显示需要溢出的元素。

[BFC神奇的背后原理](https://www.cnblogs.com/lhb25/p/inside-block-formatting-ontext.html)

### 使用after伪元素清除浮动

**:after 方式为空元素的升级版，好处是不用单独加标签了** 

使用方法：

```css
 .clearfix:after {  
     content: "";
     display: block;
     height: 0;
     clear: both;
     visibility: hidden;
}   

 .clearfix {*zoom: 1;}   /* IE6、7 专有 * ie7以下版本识别 */

```

优点： 符合闭合浮动思想  结构语义化正确

缺点： 由于IE6-7不支持:after，使用 zoom:1触发 hasLayout。

代表网站： 百度、淘宝网、网易等

注意： content:""  

### 使用before和after双伪元素清除浮动

使用方法：

```css
.clearfix:before,.clearfix:after { 
  content:"";
  display:table;  /* 这句话可以触发BFC BFC可以清除浮动 */
}
.clearfix:after {
 clear:both;
}
.clearfix {
  *zoom:1;
}

```

优点：  代码更简洁

缺点：  由于IE6-7不支持:after，使用 zoom:1触发 hasLayout。

代表网站： 小米、腾讯等

# 定位(position)

如果，说浮动， 关键在一个 “浮” 字上面， 那么 我们的定位，关键在于一个 “位” 上。

## 元素的定位属性

元素的定位属性主要包括定位模式和边偏移两部分。

1、边偏移

| 边偏移属性 | 描述                                           |
| ---------- | ---------------------------------------------- |
| top        | 顶端偏移量，定义元素相对于其父元素上边线的距离 |
| bottom     | 底部偏移量，定义元素相对于其父元素下边线的距离 |
| left       | 左侧偏移量，定义元素相对于其父元素左边线的距离 |
| right      | 右侧偏移量，定义元素相对于其父元素右边线的距离 |

也就说，以后定位要和这边偏移搭配使用了， 比如 top: 100px;  left: 30px; 等等

2、定位模式(定位的分类)

在CSS中，position属性用于定义元素的定位模式，其基本语法格式如下：

选择器{position:属性值;}

position属性的常用值

| 值       | 描述                                             |
| -------- | ------------------------------------------------ |
| static   | 自动定位（默认定位方式）                         |
| relative | 相对定位，相对于其原文档流的位置进行定位         |
| absolute | 绝对定位，相对于其上一个已经定位的父元素进行定位 |
| fixed    | 固定定位，相对于浏览器窗口进行定位               |

## 静态定位(static)

静态定位是所有元素的默认定位方式，当position属性的取值为static时，可以将元素定位于静态位置。 所谓静态位置就是各个元素在HTML文档流中默认的位置。

在静态定位状态下，无法通过边偏移属性（top、bottom、left或right）来改变元素的位置。

应用：取消定位

## 相对定位relative

相对定位是将元素相对于它在标准流中的位置进行定位，当position属性的取值为relative时，可以将元素定位于相对位置。

定位时的百分比是相对父元素宽度的百分比

注意：   

1. 相对定位最重要的一点是，它可以通过边偏移移动位置，但是原来的所占的位置，继续占有。
2. 其次，每次移动的位置，是以自己的左上角为基点移动（相对于自己来移动位置）

就是说，相对定位的盒子仍在标准流中，它后面的盒子仍以标准流方式对待它。（相对定位不脱标）

如果说浮动的主要目的是 让多个块级元素一行显示，那么定位的主要价值就是 移动位置， 让盒子到我们想要的位置上去。

## 绝对定位absolute 

如果文档可滚动，绝对定位元素会随着它滚动，因为元素最终会相对于正常流的某一部分定位。

当position属性的取值为absolute时，可以将元素的定位模式设置为绝对定位。

注意： 绝对定位最重要的一点是，它可以通过边偏移移动位置，但是它完全脱标，完全不占位置。

绝对定位是将元素依据最近的已经定位（绝对、固定或相对定位）的父元素（祖先）进行定位。 若所有父元素都没有定位，以浏览器为准对齐(document文档)。

### 子绝父相

这句话的意思是 子级是绝对定位的话， 父级要用相对定位。

子绝父相：因为子级是绝对定位，不会占有位置， 可以放到父盒子里面的任何一个地方。父盒子布局时，需要占有位置，因此父亲只能是相对定位。

## 绝对定位的盒子水平/垂直居中

普通的盒子是左右margin 改为 auto就可， 但是对于绝对定位就无效了

定位的盒子也可以水平或者垂直居中，有一个算法。

1. 首先left 50%   父盒子的一半大小
2. 然后走自己外边距负的一半值就可以了 margin-left。

## 固定定位fixed

固定定位是绝对定位的一种特殊形式，类似于 正方形是一个特殊的 矩形。它以浏览器窗口作为参照物来定义网页元素。当position属性的取值为fixed时，即可将元素的定位模式设置为固定定位。

固定定位有两点：

1. 固定定位的元素跟父亲没有任何关系，只认浏览器。
2. 固定定位完全脱标，不占有位置，不随着滚动条滚动。

ie6等低版本浏览器不支持固定定位。

## 叠放次序（z-index）

当对多个元素同时设置定位时，定位元素之间有可能会发生重叠。

在CSS中，要想调整重叠定位元素的堆叠顺序，可以对定位元素应用z-index层叠等级属性，其取值可为正整数、负整数和0。

比如：  z-index: 2;

注意：

1. z-index的默认属性值是0，取值越大，定位元素在层叠元素中越居上。
2. 如果取值相同，则根据书写顺序，后来居上。
3. 后面数字一定不能加单位。
4. 只有相对定位，绝对定位，固定定位有此属性。

## 四种定位总结

| 定位模式         | 是否脱标占有位置     | 是否可以使用边偏移 | 移动位置基准                     |
| ---------------- | -------------------- | ------------------ | -------------------------------- |
| 静态static       | 不脱标，正常模式     | 不可以             | 正常模式                         |
| 相对定位relative | 不脱标，占有位置     | 可以               | 相对自身位置移动（自恋型）       |
| 绝对定位absolute | 完全脱标，不占有位置 | 可以               | 相对于定位父级移动位置（拼爹型） |
| 固定定位fixed    | 完全脱标，不占有位置 | 可以               | 相对于浏览器移动位置（认死理型） |

## 定位模式转换

跟浮动一样， 元素添加了 绝对定位和固定定位之后， 元素模式也会发生转换， 都转换为行内块模式。

**因此 比如 行内元素 如果添加了 绝对定位或者 固定定位后 浮动后，可以不用转换模式，直接给高度和宽度就可以了。**

# 元素的显示与隐藏

在CSS中有三个显示和隐藏的单词比较常见，我们要区分开，他们分别是 display visibility 和 overflow。

## display 显示

display 设置或检索对象是否及如何显示。

display : none 隐藏对象 与它相反的是 display:block 除了转换为块级元素之外，同时还有显示元素的意思。

特点： 隐藏之后，**不再保留位置**。

## visibility 可见性

设置或检索是否显示对象。

visible : 　对象可视

hidden : 　对象隐藏

特点： 隐藏之后，继续**保留原有位置**。（停职留薪）

## overflow 溢出

检索或设置当对象的内容超过其指定高度及宽度时如何管理内容。

visible : 　不剪切内容也不添加滚动条。

auto : 　 超出自动显示滚动条，不超出不显示滚动条

hidden : 　不显示超过对象尺寸的内容，超出的部分隐藏掉

scroll : 　不管超出内容否，总是显示滚动条

# CSS是如何工作的

## 页面渲染机制

页面渲染可分为下面5个步骤：

1. 处理 `HTML`来创建 `DOM tree`；
2. 处理 `CSS`来创建 `CSSOM tree；`
3. 根据 `DOM`跟 `CSSOM`来合并 `render tree；`
4. 根据 `render tree`来布局；
5. 绘制 `render tree`。

## CSS的工作流程

从上面的页面渲染流程可以知道浏览器在解析了 `HTML`跟 `CSS`之后便开始合并渲染，简单来说就是绘制带有样式的 `HTML`规则。

`CSS`的工作流程就是把 `CSS`规则定义到 `DOM tree`上。

在 `CSS`工作的过程中有两个词值得注意的就是**重排（reflow）**跟**重绘（repaint）**。

- **重排**： `render tree`的重新构建叫**重排**。也就是当页面布局或者 `DOM`元素的几何属性发生变化时，就会发生浏览器重排。以下几种情况便会引发浏览器回流：
  - 页面渲染初始化；
  - `DOM`元素的增删；
  - `DOM`元素的位置、尺寸以及引起尺寸变化的内容改变；
  - `resize`事件发生时。
- **重绘**： `render tree`中只影响外观而不影响风格的属性改变就叫**重绘**。例如 `color`与 `background-color`的改变。

[前端性能优化 —— reflow(回流)和repaint(重绘)](https://www.cnblogs.com/zhutao/p/6551216.html)

[回流(reflow)与重绘(repaint)](https://www.cnblogs.com/dll-ft/p/5810639.html)

# 逻辑属性

 `CSS逻辑属性`的变革，从**物理概念**跳跃到了**逻辑概念**，也就是从 `top`、 `right` 、 `bottom`、 `left`更新为 `block`、 `inline`、 `start`、 `end`。由于**Flex box**跟**Grid box**是 `CSS3`的布局模式，所以自然而然会使用更加适应于新时代的语言属性。

> 2017年5月18日，W3C的 CSS工作组(CSS Working Group) 发布了 CSS逻辑属性和值(CSS Logical Properties and Values Level 1) 的首份工作草案(First Public Working Draft)。不同的书写模式(writing mode)中，可以抽取出共性的抽象概念(如开始位置，或行)，这些逻辑抽象概念需要在不同书写模式下映射到左或右、上或下等物理的概念上。一些CSS布局可能依赖这些共性的逻辑概念。该 CSS 模块给出了用于通过逻辑方式(而不是基于物理坐标、书写方向和维映射等)控制布局的逻辑属性和取值(logical properties and values)。这个模块来源于CSS21中关于逻辑属性和值的特性。

| 旧的逻辑属性   | 新的逻辑属性         |
| :------------- | :------------------- |
| margin-top     | margin-block-start   |
| margin-right   | margin-inline-end    |
| margin-bottom  | margin-block-end     |
| margin-left    | margin-inline-start  |
| border-top     | border-block-start   |
| border-right   | border-inline-end    |
| border-bottom  | border-block-end     |
| border-left    | border-inline-start  |
| padding-top    | padding-block-start  |
| padding-right  | padding-inline-end   |
| padding-bottom | padding-block-end    |
| padding-left   | padding-inline-start |
| width          | inline-size          |
| height         | block-size           |

`CSS`的定位属性变化如下：

| 旧的逻辑属性 | 新的逻辑属性       |
| :----------- | :----------------- |
| top          | inset-block-start  |
| bottom       | inset-block-end    |
| left         | inset-inline-start |
| right        | inset-inline-end   |

浮动 `float`的属性也改了。

| 旧的逻辑属性 | 新的逻辑属性        |
| :----------- | :------------------ |
| float: left  | float: inline-start |
| float: right | float: inline-end   |

文本 `text-align`的属性也改了。

| 旧的逻辑属性      | 新的逻辑属性      |
| :---------------- | :---------------- |
| text-align: left  | text-align: start |
| text-align: right | text-align: end   |

# 浏览器的试图与坐标

## 关于设备屏幕

### 像素(Pixel)

像素(pixel)是影像显示的基本单位，一个像素通常被视为影像的最小的完整取样。用来表示一幅影像的像素越多，结果更接近原始的影像。

### 分辨率(Image resolution)

分辨率越高代表影像质量越好，越能表现出更多的细节。

### 每英寸像素(PPI)

每英寸像素（英语：**P**ixels **P**er **I**nch，缩写：**PPI**），又被称为**像素密度**，是一个表示打印图像或显示器单位面积上像素数量的指数。一般用于计量电子设备屏幕的精细程度。通常情况下，每英寸像素值越高，屏幕能显示的图像也越精细。

### 视网膜显示屏(Retina Display)

视网膜显示屏(Retina Display)是一种由**苹果公司**设计和委托制造的显示屏。有研究表明，人类肉眼能够分辨的最高**PPI**是**300PPI**，所以超过**PPI**超过**300**的往往被称为**Retina显示屏**，这个概念是不对的，**Retina显示屏**指的是在人体正常使用距离下，无法用肉眼看到屏幕像素的显示屏。

### 每英寸点数(DPI)

**DPI**（英语：**D**ots **P**er **I**nch，每英寸点数）是一个量度单位，用于点阵数位影像，意思是指每一英寸长度中，取样或可显示或输出点的数目。如：打印机输出可达600DPI的分辨率，表示打印机可以在每一平方英寸的面积中可以输出**600X600＝360000**个输出点。

### 设备独立像素(DIP, DP)

设备独立像素(Device Independent Pixels，DIP，又称设备无关像素)是一种物理测量单位，基于计算机控制的坐标系统和抽象像素（虚拟像素），是定义UI布局时使用的虚拟像素单位。

### 设备像素比(DPR)

设备像素比(DPR)是设备上**物理像素**和**DIP**的比例。公式如下：

`window.devicePixelRatio = 物理像素 / dips`

### CSS像素(CSS Pixels)

**CSS像素(CSS Pixels)**是**WEB**编程中诞生的概念，用于定于浏览器中每个模型不同 `CSS`的值大小。由于**CSS像素（CSS Pixels）**是个**逻辑性**的像素，而非物理性的像素，所以1个**CSS像素**在不同设备上大小可能会有不同。但即便是如此，对于**CSS**来说，还是希望在不同设备上大小尽可能地看起来相同。

> 对于CSS设备而言，这些尺寸要么锚定(i)通过将物理单元与其物理测量关联起来，或者锚定(ii)通过将像素单元与参考像素关联起来。对于打印介质和类似的高分辨率设备，锚单元应该是标准物理单位之一（像英尺，厘米等）。对于低分辨率的设备和具有不寻常观看距离的设备，建议将锚单元作为像素大圆。对于此类设备，建议像素单元参考最接近参考像素的设备像素的整数。

以上就是**1px CSS像素**的定义。也合理的解释了为什么显示设备的物理尺寸与物理像素不同，但是同样CSS值的元素大小却相差无几了。这是因为不同设备的**px**实现的参考锚点不同。

## 视图

### 视口(viewport)

视口(viewport)代表当前可见的计算机图形区域。

#### 设置视口

1. HTML标签

   `<meta name='viewport' content=''>`

   `<meta name="viewport" content="width=device-width, initial-scale=1.0, minimum-scale=0.5, maximum-scale=2.0, user-scalable=yes">`

   | Value           | 可能值                               | 描述                                                         |
   | :-------------- | :----------------------------------- | :----------------------------------------------------------- |
   | `width`         | 一个正整数或者字符串 `device-width`  | 以pixels（像素）为单位， 定义viewport（视口）的宽度。        |
   | `height`        | 一个正整数或者字符串 `device-height` | 以pixels（像素）为单位， 定义viewport（视口）的高度。        |
   | `initial-scale` | `一个0.0` 到 `10.0之间的正数`        | 定义设备宽度（纵向模式下的设备宽度或横向模式下的设备高度）与视口大小之间的缩放比率。 |
   | `maximum-scale` | `一个0.0` 到 `10.0之间的正数`        | 定义缩放的最大值；它必须大于或等于 `minimum-scale`的值，不然会导致不确定的行为发生。 |
   | `minimum-scale` | 一个 `0.0` 到 `10.0`之间的正数       | 定义缩放的最小值；它必须小于或等于 `maximum-scale`的值，不然会导致不确定的行为发生。 |
   | `user-scalable` | 一个布尔值（ `yes`或者 `no`）        | 如果设置为 `no`，用户将不能放大或缩小网页。默认值为 `yes`。  |

2. css的伪类选择器@viewport

   语法如下：

   ```css
   @viewport {
       <group-rule-body>
   }
   ```
   
   ```css
   @viewport {
       width: device-width;
       zoom: 1.0;
       min-zoom: 0.5;
       max-zoom: 2;
       user-zoom: zoom;
   }
   ```
   
   | 属性值         | 描述                                  |
| :------------- | :------------------------------------ |
   | `min-width`    | 设置viewport的最小宽度                |
   | `max-width`    | 设置viewport的最大宽度                |
   | `width`        | 同时设置 `min-width` 和 `max-width`   |
   | `min-height`   | 设置viewport的最小高度                |
   | `max-height`   | 设置viewport的最大高度                |
   | `height`       | 同时设置 `min-height` 和 `max-height` |
   | `zoom`         | 设置初始缩放系数                      |
   | `min-zoom`     | 设置最小缩放系数                      |
   | `max-zoom`     | 设置最大缩放系数                      |
   | `user-zoom`    | 设置用户是能更改缩放系数              |
   | `orientation`  | 控制文档的方向                        |
   | `viewport-fit` | 控制非矩形显示屏上文档的显示。        |

3. VisualViewport

   Window.visualViewport

   这是一个**只读**的实验性的**web api**，目前只有**chrome 60 +**跟**Opera 47+**支持。

   属性如下：

   ```css
   {    
       height: 936, // 视觉视口高度，返回值为CSS像素值。    
       offsetLeft: 0, // 视觉视口边缘与布局视口左边的偏移量    
       offsetTop: 0, // 视觉视口边缘与布局视口顶边的偏移量    
       onresize: null, // 视觉视口大小变化时触发    
       onscroll: null, // 滚动视觉视口时触发。    
       pageLeft: 0, // 视觉视口边缘的初始化包含原点的X坐标，返回值为CSS像素值。    
       pageTop: 6680, // 视觉视口边缘的初始化包含原点的Y坐标，返回值为CSS像素值。    
       scale: 1, // 返回值为视觉视口的缩放比例   
       width: 1364, // 视觉视口宽度，返回值为CSS像素值。
   }
   ```

### 坐标系

# CSS精灵技术（sprite） 小妖精  雪碧

## 精灵技术本质

简单地说，CSS精灵是一种处理网页背景图像的方式。它将一个页面涉及到的所有零星背景图像都集中到一张大图中去，然后将大图应用于网页，这样，当用户访问该页面时，只需向服务发送一次请求，网页中的背景图像即可全部展示出来。

## 精灵技术的使用

CSS 精灵其实是将网页中的一些背景图像整合到一张大图中（精灵图），但是各个网页元素通常只需要精灵图中不同位置的某个小图，要想精确定位到精灵图中的某个小图，就需要使用CSS的background-image、background-repeat和background-position属性进行背景定位，其中最关键的是使用background-position属性精确地定位。

## 制作精灵图

```
我们精灵图的宽度取决于最宽的那个背景。 
我们可以横向摆放也可以纵向摆放，但是每个图片之间，间隔至少隔开偶数像素合适。
在我们精灵图的最低端，留一片空隙，方便我们以后添加其他精灵图。

```

结束语：   小公司，背景图片很少的情况，没有必要使用精灵技术，维护成本太高。 如果是背景图片比较多，可以建议使用精灵技术。

# Ｗeb字体

## 字体格式

不同浏览器所支持的字体格式是不一样的，我们有必要了解一下有关字体格式的知识。

1、TureType(.ttf)格式

.ttf字体是Windows和Mac的最常见的字体，是一种RAW格式，支持这种字体的浏览器有IE9+、Firefox3.5+、Chrome4+、Safari3+、Opera10+、iOS Mobile、Safari4.2+；

2、OpenType(.otf)格式

.otf字体被认为是一种原始的字体格式，其内置在TureType的基础上，支持这种字体的浏览器有Firefox3.5+、Chrome4.0+、Safari3.1+、Opera10.0+、iOS Mobile、Safari4.2+；

3、Web Open Font Format(.woff)格式

woff字体是Web字体中最佳格式，他是一个开放的TrueType/OpenType的压缩版本，同时也支持元数据包的分离，支持这种字体的浏览器有IE9+、Firefox3.5+、Chrome6+、Safari3.6+、Opera11.1+；

4、Embedded Open Type(.eot)格式

.eot字体是IE专用字体，可以从TrueType创建此格式字体，支持这种字体的浏览器有IE4+；

5、SVG(.svg)格式

.svg字体是基于SVG字体渲染的一种格式，支持这种字体的浏览器有Chrome4+、Safari3.1+、Opera10.0+、iOS Mobile Safari3.2+；

了解了上面的知识后，我们就需要为不同的浏览器准备不同格式的字体，通常我们会通过字体生成工具帮我们生成各种格式的字体，因此无需过于在意字体格式间的区别差异。

# 字体图标

图片是有诸多优点的，但是缺点很明显，比如图片不但增加了总文件的大小，还增加了很多额外的"http请求"，这都会大大降低网页的性能的。更重要的是图片不能很好的进行“缩放”，因为图片放大和缩小会失真。 

## 字体图标优点

```
可以做出跟图片一样可以做的事情,改变透明度、旋转度，等..
但是本质其实是文字，可以很随意的改变颜色、产生阴影、透明效果等等...
本身体积更小，但携带的信息并没有削减。
几乎支持所有的浏览器
移动端设备必备良药...

```

### 上传生成字体包

   当UI设计人员给我们svg文件的时候，我们需要转换成我们页面能使用的字体文件， 而且需要生成的是兼容性的适合各个浏览器的。

​    推荐网站： http://icomoon.io

**icomoon字库**

IcoMoon成立于2011年，推出的第一个自定义图标字体生成器，它允许用户选择他们所需要的图标，使它们成一字型。 内容种类繁多，非常全面，唯一的遗憾是国外服务器，打开网速较慢。

   推荐网站： http://icomoon.io

**阿里icon font字库**

http://www.iconfont.cn/

这个是阿里妈妈M2UX的一个icon font字体图标字库，包含了淘宝图标库和阿里妈妈图标库。可以使用AI制作图标上传生成。 一个字，免费，免费！！

**fontello**

[http://fontello.com/](http://fontello.com/)

在线定制你自己的icon font字体图标字库，也可以直接从GitHub下载整个图标集，该项目也是开源的。

**Font-Awesome**

[http://fortawesome.github.io/Font-Awesome/](http://fortawesome.github.io/Font-Awesome/)

这是我最喜欢的字库之一了，更新比较快。目前已经有369个图标了。

**Glyphicon Halflings**

[http://glyphicons.com/](http://glyphicons.com/)

这个字体图标可以在Bootstrap下免费使用。自带了200多个图标。

**Icons8**

[https://icons8.com/](https://icons8.com/)

提供PNG免费下载，像素大能到500PX

### 下载兼容字体包

上传完毕， 网站会给我们把UI做的svg图片转换为我们的字体格式， 然后下载下来就好了

当然，我们不需要自己专门的图标，是想网上找几个图标使用，以上2步可以直接省略了， 直接到刚才的网站上找喜欢的下载使用吧。

### 字体引入到HTML

得到压缩包之后，最后一步，是最重要的一步了， 就是字体文件已经有了，我们需要引入到我们页面中。

1. 首先把文件放入到 fonts文件夹里面。 通俗的做法

   #### 第一步：在样式里面声明字体： 告诉别人我们自己定义的字体

   ```css
   @font-face {
     font-family: 'icomoon';
     src:  url('fonts/icomoon.eot?7kkyc2');
     src:  url('fonts/icomoon.eot?7kkyc2#iefix') format('embedded-opentype'),
       url('fonts/icomoon.ttf?7kkyc2') format('truetype'),
       url('fonts/icomoon.woff?7kkyc2') format('woff'),
       url('fonts/icomoon.svg?7kkyc2#icomoon') format('svg');
     font-weight: normal;
     font-style: normal;
   }
   
   ```

   #### 第二步：给盒子使用字体

   ```css
   span {
   		font-family: "icomoon";
   	}
   
   ```

   #### 第三步：盒子里面添加结构

   ```css
   span::before {
   		 content: "\e900";
   	}
   或者  
   <span></span>  
   
   ```

   ## 追加新图标到原来库里面

   如果工作中，原来的字体图标不够用了，我们需要添加新的字体图标，但是原来的不能删除，继续使用，此时我们需要这样做

   把压缩包里面的selection.json 从新上传，然后，选中自己想要新的图标，从新下载压缩包，替换原来文件即可。

# 滑动门

## 滑动门出现的背景

为了使各种特殊形状的背景能够自适应元素中文本内容的多少，出现了CSS滑动门技术。它从新的角度构建页面，使各种特殊形状的背景能够自由拉伸滑动，以适应元素内部的文本内容，可用性更强。 最常见于各种导航栏的滑动门。

## 核心技术

核心技术就是利用CSS精灵（主要是背景位置）和盒子padding撑开宽度, 以便能适应不同字数的导航栏。

一般的经典布局都是这样的：

```html
<li>
  <a href="#">
    <span>导航栏内容</span>
  </a>
</li>

```

总结： 

1. a 设置 背景左侧，padding撑开合适宽度。    
2. span 设置背景右侧， padding撑开合适宽度 剩下由文字继续撑开宽度。
3. 之所以a包含span就是因为 整个导航都是可以点击的。

# before和after伪元素(详解)

之所以被称为伪元素，是因为他们不是真正的页面元素，html没有对应的元素，但是其所有用法和表现行为与真正的页面元素一样，可以对其使用诸如页面元素一样的css样式，表面上看上去貌似是页面的某些元素来展现，实际上是css样式展现的行为，因此被称为伪元素。是伪元素在html代码机构中的展现，可以看出伪元素的结构无法审查

**注意**

伪元素:before和:after添加的内容默认是**inline元素**；这个两个伪元素的`content`属性，表示伪元素的内容,设置:before和:after时必须设置其`content`属性，否则伪元素就不起作用。

# 过渡(CSS3)

过渡（transition)是CSS3中具有颠覆性的特征之一，我们可以在不使用 Flash 动画或 JavaScript 的情况下，当元素从一种样式变换为另一种样式时为元素添加效果。

帧动画：通过一帧一帧的画面按照固定顺序和速度播放。如电影胶片

在CSS3里使用transition可以实现补间动画（过渡效果），并且当前元素只要有“属性”发生变化时即存在两种状态(我们用A和B代指），就可以实现平滑的过渡。

语法格式:

```
transition: 要过渡的属性  花费时间  运动曲线  何时开始;
如果有多组属性变化，还是用逗号隔开。

```

| 属性                       | 描述                                         | CSS  |
| -------------------------- | -------------------------------------------- | ---- |
| transition                 | 简写属性，用于在一个属性中设置四个过渡属性。 | 3    |
| transition-property        | 规定应用过渡的 CSS 属性的名称。              | 3    |
| transition-duration        | 定义过渡效果花费的时间。默认是 0。           | 3    |
| transition-timing-function | 规定过渡效果的时间曲线。默认是 "ease"。      | 3    |
| transition-delay           | 规定过渡效果何时开始。默认是 0。             | 3    |

如果想要所有的属性都变化过渡， 写一个all 就可以

transition-duration  花费时间  单位是  秒     s    比如 0.5s    这个s单位必须写      ms 毫秒

运动曲线   默认是 ease

何时开始  默认是 0s  立马开始

运动曲线示意图：

![1498445454760](E:/Jennifer/other/notes/media/1498445454760.png)

```css
div {
			width: 200px;
			height: 100px;
			background-color: pink;
			/* transition: 要过渡的属性  花费时间  运动曲线  何时开始; */
			transition: width 0.6s ease 0s, height 0.3s ease-in 1s;
			/* transtion 过渡的意思  这句话写到div里面而不是 hover里面 */
  
			
}
div:hover {  /* 鼠标经过盒子，我们的宽度变为400 */

			width: 600px;
			height: 300px
}

transition: all 0.6s;  /* 所有属性都变化用all 就可以了  后面俩个属性可以省略 */

```

# 边框图片

border-image-source: url();默认只是填充到四个角点

border-image-slice:27px fill;指从四个方向往图形内部裁切27px放到背景的对应位置，fill指填充

border-image-width:27px;边框图片的宽度，本质是背景不会影响内容放置，一般设为原始边框宽度

border-image-outset:0px;边框延伸

border-image-repeat:repeat/round/stretch(默认);round会进行缩放

缩写：border-image: url() slice / width / outset repeat

应用：消息背景

# 2D变形(CSS3) transform

transform是CSS3中具有颠覆性的特征之一，可以实现元素的位移、旋转、倾斜、缩放，甚至支持矩阵方式，配合过渡和即将学习的动画知识，可以取代大量之前只能靠Flash才可以实现的效果。

变形转换 transform    transform  变换 变形的意思             《 transformers 变形金刚》

## 移动 translate(x, y)    

translate 移动平移的意思

![1498443715586](E:/Jennifer/other/notes/media/1498443715586.png)

```css
translate(50px,50px);

```

使用translate方法来将文字或图像在水平方向和垂直方向上分别垂直移动50像素。

可以改变元素的位置，x、y可为负值；

```
 translate(x,y)水平方向和垂直方向同时移动（也就是X轴和Y轴同时移动）
 translateX(x)仅水平方向移动（X轴移动）
 translateY(Y)仅垂直方向移动（Y轴移动）

```

```css
.box {
  width: 499.9999px;
  height: 400px;
  background: pink;
  position: absolute;
  left:50%;
  top:50%;
  transform:translate(-50%,-50%);  /* 走的自己的一半 */
}

```

 让定位的盒子水平居中

## 缩放 scale(x, y) 

![1498444645795](E:/Jennifer/other/notes/media/1498444645795.png)

```css
transform:scale(0.8,1);

```

可以对元素进行水平和垂直方向的缩放。该语句使用scale方法使该元素在水平方向上缩小了20%，垂直方向上不缩放。

```
scale(X,Y)使元素水平方向和垂直方向同时缩放（也就是X轴和Y轴同时缩放）
scaleX(x)元素仅水平方向缩放（X轴缩放）
scaleY(y)元素仅垂直方向缩放（Y轴缩放）

```

 scale()的取值默认的值为1，当值设置为0.01到0.99之间的任何值，作用使一个元素缩小；而任何大于或等于1.01的值，作用是让元素放大

## 旋转 rotate(deg) 

可以对元素进行旋转，正值为顺时针，负值为逆时针；

![1498443651293](E:/Jennifer/other/notes/media/1498443651293.png)

```css
transform:rotate(45deg);

```

 注意单位是 deg 度数  	

## 元素转换变形原点（origin）

![1498443912530](E:/Jennifer/other/notes/media/1498443912530.png)

```css
 div{transform-origin: left top;transform: rotate(45deg); }  /* 改变元素原点到左上角，然后进行顺时旋转45度 */    

```

 如果是4个角，可以用 left top这些，如果想要精确的位置， 可以用  px 像素。

```css
 div{transform-origin: 10px 10px;transform: rotate(45deg); }  /* 改变元素原点到x 为10  y 为10，然后进行顺时旋转45度 */ 

```

案例旋转

```css
div {
			width: 250px;
			height: 170px;
			border: 1px solid pink;
			margin: 200px auto;
			position: relative;

		}
		div img {
			width: 100%;
			height: 100%;
			position: absolute;
			top: 0;
			left: 0;
			transition: all 0.6s;
			transform-origin: top right;
		
		}
		div:hover img:nth-child(1) {  /* 鼠标经过div  第一张图片旋转 */
			transform: rotate(60deg);
		}
		div:hover img:nth-child(2) {  
			transform: rotate(120deg);
		}
		div:hover img:nth-child(3) {  
			transform: rotate(180deg);
		}
		div:hover img:nth-child(4) {  
			transform: rotate(240deg);
		}
		div:hover img:nth-child(5) {  
			transform: rotate(300deg);
		}
		div:hover img:nth-child(6) {  
			transform: rotate(360deg);
		}

```

## 倾斜 skew(deg, deg) 

![1498443827389](E:/Jennifer/other/notes/media/1498443827389.png)

```css
transform:skew(30deg,0deg);

```

该实例通过skew方法把元素水平方向上倾斜30度，处置方向保持不变。

可以使元素按一定的角度进行倾斜，可为负值，第二个参数不写默认为0。



# 3D变形(CSS3) transform

2d    x  y  

3d  x  y  z

 左手坐标系

伸出左手，让拇指和食指成“L”形，大拇指向右，食指向上，中指指向前方。这样我们就建立了一个左手坐标系，拇指、食指和中指分别代表X、Y、Z轴的正方向。如下图

![1498445587576](E:/Jennifer/other/notes/media/1498445587576.png)



CSS3中的3D坐标系与上述的3D坐标系是有一定区别的，相当于其绕着X轴旋转了180度，如下图

![1498459001951](E:/Jennifer/other/notes/media/1498459001951.png)

简单记住他们的坐标：

 x左边是负的，右边是正的

y 上面是负的， 下面是正的

z 里面是负的， 外面是正的

## rotateX() 

 就是沿着 x 立体旋转.

```css
img {
  transition:all 0.5s ease 0s;
}
img:hove {

  transform:rotateX(180deg);
}

```

## rotateY()

沿着y轴进行旋转

```css
img {
  transition:all 0.5s ease 0s;
}
img:hove {

  transform:rotateX(180deg);
}

```

## rotateZ()

沿着z轴进行旋转

```css
img {
  transition:all .25s ease-in 0s;
}
img:hover {
  /* transform:rotateX(180deg); */
  /* transform:rotateY(180deg); */
  /* transform:rotateZ(180deg); */
  /* transform:rotateX(45deg) rotateY(180deg) rotateZ(90deg) skew(0,10deg); */
}

```

## 透视(perspective)

电脑显示屏是一个2D平面，图像之所以具有立体感（3D效果），其实只是一种视觉呈现，通过透视可以实现此目的。

透视可以将一个2D平面，在转换的过程当中，呈现3D效果。

- 透视原理： 近大远小 。
- 浏览器透视：把近大远小的所有图像，透视在屏幕上。
- perspective：视距，表示视点距离屏幕的长短。视点，用于模拟透视效果时人眼的位置

注：并非任何情况下需要透视效果，根据开发需要进行设置。

perspective 一般作为一个属性，设置给父元素，作用于所有3D转换的子元素

理解透视距离原理：

![1498446715314](E:/Jennifer/other/notes/media/1498446715314.png)

## translateX(x)

仅水平方向移动**（X轴移动）

![1498459697576](E:/Jennifer/other/notes/media/1498459697576.png)

主要目的实现移动效果

## translateY(y)

仅垂直方向移动（Y轴移动）

![1498459770252](E:/Jennifer/other/notes/media/1498459770252.png)

## translateZ(z)

transformZ的直观表现形式就是大小变化，实质是XY平面相对于视点的远近变化（说远近就一定会说到离什么参照物远或近，在这里参照物就是perspective属性）。比如设置了perspective为200px;那么transformZ的值越接近200，就是离的越近，看上去也就越大，超过200就看不到了，因为相当于跑到后脑勺去了，我相信你正常情况下，是看不到自己的后脑勺的。

## translate3d(x,y,z)

[注意]其中，x和y可以是长度值，也可以是百分比，百分比是相对于其本身元素水平方向的宽度和垂直方向的高度和；z只能设置长度值

## backface-visibility 

backface-visibility：visible/hidden 属性定义当元素不面向屏幕时是否可见。

# 动画(CSS3) animation

动画是CSS3中具有颠覆性的特征之一，可通过设置多个节点来精确控制一个或一组动画，常用来实现复杂的动画效果。

语法格式：

```css
animation:动画名称 动画时间 运动曲线  何时开始  播放次数  是否反方向;

```

![1498461096243](E:/Jennifer/other/notes/media/1498461096243.png)

关于几个值，除了名字，动画时间，延时有严格顺序要求其它随意r

```css
@keyframes 动画名称 {
  from{ 开始位置 }  0%
  to{  结束  }  100%
}

```

```
animation-iteration-count:infinite;  无限循环播放
animation-play-state:paused;   暂停动画"

```

## 小汽车案例

```css
body {
  background: white;
}
img {
  width: 200px;
}
.car {
  animation-name: goback;
  animation-duration: 5s;
  animation-timing-function: ease;
  animation-iteration-count: infinite;
}
@keyframes goback {
  0%{}
  49%{
    transform: translateX(1000px);
  }
  55%{
    transform: translateX(1000px) rotateY(180deg);
  }
  95%{
    transform: translateX(0) rotateY(180deg);
  }
  100%{
    transform: translateX(0) rotateY(0deg);
  }
}

```

# 伸缩布局(CSS3)



# 京东项目

## 几点思考

(1). 开发工具  sublime  、fireworks（ps）、各种浏览器

(2). CSS Reset 类库,为跨浏览器兼容做准备(也可以直接运用jd网站的初始化)

```
normalize.css   只是一个很小的CSS文件，但它在默认的HTML元素样式上提供了跨浏览器的高度一致性。相比于传统的CSS reset，Normalize.css是一种现代的、为HTML5准备的优质替代方案。Normalize.css现在已经被用于Twitter Bootstrap、HTML5 Boilerplate、GOV.UK、Rdio、CSS Tricks 以及许许多多其他框架、工具和网站上。 你值得拥有。。 

- 保护有用的浏览器默认样式而不是完全去掉它们

- 一般化的样式：为大部分HTML元素提供

- 修复浏览器自身的bug并保证各浏览器的一致性

- 优化CSS可用性：用一些小技巧

- 解释代码：用注释和详细的文档来

```

(3). 低版本浏览器 单独制作一个跳转页面 

https://h5.m.jd.com/dev/3dm8aE4LDBNMkDfcCaRxLnVQ7rqo/index.html

<img src="./media/di.png" width="600" />

## 目录说明

要实现结构和样式相分离的设计思想。 根目录下有这4个文件（目录）。

| 名称   | 说明                       |
| ------ | -------------------------- |
| css    | 用于存放CSS文件            |
| images | 用于存放图片               |
| index  | 京东首页 HTML              |
| js     | 用于后期存放javascript文件 |

## 运用知识点

### 引入ico图标

```
代码：  <link rel="shortcut icon" href="favicon.ico"  type="image/x-icon"/>     
```

注意： 

1. 她(它)不是iconfont字体哦 也不是图片。
2. 位置是放到 head 标签中间。
3. 后面的type="image/x-icon"  属性可以省略。（我相信你也愿意省略。）
4. 为了兼容性，请将favicon.ico 这个图标放到根目录下。

### 转换ico图标

我们可以自己做的图片，转换为 ico图标，以便放到我们站点里面。 http://www.bitbug.net/

### logo写法

```html
<style>
  .logo a {
      text-indent: -2em;
      overflow: hidden;
  }
</style>

<div class='logo'>
  <h1>
  	<a href='#' title='京东'>京东</a>
  </h1>
</div>
```



### 网站优化三大标签

SEO是由英文Search Engine Optimization缩写而来， 中文意译为“搜索引擎优化”！SEO是指通过对网站进行站内优化、网站结构调整、网站内容建设、网站代码优化等)和站外优化，从而提高网站的关键词排名以及公司产品的曝光度。 简单的说就是，把产品做好，搜索引擎就会介绍客户来。  

 我们现在阶段主要进行站内优化。网站优化，我们应该要懂。。。

<img src="./media/san.png" />

#### 网页title 标题

title具有不可替代性，是我们的内页第一个重要标签，是搜索引擎了解网页的入口，和对网页主题归属的最佳判断点。

<img src="./media/title.png" width="500" />

建议：

首页标题：网站名（产品名）- 网站的介绍    

例如：

京东(JD.COM)-综合网购首选-正品低价、品质保障、配送及时、轻松购物！

小米商城 - 小米5s、红米Note 4、小米MIX、小米笔记本官方网站

#### Description  网站说明

对于关键词的作用明显降低，但由于很多搜索引擎，仍然大量采用网页的MATA标签中描述部分作为搜索结果的“内容摘要”。 就是简要说明我们网站的主要做什么的。
我们提倡，Description作为网站的总体业务和主题概括，多采用“我们是…”“我们提供…”“×××网作为…”“电话：010…”之类语句。

京东网：

```html
<meta name="description" content="京东JD.COM-专业的综合网上购物商城,销售家电、数码通讯、电脑、家居百货、服装服饰、母婴、图书、食品等数万个品牌优质商品.便捷、诚信的服务，为您提供愉悦的网上购物体验!" />

```

注意点：

1. 描述中出现关键词，与正文内容相关，这部分内容是给人看的，所以要写的很详细，让人感兴趣， 吸引用户点击。
2. 同样遵循简短原则，字符数含空格在内不要超过 120  个汉字。
3. 补充在 title  和 keywords  中未能充分表述的说明.
4. 用英文逗号 关键词1,关键词2

```html
<meta name="description" content="小米商城直营小米公司旗下所有产品，囊括小米手机系列小米MIX、小米Note 2，红米手机系列红米Note 4、红米4，智能硬件，配件及小米生活周边，同时提供小米客户服务及售后支持。" />

```

#### Keywords 关键字

Keywords是页面关键词，是搜索引擎关注点之一。Keywords应该限制在6～8个关键词左右，电商类网站可以多 少许。

京东网：

```html
<meta name="Keywords" content="网上购物,网上商城,手机,笔记本,电脑,MP3,CD,VCD,DV,相机,数码,配件,手表,存储卡,京东" />

```

小米网：

```html
<meta name="keywords" content="小米,小米6,红米Note4,小米MIX,小米商城" />

```

## 顶部（快捷菜单）所用知识点

| 知识点                                 | 说明                                                         |
| -------------------------------------- | ------------------------------------------------------------ |
| 通栏的盒子                             | 不用给宽度  默认为 100% &nbsp;但是加了浮动和定位的盒子需要 添加 100% |
| 盒子居中对齐                           | margin: auto;  注意必须有宽度的块级元素，文字水平居中对齐是 text-align:center; |
| 行高会继承                             | 文字性质的，比如 颜色、文字大小、字体、行高等会继承父级元素  |
| 浮动元素、固定定位，绝对定位会模式转换 | 具有行内块特性，比如一行放多个，有高度和宽度，如果没有指定宽度，则会根据内容多少撑开。 |

## logo 和搜索 header 区域所用知识点

### 网页布局稳定性

<img src="H:/01%20study/09%20%E7%BC%96%E7%A8%8B/01.html%E5%92%8Ccss(%E5%85%B1160%E5%A4%9A%E9%9B%86)/%E8%B5%84%E6%96%99/%E5%89%8D%E7%AB%AF%E5%9F%BA%E7%A1%80%E7%AC%AC%E5%85%AB%E5%A4%A9/%E7%AC%94%E8%AE%B0/media/x.png" />

### 宽度剩余法：

<img src="./media/w.png" />

| 知识点       | 说明                                                         |
| ------------ | ------------------------------------------------------------ |
| 浮动元素特性 | 1. 浮动可以让多个元素同一行显示 2. 浮动的元素是顶部对齐      |
| logo优化     | text-indent: -20000px; 隐藏文字， 背景图片                   |
| 清除浮动     | 清除浮动的目的就是为了解决父亲高度为0的问题                  |
| 鼠标样式     | cursor: pointer;           小手      cursor: move;            四角箭头     cursor: text;  插入光标     cursor: default;  小白 |
| 不允许换行   | white-space: nowrap;                                         |

## nav导航栏所用知识点

| 名称         | 说明                                                         |
| ------------ | ------------------------------------------------------------ |
| 边框底侧     | border-bottom: 2px solid #ccc;                               |
| 定位重点     | 绝对定位不占位置  相对定位占有位置                           |
| 标签语义化dl | dl也是块级元素 dt 是 定义标题  dd 是定义描述，dd是围绕这dt来描述的，也就是说，dd算是dt 的解释说明详细分解。 |
| 标题标签h    | 尽量少用h1，可以多用h2和h3等标签                             |

## 页面底部所用知识点

| 名称                   | 说明                                                         |
| ---------------------- | ------------------------------------------------------------ |
| 绝对定位的盒子居中对齐 | 盒子 left 50%  然后通过 margin 负值自己的宽度一半（固定定位也是如此） |



### 固定定位的盒子靠近版心右侧对齐

跟绝对定位的盒子居中对齐原理差不多。

left 50%   然后 margin-left  版心宽度一半。

<img src="./media/guding.png" width="500" />

typora-copy-images-to: media

## nav导航栏所用知识点

| 名称         | 说明                                                         |
| ------------ | ------------------------------------------------------------ |
| 边框底侧     | border-bottom: 2px solid #ccc;                               |
| 定位重点     | 绝对定位不占位置  相对定位占有位置                           |
| 标签语义化dl | dl也是块级元素 dt 是 定义标题  dd 是定义描述，dd是围绕这dt来描述的，也就是说，dd算是dt 的解释说明详细分解。 |
| 标题标签h    | 尽量少用h1，可以多用h2和h3等标签                             |

### 固定定位的盒子靠近版心右侧对齐

跟绝对定位的盒子居中对齐原理差不多。

left 50%   然后 margin-left  版心宽度一半。

<img src="./media/guding.png" width="500" />

## 焦点图部分所用知识点

| 名称     | 说明                                          |
| -------- | --------------------------------------------- |
| 圆角矩形 | border-radius: 左上角 右上角 右下角  左下角。 |

负值自己的宽度一半（固定定位也是如此）

## 背景半透明

1.强烈推荐：  background: rgba(r,g,b,alpha);

​     r,g,b 是红绿蓝的颜色，  alpha 是透明度的意思，取值范围是 0~1 之间。

2.了解ie低版本浏览器 半透明

`filter:Alpha(opacity=50) ；   // opacity值为0 到 100`

但是 此属性是盒子半透明，不是背景半透明哦，因为里面的内容也一起半透明了

因此，低版本的 ie6.7浏览器，我们不需要透明了，直接采用优雅降级的做法。

`background: gary;`

`background: rgba(0,0,0,.2);`

写上两句 背景， 低版本ie只执行gray， 其他浏览器执行 半透明下面这一句。

## 优雅降级和渐进增强

**渐进增强 progressive enhancement：**

针对低版本浏览器进行构建页面，保证最基本的功能，然后再针对高级浏览器进行效果、交互等改进和追加功能达到更好的用户体验。

 类似 爬山，由低出往高处爬

 <b>优雅降级 graceful degradation：</b>

一开始就构建完整的功能，然后再针对低版本浏览器进行兼容。

类似蹦极，由高处往低处下落

区别：渐进增强是向上兼容，优雅降级是向下兼容。

## 浏览器前缀

| 浏览器前缀 | 浏览器                                 |
| ---------- | -------------------------------------- |
| -webkit-   | Google Chrome, Safari, Android Browser |
| -moz-      | Firefox                                |
| -o-        | Opera                                  |
| -ms-       | Internet Explorer, Edge                |
| -khtml-    | Konqueror                              |

常用的解决H5和C3 的兼容解决文件

## 背景渐变

在线性渐变过程中，颜色沿着一条直线过渡：从左侧到右侧、从右侧到左侧、从顶部到底部、从底部到顶部或着沿任何任意轴。如果你曾使用过制作图件，比如说Photoshop，你对线性渐变并不会陌生。

兼容性问题很严重，我们这里之讲解线性渐变

语法格式： 

```css
background:-webkit-linear-gradient(渐变的起始位置， 起始颜色， 结束颜色)；
```

```css
background:-webkit-linear-gradient(渐变的起始位置， 颜色 位置， 颜色位置....)；
```



## CSS W3C 统一验证工具

CssStats 是一个在线的 CSS 代码分析工具

```
网址是：  http://www.cssstats.com/
```

如果你想要更全面的，这个神奇，你值得拥有：

W3C 统一验证工具：    http://validator.w3.org/unicorn/  ☆☆☆☆☆

因为它可以检测本地文件哦！！