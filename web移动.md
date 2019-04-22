# WEB移动

## 流式布局

百分比自适应布局，非固定像素，内容向两侧填充的布局

无法准确计算容器尺寸

## 视口

```html
<meta name="viewport" content="width=device-width, initial-scale=1, user-scalable=0">
```

- 视口的作用：在移动浏览器中，当页面宽度超出设备，浏览器内部虚拟的一个页面容器，将页面容器缩放到设备这么大，然后展示
- 目前大多数手机浏览器的视口（承载页面的容器）宽度都是980；
- 视口的宽度可以通过meta标签设置
- 此属性为移动端页面视口设置，当前值表示在移动端页面的宽度为设备的宽度，并且不缩放（缩放级别为1）
  - width:视口的宽度
  - initial-scale：初始化缩放
  - user-scalable:是否允许用户自行缩放（值：yes/no; 1/0）
  - minimum-scale:最小缩放，一般设置了用户不允许缩放，就没必要设置最小和最大缩放
  - maximum-scale:最大缩放

###主流的适配方案

``````html
<meta name="viewport" content="width=device-width,initial-scale=1.0,user-scalable=0">
``````

meta:vp + tab  快捷方式 

### 非主流的适配方案：

​    1.页面的真实尺寸会比在设备的上尺寸要大几倍

​    2.假设设备是iphone4 -> 320px -> 网页尺寸 640px

​    4.屏幕像素（物理像素，像素点） 设备独立像素：与设备无关的逻辑像素，代表可以通过程序控制使用的虚拟像素，是一个总体概念 （包括了CSS像素 ）

​    5.物理像素 是设备显示屏的最小可视颗粒的大小

​    6.现在有 高清显示屏  视网膜屏  retina屏

​    8.在屏幕像素比（物理像素 / 设备独立像素）高的设备  图片（非矢量）显示会模糊

​    9.提高网页的清晰度  根据屏幕的像素比 来缩放网页

​    10.但是这样的适配方案成本非常高

​    11.一般的企业开发当中使用的还是标准化设置

​    在高清显示屏当中：图片可能会失真（模糊）

参考：https://www.cnblogs.com/jingwhale/p/5741567.html

## js库

不推荐使用jquery，移动端没有IE浏览器

## reset css

由于百分比布局无法准确计算容器尺寸，padding等可能会造成溢出，所有元素和伪元素从边框计算宽度，防止内容溢出出现滚动条

``````css
*,
*::before,
*::after {
	margin:0;
	padding:0;
	box-sizing:border-box;
    -webkit-box-sizing:border-box;
}
``````

点击高亮效果的清除

``````css
*,
*::before,
*::after {
    tab-hightlight-color：transparent；
	-webkit-tab-hightlight-color：transparent；
}
``````

其他

``````css
ul, ol {
    list-style: none;
}
a {
    text-decoration: none;
}
input, textarea {
    outline: none;
    border: none;
    resize: none;
    /*清除元素外观*/
    -webkit-appearance: none;
    appearance: none;
}
``````

版心：设置最大宽度，最小宽度

## 头部搜索框

让固定定位的头部搜索框版心居中：增加子元素让它居中

百分比的计算：基于父容器的内容

双飞翼结构：左右固定宽度，中间适应。左右两边定位，中间增加父容器，父容器100%宽度，用padding固定左右两边的宽度，中间100%宽度。

二倍图解决失真：压缩背景图

`background: url('') no-repeat 0 -100px / 200px 200px`

设置精灵图公共样式：

``````css
[class^='icon_'], [class*=' icon_'] {
    background-image: '';
    background-repeat: no-repeat;
    backgrount-size: 200px 200px;
}
``````

## 轮播图

html+css

图片自适应：width设为百分比

前后都需要增加一张图片

js：使用定时器、transitioned事件、touch事件组完成

滑动前停止定时器

滑动结束后重置startX、distanceX和move标志，添加标志在结束时判断是否move过

设置定时器之前先清除定时器

## 组合样式

利用.fl，.fr，.bl，.br等基本样式进行组合

## 常用事件 

### 页面滚动事件

scroll

获取页面滚动距离：document.body.scrollTop

transitioned

### 触摸事件组 touch

**touchstart**

触摸

**touchmove**

滑动

**touchend**

离开

**touchcancel**

被迫中止滑动（来电，消息）

#### 事件对象 TouchEvent

**changedTouches **

改变后的触摸点集合             每个事件都会记录

**targetTouches**    

 当前元素的触摸点集合        离开的事件不会记录

**touches**  

页面上的触摸点集合             离开的事件不会记录

每个触摸点都会记录当前触摸点的坐标：clientXY（浏览器窗口/视口），screenXY（屏幕），pageXY（页面）

### 手势事件 Swipe

滑动事件衍生，非原生

原理：

产生滑动

超过一定距离

**swipeLeft**

左滑

**swipeRight**

右滑

**swipeUp**

上滑

**swipeDown**

下滑

### tap事件

touch事件衍生，非原生，响应速度快

移动端也有click事件，为了区分是滑动还是点击，click事件会有一定的延迟300ms

原理：

不滑动：move不调用

小于150ms：start和end之间小于150ms

​	时间使用：new Date().getTime()/Date.now()（性能更好）

### fastclick.js

提高移动端click响应速度

``````javascript
// 当dom元素加载完
document.addEventListener('DOMContentLoaded', function() {
	// 初始化方法
	FastClick.attach(document.body)
}, false)
// 正常使用click事件即可
``````

## 扩大精灵图范围

``````javascript
// 背景从内容开始平铺：
background-origin: content-box;
// 背景裁剪，默认从边框开始：
background-clip: contend-box;
``````

## 占满剩余宽/高度

1. 利用padding将已经使用的距离空出来，宽/高度为100%
2. 两栏自适应：文本环绕（浮动+BFC）

## 区域滚动

插件iScroll：

条件：一个容器装着另一个容器的结构，子容器大于父容器

1. 引入
2. new IScroll(大容器， {scrollX：false， scrollY：true}) // 初始化容器，设置滑动方向
3. 其他功能参照文档