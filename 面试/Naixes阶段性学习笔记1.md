## css

### css预处理器

处理特定格式源文件到目标css的处理程序。

sass，太重，老

less，轻一点

stylus

常用规范：

变量 混合(Mixin)Extend

嵌套规则

运算

函数

Namespaces & Accessors

Scope

注释

原生css也都能提供了

### css后处理器

CSS压缩 CLEAN-CSS

自动添加浏览器前缀 Autoprefixer

CSS更加美观排序 CSScomb

Rework取代Stylus 后处理器发热

前后通吃 **PostCSS**

#### postcss

css处理器

插件：

POSTCSS-CUSTOM-PROPERTIES 运行时变量

POSTCSS-SIMPLE-VARS 与SCSS一致的变量实现

POSTCSS-MIXINS 实现类似SASS的@MIXIN的功能

POSTCSS-EXTEND 实现类似SASS的继承功能

POSTCSS-IMPORT 实现类似SASS的IMPORT

CSSNext 面向未来 CSS Grace 修复过去

### cssnext

已弃用

postcss-preset-env

### js in css

原生可使用

vue3可以使用，自己写的，vite

### 原子css

代表库：Tailwind css

项目参考：

```js
// postcss.config.js
module.exports = {
  plugins: {
    'postcss-preset-env': {
      stage: 0,
      features: {
        'nesting-rules': true,
      },
    },
  },
};


// webpack.config.js
module.exports = {
  module: {
    rules: [
      {
        enforce: 'pre',
        test: /\.css$/,
        exclude: /node_modules/,
        loader: 'typed-css-modules-loader',
      },
      {
        test: /\.css$/i,
        use: [
          'style-loader',
          {
            loader: 'css-loader',
            options: {
              modules: true,
            },
          },
          'postcss-loader',
        ],
      },
    ],
  },
};

// index.js
// 不能这样引入，异步的，独立的chunk
// import('./index.css');
// css in js
import index from './index.css';
const _html = `<div  class='${index.test}'><h1>京程一灯🏮</h1></div>`;
console.log('index: ', index);
document.getElementById('app').innerHTML = _html;

// index.css
:root {
  --sinColor: black;
}
body {
  background: var(--sinColor);
}
.test {
  & h1 {
    color: yellowgreen;
  }
}
```

css-doodle，做了支持

是一个web compoments

### css in js

额外加载css会导致js的执行，css in js可以减少css的请求，但是js会多一些额外的polyfill

styled components

twin

emotion

### CSSHoudini

在现今的 Web 开发中，JavaScript 几乎占据所有版面，除了控制页面逻辑与操作 DOM 对象以外，连 CSS 都直接写在 JavaScript 里面了，就算浏览器都还沒有实现的特性，总会有人做出对应的 Polyfills，让你快速的将新 Feature 应用到 Production 环境中，更別提我们还有 Babel 等工具帮忙转译。

而 CSS 就不同了，除了制定 CSS 标准规范所需的时间外，各家浏览器的版本、实战进度差异更是 旷日持久，顶多利用 PostCSS、Sass 等工具來帮我們转译出浏览器能接受的 CSS。开发者们能操作的就是通过 JS 去控制 DOM 与 CSSOM来影响页面的变化，但是对于接下來的 Layout、Paint 与 Composite 就几乎沒有控制权了。

为了解決上述问题，为了让 CSS 的魔力不再浏览器把持，Houdini 就诞生了!
CSS Houdini 是由一群來自 Mozilla, Apple, Opera, Microsoft, HP, Intel, IBM, Adobe 与 Google 的工程 师所组成的工作小组，志在建立一系列的 API，让开发者能够介入浏览器的 CSS engine

#### Parser、Paint、Layout API 扩展CSS词法分析器

**CSS Parser API** 还没有被写入规范，所以下面的内容随时都会有变化，但是它的基本思想不会变:允许开发者自由扩展 CSS 词法分析器，引入新的结构(constructs)， 比如新的媒体规则、新的伪类、嵌套、@extends、 @apply 等等。只要新的词法分析器知道如何 解析这些新结构，CSSOM 就 不会直接忽略它们，而是把这些结构放到正确的地方。

**CSS Layout API**允许开发 者可以通过 CSS Layout API 实现自己的布局模块 (layout module)，这里 的“布局模块”指的是 display 的属性值。也就是 说，这个 API 实现以后， 开发者首次拥有了像 CSS 原生代码(比如 display:flex、 display:table)那样的布局能力。

**CSS Paint API** Layout API 非常相似。它提供了一个 registerPaint 方法，操作方式和 Worklet 相似。当想要构建一个CSS 图像的时候，开发者随时可以调用paint() 函 数，也可以使用刚刚注册好的名字。

具体的coding过程要借助Worklet

**CSS Layout API** 

`.item-list { display: layout(waterfall); } // https://www.jasondavies.com/wordcloud/`

<img src="/Users/huangsiying/data/yd/Naixes阶段性学习笔记.assets/截屏2021-05-24 下午3.39.39.png" alt="截屏2021-05-24 下午3.39.39" style="zoom:50%;" />

**Box tree API** 目的就是希望让开发者能够取得这些 fragments 的信息，至于取得后要如何使用，基本上应该会跟后 面介绍的 Parser API、Layout API 与 Paint API 有关联，当我们能取得详细的 Box Modal 信息时，要客制化 Layout Module 才更为方便。

<img src="/Users/huangsiying/data/yd/Naixes阶段性学习笔记.assets/截屏2021-05-24 下午3.44.29.png" alt="截屏2021-05-24 下午3.44.29" style="zoom:50%;" />

**CSS Paint API**

`.test { background-image: paint(circle); } `

<img src="/Users/huangsiying/data/yd/Naixes阶段性学习笔记.assets/截屏2021-05-24 下午3.47.31.png" alt="截屏2021-05-24 下午3.47.31" style="zoom:50%;" />

canvas劣势，dom元素增多，独立成层，GPU渲染变慢

#### Worklets

`xxxWorklet.addModule('xxx.js').then(...)`

( registerLayout 和 registerPaint)已经了解过了，估计现在你想知 道的是，这些代码得放在哪里呢?答案就是 worklet 脚本(工作流脚本 文件)。
 Worklets 的概念和 web worker 类似，它们允许你引入脚本文件并执 行特定的 JS 代码，这样的 JS 代码要满足两个条件:

第一，可以在渲染 流程中调用;

第二，和主线程独立。

Worklet 脚本严格控制了开发者所能执行的操作类型，这就保证了性能 Worklets 的特点就是轻量以及生命周期较短。

> 全局变量CSS

`CSS.paintWorklet.addModule('xxx.js') CSS.layoutWorklet.addModule(‘xxx.js')`

<img src="/Users/huangsiying/data/yd/Naixes阶段性学习笔记.assets/截屏2021-05-24 下午4.11.40.png" alt="截屏2021-05-24 下午4.11.40" style="zoom:30%;" />

<img src="/Users/huangsiying/data/yd/Naixes阶段性学习笔记.assets/截屏2021-05-24 下午4.12.05.png" alt="截屏2021-05-24 下午4.12.05" style="zoom:20%;" />

<img src="/Users/huangsiying/data/yd/Naixes阶段性学习笔记.assets/截屏2021-05-24 下午4.12.19.png" alt="截屏2021-05-24 下午4.12.19" style="zoom:20%;" />

