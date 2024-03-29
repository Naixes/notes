# jQuery基本概念

## jQuery的优点

优点总结：

```javascript
1. 查找元素的方法多种多样，非常灵活
2. 拥有链式编程、隐式迭代等特性，因此不再需要手写for循环了。
3. 完全没有兼容性问题。
4. 实现动画非常简单，而且功能更加的强大。
5. 操作方便，体积小，插件丰富，开源，免费。
```

## 什么是jQuery?

> jQuery的官网 [http://jquery.com/](http://jquery.com/) 
> jQuery就是一个js库，使用jQuery的话，会比使用JavaScript更简单。

js库：把一些常用到的方法写到一个单独的js文件，使用的时候直接去引用这js文件就可以了。（animate.js、common.js）

我们知道了，jQuery其实就是一个js文件，里面封装了一大堆的方法方便我们的开发，其实就是一个加强版的common.js，因此我们学习jQuery，其实就是学习jQuery这个js文件中封装的一大堆方法。

## jQuery的版本

> 官网下载地址：[http://jquery.com/download/](http://jquery.com/download/)
> jQuery版本有很多，分为1.x 2.x 3.x

大版本分类：

```javascript
1.x版本：能够兼容IE678浏览器
2.x版本：不兼容IE678浏览器
1.x和2.x版本jquery都不再更新版本了，现在只更新3.x版本。

3.x版本：不兼容IE678，更加的精简（在国内不流行，因为国内使用jQuery的主要目的就是兼容IE678）
```

关于压缩版和未压缩版

```javascript
jquery-1.12.4.min.js:压缩版本，适用于生产环境，因为文件比较小，去除了注释、换行、空格等东西，但是基本没有颗阅读性。
jquery-1.12.4.js:未压缩版本，适用于学习与开发环境，源码清晰，易阅读。
```

## jQuery的中的顶级对象

jquery---$

## jQuery 的入口函数

使用jQuery的三个步骤：

```javascript
1. 引入jQuery文件
2. 入口函数
3. 功能实现
```

关于jQuery的入口函数：

```javascript
//第一种写法
$(window).load(function() {
    
});// 和DOM的onload的加载特点一样；可以有多个入口函数。

//第二种写法
$(document).ready(function() {
	
});
// 不会等待图片、文件的加载；可以有多个入口函数。
// 可以传参，第一个参数为jquery，不传为全局变量
$(function($) {
	
});// 不会等待图片、文件的加载；可以有多个入口函数。
```

jQuery入口函数与js入口函数的对比

```javascript
1.JavaScript的入口函数要等到页面中所有资源（包括图片、文件）加载完成才开始执行。
  只能有一个入口函数，以最后一个为准。
2.jQuery的入口函数只会等待文档树加载完成就开始执行，并不会等待图片、文件的加载。
  可以有多个入口函数。
```



## jQuery对象与DOM对象的区别（重点）

```javascript
1. DOM对象：使用JavaScript中的方法获取页面中的元素返回的对象就是dom对象。
2. jQuery对象：jquery对象就是使用jquery的方法获取页面中的元素返回的对象就是jQuery对象。
3. jQuery对象其实就是DOM对象的包装集（包装了DOM对象的集合（伪数组））
4. DOM对象与jQuery对象的方法不能混用。
```

DOM对象转换成jQuery对象：

```javascript
var $obj = $(domObj);
// $(document).ready(function(){});就是典型的DOM对象转jQuery对象
```

jQuery对象转换成DOM对象：

```javascript
var $li = $("li");
//第一种方法（推荐使用）
$li[0]
//第二种方法
$li.get(0)
```

# 选择器

注意：jQuery选择器返回的是jQuery对象。

jQuery选择器有很多，基本兼容了CSS1到CSS3所有的选择器，并且jQuery还添加了很多更加复杂的选择器。【查看jQuery文档】

jQuery选择器虽然很多，但是选择器之间可以相互替代。所以我们平时真正能用到的只是少数的最常用的选择器。

选择器的属性：length，选中元素的个数

## 基本选择器

| 名称    | 用法                 | 描述                     |
| ----- | ------------------ | :--------------------- |
| ID选择器 | $(“#id”);          | 获取指定ID的元素              |
| 类选择器  | $(“.class”);       | 获取同一类class的元素          |
| 标签选择器 | $(“div”);          | 获取同一类标签的所有元素           |
| 并集选择器 | $(“div,p,li”);     | 使用逗号分隔，只要符合条件之一就可。     |
| 交集选择器 | $(“div.redClass”); | 获取class为redClass的div元素 |

> 总结：跟css的选择器用法一模一样。

## 层级选择器

| 名称       | 用法        | 描述                                                        |
| ---------- | ----------- | :---------------------------------------------------------- |
| 子代选择器 | $(“ul>li”); | 使用>号，获取儿子层级的元素，注意，并不会获取孙子层级的元素 |
| 后代选择器 | $(“ul li”); | 使用空格，代表后代选择器，获取ul下的所有li元素，包括孙子等  |
| 相邻选择器 | $(“li+li”); |                                                             |
| 兄弟选择器 | $(“li~li”); |                                                             |

> 跟CSS的选择器一模一样。

## 过滤选择器

> 这类选择器都带冒号:

| 名称           | 用法                               | 描述                                                         |
| -------------- | ---------------------------------- | :----------------------------------------------------------- |
| :eq（index）   | $(“li:eq(2)”).css(“color”, ”red”); | 获取到的li元素中，选择索引号为2的元素，索引号index从0开始。  |
| :odd           | $(“li:odd”).css(“color”, ”red”);   | 获取到的li元素中，选择索引号为奇数的元素                     |
| :even          | $(“li:even”).css(“color”, ”red”);  | 获取到的li元素中，选择索引号为偶数的元素                     |
| :lt（index）   |                                    | 索引号小于index的元素，索引号index从0开始。                  |
| :gt（index）   |                                    | 索引号大于index的元素，索引号index从0开始。                  |
| :input         |                                    | 表单type为input的元素类似的还有：text、password、radio、checkbox、submit、image、reset、button、file、hidden |
| :selected      |                                    | 表单属性为selected的元素类似的还有：enabled、disabled、checked |
| :first-child   |                                    | 类似的：:first-child                                         |
| :first-of-type |                                    | 类似的：:last-of-child                                       |
| :nth-child()   |                                    | 类似的：:nth-last-child()                                    |
| :nth-of-type() |                                    | 类似的：:nth-last-of-type()                                  |
| :only-child    |                                    | 类似的：:only-of-type()                                      |
| :first         |                                    | 类似的：last                                                 |
| :contains('x') |                                    | 选择内容包含x的元素                                          |

##  筛选选择器(方法)

> 筛选选择器的功能与过滤选择器有点类似，但是用法不一样，筛选选择器主要是方法。

| 名称               | 用法                        | 描述                             |
| ------------------ | --------------------------- | :------------------------------- |
| children(selector) | $(“ul”).children(“li”)      | 相当于$(“ul>li”)，子类选择器     |
| find(selector)     | $(“ul”).find(“li”);         | 相当于$(“ul li”),后代选择器      |
| siblings(selector) | $(“#first”).siblings(“li”); | 查找兄弟节点，不包括自己本身。   |
| parent()           | $(“#first”).parent();       | 查找父亲                         |
| eq(index)          | $(“li”).eq(2);              | 相当于$(“li:eq(2)”),index从0开始 |
| next()             | $(“li”).next()              | 找下一个兄弟                     |
| prev()             | $(“li”).prev()              | 找上一次兄弟                     |
| nextAll()          |                             | 之前所有兄弟                     |
| prevAll()          |                             | 之后所有兄弟                     |

# jQuery特殊属性操作

## css方法

样式操作：设置css属性/获取属性值，获取的为字符串操作起来比较复杂一般不用css获取属性

``````javascript
// 获取属性
$("#id").css("backgroundColor")
// 设置一个属性
$("#id").css("backgroundColor", "red")
// 设置多个属性
$("#id").css("backgroundColor": "red", "width": "30px")
$("#id").css(json)
``````

### 操作类名方法

addClass(类名)：增加类名

removeClass(类名)：删除指定类名，不写类名全部删除

hasClass(类名)：是否应用了类样式

toggleClass(类名)：如果存在（不存在）就删除（添加）一个类。

## val方法

> val方法用于设置和获取表单元素的值，例如input、textarea的值

```javascript
//设置值
$("#name").val(“张三”);
//获取值
$("#name").val();
```

textarea中的值也可以用text()改变但是推荐val()

val()也可以改变下拉的某一项选中

## index方法

index()：获取索引，会返回当前元素在所有兄弟元素中的索引

## html方法与text方法

> html方法相当于innerHTML  text方法相当于innerText

```javascript
//设置内容
$(“div”).html(“<span>这是一段内容</span>”);
//获取内容
$(“div”).html()

//设置内容
$(“div”).text(“<span>这是一段内容</span>”);
//获取内容
$(“div”).text()
```

区别：html方法会识别html标签，text方法会那内容直接当成字符串，并不会识别html标签。

## width方法与height方法

> 设置或者获取高度，数字类型易于操作

```javascript
//带参数表示设置高度
$(“img”).height(200);
//不带参数获取高度
$(“img”).height();
```

获取网页的可视区宽高

```javascript
//获取可视区宽度
$(window).width();
//获取可视区高度
$(window).height();
```

## 获取宽度的四种方法

``````javascript
$(.class).width();
//获取当前匹配元素的内宽度，内宽度包括元素的padding，但是不包括border、margin部分的宽度
$(.class).innerWidth();
//设置或返回当前匹配元素的外宽度，外宽度默认包括元素的padding、border但是不包括margin部分的宽度
$(.class).outerWidth();
//设置或返回当前匹配元素的外宽度，外宽度默认包括元素的padding、border和margin的宽度
$(.class).outerWidth(true);
``````

![img](http://api.jquery.com/resources/0042_04_06.png) 

## scrollTop与scrollLeft

> 设置或者获取垂直滚动条的位置，数字类型

```javascript
//获取页面被卷曲的高度
$(window).scrollTop();
//获取页面被卷曲的宽度
$(window).scrollLeft();
```

## offset方法与position方法

> offset方法获取元素距离document的位置，position方法获取的是元素距离有定位的父元素的位置。

```javascript
//获取元素距离document的位置,返回值为对象：{left:100, top:100}
$(selector).offset();
$(selector).offset().left;// 数字类型
$(selector).offset().top;// 数字类型
//获取相对于其最近的有定位的父元素的位置。
$(selector).position();
```

## 操作属性

attr()：获取或设置属性，1.0版本，针对DOM对象，属性值只为字符串

```js
$("img").attr("src");
$("img").attr({ src: "test.jpg", alt: "Test Image" });
```

- 1.0：对于checked，selected，disabled返回布尔
- 1.6：返回字符串，否则为undefined

prop()：用法参数和attr()一样，1.6版本，针对JS对象，属性值只为任意类型

- 对于checked，selected，disabled返回布尔

## 效果

### show方法

显示隐藏的匹配元素。

**speed**:三种预定速度之一的字符串("slow","normal", or  "fast")或表示动画时长的毫秒数值(如：1000)

**easing**:(Optional) 用来指定切换效果，默认是"swing"，可用参数"linear"

**fn:**在动画完成时执行的函数，每个元素执行一次。

### hide方法

隐藏显示的元素

**speed**:三种预定速度之一的字符串("slow","normal", or  "fast")或表示动画时长的毫秒数值(如：1000)

**easing**:(Optional) 用来指定切换效果，默认是"swing"，可用参数"linear"

**fn:**在动画完成时执行的函数，每个元素执行一次。

### slideDown方法

通过高度变化（向下增大）来动态地显示所有匹配的元素，在显示完成后可选地触发一个回调函数。

**speed**:三种预定速度之一的字符串("slow","normal", or  "fast")或表示动画时长的毫秒数值(如：1000)

**easing**:(Optional) 用来指定切换效果，默认是"swing"，可用参数"linear"

**fn**在动画完成时执行的函数，每个元素执行一次。

类似方法：slideUp、slideToggle

### fadeIn方法

通过不透明度的变化来实现所有匹配元素的淡入效果，并在动画完成后可选地触发一个回调函数。

**speed**:三种预定速度之一的字符串("slow","normal", or  "fast")或表示动画时长的毫秒数值(如：1000)

**easing**:(Optional) 用来指定切换效果，默认是"swing"，可用参数"linear"

**fn**:在动画完成时执行的函数，每个元素执行一次。

类似方法：fadeOut、fadeTo（speed、opacity、easing、fn）、fadeToggle

### animate方法

用于创建自定义动画的函数。

**params**:一组包含作为动画属性和终值的样式属性和及其值的集合

**speed**:三种预定速度之一的字符串("slow","normal", or  "fast")或表示动画时长的毫秒数值(如：1000)

**easing**:要使用的擦除效果的名称(需要插件支持).默认jQuery提供"linear" 和 "swing".

**fn**:在动画完成时执行的函数，每个元素执行一次。

### stop方法

停止所有在指定元素上正在运行的动画。

如果队列中有等待执行的动画(并且clearQueue没有设为true)，他们将被马上执行

# 元素操作

## 创建元素

1. $("标签中的代码")
2. 对象.html("对象的代码")

选择器.append(创建的标签对象)：追加到最后（子元素）

- 如果参数为选择器（即页面上已经有的元素）会改变这个元素的位置

  创建的标签对象.appendTo(选择器)

选择器.prepend(创建的标签对象)：追加到前面（子元素）

选择器.after(创建的标签对象)：追加到某元素后面（兄弟元素）

选择器.before(创建的标签对象)：追加到某元素前面（兄弟元素）



案例：动态创建表格，不要大量使用字符串拼接，用数组替代

3. clone()：克隆这个元素

## 删除元素/清空内容

1. html("")：清空元素中的内容
2. empty()
3. remove()：删除这个元素

# jQuery事件机制

> JavaScript中已经学习过了事件，但是jQuery对JavaScript事件进行了封装，增加并扩展了事件处理机制。jQuery不仅提供了更加优雅的事件处理语法，而且极大的增强了事件的处理能力。

## jQuery事件发展历程(了解)

简单事件绑定>>bind事件绑定>>delegate事件绑定>>on事件绑定(推荐)

> 简单事件注册，可使用链式编程

```javascript
click(handler)			单击事件
mouseenter(handler)		鼠标进入事件
mouseleave(handler)		鼠标离开事件
```

缺点：不能同时注册多个事件

> bind方式注册事件

```javascript
//第一个参数：事件类型
//第二个参数：事件处理程序
// 不同事件绑定相同方法
$("p").bind("click mouseenter", function(){
    //事件响应方法
});
// 不同事件绑定不同方法
$("p").bind(
  {"click"： function(){
     //事件响应方法
   }，
   "mouseenter"： function(){
     //事件响应方法
   }
  }
);
```

缺点：不支持动态事件绑定

> delegate注册委托事件

```javascript
// 第一个参数：selector，要绑定事件的元素
// 第二个参数：事件类型
// 第三个参数：事件处理函数
$(".parentBox").delegate("p", "click", function(){
    //为 .parentBox下面的所有的p标签绑定事件
});
```

缺点：只能注册委托事件，因此注册事件需要记得方法太多了

> on注册事件

## on注册事件(重点)

> jQuery1.7之后，jQuery用on统一了所有事件的处理方法。
>
> 最现代的方式，兼容zepto(移动端类似jQuery的一个库)，强烈建议使用。

on注册简单事件

```javascript
// 表示给$(selector)绑定事件，并且由自己触发，不支持动态绑定。
$(selector).on( "click", function() {});
```

on注册委托事件

```javascript
// 表示给$(selector)绑定代理事件，当必须是它的内部元素span才能触发这个事件，支持动态绑定
// 委托事件先于自身事件执行
$(selector).on( "click", "span", function() {});

```

on注册事件的语法：

```javascript
// 第一个参数：events，绑定事件的名称可以是由空格分隔的多个事件（标准事件或者自定义事件）
// 第二个参数：selector, 执行事件的后代元素（可选），如果没有后代元素，那么事件将有自己执行。
// 第三个参数：data，传递给处理函数的数据，事件触发的时候通过event.data来使用（不常使用）
// 第四个参数：handler，事件处理函数
$(selector).on(events[,selector][,data],handler);

```

## 事件解绑

> unbind方式（不用）

```javascript
$(selector).unbind(); //解绑所有的事件
$(selector).unbind("click"); //解绑指定的事件
```

> undelegate方式（不用）

```javascript
$( selector ).undelegate(); //解绑所有的delegate事件
$( selector).undelegate( “click” ); //解绑所有的click事件
```

> off方式（推荐）

```javascript
// 解绑匹配元素的所有事件，包括子元素事件
$(selector).off();
// 解绑匹配元素的所有click事件
$(selector).off("click");
// 解绑子元素click事件
$(selector).off("click", "**");
```

通过委托方法给子元素绑定的事件，解绑父元素事件时子元素的相同也会被解绑

## 触发事件

```javascript
$(selector).click(); //触发 click事件
$(selector).trigger("click");
$(selector).triggerHandler("click");
```

triggerHandler()：这个特别的方法将会触发指定的事件类型上所有绑定的处理函数。但不会执行浏览器默认动作，也不会产生事件冒泡。

这个方法的行为表现与trigger类似，但有以下三个主要区别： 

1. 他不会触发浏览器默认事件。
2. 只触发jQuery对象集合中第一个元素的事件处理函数。
3. 这个方法的返回的是事件处理函数的返回值，而不是据有可链性的jQuery对象。此外，如果最开始的jQuery对象集合为空，则这个方法返回  undefined 。

## jQuery事件对象

jQuery事件对象其实就是js事件对象的一个封装，处理了兼容性。

```javascript
//screenX和screenY	对应屏幕最左上角的值
//clientX和clientY	距离页面左上角的位置（忽视滚动条）
//pageX和pageY	距离页面最顶部的左上角的位置（会计算滚动条的距离）

//event.keyCode	按下的键盘代码
//event.data	存储绑定事件时传递的附加数据

//event.stopPropagation()	阻止事件冒泡行为
//event.preventDefault()	阻止浏览器默认行为
//return false:既能阻止事件冒泡，又能阻止浏览器默认行为

//currentTarget：代码绑定事件的对象
//delegateTarget：绑定事件的对象
//target：真正触发的对象
```

# jQuery补充知识点

## 链式编程

> 通常情况下，只有设置操作才能把链式编程延续下去(返回值是当前对象)。因为获取操作(.val()、.html()、.text()等)的时候，会返回获取到的相应的值，无法返回 jQuery对象。

```javascript
end(); // 筛选选择器会改变jQuery对象的DOM对象，想要回复到上一次的状态，并且返回匹配元素之前的状态。
$("div").find("p").andSelf().addClass("border"); // 找到所有 div，以及其中的所有段落，并为它们添加两个类名。不加.andSelf()时不包括div
```

## each方法

> jQuery的隐式迭代会对所有的DOM对象设置相同的值，但是如果我们需要给每一个对象设置不同的值的时候，就需要自己进行迭代了。

作用：遍历jQuery对象集合，为每个匹配的元素执行一个函数

```javascript
// 参数一表示当前元素在所有匹配元素中的索引号
// 参数二表示当前元素（DOM对象）
$(selector).each(function(index,element){});
```

## 多库共存

> jQuery使用$作为标示符，但是如果与其他框架中的$冲突时，jQuery可以释放$符的控制权.

```javascript
var c = $.noConflict();//释放$的控制权,并且把$的能力给了c
```

# 插件

## 常用插件

> 插件：jquery不可能包含所有的功能，我们可以通过插件扩展jquery的功能。
>
> jQuery有着丰富的插件，使用这些插件能给jQuery提供一些额外的功能。

### jquery.color.js

> animate不支持颜色的渐变，但是使用了jquery.color.js后，就可以支持颜色的渐变了。

使用插件的步骤

```javascript
1. 引入jQuery文件
2. 引入插件（如果有用到css的话，需要引入css）
3. 使用插件

```

### jquery.lazyload.js

懒加载插件

### jquery.ui.js插件

jQueryUI专指由jQuery官方维护的UI方向的插件。

官方API：[http://api.jqueryui.com/category/all/](http://api.jqueryui.com/category/all/)

其他教程：[jQueryUI教程](http://www.runoob.com/jqueryui/jqueryui-tutorial.html)

基本使用:

```javascript
1.	引入jQueryUI的样式文件
2.	引入jQuery
3.	引入jQueryUI的js文件
4.	使用jQueryUI功能
```

使用jquery.ui.js实现新闻模块的案例

## 制作jquery插件

> 原理：jquery插件其实说白了就是给jquery对象增加一个新的方法，让jquery对象拥有某一个功能。

```javascript
//通过给$.fn添加方法就能够扩展jquery对象
$.fn.pluginName = function() {};
```

制作手风琴插件

# 原理

```js
(function(w, u) {
  var jQuery = function(selector, context) {
    // new $('.test')和$('.test')基本相等
    return new jQuery.fn.init(selector, context)
    
  }
  jQuery.fn = jQuery.prototype = {
    init: function(selector, context) {
      
    }
  }
  jQuery.fn.init.prototype = jQuery.fn
  // jQuery.fn.init.prototype = jQuery.fn = jQuery.protoype // 为了让fn上面有所有的方法
})(window) // 保护全局变量，加快查找速度
```

