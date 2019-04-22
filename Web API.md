# Web API

## Web API介绍

### API的概念

API（Application Programming Interface,应用程序编程接口）是一些预先定义的函数，目的是提供应用程序与开发人员基于某软件或硬件得以访问一组例程的能力，而又无需访问源码，或理解内部工作机制的细节。

- 任何开发语言都有自己的API
- API的特征输入和输出(I/O)
- API的使用方法(console.log())

### Web API的概念

浏览器提供的一套操作浏览器功能和页面元素的API(BOM和DOM)

此处的Web API特指浏览器提供的API(一组方法)，Web API在后面的课程中有其它含义


### 掌握常见的浏览器提供的API的调用方式
[MDN-Web API](https://developer.mozilla.org/zh-CN/docs/Web/API)


### JavaScript的组成

![1496912475691](media/1496912475691.png)

#### ECMAScript - JavaScript的核心 

定义了javascript的语法规范

JavaScript的核心，描述了语言的基本语法和数据类型，ECMAScript是一套标准，定义了一种语言的标准与具体实现无关

#### BOM - 浏览器对象模型

一套操作浏览器功能的API

通过BOM可以操作浏览器窗口，比如：弹出框、控制浏览器跳转、获取分辨率等

#### DOM - 文档对象模型

一套操作页面元素的API

DOM可以把HTML看做是文档树，通过DOM提供的API可以对树上的节点进行操作

文档：一个页面就是一个文档

节点：页面上所有的内容，包括：属性，标签，文本

元素：页面上所有的标签

## BOM

### BOM的概念

BOM(Browser Object Model) 是指浏览器对象模型，浏览器对象模型提供了独立于内容的、可以与浏览器窗口进行互动的对象结构。BOM由多个对象组成，其中代表浏览器窗口的Window对象是BOM的顶层对象，其他对象都是该对象的子对象。

我们在浏览器中的一些操作都可以使用BOM的方式进行编程处理，

比如：刷新浏览器、后退、前进、在浏览器中输入URL等

### BOM的顶级对象window

window是浏览器的顶级对象，当调用window下的属性和方法时，可以省略window
注意：window下一个特殊的属性 window.name

### 对话框

- alert()
- prompt()
- confirm()


### 页面加载事件

- onload

```javascript
window.onload = function () {
  // 当页面加载完成执行
  // 当页面完全加载所有内容（包括图像、脚本文件、CSS 文件等）执行
}
```

- onunload

```javascript
window.onunload = function () {
  // 当用户退出页面时执行 ie8 还有onbeforeunload事件
}
```

### 定时器

#### setTimeout()和clearTimeout()

在指定的毫秒数到达之后执行指定的函数，只执行一次

```javascript
// 创建一个定时器，1000毫秒后执行，返回定时器的标示
var timerId = setTimeout(function () {
  console.log('Hello World');
}, 1000);

// 取消定时器的执行
clearTimeout(timerId);
```

#### setInterval()和clearInterval()

定时调用的函数，可以按照给定的时间(单位毫秒)周期调用函数

```javascript
// 创建一个定时器，每隔1秒调用一次
var timerId = setInterval(function () {
  var date = new Date();
  console.log(date.toLocaleTimeString());
}, 1000);

// 取消定时器的执行
clearInterval(timerId);
```

### console对象

console.log()：在控制台输出信息。

console.dir()：可以显示一个对象所有的属性和方法。 

console.trace()：用来追踪函数的调用轨迹。 

console.dirxml()：用来显示网页的某个节点(node)所包含的html/xml代码) 。

console.assert()：用来判断一个表达式或变量是否为真，只有表达式为false时，才输出一条相应作息，并且抛出一个异常 。

console.time()和console.timeEnd()：用来显示代码的运行时间，传入计时器标志

性能分析：就是分析程序各个部分的运行时间，找出瓶颈所在，使用的方法是console.profile()和console.proileEnd(); 

console.count()：统计代码被执行的次数 ，计数器

### location对象

location对象是window对象下的一个属性，时候的时候可以省略window对象

location可以获取或者设置浏览器地址栏的URL

#### URL

统一资源定位符 (Uniform Resource Locator, URL)