#### Typed OM Object

 解决目前模型的一些问题，并实现 CSS Parsing API 和 CSS 属性与值 API 相关的特性。

<img src="/Users/huangsiying/data/yd/Naixes阶段性学习笔记.assets/截屏2021-05-24 下午4.23.03.png" alt="截屏2021-05-24 下午4.23.03" style="zoom:30%;" />

```js
el.attributeStyleMap.set('padding', CSS.px(42))
const padding = el.attributeStyleMap.get('padding')
console.log(padding.value, padding.unit)
// 42, 'px'
```

更少的bug。例如数字值总是以数字形式返回，而不是字符串。

el.style.opacity += 0.1; el.style.opacity === '0.30.1' // dragons!

算术运算和单位转换。在绝对长度单位(例如 px -> cm)之间进行转换并进行基本的数学运算。

数值范围限制和舍入。Typed OM 通过对值进行范围限制和舍入，以使其在属性的可接受范围内。

更好的性能。浏览器必须做更少的工作序列化和反序列化字符串值。现在，对于 CSS 值，引擎可以对 JS 和 C++ 使用相似的理解。Tab Akins 已经展示了一些早期的性能基准测试，与使用旧的 CSSOM 和字符串相 比，Typed OM 的运行速度快了 ~30%。这对使用 requestionAnimationFrame() 处理快速 CSS 动画可能很重 要 。crbug.com/808933 可以追踪 Blink 的更多性能演示。

错误处理。新的解析方法带来了 CSS 世界中的错误处理。

你不再需要猜测名字是骆驼还或字符串(例如：el.style.backgroundColor vs el.style['background-color'])。Typed OM 中的 CSS 属性名称始终是字符串，与 您实际在 CSS 中编写的内容一致:)

### 面向对象

注意事项:

1. 不要直接定义子节点，应把共性声明放到父类。
2. 结构和皮肤相分离。
3. 容器和内容相分离。
4. 抽象出可重用的元素，建好组件库，在组件库内寻找可用的元素组装⻚面。
5. 往你想要扩展的对象本身增加class而不是他的父节点。
6. 对象应保持独立性。
7. 避免使用ID选择器，权重太高，无法重用。
8. 避免位置相关的样式。
9. 保证选择器相同的权重。
10. 类名 简短 清晰 语义化 OOCSS的名字并不影响HTML语义化。

### 分层

> 如何控制css scoped
>
> 使用css module（将类md5）/style component（将css维护到组件里边）

SMACSS 

**BEM**，antdesign使用，名字长（cssnano）

- block -代表了更高级别的抽象或组件

- block\__element -代表.block的后代，用于形成一个完整的.block的整体。

- .block--modifier -代表.block的不同状态或不同版本。

- 修饰符使用的是_，子模块使用__符号。(不用一个-的原因是CSS单词连接)

SUIT

**ACSS**，原子css，代表库：Tailwind css

 ITCSS

### css矩阵

2D&3D矩阵应用

前者是元素2D平面的移动变换(transform)，后者则是3D变换。2D变换矩阵为3\*3;3D变换则是4*4的矩阵。 						

skew scale rotate translate 斜拉 缩放 旋转 位移

#### 2D

`transform: matrix(a,b,c,d,e,f)`，矩阵为3*3，无论是旋转还是位移，本质上都是由matrix()实现的

偏移

![transform矩阵计算](/Users/huangsiying/data/yd/Naixes阶段性学习笔记.assets/transform矩阵计算.png)

```js
matrix(sx,tan(θy),tan(θx),sy,n,m) // n:水平偏移，m:垂直偏移，sx:缩放x，sy:缩放y
// 缩放
x' = ax+cy+e = s*x+0*y+0 = s*x; 
y' = bx+dy+f = 0*x+s*y+0 = s*y;
matrix(sx, 0, 0, sy, 0, 0); 
等同于scale(sx, sy);
// 旋转
Math.cos(this.value * Math.PI / 180);
Math.sin(this.value * Math.PI / 180); 
transform: matrix(0.866025,0.500000,-0.500000,0.866025,0,0); transform:rotate(30deg);
//拉伸(skew)
matrix(1,tan(θy),tan(θx),1,0,0)
x' = x+y*tan(θx)+0 = x+y*tan(θx) 
y' = x*tan(θy)+y+0 = x*tan(θy)+y
```

旋转

<img src="/Users/huangsiying/project/00 github/notes/CSS.assets/截屏2021-05-25 下午4.03.49.png" alt="截屏2021-05-25 下午4.03.49" style="zoom:50%;" />

http://www.css88.com/tool/css3Preview/Transform-Matrix.html

#### 3D

矩阵为4*4

<img src="/Users/huangsiying/project/00 github/notes/CSS.assets/截屏2021-05-25 下午3.57.27.png" alt="截屏2021-05-25 下午3.57.27" style="zoom:50%;" />

#### 更多场景

```
// SVG 
transform="matrix(a b c d e f)"
<!--other elements> ...</g>
// Canvas 
context.transform(2,0,0,2,150,150);
// CSS3D
transform: matrix3d(sx, 0, 0, 0, 0, sy, 0, 0, 0, 0, sz, 0, 0, 0, 0, 1)
```

WebGL

矩阵在3D渲染中不可缺少，坐标变换有模型变换，视图变换，投影变换等多种。

#### 工具

参考：

http://wow.techbrood.com/fiddle/25741

matrix3d
http://ds-overdesign.com/transform/matrix3d.html 

CSS-Matrix3d：webpack转换
https://github.com/Zhangdroid/CSS-Matrix3d 

matrix
http://meyerweb.com/eric/tools/matrix/ 

tools：设计动画
http://www.f2e.name/case/css3/tools.html 

css 3d

tridiv.com

> bestofjs.org // 优秀库
>
> css揭秘 // 书

## vue

> web components，小程序底层架构用到

### 架构

- dist：

  - compile 编译时

    - 离线编译，未上线前，template -> js，运行之前

    - 在线编译，运行时编译

    `new vue({template: ""}) // 在线编译`

  - runtime 运行时，反映内存里的数据状态，有虚拟dom，被处理过的响应式数据等

  - 打包出来的

    - runtime only，无编译器
    - runtime+compile

- flow（js类型框架，Facebook已经不支持了，和ts不同，ts是语言）

- packages：

  - vue提供的，工程化使用到的东西，比如，模版打包，服务端渲染的一些东西

​	比如，模版打包，服务端渲染的一些东西

- scripts：
  - 打包规范等

- src，核心代码

  - compiler，编译代码
  - core，核心运行时
  - platforms，不同端的处理，不同平台
  - server，服务端
  - sfc，单文件组件
  - shared，

vue有一套固定的语法，编译时优化，react在运行时优化（fiber），编译时就是js优化不了

Vue打包出来的代码：

```js
// 用with绑定this，this是vue实例，因为模版分析不能准确分析出当前的this，需要单独的js解析器才行，所以需要统一绑定

with(this) {
	// 创建虚拟dom
	return _c(...)
}
```

在vue3中，离线编译和在线编译使用了不同的方案，离线编译集成了js编译器分析js，没有使用with，在线编译还是使用的with

#### **vue2编译**

缺点：使用正则匹配模版，回溯问题，性能问题，扩展问题

编译时优化：静态节点优化，分析静态节点，跳过dom diff

