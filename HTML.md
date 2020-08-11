# HTML

HTML（英文Hyper Text Markup Language的缩写）中文译为“超文本标签语言”，主要是通过HTML标签对网页中的文本、图片、声音等内容进行描述。

在上世纪80年代，“富文本”的概念在计算机领域的热门，犹如如今的“AI”和“区块链”，而TimBerners-Lee当时去设计HTML，也并非是凭空造出来，他使用了当时已有的一种语言：SGML。

SGML是一种古老的标记语言，可以追溯到1969年IBM公司所使用的技术，SGML十分复杂，严格来说，HTML是SGML中规定的一种格式，但是实际的浏览器没有任何一个是通过SGML引擎来解析HTML的。

今天的HTML仍然有SGML的不少影子，SGML留给HTML的重要的遗产：基本语法和DTD。

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

```html
<!DOCTYPE html>

<!DOCTYPE> 标签位于文档的最前面，用于向浏览器说明当前文档使用哪种 HTML 或 XHTML 标准规范，这里使用的是 html 5 的版本。
```

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

#### 自动刷新/跳转

假设要实现一个类似 PPT 自动播放的效果，你很可能会想到使用 JavaScript 定时器控制页面跳转来实现。但其实有更加简洁的实现方法，比如通过 meta 标签来实现：

<meta http-equiv="Refresh" content="5; URL=page2.html">

上面的代码会在 5s 之后自动跳转到同域下的 page2.html 页面。我们要实现 PPT 自动播放的功能，只需要在每个页面的 meta 标签内设置好下一个页面的地址即可。

另一种场景，比如每隔一分钟就需要刷新页面的大屏幕监控，也可以通过 meta 标签来实现，只需去掉后面的 URL 即可：

<meta http-equiv="Refresh" content="60">

既然这样做又方便又快捷，为什么这种用法比较少见呢？

一方面是因为不少前端工程师对 meta 标签用法缺乏深入了解，另一方面也是因为在使用它的时候，刷新和跳转操作是不可取消的，所以对刷新时间间隔或者需要手动取消的，还是推荐使用 JavaScript 定时器来实现。但是，如果你只是想实现页面的定时刷新或跳转（比如某些页面缺乏访问权限，在 x 秒后跳回首页这样的场景）可以实践下 meta 标签的用法。

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
> h1 标签因为重要，尽量少用， 一般h1 都是给logo使用。
>
> 默认情况下，HTML 会自动地在块级元素前后添加一个额外的空行，比如段落、标题元素前后。

### 段落标签-p

**块级元素**

```html
<p>  文本内容  </p>
```

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

#### 语义化标签呈现Wiki百科

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

## div span标签

div（分类**块级元素**）  span（分类**行内元素**）    

是没有语义的，是我们网页布局主要的2个容器，可用于对大的内容块设置样式属性。 

```html
<div> 这是头部 </div>    <span>今日价格</span>
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

>**_blank的安全问题和性能问题**
>
>**安全：**如果只是加上`target="_blank"`，打开新窗口后，新页面能通过`window.opener`获取到来源页面的`window`对象，即使跨域也一样。虽然跨域的页面对于这个对象的属性访问有所限制，但还是有漏网之鱼。
>
>这是某网页打开新窗口的页面控制台输出结果。可以看到`window.opener`的一些属性，某些属性的访问被拦截，是因为跨域安全策略的限制。
>
>即便如此，还是给一些操作留下可乘之机。比如修改`window.opener.location`的值，指向另外一个地址。你刚刚还是在某个网站浏览，随后打开了新窗口，结果这个新窗口神不知鬼不觉地把原来的网页地址改了。这个可以用来做什么？**钓鱼**啊！等你回到那个钓鱼页面，已经伪装成登录页，你可能就稀里糊涂把账号密码输进去了。
>
>还有一种玩法，如果你处于登录状态，有些操作可能只是发送一个`GET`请求就完事了。通过修改地址，就执行了非你本意的操作，其实就是 **CSRF 攻击**。
>
>**性能：**通过`target="_blank"`打开的新窗口，跟原来的页面窗口共用一个进程。如果这个新页面执行了一大堆性能不好的 JavaScript 代码，占用了大量系统资源，那你原来的页面也会受到池鱼之殃。
>
>**解决：**尽量不使用`target="_blank"`，如果一定要用，需要加上`rel="noopener"`或者`rel="noreferrer"`。这样新窗口的`window.openner`就是`null`了，而且会让新窗口运行在独立的进程里，不会拖累原来页面的进程。不过，有些浏览器对性能做了优化，即使不加这个属性，新窗口也会在独立进程打开。不过为了安全考虑，还是加上吧。
>
>另外，对于通过`window.open`的方式打开的新页面，可以这样做：
>
>```js
>var yourWindow = window.open();
>yourWindow.opener = null;
>yourWindow.location = "http://someurl.here";
>yourWindow.target = "_blank";
>```

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

## 特殊字符

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

```
1.table用于定义一个表格。
2.tr 用于定义表格中的一行，必须嵌套在 table /table标签中，在 table /table中包含几对 tr /tr，就有几行表格。
3.td ：用于定义表格中的单元格，必须嵌套在<tr></tr>标签中，一对 <tr> </tr>中包含几对<td></td>，就表示该行中有多少列（或多少个单元格）。
```

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
  <caption></caption>
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