- URL的组成

```
scheme://host:port/path?query#fragment
scheme:通信协议
	常用的http,ftp,maito等
host:主机
	服务器(计算机)域名系统 (DNS) 主机名或 IP 地址。
port:端口号
	整数，可选，省略时使用方案的默认端口，如http的默认端口为80。
path:路径
	由零或多个'/'符号隔开的字符串，一般用来表示主机上的一个目录或文件地址。
query:查询
	可选，用于给动态网页传递参数，可有多个参数，用'&'符号隔开，每个参数的名和值用'='符号隔开。例如：name=zs
fragment:信息片断
	字符串，锚点.
```

#### location成员

- 使用chrome的控制台查看

- 查MDN

  [MDN](https://developer.mozilla.org/zh-CN/)

- 成员

  assign(‘url’)：页面跳转，存入历史

  reload()：重新加载

  replace()：替换成指定页面，不存入历史

  hash：#以及后面的内容

  host：主机名及端口号

  hostname：主机名

  path：文件的相对路径

  port：端口号

  protocol：协议

  search：搜索内容 

  href：页面地址，可以页面跳转，存入历史

#### 案例

解析URL中的query，并返回对象的形式

```javascript
function getQuery(queryStr) {
  var query = {};
  if (queryStr.indexOf('?') > -1) {
    var index = queryStr.indexOf('?');
    queryStr = queryStr.substr(index + 1);
    var array = queryStr.split('&');
    for (var i = 0; i < array.length; i++) {
      var tmpArr = array[i].split('=');
      if (tmpArr.length === 2) {
        query[tmpArr[0]] = tmpArr[1];
      }
    }
  }
  return query;
}
console.log(getQuery(location.search));
console.log(getQuery(location.href));
```

### history对象

- back()
- forward()
- go()

### navigator对象

- userAgent

通过userAgent可以判断用户浏览器的类型

- platform

通过platform可以判断浏览器所在的系统平台类型.

## DOM

### DOM的概念

文档对象模型（Document Object Model，简称DOM），是[W3C](http://baike.baidu.com/item/W3C)组织推荐的处理可扩展标志语言的标准编程接口。在网页上，组织页面（或文档）的对象被组织在一个树形结构中，用来表示文档中对象的标准模型就称为DOM。

DOM又称为文档树模型

![1497154623955](media/1497154623955.png)

- 文档：一个网页可以称为文档
- 节点：网页中的所有内容都是节点（标签、属性、文本、注释等）
- 元素：网页中的标签
- 属性：标签的属性

### 模拟文档树结构

![1497165666684](media/1497165666684.png)

```javascript
function Element(option) {
  this.id = option.id || '';
  this.nodeName = option.nodeName || '';
  this.nodeValue = option.nodeValue || '';
  this.nodeType = 1;
  this.children = option.children || [];
}

var doc = new Element({
  nodeName: 'html'
});
var head = new Element({
  nodeName: 'head'
});
var body = new Element({
  nodeName: 'body'
})
doc.children.push(head);
doc.children.push(body);

var div = new Element({
  nodeName: 'div',
  nodeValue: 'haha',
});

var p = new Element({
  nodeName: 'p',
  nodeValue: '段落'
})
body.children.push(div);
body.children.push(p);

function getChildren(ele) {
  for(var i = 0; i < ele.children.length; i++) {
    var child = ele.children[i];
    console.log(child.nodeName);
    getChildren(child);
  }
}
getChildren(doc);
```

### DOM经常进行的操作

- 获取元素
- 动态创建元素
- 对元素进行操作(设置其属性或调用其方法)
- 事件(什么时机做相应的操作)

## 获取页面元素

获取body：document.body // 元素

获取title：document.title // 内容

获取html：document.documentElement // 元素

### 根据id获取元素

```javascript
var div = document.getElementById('main');
console.log(div);

// 获取到的数据类型 HTMLDivElement，对象都是有类型的
// HTMLDivElement <-- HTMLElement <-- Element  <-- Node  <-- EventTarget
```

注意：由于id名具有唯一性，部分浏览器支持直接使用id名访问元素，但不是标准方式，不推荐使用。

### 根据标签名获取元素

```javascript
var divs = document.getElementsByTagName('div');// 返回伪数组
for (var i = 0; i < divs.length; i++) {
  var div = divs[i];
  console.log(div);
}
```

### 根据name获取元素*

```javascript
var inputs = document.getElementsByName('hobby');
for (var i = 0; i < inputs.length; i++) {
  var input = inputs[i];
  console.log(input);
}
```

### 根据类名获取元素

```javascript
var mains = document.getElementsByClassName('main');
for (var i = 0; i < mains.length; i++) {
  var main = mains[i];
  console.log(main);
}
```

### 根据选择器获取元素

```javascript
var text = document.querySelector('#text');
console.log(text);

var boxes = document.querySelectorAll('.box');
for (var i = 0; i < boxes.length; i++) {
    var box = boxes[i];
    console.log(box);
}
```

getXXXByXXX 获取的是动态集合，querySelector获取的是静态集合。

## 事件

事件：触发-响应机制

Event接口表示在DOM中发生的任何事件，一些是用户生成的（例如鼠标或键盘事件），而其他由API生成。

### 事件三要素

- 事件源:触发(被)事件的元素
- 事件类型:事件的触发方式(例如鼠标点击或键盘点击)
- 事件处理程序:事件**触发后**要执行的代码(函数形式)

### 注册/移除事件的三种方式

```javascript
var box = document.getElementById('box');
// onclick方式只能绑定1个事件
box.onclick = function () {
  console.log('点击后执行');
};
box.onclick = null;
// ie8不支持
// 参数1：事件类型；2：事件处理函数；3：事件触发方式
// this指当前对象
box.addEventListener('click', eventCode, false);
box.removeEventListener('click', eventCode, false);
// ie8
// 参数1：on+事件类型；2：事件处理函数；
// this指window
box.attachEvent('onclick', eventCode);
box.detachEvent('onclick', eventCode);

function eventCode() {
  console.log('点击后执行');
}
```

通常我们使用 `addEventListener` 注册事件，该函数的第三个参数可以是布尔值，也可以是对象。对于布尔值 `useCapture` 参数来说，该参数默认值为 `false` 。对于对象参数来说，可以使用以下几个属性

- `capture`：布尔值，和 `useCapture` 作用一样
- `once`：布尔值，值为 `true` 表示该回调只会调用一次，调用后会移除监听
- `passive`：布尔值，表示永远不会调用 `preventDefault`

一般来说，如果我们只希望事件只触发在目标上，这时候可以使用 `stopPropagation` 来阻止事件的进一步传播。通常我们认为 `stopPropagation` 是用来阻止事件冒泡的，其实该函数也可以阻止捕获事件。`stopImmediatePropagation` 同样也能实现阻止事件，但是还能阻止该事件目标执行别的注册事件。

```js
node.addEventListener(
  'click',
  event => {
    event.stopImmediatePropagation()
    console.log('冒泡')
  },
  false
)
// 点击 node 只会执行上面的函数，该函数不会执行
node.addEventListener(
  'click',
  event => {
    console.log('捕获 ')
  },
  true
)
```

### 兼容代码

```javascript
function addEventListener(element, type, fn) {
  if (element.addEventListener) {
    element.addEventListener(type, fn, false);
  } else if (element.attachEvent){
    element.attachEvent('on' + type,fn);
  } else {
    element['on'+type] = fn;
  }
}

function removeEventListener(element, type, fn) {
  if (element.removeEventListener) {
    element.removeEventListener(type, fn, false);
  } else if (element.detachEvent) {
    element.detachEvent('on' + type, fn);
  } else {
    element['on'+type] = null;
  }
}
```

### 事件的三个阶段

1. 捕获阶段，`window` 往事件触发处传播，遇到注册的捕获事件会触发（从外向内）true
2. 当前目标阶段，传播到事件触发处时触发注册的事件
3. 冒泡阶段，从事件触发处往 `window` 传播，遇到注册的冒泡事件会触发（从里向外）false

事件对象.eventPhase属性可以查看事件触发时所处的阶段：1，2，3

冒泡和捕获不会同时发生

### 事件委托

原理：事件冒泡

使用：同时给拥有共同父元素的多个子元素绑定事件

优点：减少与dom的交互次数，节省内存，提高性能，不需要给子节点注销事件

给父元素绑定事件，由于冒泡原理，子元素会触发父元素的事件。但是父元素也会触发事件，如果不需要，可以使用事件对象中的事件源属性进行过滤

```js
window.onload = function(){
　var oUl = document.getElementById("ul1");
　oUl.onclick = function(e){
　　var e = e || window.event;
　　var target = e.target || e.srcElement;// 兼容问题：e.target，IE浏览器用event.srcElement
　　if(target.nodeName.toLowerCase() == 'li'){
　 　　// TODO
　　}
　}
}
```

子元素进行不同的操作也可以利用事件委托进行优化，结合switch

```js
window.onload = function(){
 var oBox = document.getElementById("box");
 oBox.onclick = function (ev) {
     var ev = ev || window.event;
     var target = ev.target || ev.srcElement;
     if(target.nodeName.toLocaleLowerCase() == 'input'){
         switch(target.id){
         case 'add' :
         alert('添加');
         break;
         case 'remove' :
         alert('删除');
         break;
         case 'move' :
         alert('移动');
         break;
         case 'select' :
         alert('选择');
         break;
         }
     }
  }   
}
```

新添加的子元素也是有效果的，不需要多余的dom操作

参照：https://www.cnblogs.com/liugang-vip/p/5616484.html

适合用事件委托的事件：click，mousedown，mouseup，keydown，keyup，keypress，mouseover和mouseout虽然也有事件冒泡，但是处理它们的时候需要特别的注意，因为需要经常计算它们的位置，处理起来不太容易。

不适合的：mousemove，每次都要计算它的位置，非常不好把控；focus，blur等，没用冒泡的特性，自然就不能用事件委托了。

### 事件对象的属性和方法

- type：获取事件类型

- clientX/clientY：所有浏览器都支持，窗口位置

- pageX/pageY：IE8不支持，页面位置

- target || event.srcElement：用于获取触发事件的真实元素

- currentTarget：正在触发事件处理函数的元素

- preventDefault()：取消默认行为

  ie8不存在事件对象用window.event(谷歌也支持)代替：e=window.event||e

### 阻止事件传播的方式

- 标准方式 e（事件对象）.stopPropagation();
- IE低版本 window.event.cancelBubble = true; 标准中已废弃

### 阻止默认事件

- 阻止超链接跳转，在事件中return false
- event.preventDefault() 取消默认行为
- window.event.returnValue = false // IE

### 兼容代码

```js
function preventDefa(e){ 
	if(window.event){ 
		//IE中阻止函数器默认动作的方式  
		window.event.returnValue = false;  
	}else{ 
		//阻止默认浏览器动作(W3C)  
		e.preventDefault(); 
	}  
} 

function stopBubble(e) { 
	if(e && e.stopPropagation) { //非IE 
		e.stopPropagation(); 
	} else { //IE 
		window.event.cancelBubble = true; 
	} 
} 
```

### 常用的事件

鼠标键盘事件

- onmouseup 鼠标按键放开时触发
- onmousedown 鼠标按键按下触发
- onmousemove 鼠标移动触发
- onkeyup 键盘按键抬起触发
- onkeydown 键盘按键按下触发
- onfocus 获取焦点
- onblur 失去焦点



- scroll 滚动事件

#### enter、leave、over、out 的区别

![1542079902802](C:\Users\ADMINI~1\AppData\Local\Temp\1542079902802.png)

## 属性操作

### 非表单元素的属性

href、title、id、src、className

```javascript
var link = document.getElementById('link');
console.log(link.href);
console.log(link.title);

var pic = document.getElementById('pic');
console.log(pic.src);
```

- innerHTML和innerText

  获取：innerText会拿到子元素的内文本不包括标签；

  ​	    innerHTML也会拿到子元素中的内容包括标签

```javascript
var box = document.getElementById('box');
box.innerHTML = '我是文本<p>我会生成为标签</p>';
console.log(box.innerHTML);
box.innerText = '我是文本<p>我不会生成为标签</p>';
console.log(box.innerText);
```
- innerText（低版本火狐不支持）和textContent（ie8不支持）

  获取：innerText会拿到子元素的内容不包括标签

  总结：设置文本也推荐使用innerHTML，因为没有兼容问题

- HTML转义符

```
"		&quot;
‘		&apos;
&		&amp;
<		&lt;    //less than  小于
>		&gt;   // greater than  大于
空格	   &nbsp;
©		&copy;
```

属性名中有-的属性js中改为驼峰表示

width和height属性不用加px

css中的样式是获取不到的只能获取style属性里的样式

### 表单元素属性

- value 用于大部分表单元素的内容获取(option除外)
- type 可以获取input标签的类型(输入框或复选框等)
- disabled 禁用属性
- checked 复选框选中属性
- selected 下拉菜单选中属性

属性值只有一个且和属性名相同的属性在js中的值可以写true或false

### 自定义属性操作

- getAttribute(“属性名”) 获取标签行内属性，可获取自定义属性
- setAttribute(“属性名”，“属性值”) 设置标签行内属性，可设置自定义属性
- removeAttribute(“属性名”) 移除标签行内属性，可移除自定义属性
- 与element.属性的区别: 上述三个方法用于获取任意的行内属性。

### 样式操作

- 使用style方式设置的样式显示在标签行内
```javascript
var box = document.getElementById('box');
box.style.width = '100px';
box.style.height = '100px';
box.style.backgroundColor = 'red';
```

- 注意

  通过样式属性设置宽高、位置的属性类型是字符串，需要加上px

  如果一次样式操作过多应该改用类名操作

### 类名操作

- 修改标签的className属性相当于直接修改标签的类名
```javascript
var box = document.getElementById('box');
box.className = 'clearfix';
```

- **classList属性**

  classList 属性返回元素的类名，作为 DOMTokenList 对象。

  该属性用于在元素中添加，移除及切换 CSS 类。

  classList 属性是只读的，但你可以使用 add() 和 remove() 方法修改它。

``````
document.getElementById("myDIV").classList.add("mystyle");
document.getElementById("myDIV").classList.remove("mystyle");
``````



## 创建元素的三种方式

### document.write()

```javascript
document.write('新设置的内容<p>标签也可以生成</p>');
```

页面加载完之后创建会清空页面上的所有内容

### innerHTML

```javascript
var box = document.getElementById('box');
box.innerHTML = '新内容<p>新标签</p>';
```

### document.createElement()

```javascript
var div = document.createElement('div');
document.body.appendChild(div);// 插入到最后面
```

### 性能问题

- innerHTML方法由于会对字符串进行解析，需要避免在循环内多次使用。
- 可以借助字符串或数组的方式进行替换，再设置给innerHTML
- 优化后与document.createElement性能相近

## 节点操作

在 HTML DOM （文档对象模型）中，每个部分都是节点：

- 文档本身是文档节点
- 所有 HTML 元素是元素节点
- 所有 HTML 属性是属性节点
- HTML 元素内的文本是文本节点 （包括回车符也是属于文本节点）
- 注释是注释节点

 Element 对象可以拥有类型为元素节点、文本节点、注释节点的子节点。

 NodeList 对象表示节点列表，比如 HTML 元素的子节点集合。

 元素也可以拥有属性。属性是属性节点。

 总结：元素是元素节点，是节点中的一种，但元素节点中可以包含很多的节点。

```javascript
var body = document.body;
var div = document.createElement('div');
body.appendChild(div);

var firstEle = body.children[0];
body.insertBefore(div,firstEle);// 插入子元素

body.removeChild(firstEle);// 移除子元素

var text = document.createElement('p');
body.replaceChild(text, div);// 替换子元素

div.cloneNode(true); //克隆节点，false表示只克隆标签，true表示克隆标签属性以及内容
```

### 节点属性

nodeType：1---标签，2---属性，3---文本

nodeName：标签，大写的标签名；属性，小写的属性名；文本，#text

nodeValue：标签，null；属性，属性值；文本，文本内容

### 节点获取

```javascript
var box = document.getElementById('box');
console.log(box.parentNode);// 获取父节点，最顶级为document
console.log(box.parentElement);// 获取父元素
console.log(box.childNodes);// 获取子节点，包括标签 文本
console.log(box.children);// 获取子元素
console.log(box.getAttributeNode("属性名"));// 获取属性节点
// 以下代码ie8节点表示元素，元素不支持undefined
console.log(box.nextSibling);
console.log(box.nextElementSibling);
console.log(box.previousSibling);
console.log(box.previousElementSibling);
console.log(box.firstChild);// 第一个子节点
console.log(box.firstElementChild);// 第一个子元素
console.log(box.lastChild);
console.log(box.lastElementChild);// 最后一个子元素
```

- 注意

  nextElementSibling，previousElementSibling，firstElementChild，lastElementChild有兼容性问题，IE9以后才支持

- 总结

```
节点操作，方法
	appendChild()
	insertBefore()
	removeChild()
	replaceChild()
节点层次，属性
	parentNode
	childNodes
	children
	nextSibling/previousSibling
	firstChild/lastChild
```

## 特效

### 偏移量offset

- offsetParent用于获取定位的父级元素

```javascript
var box = document.getElementById('box');
console.log(box.offsetParent);
console.log(box.offsetLeft); //脱标：自身的left和margin；未脱标：父margin至子margin
console.log(box.offsetTop);
console.log(box.offsetWidth);
console.log(box.offsetHeight);
```

![1498743216279](media/1498743216279.png)

### 客户区大小client

```javascript
var box = document.getElementById('box');
console.log(box.clientLeft); // 包含左边框宽度
console.log(box.clientTop); // 包含上边框宽度	
console.log(box.clientWidth);
console.log(box.clientHeight);
```

![1498743269100](media/1498743269100.png)

### 滚动偏移scroll

```javascript
var box = document.getElementById('box');
console.log(box.scrollLeft)
console.log(box.scrollTop)
console.log(box.scrollWidth)// 内容实际宽度，内容没有超出时是元素的宽，没有边框
console.log(box.scrollHeight)// 内容实际高度，内容没有超出时是元素的高，没有边框

// 浏览器
window.pageYOffset||document.documentElement.scrollTop||document.body.scrollTop||0// 浏览器向上滚动的距离兼容
window.pageXOffset||document.documentElement.scrollLeft||document.body.scrollLeft||0// 浏览器向左滚动的距离兼容
```

![1498743288621](media/1498743288621.png)

### 获取元素计算后的样式属性值

``````
window.getComputedStyle(ele, 伪类) // ie8不支持
ele.currentStyle // ie8

function getStylr(ele, attr) {
	return window.getComputedStyle ? window.getComputedStyle(ele, null)[attr] : ele.currentStyle[attr] // 兼容
}
``````

### 获取元素相对于视窗位置的集合getBoundingClientRect

**getBoundingClientRect()**

这个方法返回一个矩形对象，包含四个属性：left、top、right和bottom。分别表示元素各边与页面上边和左边的距离。

![1544078450154](C:\Users\ADMINI~1\AppData\Local\Temp\1544078450154.png)

 ```javascript
var box=document.getElementById('box');         // 获取元素
alert(box.getBoundingClientRect().top);         // 元素上边距离页面上边的距离
alert(box.getBoundingClientRect().right);       // 元素右边距离页面左边的距离
alert(box.getBoundingClientRect().bottom);      // 元素下边距离页面上边的距离
alert(box.getBoundingClientRect().left);        // 元素左边距离页面左边的距离
 ```

注意：IE、Firefox3+、Opera9.5、Chrome、Safari支持，在IE中，默认坐标从(2,2)开始计算

```javascript
document.documentElement.clientTop;  // 非IE为0，IE为2
document.documentElement.clientLeft; // 非IE为0，IE为2
functiongGetRect (element) {
    var rect = element.getBoundingClientRect();
    var top = document.documentElement.clientTop;
    var left= document.documentElement.clientLeft;
    return{
        top    :   rect.top - top,
        bottom :   rect.bottom - top,
        left   :   rect.left - left,
        right  :   rect.right - left
    }
}
```



## 附录

### 元素的类型 

![1497169919418](media/1497169919418.png)