过程：

baseCompile

​	parse: html -> ast

​		构建数据类型

​		执行parseHTML

​			判断处理不同标签，执行回调，开始，结束（维护了一个堆栈，结束时出栈），文本，注释标签

​			正则匹配

​	optimize静态分析，优化

​		深度优先遍历标记静态节点

​	generate：ast -> 可执行代码

​		genElement，通过ast拼接字符串

​			判断静态节点

​		返回拼接的render和staticRenderFns方法（拼接成的with方法）

​	返回ast，render和staticRenderFns

vue3编译，状态机

#### **运行时核心**

components，自定义的组件，keep-alive

global-api

​	assets，extend，index（在vue上挂载一些api），minxin，use

**instance**，vue实例，生命周期，初始化，事件等

observer，数据收集与订阅，双向绑定

vdom，真实dom也存在js对象，无用属性过多

### 双向数据绑定

```js
Object.defineProperty(obj, 'a', {
	get: fn,
	set: fn

})
```

重写数据的某一个key，不能监听新增的key，可以监听数组，但是行为不符合预期，因为数组是连续内存，下标和值不是绑定的，比如删除第一项，所有的key都会改变，会重复触发渲染

vue重写数组的七种方法，监控新增数据，手动调用触发渲染

<img src="/Users/huangsiying/data/yd/Naixes阶段性学习笔记.assets/截屏2021-05-26 下午2.33.47.png" alt="截屏2021-05-26 下午2.33.47" style="zoom:50%;" />

指令（会编译成with代码），使用动态属性，**一个指令对应一个watcher（vue1）不需要diff直接定向修改，一个组件对应一个watcher（vue2）**

setter 触发消息到 Watcher watcher帮忙告诉 Directive 更新DOM，DOM中修改了数据 也会通知给 Watcher，watcher 帮忙修改数据。

Dep：收集watcher，通知watcher更新

Observer：响应式数据

Watcher：监听数据，更新数据

#### **Vue**

将所有数据挂载到vue实例上

observer

​	初始化Dep电话本（**new Dep()**）**一个数据对应一个Dep**

​	数组判断

​	非数组，walk 

​		defineReactive，defineProperty

​			**new Dep()**

​			get：通知载体（watcher电话），记录通知方法/映射关系（dep电话本），方便通知；获取页面时，即执行with返回vnode时触发；每次指令执行时触发

​			set：通知dep.notify()

compiler

​	判断节点类型

​		元素节点，解析属性，v-model属性添加input事件，input事件触发时修改数据值

​	**new Watcher()**，源码是在初始化生命周期时创建的

​		Dep.target = this // watcher，记录信息

​		this.update() // 执行render，首次渲染，触发get

​			this.get() // this.value = this.vm[this.name]，触发get，收集依赖（使用了控制反转的写法），更新时target为空不会触发依赖收集

​			更新数据this.node[this.type] = this.value

​		Dep.target = null

update流程：

​	判断没有上一个节点的vnode

​	render生成新的vnode

​	创建dom

​	有上一个节点

​	render生成新的节点

​	diff

​	定向修改

#### **vue2**

一个组件对应一个watcher，需要dom diff，需要维护一套映射关系，应用过大时内存占用过高，react没有维护这样的关系

### 批量更新

update中的queueWatcher，把所有的更新放到下一个异步任务

### keep-alive算法

缓存vnode

LRU算法，缓存最新最常用的

### vue3

flow -> ts

模块化，vue2引用时是完整的包，vue3分了单独功能的模块，使用了esmodule特性，monorepo代码管理，分包单独功能引用，使用了lerna多包管理工具，管理多个package.json -> 方便源码架构上改变，composition api

#### 数据监听

runtime阶段

vue2：Object.defineProperty --> 遍历所有的key，监听不到新增，重写每个key的值

vue3：**proxy** --> 拦截，数组的部分方法还是会多次拦截，不能拦截到内部嵌套对象

#### 模版处理解析区别

编译阶段

vue2正则匹配，贪婪匹配，造成回溯，重复计算，比如si{1}iin匹配siiin，分析功能有限，不能做更多的编译时优化

vue3状态机：ast，根据自身语法和状态机的模型写了complier，强化了模版分析的能力，能做**更多的编译时优化**

> var a = 1 + 2
>
> 分析：
>
> String var
>
> Space 
>
> String a
>
> 符号 =
>
> number 1
>
> ...
>
> 最终分割为，var， ，a，=，1，+，2，（token）
>
> 按照语法结构进行遍历，构建抽象语法树astexplorer.net

#### 文件结构

packages，功能独立

​	compiler-core，与平台无关的编译器，编译模版等

​	compiler-dom，浏览器而言的编译器

​	complier-sfc，单文件编译

​	compiler-ssr

​	**reactivity**，runtime，核心，响应式处理

​	runtime-core，与平台无关的运行时，虚拟dom，vue组件等

​	runtime-dom，浏览器的runtime，原生dom api，原生dom事件

​	runtime-test，测试

​	server-renderer，服务端渲染运行时

​	sfc-playground，在线demo

​	shared，公共

​	template-explorer，在线编译，没有with，runtime时还是有with

#### **reactivity**

reactive，返回一个被监听的数据，proxy

​	判断是否响应式只读，数组，对象

​	数组重写，收集依赖

​	嵌套数据，懒代理，使用时才会代理，不会一开始就深度递归

​	get，收集依赖track

​	set，派发通知trigger

effect，会先执行一次传递进来的函数，首次渲染render，收集依赖，数据变动就会执行，重新渲染

​	判断是否effectFn

​	返回effect函数，并执行一次

​	触发fn()，触发get()，触发track()，构建全局映射

ref，监听基本数据

computed

#### 编译阶段

vue2dom diff需要递归diff

vue3编译分析时给动态属性的根元素增加dynamicChilren: []记录动态节点，即在编译阶段收集了动态节点

block tree，_createBlock，不稳定，v-if，要单独作为一个block tree，还是需要dom diff，还有v-for的情况也是不稳定的

静态树提升

预字符串，多个静态节点会合并成一个字符串节点

事件缓存

keep-alive没变

批处理没变

#### 流程

createApp

​	创建app实例

​		判断渲染器，不同端

​		创建render

​		createAppAPI

​	重写mount方法

​		判断是否传入render和template方法

​		执行mount，传入render

​			判断是否挂载，否，创建根节点，content挂载到根节点

​			render

​				创建或者更新组件

​				代理数据

​				执行setup，返回render

​				兼容options

## vue/react ssr

参考代码：demo-collection

## react

redux基于context实现

源码学习：

- 熟悉api

- debug相关api

- 抓大放小

- 查看相关issue

- demo复现

### react16前架构

两部分

reconciler，找出变化的组件，使用递归的方式和js自身的函数调用栈，递归不好打断，如果层级很深，会一直占用主线程

renderer，通过变化的组件做dom-diff，渲染最终页面

缺点：

长任务会造成阻塞交互，会卡顿

### react16 fiber架构

解决15的长任务阻塞问题，增加了scheduler调度器模块，自己实现了组件调用栈，以链表的形式遍历fiber tree，fiber其实指一种数据结构，是一种基于浏览器的单线程调度算法

用循环代替递归

使用requestldeCallback实现分片

1. 执行异步的调度任务会在宏任务中执行，保证让用户不会失去响应，之前一直在主线程执行所有任务，造成阻塞

2. 同时对所有的更新做了一个优先级的绑定，控制哪些人物可以先进入reconciler，可以中断低优先级的更新，先执行高优先级的更新（schedular模块）

**fiber tree，双向链表结构，之前是数组结构，因为中断，恢复的性能，只要保存链表头**

<img src="/Users/huangsiying/data/yd/Naixes阶段性学习笔记.assets/截屏2021-06-01 下午6.27.18.png" alt="截屏2021-06-01 下午6.27.18" style="zoom:40%;" />

通过expirationTime的比较确定优先级，取决于任务优先级（固定的，不同优先级增加不同的偏移量）+currentTime（避免一直阻塞），小于当前时间时会立即执行

优先级相同，批处理

### react17扩展

### lanes

expirationtime的不足，在大部分时间都是够用的，但是suspence（IO）出现后，高优先级的IO任务会阻塞低优先级的cpu任务

> react的IO任务是suspence机制相关的任务，其他都是cpu任务

suspence会等待接口返回后再执行后续操作，是异步的，如果有一个高优先级的IO任务和低优先级的cpu任务，低优先级会一直等待高优先级的IO完成后执行，导致页面卡顿

使用lanes代替expirationTime，兼容expirationTime，

**优先级和批处理分离**

lane表示优先级

lanes表示批处理多个优先级

通过二进制表示，越往后优先级越大，一共31位

每发起一次更新：

react设计一个优先级

根据优先级，占用一个位置，000000000000001（高优先级的IO和低优先级的cpu，最终一起执行，expirationTime相同时才会批处理）

如果有新的更新占用剩余的位置

最终会这个lanes区间的所有更新一起处理

wiplanes表示当前处理的哪些优先级

### Scheduler

调度任务的优先级，决定哪些任务先进入Reconciler

优先级：

生命周期方法-同步

受控的用户输入-同步

交互事件-高

其他，比如数据请求-低

> 可以修改优先级，ReactDOM.unstable_runWithPriority(优先级, () => {...})

#### fiber结构

属性：

fiber tree重要属性return，child，sibling

key，标志唯一性，用来复用节点，有一些直接复用，有一些需要替换return，child，sibling属性

stateNode，对应的真实节点，shedular和reconciler阶段是可以中断，commit操作dom不能被中断并且尽可能快，所以在reconciler阶段就会将stateNode计算出来，commit时直接替换

pendingProps，本次更新的props

memoizeProps，上次的props

memoizeState，存放hooks

flags，标记更新类型，删除，新增，更改属性

lanes，https://github.com/facebook/react/pull/18796

alternate，指向上一次构建的fiber镜像

##### fiber tree

fiber节点不是按组件为单位，以元素为单位

fiber与fiber之间以链表的方式连接，方便中断

##### 调度逻辑

根据优先级**区分同步任务和异步任务**，同步任务并且处于unBatchUpdate阶段立即执行在主线程，最快渲染，直接执行performSyncWorkOnRoot（ReactDOM.render() => unBatchUpdate主线程执行，尽快渲染）

具体代码：scheduleUpdateOnFiber

> 获取优先级
>
> 判断是同步优先级（lane === SyncLane）并且处于unbatchUpdate阶段（(executionContext & LegacyUnbatchedContext) !== NoContext && (executionContext & (RenderContext | CommitContext)) === NoContext 
>
> // 已经调用过unBatchUpdate，主线程立刻执行，ReactDOM.render(）中会执行unBatchUpdate， 执行 unBatchUpdate 函数体前会 executionContext = LegacyUnbatchedContext
>
> 直接执行performSyncWorkOnRoot

异步任务走scheduler宏任务执行

具体代码：ensureRootIsScheduled（包含异步调度和中断）

> 判断是否可以复用
>
> 比如多个setState同时执行，不会多次执行，优先级相同并且时间接近，会直接复用第一个任务不会新建scheduleCallback。
>
> 第一次root.callbackNode不存在时新建newCallbackNode = scheduleCallback(...)，root.callbackNode = newCallbackNode，第二次判断root.callbackNode存在，再判断优先级是否一样，一样就直接return复用当前的root.callbackNode，优先级不一样，cancel掉重新发起一个 

计算得到 expirationTime = startTime + timeout（不同优先级时间间隔，越短优先级越大），startTime = currentTime + delay

对比 startTime 和 currentTime，将任务分为及时任务和延时任务

> startTime > currentTime - timerQueue 延时
>
> startTime < currentTime - taskQueue 及时

及时任务立刻进入调度，在宏任务中执行

> 每一批任务执行在不同的宏任务中，在MessageChannel（没有用setTimeout，不准，MessageChannel早）宏任务中执行调度逻辑，保证任务与任务之间不是连续执行，不阻塞用户交互

```js
const channel = new MessageChannel();
const port = channel.port2; channel.port1.onmessage = performWorkUntilDeadline;

requestHostCallback = function(callback) {
  scheduledHostCallback = callback;
 	if (!isMessageLoopRunning) {
    isMessageLoopRunning = true;
    // 在宏任务中执行 performWorkUntilDeadline();
    // performWorkUntilDeadline 会调度执行前面 scheduleCallback 传入的 performConcurrentWorkOnRoot.bind(null, root)
    port.postMessage(null);
    // 主线程中执行 performWorkUntilDeadline(); 
    // setTimeout(() => {
    //	进入宏任务
    // }, 0)
	}
};
```

延时任务等到currentTime >= expirationTime时进入调度，每次调度及时任务时都会执行advanceTimer判断延时任务是否到时间，从timeQueue到taskQueue

> 遍历timerQueue判断时间，从timeQueue到taskQueue
>
> performConcurrentWorkOnRoot只会执行taskQueue的任务

![截屏2021-06-02 上午8.54.48](/Users/huangsiying/data/yd/Naixes阶段性学习笔记.assets/截屏2021-06-02 上午8.54.48.png)

<img src="/Users/huangsiying/data/yd/Naixes阶段性学习笔记.assets/截屏2021-06-02 上午8.55.34.png" alt="截屏2021-06-02 上午8.54.48" style="zoom:50%;" />

### Reconciler

负责构建fiber tree，找出变化组件，标记组件变化

> react fiber 的核心原理是什么？
>
> 
>
> fiber 架构分为三个部分
>
> scheduler调度，通过任务的优先级调度任务进入后面的构建流程
>
> ​	同步任务和异步任务
>
> ​		同步任务unbatchedUpdate（ReactDom.render）
>
> ​		异步任务setState，走MessageChannel调度优先级
>
> ​			多个setState的批处理问题，lanes一致复用了同一个（react17）
>
> ​			MessageChannel和setTimeout
>
> ​			为什么不采用微任务？-微任务多了也是会卡死页面的，宏任务不会
>
> ​		异步任务能不能同步？-能，用unbatchedUpdate包裹起来unbatchedUpdate(() => {this.setState({})})
>
> reconciler协调器，构建 fiber tree 做 dom diff，给变更的 fiber 打标记，方便处理
>
> ​	构建fiber tree的流程：
>
> ​		- 从上到下，创建fiber，diff，生命周期
>
> ​		- 从下到上，创建dom元素，把effect给到根节点
>
> ​	可以被中断
>
> ​	为了让commit阶段尽量的快会做一些工作，比如标记flags（变更类型），生成effects链表，commit阶段不用重新遍历属性变化，直接处理effects链表
>
> ​	空余时间生成dom，保存起来
>
> commit（render）阶段，把变更的组件的变化渲染到页面上
>
> ​	不能被中断，因为开销大
>
> ​	三个while，渲染前中后，优先子节点执行生命周期

react每发生一次更新，比如ReactDOM.render/setState，都会从Fiber Root开始重新从上往下遍历逐一找到变化的节点。构建完成会形成一颗fiber tree，react内部会同时存在两个树

#### 双缓存结构

当前显示的称为current fiber tree，正在构建的称为workInProgress fiber tree

通过alternate属性连接，它指向workInProgress fiber，其实是上一次构建的fiber镜像（也就是current fiber tree）

如果之前没有tree就逐级创建，如果存在，会构建一个workInProgress fiber tree，可以复用current fiber tree上面没有改变的节点

> 为什么使用双缓存？（类似canvas离屏渲染优化）
>
> 
>
> 为了性能考虑，很多节点是可以复用的，这个结构也是为了复用
>
> 一个属性就可以拿到和它对应的节点
>
> 某些情况下复用结构
>
> 更新完毕后current直接指向workInProgress root 完成更新

#### 构建fiber tree

代码大致从**renderLoopSync()**开始，从优先级最高的fiber root开始递归

深度优先，只处理了子节点（从上到下）

**workInProgress**，当前处理的节点，是一个闭包

**beginWork()**创建一个fiber，赋值给workInProgress.child并返回，赋值给next，workInProgres = next

循环到workInProgres === null，执行completeUnitOfWork方法

**completeUnitOfWork()**，判断是否有兄弟节点，有赋值给workInProgres，继续beginWork，没有workInProgres返回到父节点（从下向上），继续循环

##### beginWork

fiber类型很多，每个类型都有不同的方法进行构建

Fragment，Partial，Function，Class，memo...

**生命周期在beginWork中执行**，render及render之前的所有生命周期

1. 创建或者复用fiber

   current !== null，不是初次构建，判断props或context是否改变，设置didReceiveUpdate标志组件是否需要更新，否可以复用bailout

2. 对比节点是否需要更新

   根据不同的tag生成不同的fiber节点

   都会进入reconcilerChildren方法

   mount阶段，创建fiber节点

   update阶段，对比fiber节点生成新的fiber节点

   ​	单节点diff

   ​	多节点diff

3. 打标记flags

   给变更的节点打标记，便于后面处理

4. 返回子节点fiber

   赋值给workInProgress.child并返回，继续下一次循环

###### diff算法

预设规则：

同级节点进行比较

节点变化，直接删掉，然后重建

存在key值，对比节点的key值

**单节点diff：**

reconcilerSingleChild

对比key，不一致标记删除

对比节点类型，都一致可以复用，不一致会删除

复用时ref，return，sibling需要重新生成绑定

不存在对应节点，新建

**多节点diff：**

数组reconcilerChildrenArray

对比新旧children相同index对象的key是否相等，相等返回对象，否则null

key不等不用继续对比，不能复用，跳出

判断节点是否移动，返回新位置

新数组小与老数组，删除

新数组新增，创建

创建一个existingChildren代表剩余没有匹配的节点，新的数组根据key从map中查找，有就复用，没有新建

##### completeUnitOfWork

向上递归completeWork

创建dom节点，更新dom节点，dom节点赋值给stateNode属性

把子节点的side effect附加到父节点的sideEffect链上，commit阶段使用

存在兄弟节点，将workInProgress指向它，执行beginWork

不存在兄弟，返回父节点，执行beginWork

> 学到了什么？
>
> 
>
> react-reconciler，react将reconciler封装成的独立的子模块，taro使用
>
> react的日常使用
>
> fiber的架构思想
>
> 
>
> 新特性？
>
> 
>
> hooks

### commit阶段

负责将变化的组件渲染到页面上

优先级最高，不能打断

三个阶段：三个while循环，递归节点分别执行节点的生命周期，都是先执行的子节点的生命周期，再执行父节点的

三个阶段都是先执行的子节点的生命周期，再执行父节点的

**commitBeforeMutationEffects（dom操作前）**

1. 处理dom节点渲染删除后的autofocus，blur逻辑
2. 调用getSnapshotBeforeUpdate生命周期
3. 调度useEffect，**异步**，不会阻塞，useEffect => componentDidMount + componentDidUpdate，useLayoutEffect是同步的

**commitMutationEffects（dom操作）**

1. 遍历finishWork，执行dom操作
2. 对于删除的组件，执行componentWillUnmount生命周期

**recursivelyCommitLayoutEffects（dom操作后）**

1. layout阶段也是深度优先遍历Effectlist调用生命周期，componentDidMount/componentDidUpdate，执行useEffect函数体
2. 赋值ref
3. 处理ReactDom.render回调

> componentWillMount，在beginWork中执行，由于从上往下构建的，所以render之前的生命周期是先执行的父节点的后执行的子节点的

### Hooks

**作用**

class components + 生命周期 - 逻辑被生命周期分散，不符合单一指责原则，导致代码量大，不好维护，需要拆分

functional components - 代码少，无状态，一般用于UI

functional components + hooks - 有状态（useState），模拟生命周期（useEffect异步/useLayoutEffect同步，指责单一，逻辑更加清晰简洁，代码量小于class components，mount阶段调用），使用context，功能完善，不止UI，复用简单（自定义hooks，class使用高阶组件）

> 自定义hooks，使用了hooks的函数
>
> fc在beginWork时执行，相当于render生命周期，setState的初始值只在第一次有用
>
> **useEffect异步，更新了DOM，页面渲染之后执行，此时更新Dom只会回流两次**
>
> **useLayoutEffect同步，传[]完全等价于didMount，更新了DOM，页面渲染之前（因为此时主线程还没有释放），此时更新Dom只会回流一次，会阻塞，看场景**
>
> 模拟生命周期，模拟DidMount，DidUpdate，Unmount（返回函数的函数体）

**常见的坑**

1. 只能定义在顶层，不能放在代码块中，因为是hooks是通过链表连接起来的，顺序查找，放到逻辑分支中会造成混乱

> 手动绑定的事件，回调函数必须挂在this上，卸载时要传同一个

2. 缓存解决子组件无效渲染

useCallback，每次state更新都会导致函数都会产生一个新函数，如果是传递给子组件的，还会导致子组件更新，所以需要缓存

useMemo，适用对象，数组

useCallback/useMemo + React.memo，React.memo包裹fc，浅比较相当于PureComponent

3. capture value问题，异步用到的state值会是老值，如果期间值存在变化的话，原因是闭包，useRef可以解决

useRef，在fc中使用ref

#### 更新流程

ReactDom.render：

upbatchUpdate()优先级高，直接同步运行 - updateContainer - scheduleUpdateOnFiber（schedule流程，判断同步等） - 同步处理

this.setState/hooks setState：

dispatchUserBlockingUpdate - dispatchEvent - scheduleUpdateOnFiber

#### useState

两个阶段：mount，update

**mount阶段**

mountState：

默认值是fn时执行fn得到初始值

创建一个hook对象，链表结构，state放在memoizedState属性

新建一个queue

新建dispatch，把queue和当前fiber传给dispatchAction

返回默认值和dispatch

> hook对象，memoizedState，存放值（fiber中也有，指hook），baseState，存放值，可变，baseQueue，queue，next，下一个hook 
>
> queue对象，pending（所有的更新update链表），dispatch参数2，lastRenderedReducer，lastRenderedState
>
> dispatch，给dispatchAction传queue和当前fiber生成新的函数

**update阶段**

dispatch：（dispatchAction）

创建一个update，属性lane，action（用户传入的），eagerReducer，eagerState（eagerxxx优化，空闲时使用），next

update添加到queue.pending

空闲状态时计算出最新的state，保存在eagerState

最后调用一次scheduleUpdateOnFiber，进入调度，触发function重新执行

updateState：（updateReducer的一种特殊情况）

找到对应的hook

递归计算queue中的update

计算最新的state，赋值给memoizedState，dispatchAction还是之前的

> 多次setState会多次更新，暂时没有默认做批处理，放在setTimeout可以让他变成一次更新（相当于让这几个dispatch跳出了原本的context）或者使用unstable_batchedUpdate方法（react-dom提供），class components会合并更新

#### useEffect

**MountEffect**，在beginWork里调用函数组件的时候执行，回调在commit阶段执行或进入调度

参数create和deps，**杜绝不写依赖数组**，每个state变动都会更新

创建一个hook

打上flags标记，按位与或适用于多种flags标记，不打标记不会执行

push一个effect

> effect
>
> {
>
> ​	tag,
>
> ​	create,
>
> ​	destory,
>
> ​	deps,
>
> ​	next
>
> }

**UpdateEffect**，和mount阶段类似

给destroy赋值

对比依赖的值，有变化重新发起一个effect，在commit阶段执行

打上flags标记

push一个effect

> useEffect回调的执行时机：（commit阶段）
>
> 在LayoutEffect里调用commitHookEffectListMount方法，执行了create返回给destory
>
> commitHookEffectListUnMount里执行destory

<img src="/Users/huangsiying/data/yd/Naixes阶段性学习笔记.assets/截屏2021-06-04 下午5.00.19.png" alt="截屏2021-06-04 下午5.00.19" style="zoom:50%;" />

#### useRef

创建ref，value = initialValue

把ref赋值给hook.memoizedState

#### 面试题

setState后面发生了什么？

- 在哪里调用的，onClick或生命周期
  - 标记优先级
  - 进入调度流程
    - scheduler流程...reconciler流程...commit流程
- hooks里
  - 创建一个update，添加到queue.pending，最后调用scheduleUpdateOnFiber，进入schedule调度，触发function重新执行
    - scheduler流程...reconciler流程...commit流程

生命周期里的unsafe？

- 16之后reconciler阶段是可以被更高优先级中断的可能会反复执行的生命周期加上了unsafe
- DidMount不会因为是commit阶段

useEffect什么时候执行？与didMount的区别？

- 异步调度，在页面渲染完之后才会执行
- useLayoutEffect == didMount，同步执行

useCallback和useMemo区别？

- 缓存函数/引用类型数据
- useCallback+React.memo做浅比较，避免无意义渲染子组件

capture value原理？

- 闭包，变量一直在内存中
- 通过useRef解决

dom diff原理？

虚拟dom？

- dom操作昂贵
- 虚拟dom可以只更新一次，fiber tree，双缓存结构，current tree和真实dom一一对应

怎么在setState后执行回调？

- this.setState({}, () => {})，更改到页面之后执行回调，hook不行，setState + useEffect相当于didMount

生命周期执行顺序？

useEffect和useLayoutEffect区别？

React处理异常？

- ErrorBundary

实现自定义hook？

```js
// mount阶段执行
function useMount(cb) {
  useEffect(() => {
    cb()
  }, [])
}
```

useEffect死循环？

- 逻辑上循环依赖
- useRef，减少依赖

this.setState是同步还是异步？

setState本身并不是一个异步方法，其之所以会表现出一种异步的形式，是因为react框架本身的一个性能优化机制。

为什么hooks函数顶部？

链表结构

ref使用注意事项？

- 既可以用来得到dom节点，又可以存值，class comp中可以获取组件实例，fc中useRef只能获取dom节点
  - fc获取实例需要结合转发ref，forwardedRef和useImperativeHandle自定义暴露给父组件的实例值，可以让父组件访问子组件方法
- 监听ref，可以给ref字段传useCallback函数

#### jsx转换

旧的是React.createElement()，要引入React，新的jsx转换_jsx(...)

#### 事件委托

16：注册到document节点

17：注册到React的根节点容器中

可以写多个ReactDom.render

解决阻止事件冒泡的问题

<img src="/Users/huangsiying/data/yd/Naixes阶段性学习笔记.assets/截屏2021-06-04 下午6.11.49.png" alt="截屏2021-06-04 下午6.11.49" style="zoom:50%;" />

## vite

项目参考：demo-collection

## recoil

redux - 中心化管理

​	useReducer

mobx - 中心化管理

​	mobx-lite - 轻量，深层状态有问题，+ mobx-state-tree，使用*函数（性能影响大，过渡语法没优化）

recoil - 只适用于react，原子state，状态独立，只有action

​	刷新两遍

微前端

​	xstate，通用

> redux 中心化管理
>  useReducer    
>  基于useReducer状态管理
>
>      provider  
>          provider
>              provider
>                  provider 
>                      provider
>
> Vuex ->  
> mobx 中心化管理 麻烦 
>  mobx-lite + mobx-state-tree 
>      *函数 
>      useXxxxxxxxx.....
>  @xxxxxxxx
>  const x = function(){}
>
>
> recoil  Atom State
>  react中 ---> action
>  运行2遍 useState({})  = setState({})  {} == {}
>
>
> 微前端
> index.html xstate poroxy

## C

最底层：cpu和内存

### cpu与内存的工作原理

#### CPU的指令集

不同的cpu指令集不一样，相当于cpu使用的语言，机器指令不是汇编，汇编也是给人用的，前两个民用：

x86/x64指令集，PC，MAC一般是x86，x64一般用在服务器 

ARM指令集，手机，平板常用

MIPS指令集，多用于服务器，国产龙芯cpu用的这个

RISC指令集，多用于工业

##### 程序的执行过程

程序最开始在硬盘，执行时装到内存中去。内存中的程序（进程）分两部分，**代码段和数据段**，放在不同的区域。

代码段驱动cpu。程序放进内存中就变成了进程，操作系统会划分出专门的内存空间，叫进程空间，操作系统计算好偏移量然后从进程的第一条指令开始拿，cpu通过指令地址找到指令，cpu的指令计数器会计算指令的长度，cpu拿到指令后会放在指令寄存器中，然后开始执行，通过电路执行（门电路）。

有的指令负责从内存数据段拿数据到存储单元（MOV），有的负责进行计算（ADD），比如指令将数据从数据段拿出给运算单元，然后将结果返回给存储单元（较小），然后根据一定的算法，数据还会回写到内存的数据段。

指令是单向的，数据是双向的，因为指令不需要回写，除非是恶意程序（早期的内存大战，把指令当成数据写进内存，当时的内存划分不是很严格）

cpu操作内存，操作的就是地址，C语言通过指针操作地址

<img src="/Users/huangsiying/data/yd/Naixes阶段性学习笔记.assets/截屏2021-06-08 下午5.05.29.png" alt="截屏2021-06-08 下午5.05.29" style="zoom:50%;" />

#### cpu的组成

控制器，执行指令，指令从内存来

运算器，处理数据，计算基于加法

存储器，不是内存，数据从内存来

<img src="/Users/huangsiying/data/yd/Naixes阶段性学习笔记.assets/截屏2021-06-08 下午4.48.10.png" alt="截屏2021-06-08 下午4.48.10" style="zoom:50%;" />

<img src="/Users/huangsiying/data/yd/Naixes阶段性学习笔记.assets/截屏2021-06-08 下午5.57.20.png" alt="截屏2021-06-08 下午5.57.20" style="zoom:50%;" />

### 计算机语言的本源和发展

本源:二进制数据

第一代语言:机器指令 (痛苦指数 ✮✮✮✮✮)，0101

第二代语言:汇编指令(痛苦指数 ✮✮✮✮✩)，对机器指令的映射，人可以理解

第三代语言:高级语言(主要特征:面向过程)，C

第四代语言:面向对象语言(面向互联网、天然支持数据库)，java，C++

#### 了解汇编语言

汇编语言是最贴近底层的计算机语言

汇编语言是直接操作硬件的，没有任何抽象，不同的指令集对应的汇编语言不一样，不能通用

汇编语言由指令与数据组成，没有任何语句

汇编指令受到硬件平台限制，可移植性很低

了解一些底层语言知识，对理解计算机的运作机制和内存管理大有好处

<img src="/Users/huangsiying/data/yd/Naixes阶段性学习笔记.assets/截屏2021-06-08 下午6.09.32.png" alt="截屏2021-06-08 下午6.09.32" style="zoom:50%;" />

Hello word伪代码，给编译器用的，编译器转码之后生成二进制文件，指令和数据要根据规则分开放

定义数据，没有类型，包含数据和数据长度

指定程序入口_start

mov把一个数据放到一个寄存器，把4放入ax寄存器，两位字母的寄存器用了16位，三个字母的32位

mov相当于给api传参，第一个mov是函数后面是参数，int 80h是调用操作系统的api

### C语言

#### 发展历史

天生的系统级语言

最早用来编写Unix内核

曾经最流行的语言

至今仍在不断发展

<img src="/Users/huangsiying/data/yd/Naixes阶段性学习笔记.assets/截屏2021-06-08 下午8.07.01.png" alt="截屏2021-06-08 下午8.07.01" style="zoom:50%;" />

#### 与js区别

C语言是编译型语言，必须经过编译成机器指令，然后链接（组装成整体）才能执行

JavaScript是解释型语言，也会经过编译，ts-js，nodejs-字节码-jit

C语言要借助编译器转换成可执行程序

JavaScript要借助解释引擎运行

<img src="/Users/huangsiying/data/yd/Naixes阶段性学习笔记.assets/截屏2021-06-08 下午8.10.52.png" alt="截屏2021-06-08 下午8.10.52" style="zoom:50%;" />

#### c与c++的区别

1、C++是新的编程语言，并不是C的扩展，比c复杂很多，面向对象的特性是最多的，子类可以继承多父类，多继承，比如它的io库，友元friend，可以操作私有属性

2、C语言是面向过程的，C++是面向对象的

3、C和C++语言都有标准库

4、目前C大多用在网络相关和嵌入式等方面

5、目前C++大多用在复杂引擎和应用软件方面

C#和java是同一类，互相抄，C#原身是J++，java在前，sun开源java

C和C++没有GC

go，rust，手动+GC

语言的发展，面向对象，GC

### 配置环境

Windows环境: Visual C++/MingWin

Linux/unix环境:gcc/g++

Mac环境:Xcode/gcc

推荐Linux/Unix/Mac环境

### 语法

推荐learnxinyminutes.com

数据类型

整型，有符号/无符号，32位2字节/64位4字节，长整型/短整型2字节16比特

int，short，long，int64

浮点型，单精度4字节/双精度8字节

float，double

字符型，最小的整型，1字节，有符号/无符号

chart

结构体，没有方法，内存里罗列

union，联合体，复用一块内存

枚举

boolean

### 内存与指针

c是最接近硬件（内存和cpu）的语言，可嵌入汇编代码

内存的最小单位，字节，8位

内存与内存地址，依靠内存地址变量

指针、地址与引用，指针是一个变量用来保存内存地址，指针也在内存里，引用是被封装的指针，引用中的指针系统维护，不用对地址进行计算，加减，对单位进行运算，比如一个整型单位，指针可以指向内存中的任何东西

指向变量的指针，int a = 10; int *pa = &a; printf('%d', *pa)（间接寻址）;prints('%d', a)（直接寻址）

指向指针的指针，二级指针，int ** ppa = &pa; printf('%d', **ppa); // *pa是a的地址

指向函数的指针

<img src="/Users/huangsiying/data/yd/Naixes阶段性学习笔记.assets/截屏2021-06-08 下午8.52.27.png" alt="截屏2021-06-08 下午8.52.27" style="zoom:50%;" />

<img src="/Users/huangsiying/data/yd/Naixes阶段性学习笔记.assets/截屏2021-06-08 下午9.39.45.png" alt="截屏2021-06-08 下午9.39.45" style="zoom:50%;" />

<img src="/Users/huangsiying/data/yd/Naixes阶段性学习笔记.assets/截屏2021-06-08 下午9.40.13.png" alt="截屏2021-06-08 下午9.40.13" style="zoom:50%;" />

动态内存分配

c和c++对数据段进行了更加详细的划分

内存4区，代码+数据

栈区：函数调用栈，保存局部变量本质上是在保存寄存器状态，要复制到一块内存里就在栈区

堆区：内存的动态分配，c用多少请求多少，c操作系统管，nodejs申请一大块，nodejs自己管

静态区：保存全局变量和静态变量，字符串就是在全局区里

<img src="/Users/huangsiying/data/yd/Naixes阶段性学习笔记.assets/截屏2021-06-08 下午9.50.24.png" alt="截屏2021-06-08 下午9.50.24" style="zoom:50%;" />

## Docker

### 微服务

与docker无必然联系，本质是业务模块化

微服务属于**架构层面**的设计模式

微服务的设计概念以**业务功能**为主

微服务**独立提供**对应的业务功能

微服务**不拘泥**于具体的实现**语言**，灵活

微服务架构 ≈ **模块化开发 + 分布式计算**

<img src="/Users/huangsiying/data/yd/Naixes阶段性学习笔记.assets/截屏2021-06-12 下午2.11.19.png" alt="截屏2021-06-12 下午2.11.19" style="zoom:50%;" />

左，传统结构，右，微服务

传统结构：函数级调用，调用方便，快；复杂系统不易维护

微服务

DBMS：数据库管理系统

单体应用架构：数据库管理系统对外提供的服务通过socket（网络套接字，属于数据传输层），传输层包含tcp和udp，在tcp之上封装自己的私有协议，链接tcp时会有消耗，消耗数据库服务器的端口，每个链接都会维护tcp的会话，有上限，数据库有连接池，每个连接池都是维护tcp会话的，应用方面也需要一个连接池，维护客户端会话。单体应用服务压力过大时，负载均衡，每加一个负载，复制一份代码，比如一个单体应用的会话连接池是10个，每多一个负载连接池多10个，数据库也是一样多，数据库就需要做扩展，分布式，数据库做扩展有障碍，数据一致性问题，复杂性极高。并发瓶颈难以突破

toB，稳定性

toC，并发树

> 数据中台，业务角度和技术无关，管理业务

微服务：以业务为单位拆分，相互独立，独立进程，通过ip端口进行定位，客户端通过**api网关**找到对应服务，api网关也是架构模式，把请求统一入口进行服务。api做的事情，请求代理到微服务，将后面的服务提供的数据聚合（在前端是BFF）。业务模块之间需要关联，所以还需要提供服务之间的通讯手段，有多种封装方式，比如restful接口，消息队列，微服务框架（提供模块之间的调用手段，也是基于tcp，封装私有协议），每个业务都有自己的数据库实例（一般不同机器，分流了数据库的压力）分流了数据库和业务服务器的压力，数据库之间的关联，索引关联。压力大时增加实例，其余时间关掉

特点：

小, 且专注于做一件事情，unix哲学

处于独立的进程中

轻量级的通信机制，重量通信机制基于http，业务数据可以使用json或xml封装，较轻量，更轻量事以二进制形式进行封装，http2使用的二进制帧进行封装的

松耦合、独立部署，维护成本低一些

#### 合理使用

业务复杂度高

团队规模大

业务需要长期演进，互联网应用，业务规则不断变化

最后——没有银弹

#### 集成与部署

持续集成——jekins

虚拟化——虚拟机

容器——Docker，打包

### docker

Docker是一个开源的引擎，可以轻松的为任何应用创建一个轻量级的、可移植的、 自给自足的容器。开发者在笔记本上编译测试通过的容器可以批量地在生产环境中 部署，包括VMs(虚拟机)、bare metal、OpenStack 集群和其他的基础应用平台。

Docker通常用于如下场景:

- web应用的自动化打包和发布;
- 自动化测试和持续集成、发布; 
- 在服务型环境中部署和调整数据库或其他的后台应用; 
- 从头编译或者扩展现有的OpenShift或Cloud Foundry平台来搭建自己的PaaS环境。

#### Docker vs. VM

VM: 

运行在宿主机之上的完整的操作系统

运行自身操作系统会占用较多的资源

Docker: 通过docker使用宿主的操作系统

Docker更加轻量高效

对系统资源的利用率很高，无法控制cpu使用

比虚拟机技术更为轻便、快捷

隔离效果不如VM

<img src="/Users/huangsiying/data/yd/Naixes阶段性学习笔记.assets/截屏2021-06-12 下午3.59.24.png" alt="截屏2021-06-12 下午3.59.24" style="zoom:50%;" />

进程两种状态：用户态he内核态，内核态需要操作系统调用，容器通过docker使用宿主的操作系统，所以轻量，但是隔离效果不好，可能影响到其他进程

#### 概念

Docker是CS架构，主要有两个概念: 

Docker daemon:

运行在宿主机上

Docker守护进程

用户通过Docker client(Docker命令)与Docker daemon交互

Docker client:

Docker 命令行工具，是用户使用Docker的主要方式

Docker client与Docker daemon通信并将结果返回给用户

Docker client也可以通过socket或者RESTful api访问远程的 Docker daemon

```cmd
# 客户端命令，操作
docker
# 服务器端命令，干活，构建镜像，从镜像创建容器，容器就是镜像的实例
systemctl status docker
```

docker只能跑在linux，unix

#### docker file

Dockerfile 概念

Dockerfile 文件格式

构建镜像

镜像标签

修改容器内容

.dockerignore

两种启动模式：第一次run，镜像到容器的转换，初始化，n次使用start

## k8s

运维

### 定义

Kubernetes，因为首尾字母中间有8个字符，所以被简写成 K8s。

K8s 是底层资源（硬件，cpu，内存，网络资源，网关系统）与容器间的一个抽象层，如果和单机架构类比，可以算作是一个**分布式**时代的Linux。

K8s 是 Google 开源的容器集群管理系统。在 Docker 技术的基础上，为 容器化的应用提供部署运行、资源调度、服务发现和动态伸缩等一系列 完整功能，提高了大规模容器集群管理的便捷性。

### 特点

k8s是一个管理容器的工具，也是**管理应用整个生命周期的一个工具， 从创建应用，应用的部署，应用提供服务，扩容缩容应用，应用更新**， 而且可以做到故障自愈。

可移植:  支持公有云，私有云，混合云;

可扩展: 模块化，热插拨（自动接入新设备，服务器有问题可退出），可组合;

自愈: 自动替换，自动重启，自动复制，自动扩展。

### 步骤

在k8s进行管理应用的时候，基本步骤是: 

创建集群

部署应用

发布应用

扩展应用

更新应用

### 架构结构

生态系统，外围支持

接口层，对外提供接口

管理层，常用

应用层，具体做事

核心层，对外技术

<img src="/Users/huangsiying/data/yd/Naixes阶段性学习笔记.assets/截屏2021-06-12 下午7.09.11.png" alt="截屏2021-06-12 下午7.09.11" style="zoom:50%;" />

### 概念 

主机(Master): 管理，用于控制 Kubernetes 节点的计算机。所有任务分配都来自于此。

节点(Node): 干活，执行请求和分配任务的计算机。由 Kubernetes 主机负责对节点进行控制。

容器集(Pod): 部署在单个节点上的，且包含一个或多个容器的容器组。同一容器集中的所有容器共享同一个 IP 地址、IPC、主机名称及其它资源。容器集会将网络和存储从底层容器中抽象出来。这样， 您就能更加轻松地在集群中移动容器。

复制控制器(Replication controller): 跑在主机，用于控制应在集群某处运行的完全相同的容器集副本数量。

服务(Service): 跑在节点，服务可将工作定义（k8s自己的业务）与容器集分离。Kubernetes 服务代理会自动将服务请求分配到正 确的容器集——无论这个容器集会移到集群中的哪个位置，即使它已被替换。

Kubelet: 这是一个在节点上运行的服务，运行核心，可读取容器清单，确保指定的容器启动并运行。 

kubectl: Kubernetes 的命令行配置工具。

etcd，管理配置文件的进程

两个节点

代理

<img src="/Users/huangsiying/data/yd/Naixes阶段性学习笔记.assets/截屏2021-06-12 下午7.25.02.png" alt="截屏2021-06-12 下午7.25.02" style="zoom:50%;" />

### 安装

在Linux下安装单机版的集群环境

以root身份执行以下操作: 

1、关闭Linux防火墙

systemctl stop firewalld

systemctl disable firewalld 

2、安装Kubernetes和依赖组件etcd

yum install -y etcd kubernetes 

3、修改配置

Docker配置文件/etc/sysconfig/docker, OPTIONS=‘-- selinux-enabled=false --insecure-registry gcr.io'

Kubernetes apiservce配置文件/etc/kubernetes/apiserver, 把--admission-control参数中的ServiceAccount删除

4、按顺序启动所有的服务

systemctl start etcd，读取配置文件用到，master进程ongdao

systemctl start docker，在scheduler前执行， node进程

systemctl start kube-apiserver，master进程

systemctl start kube-controller-manager，master进程

systemctl start kube-scheduler， node进程

systemctl start kubelet， node进程

systemctl start kube-proxy， node进程

1、官网 https://kubernetes.io

2、Chart 应用仓库 https://hub.kubeapps.com/

3、中文手册 https://www.kubernetes.org.cn/docs

minikuber

