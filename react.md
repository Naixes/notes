# React.js

## React简介

- React 起源于 Facebook 的内部项目，因为该公司对市场上所有 JavaScript MVC 框架，都不满意，就决定自己写一套，用来架设 Instagram（照片交友） 的网站。做出来以后，发现这套东西很好用，**就在2013年5月开源了**。
- 由于 React 的**设计思想极其独特**，属于革命性创新，性能出众，代码逻辑却非常简单。所以，越来越多的人开始关注和使用，认为它可能是将来 Web 开发的主流工具。
- 清楚两个概念：
  - library（库）：小而巧的库，只提供了特定的API；优点就是 船小好掉头，可以很方便的从一个库切换到另外的库；但是代码几乎不会改变；
  - Framework（框架）：大而全的是框架；框架提供了一整套的解决方案；所以，如果在项目中间，想切换到另外的框架，是比较困难的；

### 前端三大主流框架

### React与vue的对比

Vue 的表单可以使用 `v-model` 支持**双向绑定**，相比于 React 来说开发上更加方便，当然了 `v-model`其实就是个语法糖，本质上和 React 写表单的方式没什么区别。

改变数据方式不同，Vue **修改状态**相比来说要简单许多，React 需要使用 `setState` 来改变状态，并且使用这个 API 也有一些坑点。并且 Vue 的底层使用了依赖追踪，页面更新渲染已经是最优的了，但是 React 还是需要用户手动去优化这方面的问题。

React 16以后，有些钩子函数会执行多次，这是因为引入 Fiber 的原因。

React 需要**使用 JSX**，有一定的上手成本，并且需要一整套的**工具链支持**，但是**完全可以通过 JS 来控制页面，更加的灵活**。Vue 使用了**模板语法**，相比于 JSX 来说**没有那么灵活，但是完全可以脱离工具链**，通过直接编写 `render` 函数就能在浏览器中运行。

在生态上来说，两者其实没多大的差距，当然 React 的用户是远远高于 Vue 的。

在上手成本上来说，Vue 一开始的定位就是尽可能的降低前端开发的门槛，然而 React 更多的是去改变用户去接受它的概念和思想，相较于 Vue 来说上手成本略高。

#### 组件化方面

1. **什么是模块化：**是从**代码**的角度来进行分析的；把一些可复用的代码，抽离为单个的模块；便于项目的维护和开发；
2. **什么是组件化：** 是从 **UI 界面**的角度来进行分析的；把一些可服用的UI元素，抽离为单独的组件；便于项目的维护和开发；
3. **组件化的好处：**随着项目规模的增大，手里的组件越来越多；很方便就能把现有的组件，拼接为一个完整的页面；
4. **Vue是如何实现组件化的：** 通过 `.vue` 文件，来创建对应的组件；
   - template  结构
   - script        行为
   - style           样式

5. **React如何实现组件化**：React中有组件化的概念，但是，并没有像vue这样的组件模板文件；React中，一切都是以JS来表现的；因此要学习React，JS要合格；ES6 和 ES7 （async  和 await） 要会用；

#### 开发团队方面

- React是由FaceBook前端官方团队进行维护和更新的；因此，React的维护开发团队，技术实力比较雄厚；
- Vue：第一版，主要是有作者 尤雨溪 专门进行维护的，当 Vue更新到 2.x 版本后，也有了一个以 尤雨溪 为主导的开源小团队，进行相关的开发和维护；

#### 移动APP开发体验方面

- Vue，结合 Weex 这门技术，提供了 迁移到 移动端App开发的体验（Weex，目前只是一个 小的玩具， 并没有很成功的 大案例；）
- React，结合 ReactNative，也提供了无缝迁移到 移动App的开发体验（RN用的最多，也是最火最流行的）；

### React的优点

1. 和Angular1相比，React设计很优秀，一切基于JS并且实现了组件化开发的思想；
2. 开发团队实力强悍，不必担心断更的情况；
3. 社区强大，很多问题都能找到对应的解决方案；
4. 提供了无缝转到 ReactNative 上的开发体验，让我们技术能力得到了拓展；增强了我们的核心竞争力；
5. 很多企业中，前端项目的技术选型采用的是React.js；

## 几个核心的概念

### 虚拟DOM（Virtual Document Object Model）

- **DOM的本质是什么**：浏览器中的概念，浏览器中用JS对象来表示页面上的元素，并提供了操作DOM 对象的API；

- **什么是React中的虚拟DOM**：是框架中的概念，框架中用JS对象来模拟页面上的 DOM 和 DOM嵌套；

- **为什么要实现虚拟DOM：**为了实现页面中， DOM 元素的高效更新

- **DOM和虚拟DOM的区别**：

  - **DOM：**浏览器中，提供的概念；用JS对象，表示页面上的元素，并提供了操作元素的API；

  - 网页的呈现

    - 浏览器请求获取HTML代码
    - 在内存中解析DOM结构，渲染出DOM树
    - 将DOM树呈现到页面

  - **虚拟DOM：**是框架中的概念；而是开发框架的程序员，手动用JS对象来模拟DOM元素和嵌套关系；

    - 本质： 用JS对象，来模拟DOM元素和嵌套关系；
    - 目的：就是为了实现页面元素的高效更新；


相较于 DOM 来说，操作 JS 对象会快很多，可以通过 JS 来模拟 DOM

```js
const ul = {
  tag: 'ul',
  props: {
    class: 'list'
  },
  children: {
    tag: 'li',
    children: '1'
  }
}
```

上述代码对应的 DOM 就是

```html
<ul class='list'>
  <li>1</li>
</ul>
```

### Diff算法

那么既然 DOM 可以通过 JS 对象来模拟，反之也可以通过 JS 对象来渲染出对应的 DOM。当然了，通过 JS 来模拟 DOM 并且渲染对应的 DOM 只是第一步，难点在于如何判断新旧两个 JS 对象的**最小差异**并且实现**局部更新** DOM。

首先 DOM 是一个多叉树的结构，如果需要完整的对比两颗树的差异，那么需要的时间复杂度会是 O(n ^ 3)，这个复杂度肯定是不能接受的。于是 React 团队优化了算法，实现了 O(n) 的复杂度来对比差异。 实现 O(n) 复杂度的关键就是**只对比同层的节点**，而不是跨层对比，这也是考虑到在实际业务中很少会去跨层的移动 DOM 元素。 所以判断差异的算法就分为了两步

- 首先从上至下，从左往右遍历对象，也就是树的深度遍历，这一步中会给每个节点添加索引，便于最后渲染差异
- 一旦节点有子元素，就去判断子元素是否有不同

在第一步算法中我们需要判断新旧节点的 `tagName` 是否相同，如果不相同的话就代表节点被替换了。如果没有更改 `tagName` 的话，就需要判断是否有子元素，有的话就进行第二步算法。

在第二步算法中，我们需要判断原本的列表中是否有节点被移除，在新的列表中需要判断是否有新的节点加入，还需要判断节点是否有移动。

举个例子来说，假设页面中只有一个列表，我们对列表中的元素进行了变更

```js
// 假设这里模拟一个 ul，其中包含了 5 个 li
[1, 2, 3, 4, 5]
// 这里替换上面的 li
[1, 2, 5, 4]
```

从上述例子中，我们一眼就可以看出先前的 `ul` 中的第三个 `li` 被移除了，四五替换了位置。

那么在实际的算法中，我们如何去识别改动的是哪个节点呢？这就引入了 `key` 这个属性，想必大家在 Vue 或者 React 的列表中都用过这个属性。这个属性是用来给每一个节点打标志的，用于判断是否是同一个节点。

当然在判断以上差异的过程中，我们还需要判断节点的属性是否有变化等等。

当我们判断出以上的差异后，就可以把这些差异记录下来。当对比完两棵树以后，就可以通过差异去局部更新 DOM，实现性能的最优化。

当然了 Virtual DOM 提高性能是其中一个优势，其实**最大的优势**还是在于：

1. 将 Virtual DOM 作为一个兼容层，让我们还能对接非 Web 端的系统，实现跨端开发。
2. 同样的，通过 Virtual DOM 我们可以渲染到其他的平台，比如实现 SSR、同构渲染等等。
3. 实现组件的高度抽象化

- **tree diff:**新旧两棵DOM树，逐层对比的过程，就是 Tree Diff； 当整颗DOM逐层对比完毕，则所有需要被按需更新的元素，必然能够找到；

- **component diff：**在进行Tree Diff的时候，每一层中，组件级别的对比，叫做 Component Diff；

  - 如果对比前后，组件的类型相同，则**暂时**认为此组件不需要被更新；
  - 如果对比前后，组件类型不同，则需要移除旧组件，创建新组件，并追加到页面上；

- **element diff:**在进行组件对比的时候，如果两个组件类型相同，则需要进行 元素级别的对比，这叫做 Element Diff；

  ![Diff算法图](./media/Diff.png)

## 初识React

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <!-- 解析jsx,babel中的 -->
    <script src="browser.js" charset="utf-8"></script>
    <script src="react.development.js" charset="utf-8"></script>
    <!-- 渲染 -->
    <script src="react-dom.development.js" charset="utf-8"></script>
</head>
<body>
    <div id="div"></div>
</body>
<!-- 必须使用text/babel -->
<script type="text/babel">
let root = document.getElementById("div")

// 渲染页面
ReactDOM.render(
    // className替换class,htmlFor替换label的for
    // 只能有一个根元素
    <div className="box">
        <div>aaa</div>
        <div>bbb</div>
        <div>
            <label htmlFor="user">用户名：</label>
            <input id="user" type="text" />
        </div>
    </div>,
    root
)
</script>
</html>
```

## 创建基本的webpack4.x项目

1. 运行`npm init -y` 快速初始化项目
2. 在项目根目录创建`src`源代码目录和`dist`产品目录
3. 在 src 目录下创建 `index.html`
4. 使用 cnpm 安装 webpack ，运行`cnpm i webpack webpack-cli -D`
   - 如何安装 `cnpm`: 全局运行 `npm i cnpm -g`
5. 注意：webpack 4.x 提供了 约定大于配置的概念；目的是为了尽量减少 配置文件的体积；
   - 默认约定了：
   - 打包的入口是`src` -> `index.js`
   - 打包的输出文件是`dist` -> `main.js`
   - 4.x 中 新增了 `mode` 选项(为必选项)，可选的值为：`development` 开发模式和 `production`;

### 配置webpack-dev-server

### 配置html-webpack-plugin配置

## 使用react

需要用到

```html
<script src="browser.js" charset="utf-8"></script>
<script src="react.development.js" charset="utf-8"></script>
<script src="react-dom.development.js" charset="utf-8"></script>
```

react：核心

react-dom：渲染

jsx：创建元素方便，语法糖，会编译成js

## 在项目中使用 react

1. 运行 `cnpm i react react-dom -S` 安装包

   - react： React负责逻辑控制，专门用于创建组件和虚拟DOM的，同时组件的生命周期都在这个包中，数据 -> VDOM
   - react-dom： 渲染实际DOM，专门进行DOM操作的，如果换到移动端，就用别的库来渲染，最主要的应用场景，就是`ReactDOM.render()`，VDOM -> DOM

2. 在`index.html`页面中，创建容器：

   ```html
   <!-- 容器，将来，使用 React 创建的虚拟DOM元素，都会被渲染到这个指定的容器中 -->
   <div id="app"></div>
   ```

3. 导入包：

   ```js
   import React from 'react' // 名字必须是React
   import ReactDOM from 'react-dom' // 名字必须是ReactDOM
   ```

4. 创建虚拟DOM元素：

   ```jsx
   // 这是 创建虚拟DOM元素的 API    <h1 title="啊，五环" id="myh1">你比四环多一环</h1>
   //  第一个参数： 字符串类型的参数，表示要创建的标签的名称
   //  第二个参数： 对象类型的参数， 表示 创建的元素的属性节点
   //  第三个参数及以后： 子节点
   const myh1 = React.createElement('h1', { title: '啊，五环', id: 'myh1' }, '你比四环多一环')
   ```

5. 渲染：

   ```js
   // 3. 渲染虚拟DOM元素
   // 参数1： 表示要渲染的虚拟DOM对象
   // 参数2： 指定容器,注意：这里不能直接放 容器元素的Id字符串，需要放一个容器的DOM对象
   ReactDOM.render(myh1, document.getElementById('app'))
   ```

### 使用脚手架-create-react-app

`npm i -g create-react-app`

`create-react-add xxx`

由于cra项目是打包封装过的，有一些细节会看不到，使用`npm run eject`命令会多出两个目录，可以用来查看具体配置

```
├── config 
	├── env.js 处理.env环境变量配置文件 
	├── paths.js 提供各种路径 
	├── webpack.config.js webpack配置文件 
	└── webpackDevServer.config.js 测试服务器配置文件 
└── scripts 启动、打包和测试脚本 
	├── build.js 打包脚本、 
	├── start.js 启动脚本 
	└── test.js 测试脚本
```

env.js用来处理.env文件中配置的环境变量

```js
// node运行环境：development、production、test等 
const NODE_ENV = process.env.NODE_ENV; // 要扫描的文件名数组 
var dotenvFiles = [
    `${paths.dotenv}.${NODE_ENV}.local`, // .env.development.local
    `${paths.dotenv}.${NODE_ENV}`, // .env.development 
    NODE_ENV !== 'test' && `${paths.dotenv}.local`, // .env.local 
    paths.dotenv, // .env 
].filter(Boolean); 
// 从.env*文件加载环境变量 
dotenvFiles.forEach(dotenvFile => {
    if (fs.existsSync(dotenvFile)) {
        require('dotenv-expand')( 
            require('dotenv').config({ 
            path: dotenvFile, 
            }) 
        ); 
    } 
});
```

实践一下，修改一下默认端口号，创建.env文件

```js
PORT=8080	
```

webpack.confifig.js 是webpack配置文件，开头的常量声明可以看出cra能够支持ts、sass及css模块化

```js
// Check if TypeScript is setup 
const useTypeScript = fs.existsSync(paths.appTsConfig); 
// style files regexes 
const cssRegex = /\.css$/; 
const cssModuleRegex = /\.module\.css$/; 
const sassRegex = /\.(scss|sass)$/; 
const sassModuleRegex = /\.module\.(scss|sass)$/;
// 入口文件定义
entry: [ 
    // WebpackDevServer客户端，它实现开发时热更新功能 
    isEnvDevelopment && require.resolve('react-dev-utils/webpackHotDevClient'), 
    // 应用程序入口：
    src/index paths.appIndexJs, 
].filter(Boolean),
```

## JSX语法

> 什么是JSX语法：就是符合 xml 规范的 JS 语法；（语法格式相对来说，要比HTML严谨很多），可以理解成虚拟dom
>
> JSX是一种JavaScript的语法扩展，其格式比较像模版语言，但事实上完全是在JavaScript内部实现的。 
>
> JSX可以很好地描述UI，能够有效提高开发效率

1. **如何启用 jsx 语法？**

   - 安装 `babel` 插件

     - 运行`cnpm i babel-core babel-loader babel-plugin-transform-runtime -D`
     - 运行`cnpm i babel-preset-env babel-preset-stage-0 -D`

   - 安装能够识别转换jsx语法的包 `babel-preset-react` 

     - 运行`cnpm i babel-preset-react -D`

   - 添加 `.babelrc` 配置文件

     ```json
     {
       "presets": ["env", "stage-0", "react"],
       "plugins": ["transform-runtime"]
     }
     ```

   - 添加babel-loader配置项：

     ```js
     module: { //要打包的第三方模块
         rules: [
           { test: /\.js|jsx$/, use: 'babel-loader', exclude: /node_modules/ }
         ]
     }
     ```

2. **jsx 语法的本质：**并不是直接把 jsx 渲染到页面上，而是内部先转换成了 createElement 形式，再渲染的；

3. **在 jsx 中混合写入 js 表达式**：在 jsx 语法中，要把 JS代码写到 `{ }` 中

   - 渲染数字
   - 渲染字符串
   - 渲染布尔值
   - 为属性绑定值
   - 渲染jsx元素
   - 渲染jsx元素数组
   - 将普通字符串数组，转为jsx数组并渲染到页面上【两种方案】
   - 条件语句和循环语句不能使用 

```jsx
const arr = ['aa', 'bb', 'cc']
// map，数据是对象时注意加上key属性
ReactDOM.render({arr.map(item => <h3>{item}</h3>)}, document.getElementById('app'))
```

1. **在 jsx 中 写注释**：推荐使用`{ /* 这是注释 */ }`

2. **为 jsx 中的元素添加class类名**：需要使用`className` 来替代 `class`；`htmlFor`替换label的`for`属性

3. 在JSX创建DOM的时候，所有的节点，必须有唯一的根元素进行包裹；

4. 在 jsx 语法中，标签必须 成对出现，如果是单标签，则必须自闭和！

> 当 编译引擎，在编译JSX代码的时候，如果遇到了`<`那么就把它当作 HTML代码去编译，如果遇到了 `{}` 就把 花括号内部的代码当作 普通JS代码去编译；

## 相关文章

- [2018 年，React 将独占前端框架鳌头？](https://mp.weixin.qq.com/s/gV-w_rRfdBVAqsOpBGZaVw)
- [前端框架三巨头年度走势对比：Vue 增长率最高](https://mp.weixin.qq.com/s/0wXWqKIigaKzMSfy4vJMVw)

- [React数据流和组件间的沟通总结](http://www.cnblogs.com/tim100/p/6050514.html)
- [单向数据流和双向绑定各有什么优缺点？](https://segmentfault.com/q/1010000005876655/a-1020000005876751)
- [怎么更好的理解虚拟DOM?](https://www.zhihu.com/question/29504639?sort=created)
- [React中文文档 - 版本较低](http://www.css88.com/react/index.html)
- [React 源码剖析系列 － 不可思议的 react diff](http://blog.csdn.net/yczz/article/details/49886061)
- [深入浅出React（四）：虚拟DOM Diff算法解析](http://www.infoq.com/cn/articles/react-dom-diff?from=timeline&isappinstalled=0)
- [一看就懂的ReactJs入门教程（精华版）](http://www.cocoachina.com/webapp/20150721/12692.html)
- [CSS Modules 用法教程](http://www.ruanyifeng.com/blog/2016/06/css_modules.html)
- [将MarkDown转换为HTML页面](http://blog.csdn.net/itzhongzi/article/details/66045880)
- [win7命令行 端口占用 查询进程号 杀进程](https://jingyan.baidu.com/article/0320e2c1c9cf0e1b87507b26.html)

##  安装 React Developer Tools 调试工具

[React Developer Tools - Chrome 扩展下载安装地址](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi?hl=zh-CN)

## React中创建组件

### function组件

> **使用构造函数来创建组件**，如果要接收外界传递的数据，需要在构造函数的参数列表中使用`props`来接收；
>
> 必须要向外return一个合法的JSX创建的虚拟DOM；

- 创建组件：

  ```jsx
  function Hello (props) { 
  	// return null 
  	return <div>Hello 组件</div>
  }
  ```

- 为组件传递数据：

  ```jsx
  // 使用组件并为组件传递 props 数据
  <Hello name={dog.name} age={dog.age} gender={dog.gender}></Hello>
  <Hello {...dog}></Hello>
  
  // 在构造函数中，使用 props 形参，接收外界传递过来的数据
  function Hello(props) {
    // props.name = 'zs'
    console.log(props)
    // 结论：不论是 Vue 还是 React，组件中的 props 永远都是只读的；不能被重新赋值；
    return <div>这是 Hello 组件 --- {props.name} --- {props.age} --- {props.gender}</div>
  }
  ```


1. 父组件向子组件传递数据

2. 使用{...obj}属性扩散传递数据

3. 将组件封装到单独的文件中

4. 注意：组件的名称首字母必须是大写

5. 在导入组件的时候，如何省略组件的`.jsx`后缀名：

   ```js
   // 打开 webpack.config.js ，并在导出的配置对象中，新增 如下节点：
   resolve: {
       extensions: ['.js', '.jsx', '.json'], // 表示，这几个文件的后缀名，可以省略不写
       alias: {
           '@': path.join(__dirname, './src')
       }
     }
   ```

6. 在导入组件的时候，配置和使用`@`路径符号

#### 状态管理

```js
import { useState, useEffect } from "react"; 
function ClockFunc() { 
    // useState创建一个状态和修改该状态的函数 
    const [date, setDate] = useState(new Date()); 
    // useEffect编写副作用代码 
    useEffect(() => { 
        // 启动定时器是我们的副作用代码 
        const timerID = setInterval(() => { setDate(new Date()); }, 1000); 
        // 返回清理函数 
        return () => clearInterval(timerID); 
    }, []);
    // 参数2传递空数组使我们参数1函数仅执行一次 
    return <div>{date.toLocaleTimeString()}</div>; 
}
```

### class组件

#### ES6中 class 关键字的使用

1. class 中 `constructor` 的基本使用
2. 实例属性和实例方法
3. 静态属性和静态方法

```javascript
// 在类中只能写构造器实例静态方法和属性
// 本质和之前的构造函数一致
class Animal {
    // 每一个类都有构造器，没有指定时有默认的构造器
    // new的时候优先执行构造器中的代码
    constructor(参数1, 参数2) {
        // 实例属性
        this.aa = 参数1
        this.bb = 参数2
    }
    // 静态属性，通过构造函数调用
    static name = 'name'
	// 实例方法
	foo() {}
	// 静态方法
	static foo() {}
}
```

4. 使用 `extends` 关键字实现继承

```javascript
class Person {}
class Chinese extends Person{
    constructor(参数1, 参数2) {
        // extends关键字继承的父类，要在构造器最开始调用super()
        // super()是父类构造器的引用
        super(参数1, 参数2)
        this.state={}
    }
    render() {}
}
// 子类可以访问父类的实例方法
```

5. 为子类挂载独有的实例方法和属性

放到super()后面

#### 基于class关键字创建组件

1. 最基本的组件结构：

   ```jsx
   // 如果要使用 class 定义组件，必须 让自己的组件，继承自 React.Component
   class 组件名称 extends React.Component {
       constructor(...args){
           super(...args)
           // 状态：constructor中初始化，要用setState({})修改更新后会重新渲染，同时修改同一个key，只会有一个起作用
           this.state = {
           }
       }
       // 在组件内部，必须有 render 函数,作用：渲染当前组件对应的 虚拟DOM结构
       render(){
           const name = "react study"
           const user = { firstName: "tom", lastName: "jerry" }
           function formatName(user) { 
               return user.firstName + " " + user.lastName;
           }
           const greet = <p>hello, Jerry</p>;
           const arr = [1, 2, 3].map(num => <li key={num}>{num}</li>)
           // render 函数中，必须 返回合法的 JSX 虚拟DOM结构
           return ( 
               <div> 
                   {/* 条件语句 */} 
                   {name ? <h2>{name}</h2> : null} 
                   {/* 函数也是表达式 */} 
                   {formatName(user)} 
                   {/* jsx也是表达式 */} 
                   {greet} 
                   {/* 数组 */} 
                   <ul>{arr}</ul> 
                   {/* 属性 */} 
                   <img src={logo} className={style.img} alt="" /> 
               </div> 
           )
       }
   }
   // 使用<名称></名称>相当与'组件名称'类的实例对象
   ```

传递的参数不用接收，直接使用this.props访问，只读

##### setState特性

- setState是批量执行的，因此对同一个状态执行多次只起一次作用，多个状态更新可以放在同一个 

setState中进行：

```js
componentDidMount() { 
    // 假如couter初始值为0，执行三次以后其结果是多少？ 
    this.setState({counter: this.state.counter + 1}); 
    this.setState({counter: this.state.counter + 1}); 
    this.setState({counter: this.state.counter + 1}); 
}
```

- setState通常是异步的，因此如果要获取到最新状态值有以下三种方式：

1. 传递函数给setState方法，这个函数用上一个 state 作为第一个参数，将此次更新被应用时的 props 做为第二个参数

```js
this.setState((state, props) => ({ counter: state.counter + 1}));// 1 
this.setState((state, props) => ({ counter: state.counter + 1}));// 2 
this.setState((state, props) => ({ counter: state.counter + 1}));// 3
```

2. 使用定时器：

```js
setTimeout(() => { 
    console.log(this.state.counter); 
}, 0);
```

3. 原生事件中修改状态

```js
componentDidMount(){ 
    document.body.addEventListener('click', this.changeValue, false)
}
changeValue = () => { 
    this.setState({counter: this.state.counter+1}) console.log(this.state.counter) 
}
```

### 两种创建组件方式的对比

> 注意：使用 class 关键字创建的组件，有自己的私有数据（this.state） 和生命周期函数；
>
> 注意：使用 function 创建的组件，只有props，没有自己的私有数据和生命周期函数；

1. 用**构造函数**创建出来的组件：叫做“无状态组件”【不需要有自己的私有数据时使用】
2. 用**class关键字**创建出来的组件：叫做“有状态组件”【需要有自己的私有数据时使用】
3. React官方说：无状态组件，由于没有自己的state和生命周期函数，所以运行效率会比有状态组件稍微高一些；

### PropTypes检查属性类型

```react
import PropTypes from 'prop-typs'
...
PriceList.propTypes = {
  items: PropTypes.array.isRequired,
  onModifyItemL: PropTypes.func.isRequired,
  onDeleteItemL: PropTypes.func.isRequired
}

// defaultProps:默认属性
PriceList.defaultProps = {
  onModifyItemL: () => {}
}
```

### 渲染评论列表

![效果](./media/cmtlist.png)

有两个组件，一个父组件一个子组件

#### 通过for循环生成多个组件

```jsx
import React from 'react'
import ReactDOM from 'react-dom'

function CommentsItem(props) {
    return {<div>
        <h1>{props.user}</h1>
    	<p>{props.content}</p>
    </div>)}
}

class Comments extends React.Component {
    constructor() {
        super()
        this.state = CommentList: [
            { id: 1, user: '张三', content: '哈哈，沙发' },
            { id: 2, user: '李四', content: '哈哈，板凳' },
            { id: 3, user: '王五', content: '哈哈，凉席' },
            { id: 4, user: '赵六', content: '哈哈，砖头' },
            { id: 5, user: '田七', content: '哈哈，楼下山炮' }
        ]
    }
    render() {
        return (
            <div>
            	<h1>评论列表</h1>
            	{this.state.CommentList.map(item => <CommentsItem {...item} key={item.id}>				 </CommentsItem>}
        	</div>
		)
    }
}
```

### 组件通信

#### props

传递状态

传递函数：可以把子组件信息传入父组件，这个常称为状态提升

```react
// StateMgt 
<Clock change={this.onChange}/> 
// Clock 
this.timerID = setInterval(() => { 
    this.setState({ date: new Date() }, ()=>{ 
        // 每次状态更新就通知父组件 
        this.props.change(this.state.date); 
    }); 
}, 1000);
```

传递this：

```jsx
let root = document.getElementById("div")
// 父组件向子组件传值，子组件可修改
class Comp extends React.Component{
    constructor(...args){
        super(...args)
        this.state = {
            a: 0
        }
    }
    add(n){
        this.setState({
            a: this.state.a + n
        })
    }
    render() {
        return (
            <div>
                {this.state.a}
                <Sub par={this}/>
            </div>
        )
    }
}
class Sub extends React.Component {
    constructor(...args){
        super(...args)
        this.state = {
        }
    }
    fn(){
        this.props.par.add(1)
    }
    render() {
        return (
            <div>
                <input type="button" value="+1" onClick={this.fn.bind(this)} />
            </div>
        )
    }
}
ReactDOM.render(
    <div className="box">
        <div>
            <Comp a={2}/>
        </div>
    </div>,
    root
)
```

#### ref

```jsx
let root = document.getElementById("div")
// 子组件向父组件传值，父组件可修改
class Comp extends React.Component{
    constructor(...args){
        super(...args)
        this.state = {
        }
    }
    fn(){
        this.refs['sub'].add(1);
    }
    render() {
        return (
            <div>
                <input type="button" value="+1" onClick={this.fn.bind(this)} />
                <Sub ref='sub'/>
            </div>
        )
    }
}
class Sub extends React.Component{
    constructor(...args){
        super(...args)
        this.state = {
            a: 2
        }
    }
    add(n){
        this.setState({
            a: this.state.a + n
        })
    }
    render() {
        return (
            <div>
                {this.state.a}
            </div>
        )
    }
}
ReactDOM.render(
    <div className="box">
        <div>
            <Comp a={2}/>
        </div>
    </div>,
    root
)
```

#### context

跨层级组件之间通信 

```react
// 为当前的 theme 创建一个 context（“light”为默认值）。每个 Context 对象都会返回一个 Provider React 组件，它允许消费组件订阅 context 的变化。
const ThemeContext = React.createContext('light');
class App extends React.Component {
  render() {
    // 使用一个 Provider 来将当前的 theme 传递给以下的组件树。
    // 无论多深，任何组件都能读取这个值。
    // 在这个例子中，我们将 “dark” 作为当前的值传递下去。
    return (
      <ThemeContext.Provider value="dark">
        <Toolbar />
      </ThemeContext.Provider>
    );
  }
}

function Toolbar() {
  return (
    <div>
      <ThemedButton />
    </div>
  );
}

class ThemedButton extends React.Component {
  // 挂载在 class 上的 contextType 属性会被重赋值为一个由 React.createContext() 创建的 Context 对象。这能让你使用 this.context 来消费最近 Context 上的那个值。你可以在任何生命周期中访问到它，包括 render 函数中。
  // React 会往上找到最近的 theme Provider，然后使用它的值。
  static contextType = ThemeContext;
  render() {
    return <Button theme={this.context} />;
  }
}
```

Context 主要应用场景在于很多不同层级的组件需要访问同样一些的数据。请谨慎使用，因为这会使得组件的复用性变差。

```react
import React from "react"; 
// 创建上下文 
const Context = React.createContext(); 
// 获取Provider和Consumer 
const Provider = Context.Provider; 
const Consumer = Context.Consumer; 
// Child显示计数器，并能修改它，多个Child之间需要共享数据 
function Child(props) { 
    return <div onClick={() => props.add()}>{props.counter}</div>; 
}
export default class ContextTest extends React.Component { 
    // state是要传递的数据 
    state = { counter: 0 };
	// add方法可以修改状态 
	add = () => { 
        this.setState(nextState => ({ counter: nextState.counter + 1 })); 
    };
	// counter状态变更 
	render() { 
        return ( 
            <Provider value={{ counter: this.state.counter, add: this.add }}> 
                {/* Consumer中内嵌函数，其参数是传递的数据，返回要渲染的组件 */} 
                {/* 把value展开传递给Child */} 
                <Consumer>{value => <Child {...value} />}</Consumer> 
                <Consumer>{value => <Child {...value} />}</Consumer> 
            </Provider>
        ); 
    } 
}
```



**如果你只是想避免层层传递一些属性，组件组合（component composition）有时候是一个更好的解决方案**

#### redux

类似vuex，无明显关系的组件间通信

## ref

### DOM

```react
class CustomTextInput extends React.Component {
  constructor(props) {
    super(props);
    // 创建一个 ref 来存储 textInput 的 DOM 元素
    this.textInput = React.createRef();
    this.focusTextInput = this.focusTextInput.bind(this);
  }

  focusTextInput() {
    // 直接使用原生 API 使 text 输入框获得焦点
    // 注意：我们通过 "current" 来访问 DOM 节点
    this.textInput.current.focus();
  }

  render() {
    // 告诉 React 我们想把 <input> ref 关联到构造器里创建的 `textInput` 上
    return (
      <div>
        <input
          type="text"
          ref={this.textInput} />
        <input
          type="button"
          value="Focus the text input"
          onClick={this.focusTextInput}
        />
      </div>
    );
  }
}
```

### Class

```react
class AutoFocusTextInput extends React.Component {
  constructor(props) {
    super(props);
    this.textInput = React.createRef();
  }

  componentDidMount() {
    this.textInput.current.focusTextInput();
  }

  render() {
    return (
      <CustomTextInput ref={this.textInput} />
    );
  }
}
```

默认情况下，**你不能在函数组件上使用 `ref` 属性**，因为它们没有实例

如果要在函数组件中使用 `ref`，你可以使用 [`forwardRef`](https://react.docschina.org/docs/forwarding-refs.html)（可与 [`useImperativeHandle`](https://react.docschina.org/docs/hooks-reference.html#useimperativehandle) 结合使用），或者可以将该组件转化为 class 组件。

**Ref 转发是一个可选特性，其允许某些组件接收 `ref`，并将其向下传递（换句话说，“转发”它）给子组件。**

```react
const FancyButton = React.forwardRef((props, ref) => (
  <button ref={ref} className="FancyButton">
    {props.children}
  </button>
));

// 你可以直接获取 DOM button 的 ref：
const ref = React.createRef();
<FancyButton ref={ref}>Click me!</FancyButton>;
```

### 回调ref

```react
class CustomTextInput extends React.Component {
  constructor(props) {
    super(props);

    this.textInput = null;

    this.setTextInputRef = element => {
      this.textInput = element;
    };

    this.focusTextInput = () => {
      // 使用原生 DOM API 使 text 输入框获得焦点
      if (this.textInput) this.textInput.focus();
    };
  }

  componentDidMount() {
    // 组件挂载后，让文本框自动获得焦点
    this.focusTextInput();
  }

  render() {
    // 使用 `ref` 的回调函数将 text 输入框 DOM 节点的引用存储到 React
    // 实例上（比如 this.textInput）
    return (
      <div>
        <input
          type="text"
          ref={this.setTextInputRef}
        />
        <input
          type="button"
          value="Focus the text input"
          onClick={this.focusTextInput}
        />
      </div>
    );
  }
}
```

## HOC高阶组件

范例：为展示组件添加获取数据能力

请注意，HOC 不会修改传入的组件，也不会使用继承来复制其行为。相反，HOC 通过将组件*包装*在容器组件中来*组成*新组件。HOC 是纯函数，没有副作用。

不要试图在 HOC 中修改组件原型（或以其他方式改变它）。

```react
// Hoc.js 
import React from "react"; 
// Lesson保证功能单一，它不关心数据来源，只负责显示 
function Lesson(props) { 
    return ( <div> {props.stage} - {props.title} </div> ); 
}
// 模拟数据 
const lessons = [ 
    { stage: "React", title: "核心API" }, 
    { stage: "React", title: "组件化1" }, 
    { stage: "React", title: "组件化2" } 
];
// 高阶组件withContent负责包装传入组件Comp 
// 包装后组件能够根据传入索引获取课程数据，真实案例中可以通过api查询得到 
const withContent = Comp => props => { 
    const content = lessons[props.idx]; 
    // {...props}将属性展开传递下去 
    return <Comp {...content} />; 
};
// LessonWithContent是包装后的组件 
const LessonWithContent = withContent(Lesson); 
export default function HocTest() { 
    // HocTest渲染三个LessonWithContent组件 
    return ( 
        <div> {[0,0,0].map((item, idx) => ( <LessonWithContent idx={idx} key={idx} /> ))} </div> 
    ); 
}
```

范例：改造前面案例使上下文使用更优雅

```react
// withConsumer是高阶组件工厂，它能根据配置返回一个高阶组件 
function withConsumer(Consumer) { 
    return Comp => props => { 
        return <Consumer>{value => <Comp {...value} {...props} />}</Consumer>; 
    }; 
}
// Child显示计数器，并能修改它，多个Child之间需要共享数据 
// 新的Child是通过withConsumer(Consumer)返回的高阶组件包装所得 
const Child = withConsumer(Consumer)(function (props) { 
    return <div onClick={() => props.add()} title={props.name}>{props.counter}</div>; 
}); 
export default class ContextTest extends React.Component { 
    render() { 
        return ( 
        <Provider value={{ counter: this.state.counter, add: this.add }}> 
            {/* 改造过的Child可以自动从Consumer获取值，直接用就好了 */} 
            <Child name="foo"/> 
            <Child name="bar"/>
        </Provider> 
    	); 
    } 
}
```

### 链式调用

```react
// 高阶组件withLog负责包装传入组件Comp 
// 包装后组件在挂载时可以输出日志记录 
const withLog = Comp => { 
    // 返回组件需要生命周期，因此声明为class组件 
    return class extends React.Component { 
        render() { 
            return <Comp {...this.props} />; 
        }
        componentDidMount() { 
            console.log("didMount", this.props); 
        } 
    }; 
};
// LessonWithContent是包装后的组件 
const LessonWithContent = withLog(withContent(Lesson));
```

### 装饰器写法 

CRA项目中默认不支持js代码使用装饰器语法，可修改后缀名为tsx则可以直接支持 

```react
// 装饰器只能用在class上 
// 执行顺序从下往上 
@withLog 
@withContent 
class Lesson2 extends React.Component { 
    render() { 
        return ( <div> {this.props.stage} - {this.props.title} </div> ); 
    } 
}
export default function HocTest() { 
    // 这里使用Lesson2 
    return ( 
        <div> {[0, 0, 0].map((item, idx) => ( 
                <Lesson2 idx={idx} key={idx} /> 
            ))} 
        </div> 
    ); 
}
```

注意修改App.js中引入部分，添加一个后缀名 

要求cra版本高于2.1.0 

## Render Props

我们可以提供一个带有函数 prop 的 `<Mouse>` 组件，它能够动态决定什么需要渲染的，而不是将 `<Cat>` 硬编码到 `<Mouse>` 组件里，并有效地改变它的渲染结果。

```react
class Cat extends React.Component {
  render() {
    const mouse = this.props.mouse;
    return (
      <img src="/cat.jpg" style={{ position: 'absolute', left: mouse.x, top: mouse.y }} />
    );
  }
}

class Mouse extends React.Component {
  constructor(props) {
    super(props);
    this.handleMouseMove = this.handleMouseMove.bind(this);
    this.state = { x: 0, y: 0 };
  }

  handleMouseMove(event) {
    this.setState({
      x: event.clientX,
      y: event.clientY
    });
  }

  render() {
    return (
      <div style={{ height: '100vh' }} onMouseMove={this.handleMouseMove}>

        {/*
          Instead of providing a static representation of what <Mouse> renders,
          use the `render` prop to dynamically determine what to render.
        */}
        {this.props.render(this.state)}
      </div>
    );
  }
}

class MouseTracker extends React.Component {
  render() {
    return (
      <div>
        <h1>移动鼠标!</h1>
        <Mouse render={mouse => (
          <Cat mouse={mouse} />
        )}/>
      </div>
    );
  }
}
```

## 组合

### 包含关系

```react
function FancyBorder(props) {
  return (
    <div className={'FancyBorder FancyBorder-' + props.color}>
      {/* 使用一个特殊的 children prop 来将他们的子组件传递到渲染结果 */}
      {props.children}
    </div>
  );
}

function WelcomeDialog() {
  return (
    <FancyBorder color="blue">
      <h1 className="Dialog-title">
        Welcome
      </h1>
      <p className="Dialog-message">
        Thank you for visiting our spacecraft!
      </p>
    </FancyBorder>
  );
}
```

`<FancyBorder>` JSX 标签中的所有内容都会作为一个 `children` prop 传递给 `FancyBorder` 组件。因为 `FancyBorder` 将 `{props.children}` 渲染在一个 `<div>` 中，被传递的这些子组件最终都会出现在输出结果中。

少数情况下，你可能需要在一个组件中预留出几个“洞”。这种情况下，我们可以不使用 `children`，而是自行约定：将所需内容传入 props，并使用相应的 prop。

```react
function SplitPane(props) {
  return (
    <div className="SplitPane">
      <div className="SplitPane-left">
        {props.left}
      </div>
      <div className="SplitPane-right">
        {props.right}
      </div>
    </div>
  );
}

function App() {
  return (
    <SplitPane
      left={
        <Contacts />
      }
      right={
        <Chat />
      } />
  );
}
```

也可以传递对象

```react
import React from "react"; 
// 获取相应部分内容展示在指定位置 
function Dialog(props) { 
    return ( 
        <div style={{ border: "1px solid blue" }}> 
            {props.children.default} 
            <div>{props.children.footer}</div> 
        </div> 
    ); 
}
export default function Composition() { 
    return ( 
        <div> {/* 传入显示内容 */} 
            <Dialog> {{
                    default: ( 
                        <>
                            <h1>组件复合</h1> 
                            <p>复合组件给与你足够的敏捷去定义自定义组件的外观和行为</p> 
                        </> 
                    ),
                    footer: <button onClick={() => alert("react确实好")}>确定</button> 
                }} 
            </Dialog> 
        </div> 
    ); 
}
```

如果传入的是函数，还可以实现作用域插槽的功能

```react
function Dialog(props) {
    // 备选消息 
    const messages = { 
        "foo": {title: 'foo', content: 'foo~'}, 
        "bar": {title: 'bar', content: 'bar~'}, 
    }
    // 执行函数获得要显示的内容 
    const {body, footer} = props.children(messages[props.msg]); 
    return ( 
        <div style={{ border: "1px solid blue" }}> 
            {/* 此处显示的内容是动态生成的 */} 
            {body} 
            <div>{footer}</div> 
        </div> 
    ); 
}
export default function Composition() { 
    return ( 
        <div> 
            {/* 执行显示消息的key */} 
            <Dialog msg="foo"> 
                {/* 修改为函数形式，根据传入值生成最终内容 */} 
                {({title, content}) => ({ 
                    body: ( 
                    <>
                        <h1>{title}</h1>
                        <p>{content}</p>
                    </> 
                	),
                    footer: 
                    <button onClick={() => alert("react确实好")}>确定</button>
                })} 
            </Dialog> 
        </div> 
    ); 
}
```

如果props.children是jsx，此时它是**不能修改**的 

范例：实现RadioGroup和Radio组件，可通过RadioGroup设置Radio的name 

```react
function RadioGroup(props) { 
    // 不可行, 
    // React.Children.forEach(props.children, child => { 
    // child.props.name = props.name; 
    // }); 
    return ( 
        <div> {React.Children.map(props.children, child => { 
                // 要修改虚拟dom 只能克隆它
                // 参数1是克隆对象
                // 参数2是设置的属性
                return React.cloneElement(child, { name: props.name });
                })} 
        </div> 
    ); 
}
// Radio传入value,name和children，注意区分 
function Radio({ children, ...rest }) { 
    return ( <label> <input type="radio" {...rest} /> {children} </label> ); 
}
export default function Composition() { 
    return ( 
        <div> 
            {/* 执行显示消息的key */} 
            <RadioGroup name="mvvm"> 
                <Radio value="vue">vue</Radio> 
                <Radio value="react">react</Radio> 
                <Radio value="ng">angular</Radio> 
            </RadioGroup> 
        </div> 
    ); 
}
```

#### React.Children

`React.Children` 提供了用于处理 `this.props.children` 不透明数据结构的实用方法。

**React.Children.map**

```
React.Children.map(children, function[(thisArg)])
```

在 `children` 里的每个直接子节点上调用一个函数，并将 `this` 设置为 `thisArg`。如果 `children` 是一个数组，它将被遍历并为数组中的每个子节点调用该函数。如果子节点为 `null` 或是 `undefined`，则此方法将返回 `null` 或是 `undefined`，而不会返回数组。

### 特例关系

有些时候，我们会把一些组件看作是其他组件的特殊实例，比如 `WelcomeDialog` 可以说是 `Dialog` 的特殊实例。

在 React 中，我们也可以通过组合来实现这一点。“特殊”组件可以通过 props 定制并渲染“一般”组件，即对一般组件进行包装

## 设置样式

直接写样式会报错

1. 使用普通的 `style` 样式，第一层括号表示js代码，第二层括号表示样式对象

   ```jsx
   <h1 style={ {color: 'red', fontWeight: 200} }></h1>
   ```

2. 将样式封装成单独的文件

   封装成多个对象

   封装成一个对象

   封装到一个文件

   ```js
   export default {
     item: {
       border: '1px dashed #ccc',
       margin: '10px',
       padding: '5px',
       boxShadow: '0 0 3px #ccc'
     },
     user: {
       fontSize: '14px'
     },
     content: {
       fontSize: '12px'
     }
   }
   ```

   ```jsx
   import style from './style.js'
   var dom = <h1 style={style.title}></h1>
   
   {/* style.js */}
   export default {
       title: {color: 'red'}
   }
   ```

3. 使用样式表

   ```jsx
   import style from './style.css'
   {/* 由于样式表没有作用域，这样使用的样式表是全局生效的 */}
   var dom = <h1 className="title"></h1>
   ```

### 启用 css-modules

1. 修改 `webpack.config.js`这个配置文件，为 `css-loader` 添加参数：

   ```js
   { test: /\.css$/, use: ['style-loader', 'css-loader?modules'] } // 为 .css 后缀名的样式表  启用 CSS 模块化
   ```

2. 在需要的组件中，`import`导入样式表，并接收模块化的 CSS 样式对象：

   cssObj返回类名或id名和模块化类名或id名的对应关系

   ```js
   // cssObj返回类名或id名和模块化类名或id名的对应关系
   import cssObj from '../css/CmtList.css' 
   ```

3. 在需要的HTML标签上，使用`className`指定模块化的样式：

   ```jsx
   <h1 className={cssObj.title}>评论列表组件</h1>
   ```

4. 使用`localIdentName`自定义生成的类名格式，可选的参数有：

   - [path]  表示样式表 `相对于项目根目录` 所在路径
   - [name]  表示 样式表文件名称
   - [local]  表示样式的类名定义名称
   - [hash:length]  表示32位的hash值
   - 例子：`{ test: /\.css$/, use: ['style-loader', 'css-loader?modules&localIdentName=[path][name]-[local]-[hash:5]'] }`

在脚手架中配置约定xx.module.xx名称的文件可以模块化导入

### 使用 `:local()` 和 `:global()`

- `:local()`包裹的类名，是被模块化的类名，只能通过`className={cssObj.类名}`来使用

  同时，`:local`默认可以不写，这样，默认在样式表中定义的类名，都是被模块化的类名；

- `:global()`包裹的类名，是全局生效的，不会被 `css-modules` 控制，定义的类名是什么，就是使用定义的类名`className="类名"`

1. 注意：只有`.title`这样的类样式选择器，才会被模块化控制，类似于`body`这样的标签选择器，不会被模块化控制；

2. 同时指定多个类名

   `<h1 className={styleObj.title + ' test'}></h1>`

   `<h1 className={[styleObj.tetle, 'test'].join(' ')}></h1>`

### 第三方样式表

在项目中启用模块化并同时使用bootstrap，也可以像自定义样式表那样使用但是麻烦，可以使用下面的方式

1. 把自己的样式表，定义为 `.scss`  文件

2. 第三方的 样式表，还是 以 `.css` 结尾

3. 我们只需要为自己的 `.scss` 文件，启用模块化即可；

4. 运行`cnpm i sass-loader node-sass -D` 安装能够解析`scss`文件的loader

5. 添加loader规则：

   ```json
   { test: /\.scss$/, use: ['style-loader', 'css-loader?modules&localIdentName=[path][name]-[local]-[hash:5]', 'sass-loader'] } // 打包处理 scss 文件的 loader​
   ```

## 绑定事件

### 原生方式获取元素并绑定事件

在componentDidMount()中获取DOM绑定事件：

使用箭头函数保证this指向

要改变props时，定义state保存要修改的属性并从props中获取值进行初始化

### React 中的绑定事件

1. 事件的名称都是React的提供的，因此名称的首字母必须大写`onClick`、`onMouseOver`

2. 为事件提供的处理函数，必须是如下格式

   ```
   onClick= { function }
   ```

3. 用的最多的事件绑定形式为：

   ```jsx
   // 这里的this是组件实例
   <button onClick={ () => this.show('传参') }>按钮</button>
   
   // 事件的处理函数，需要定义为 一个箭头函数，然后赋值给 函数名称，如果定义为普通方法，this为undefined
   show = (arg1) => {
       console.log('show方法' + arg1)
   }
   ```

4. 在React中，如果想要修改 state 中的数据，推荐使用 `this.setState({ })`这个方法是异步的，要立即拿到更改完数据可以用回调函数`this.setState({ }, cb)`

5. 在 React 中另一个不同点是你不能通过返回 `false` 的方式阻止默认行为。你必须显式的使用 `e.preventDefault();`这里的e 是一个合成事件,你不需要担心跨浏览器的兼容性问题。

```react
import React, { Component } from "react"; 
export default class EventHandle extends Component { 
    constructor(props) { 
        super(props); 
        this.state = { name: "" };
        // 为了在回调中使用 `this`，这个绑定是必不可少的
        this.handleChange = this.handleChange.bind(this); 
    }
    handleChange(e) { 
        this.setState({ name: e.target.value }); 
    }
    render() { 
        return ( 
            <div> 
                {/* 使用箭头函数，不需要指定回调函数this，且便于传递参数 */} 
                {/* <input 
                    type="text" 
                    value={this.state.name} 
                    onChange={e => this.handleChange(e)} 
                /> */} 
                {/* 直接指定回调函数，需要指定其this指向，或者将回调设置为箭头函数属性 */} 
                <input
                    type="text" 
                    value={this.state.name} 
                    onChange={this.handleChange} 
                />
                <p>{this.state.name}</p> 
            </div> 
        ); 
    } 
}
```

**参数传递**

```react
<button onClick={(e) => this.deleteRow(id, e)}>Delete Row</button>
<button onClick={this.deleteRow.bind(this, id)}>Delete Row</button>
```

在这两种情况下，React 的事件对象 `e` 会被作为第二个参数传递。如果通过箭头函数的方式，事件对象必须**显式**的进行传递，而通过 `bind` 的方式，事件对象以及更多的参数将会被**隐式**的进行传递。

## 绑定文本框与state中的值

1. 在 Vue 中，默认提供了`v-model`指令，可以很方便的实现 数据的双向绑定，只是语法糖，实质上也是单向数据流
2. 但是，在 React 中，只是单向数据流，没有这种语法糖，也就是 只能把 state 上的数据绑定到页面，无法把页面中数据的变化，自动同步回 state ； 如果需要把 页面上数据的变化，保存到 state，则需要程序员手动监听`onChange`事件，拿到最新的数据，手动调用`this.setState({  })` 更改回去；
3. 如果文本框只是单项绑定了state状态，没有提供onChange事件，文本框是只读的并且会有警告，如果只想要一个只读的文本框，要添加readOnly属性

```jsx
    {/*只要将value属性，和state上的状态进行绑定，那么，这个表单元素就变成了受控表单元素，这时候，如果没有调用相关的事件，是无法手动修改表单元素中的值的*/}
    <input style={{ width: '100%' }} ref="txt" type="text" value={this.state.msg} onChange={this.handleTextChange} />

    // 这是文本框内容改变时候的处理函数
    handleTextChange = () => {
        this.setState({
            msg: this.refs.txt.value
        });
    }
```

1. 注意`setState的一个问题`：

```jsx
// 保存最新的state状态值，在保存的时候，是异步地进行保存的，所以，如果想要获取最新的，刚刚保存的那个状态，需要通过回掉函数的形式去获取最新state
this.setState({
    msg: this.refs.txt.value
    // msg: e.target.value
    // 或通过DOM获取
}, function () {
    // 获取最新的state状态值
    console.log(this.state.msg);
});
```

### e.target获取文本框的值

```jsx
<input type="text" style={{ width: '100%' }} value={this.state.msg} onChange={() => this.textChanged()} ref="mytxt" />

  // 响应 文本框 内容改变的处理函数
  // 获取文本框的值
  // 1.通过事件对象e.target.value
  // 2.通过ref属性
  textChanged = () => {
    // console.log(this);
    // console.log(this.refs.mytxt.value);
    this.setState({
      msg: this.refs.mytxt.value
    })
  }
```

### 使用ref获取DOM元素引用

和 Vue 中差不多，vue 为页面上的元素提供了 `ref` 的属性，如果想要获取 元素引用，则需要使用`this.$refs.引用名称`

在 React 中，也有 `ref`, 如果要获取元素的引用`this.refs.引用名称`

## 组件的生命周期

概念：在组件创建、到加载到页面上运行、以及组件被销毁的过程中，总是伴随着各种各样的事件，这些在组件特定时期，触发的事件，统称为组件的生命周期；

### 16.0之前的生命周期

![react16之前的生命周期](E:\Jennifer\other\notes\media\react16之前的生命周期.png)

**第一个是组件初始化(initialization)阶段** 

也就是以下代码中类的构造方法( constructor() ),Test类继承了react Component这个基类，也就继承这个react的 基类，才能有render(),生命周期等方法可以使用，这也说明为什么 函数组件不能使用这些方法 的原因。 

super(props) 用来调用基类的构造方法( constructor() ), 也将父组件的props注入给子组件。 而 constructor() 用来做一些组件的初始化工作，如定义this.state的初始内 容。

```react
import React, { Component } from 'react'; 
class Test extends Component { 
    constructor(props) { super(props); } 
}
```

**第二个是组件的挂载(Mounting)阶段**

此阶段分为componentWillMount，render，componentDidMount三个时期。

- componentWillMount: 

在组件挂载到DOM前调用，且只会被**调用一次**，在这边调用this.setState不会引起组件重新渲染，也可以把写在这边的内容提前到constructor()中，所以项目中很少用。 

- render: 

根据组件的props和state（两者的**重传递和重赋值**，无论值是否有变化，都可以引起组件重新render） ，return 一个React元素，不负责组件实际渲染工作，之后由React自身根据此元素去渲染出页面 DOM。render是纯函数（Pure function：函数的返回结果只依赖于它的参数；函数执行过程里面没有副作用）， 不能在里面执行this.setState，会有改变组件状态的副作用。 

- componentDidMount:

组件挂载到DOM后调用，且只会被**调用一次**

**第三个是组件的更新(update)阶段**

注意：setState引起的state更新或父组件重新render引起的props更 新，更新后的state和props相对之前无论是否有变化，都将引起子组件的重新render。

**造成组件更新有两类（三种）情况：**

1. 父组件重新render

父组件重新render引起子组件重新render的情况有两种

a. 每当父组件重新render导致的重传props，子组件将直接跟着重新渲染，无论props是否有变化。可通 过shouldComponentUpdate方法优化。 

b.在componentWillReceiveProps方法中，将props转换成自己的state

```react
class Child extends Component { 
    constructor(props) { 
        super(props); 
        this.state = { someThings: props.someThings }; 
    }
    componentWillReceiveProps(nextProps) { // 父组件重传props时就会调用这个方法 
        this.setState({someThings: nextProps.someThings}); 
    }
    render() { 
        return <div>{this.state.someThings}</div> 
    } 
}
```

根据官网的描述 

> 在该函数(componentWillReceiveProps)中调用 this.setState() 将不会引起第二次渲染。 

是因为componentWillReceiveProps中判断props是否变化了，若变化了，this.setState将引起state变化，从而引 起render，此时就没必要再做第二次因重传props引起的render了，不然重复做一样的渲染了。 

2. 组件本身调用setState，无论state有没有变化。可通过shouldComponentUpdate方法优化。

**此阶段分为componentWillReceiveProps，shouldComponentUpdate， componentWillUpdate，render，componentDidUpdate**

- componentWillReceiveProps(nextProps) 

此方法只调用于**props引起的组件更新**过程中，参数nextProps是父组件传给当前组件的新props。但父组件render 方法的调用不能保证重传给当前组件的props是有变化的，所以在此方法中根据nextProps和this.props来查明重传 的props是否改变，以及如果改变了要执行啥，比如根据新的props调用this.setState触发当前组件的重新render 

- shouldComponentUpdate(nextProps, nextState) 

此方法通过比较nextProps，nextState及当前组件的this.props，this.state，返回true时当前组件将继续执行更新 过程，返回false则当前组件更新停止，以此可用来减少组件的不必要渲染，优化组件性能。 

ps：这边也可以看出，就算componentWillReceiveProps()中执行了this.setState，更新了state，但在render前 （如shouldComponentUpdate，componentWillUpdate），this.state依然指向更新前的state，不然nextState 及当前组件的this.state的对比就一直是true了。 

- componentWillUpdate(nextProps, nextState) 

此方法在调用render方法前执行，在这边可执行一些组件更新发生前的工作，一般较少用。 

- render 

- componentDidUpdate(prevProps, prevState)

此方法在组件更新后被调用，可以**操作组件更新的DOM**，prevProps和prevState这两个参数指的是组件更新前的 props和state 

**卸载阶段**

- componentWillUnmount 

此方法在组件被卸载前调用，可以在这里执行一些清理工作，比如清楚组件中使用的定时器，清除componentDidMount中手动创建的DOM元素等，以避免引起内存泄漏。

**总结**

组件生命周期的执行顺序：

- Mounting：
  - constructor()
  - componentWillMount()
  - render()
  - componentDidMount()
- Updating：
  - componentWillReceiveProps(nextProps)
  - shouldComponentUpdate(nextProps, nextState)
  - componentWillUpdate(nextProps, nextState)
  - render()
  - componentDidUpdate(prevProps, prevState)
- Unmounting：
  - componentWillUnmount()

**React v16.4** **的生命周期**

![react16.4生命周期](E:\Jennifer\other\notes\media\react16.4生命周期.png)

### 16.4的生命周期

原来（React v16.0前）的生命周期在React v16推出的Fiber之后就不合适了，因为如果要开启async rendering， 在render函数之前的所有函数，都有可能被执行多次。

如果开发者**开了async rendering，而且又在以上这些render前执行的生命周期方法做AJAX请求的话，那AJAX将被 无谓地多次调用**。。。明显不是我们期望的结果。而且在componentWillMount里发起AJAX，不管多快得到结果 也赶不上首次render，而且componentWillMount在服务器端渲染也会被调用到（当然，也许这是预期的结 果），这样的IO操作放在componentDidMount里更合适。 

禁止不能用比劝导开发者不要这样用的效果更好，所以**除了shouldComponentUpdate，其他在render函数之前的 所有函数（componentWillMount，componentWillReceiveProps，componentWillUpdate）都被 getDerivedStateFromProps替代。** 

也就是用一个静态函数getDerivedStateFromProps来取代被deprecate的几个生命周期函数，**就是强制开发者在 render之前只做无副作用的操作，而且能做的操作局限在根据props和state决定新的state** 

React v16.0刚推出的时候，是增加了一个componentDidCatch生命周期函数，这只是一个增量式修改，完全不影 响原有生命周期函数；但是，到了React v16.3，大改动来了，引入了两个新的生命周期函数。 

**getDerivedStateFromProps** 

**static getDerivedStateFromProps(props, state)** 在组件创建时和更新时的render方法之前调用，它应该返回 一个对象来更新状态，或者返回null来不更新任何内容。 

getDerivedStateFromProps 本来（React v16.3中）是只在创建和更新（由父组件引发部分），也就是不是由父 组件引发，那么getDerivedStateFromProps也不会被调用，如自身setState引发或者forceUpdate引发。 在React v16.4中改正了这一点，让getDerivedStateFromProps无论是Mounting还是 Updating，也无论是因为什么引起的Updating，全部都会被调用，具体可看React v16.4 的生命周期图。 

**getSnapshotBeforeUpdate** 

**getSnapshotBeforeUpdate()** 被调用于render之后，**可以读取但无法使用DOM**的时候。它使您的组件可以在可 能更改之前从DOM捕获一些信息（例如滚动位置）。此生命周期返回的任何值都将作为参数传递给 componentDidUpdate（）。 

[React Native 中组件的生命周期](http://www.race604.com/react-native-component-lifecycle/)


![React中组件的生命周期](./images/LifeCycle.png)

### Counter计数器的小案例

封装组件

1. 给组件设置默认启动属性：`static defaultProps = {}`

2. 给属性进行类型校验，需要先运行`cnpm i prop-types --save`，v.15之后单独抽离了这个包

   ```jsx
   import React from 'react'
   import PropTypes from 'prop-types'
   class Counter{
       constructor(props) extends React.Componet{
           super(props)
           this.state = {}
       }
   	static defaultProps = {initCount: 0}
   	// 创建一个propTypes对象，可以给外界传递的属性进行类型校验
   	static propTypes = {initCount: PropTypes.number}
   	render() {
       	return <div>
           </div>
   	}
   }
   ```

### 组件初始化时生命周期事件总结

1. componentWillMount：可以获取props，state和已经定义的函数，相当于Vue的created函数

2. render：创建虚拟DOM

3. componentDidMount：可以获取页面的DOM元素，想要操作DOM最早在这个函数

4. shouldComponentUpdate：必须返回布尔，返回false时虚拟DOM和页面都不会更新，可能会造成画面和组件状态的不一致

   直接通过`this.state`获取的state值是上一次的值，要获取最新的值，要通过参数列表的`nextProps或nextState`获取

5. componentWillUpdate：虚拟DOM和页面上的DOM都是旧的

6. render：创建阶段和运行阶段都有，DOM还没渲染之前可以利用短路运算防止报错

7. 注意：在render函数中，不能调用`setState()`方法

8. componentDidUpdate：DOM都是最新的

9. componentWillReceiveProp：第一次渲染不会触发，`this.props`获取到的是上一次的值，要获取最新的值，要通过参数列表的`nextProps或nextState`获取

## 绑定this并传参的三种方式

1. 在事件中绑定this并传参：

```jsx
// bind可以改变前面函数的this指向，和call/apply不同，call/apply改变this后会执行前面的函数
// bind的第一个参数改变了this指向，后面就是要传递的参数
<input type="button" value="在事件中绑定this并传参" onClick={this.handleMsg1.bind(this, '🍕', '🍟')} />

// 在事件中绑定this并传参
handleMsg1(arg1, arg2) {
    console.log(this);
    // 此时this是个null
    this.setState({
        msg: '在事件中绑定this并传参：' + arg1 + arg2
    });
}
```

1. 在构造函数中绑定this并传参:

```jsx
// 修改构造函数中的代码：
// bind的返回值是改变this之后的函数的引用
// bind不会改变原函数的this指向，要使用改变之后的函数要重新接收
this.handleMsg2 = this.handleMsg2.bind(this, '🚗', '🚚');

<input type="button" value="在构造函数中绑定this并传参" onClick={this.handleMsg2} />

// 在构造函数中绑定this并传参
handleMsg2(arg1, arg2) {
    this.setState({
        msg: '在构造函数中绑定this并传参：' + arg1 + arg2
    });
}
```

1. 用箭头函数绑定this并传参：

```jsx
// 用箭头函数绑定this并传参
<input type="button" value="用箭头函数绑定this并传参" onClick={() => { this.handleMsg3('👩', '👰') }} />

handleMsg3(arg1, arg2) {
    this.setState({
        msg: '用箭头函数绑定this并传参：' + arg1 + arg2
    });
}
```

## 父组件使用Context属性

如果结构过多，参数逐层传递不方便，可以在父组件中直接共享一个Context对象

在父组件定义`getChildContext`方法返回共享数据

规定共享数据的类型：`static childContextTypes = {color: propTypes.string}`

在子组件中校验类型：`static contextType = {color: propTypes.string}`

使用：`this.context.color`

### 相关文章

[类型校验](https://facebook.github.io/react/docs/typechecking-with-proptypes.html)
[Animation Add-Ons](https://reactjs.org/docs/animation.html#high-level-api-reactcsstransitiongroup)

## Hooks

*Hook* 是 React 16.8 的新增特性。它可以让你在不编写 class 的情况下使用 state 以及其他的 React 特性

### 状态钩子 State Hook

```react
import React, { useState } from "react";
export default function HooksTest() { 
    // useState(initialState)，接收初始状态，返回一个由状态和其更新函数组成的数组
    const [fruits, setFruits] = useState(["香蕉", "西瓜"]); 
    return ( 
        <div>
            <p>{fruit === "" ? "请选择喜爱的水果：" : `您的选择是：${fruit}`}</p> 
            {/*添加列表组件*/} 
            <FruitList fruits={fruits} onSetFruit={setFruit}/> 
            {/*添加水果组件*/} 
            <FruitAdd onAddFruit={pname => setFruits([...fruits, pname])} /> 
        </div> 
    ); 
}

// 声明列表组件 
function FruitList({fruits, onSetFruit}) { 
    return ( 
        <ul>{fruits.map(f => ( 
                <li key={f} onClick={() => onSetFruit(f)}> {f} </li>
            ))} 
        </ul> ); 
}

// 声明输入组件 
function FruitAdd(props) { 
    // 输入内容状态及设置内容状态的方法 
    const [pname, setPname] = useState(""); 
    // 键盘事件处理 
    const onAddFruit = e => { 
        if (e.key === "Enter") { 
        	props.onAddFruit(pname); setPname(""); 
        }
    };
    return ( 
        <div> 
            <input type="text" value={pname} onChange={e => setPname(e.target.value)} onKeyDown={onAddFruit} /> 
        </div> ); 
}
```

### 副作用钩子 Effffect Hook

useEffect 给函数组件增加了执行副作用操作的能力。 

副作用（Side Effffect）是指一个 function 做了和本身运算返回值无关的事，比如：修改了全局变量、修改了传入的参数、甚至是 console.log()，所以 ajax 操作，修改 dom 都是算作副作用。

```react
// 异步数据获取，更新HooksTest.js
import { useEffect } from "react"; 
useEffect(()=>{ 
    setTimeout(() => { setFruits(['香蕉','西瓜']) }, 1000); 
},[])
// 设置空数组意为没有依赖，则副作用操作仅执行一次
// 如果副作用操作对某状态有依赖，务必添加依赖选项
// useEffect(() => { document.title = fruit; }, [fruit]);

// 清除工作：有一些副作用是需要清除的，清除工作非常重要的，可以防止引起内存泄露
useEffect(() => { 
    const timer = setInterval(() => { console.log('msg'); }, 1000); 
    return function(){ 
        clearInterval(timer); 
    } 
}, []);
```

### useReducer

[`useState`](https://zh-hans.reactjs.org/docs/hooks-reference.html#usestate) 的替代方案。它接收一个形如 `(state, action) => newState` 的 reducer，并返回当前的 state 以及与其配套的 `dispatch` 方法。（如果你熟悉 Redux 的话，就已经知道它如何工作了。）

在某些场景下，`useReducer` 会比 `useState` 更适用，例如 state 逻辑较复杂且包含多个子值，或者下一个 state 依赖于之前的 state 等。并且，使用 `useReducer` 还能给那些会触发深更新的组件做性能优化，因为[你可以向子组件传递 `dispatch` 而不是回调函数](https://zh-hans.reactjs.org/docs/hooks-faq.html#how-to-avoid-passing-callbacks-down) 。

常用于组件有复杂状态逻辑时，类似于redux中reducer概念。

```react
// 商品列表状态维护
import { useReducer } from "react"; 
// 添加fruit状态维护fruitReducer 
function fruitReducer(state, action) { 
    switch (action.type) { 
        case "init": return action.payload; 
        case "add": return [...state, action.payload]; 
        default: return state; 
    } 
}
export default function HooksTest() { 
    // 组件内的状态不需要了 
    // const [fruits, setFruits] = useState([]); 
    // useReducer(reducer，initState) 
    const [fruits, dispatch] = useReducer(fruitReducer, []); 
    useEffect(() => { 
        setTimeout(() => { 
            // setFruits(["香蕉", "西瓜"]); 
            // 变更状态，派发动作即可 
            dispatch({ type: "init", payload: ["香蕉", "西瓜"] }); 
        }, 1000); 
    }, []); 
    return ( 
        <div> 
            {/*此处修改为派发动作*/} 
            <FruitAdd onAddFruit={pname => dispatch({type: 'add', payload: pname})} /> 
        </div>
    );
}
```

计数器案例：

```react
const initialState = {count: 0};

function reducer(state, action) {
  switch (action.type) {
    case 'increment':
      return {count: state.count + 1};
    case 'decrement':
      return {count: state.count - 1};
    default:
      throw new Error();
  }
}

function Counter() {
  const [state, dispatch] = useReducer(reducer, initialState);
  return (
    <>
      Count: {state.count}
      <button onClick={() => dispatch({type: 'decrement'})}>-</button>
      <button onClick={() => dispatch({type: 'increment'})}>+</button>
    </>
  );
}
```

### useContext

useContext用于在快速在函数组件中导入上下文。

```react
import React, { useContext } from "react"; 
// 创建上下文 
const Context = React.createContext(); 
export default function HooksTest() { 
    // ... 
    return ( 
        {/* 提供上下文的值 */} 
        <Context.Provider value={{fruits,dispatch}}> <div> 
            {/* 这里不再需要给FruitAdd传递状态mutation函数，实现了解耦 */} 
            <FruitAdd /> </div>
        </Context.Provider> 
    ); 
}
function FruitAdd(props) { 
    // 使用useContext获取上下文 
    const {dispatch} = useContext(Context) 
    const onAddFruit = e => { 
        if (e.key === "Enter") { 
            // 直接派发动作修改状态 
            dispatch({ type: "add", payload: pname }) 
            setPname(""); 
        } 
    };
    // ... 
}
```

## Redux

provider：包在最外面

connect：状态映射，合并冲突

reducer：状态对象

状态更新：action

npm i redux react-redux -D

```js
import {createStore} from 'redux'
import {Provider} from 'react-redux'

// 初始化和每次更新状态对象都会执行
function reducer1(state, action) {
    if(!state) {
        // 初始化
    }
    return state
}
// 简写
// 传入旧状态返回新状态
function reducer1(state={xxx}, action) {
    return state
}
// 创建存储对象
const store = createStore(reducer1)
// 用<Provider>包装根组件传入store对象store = {store}
// 使用
import {connect} from 'react-redux'
// export default App
// state来自reducer，props来自组件
// 只能接收不能修改，单向数据流，组件内也不能赋值
export default connect(function(state, props){
    // 混合，解决冲突
    // 使用state，组件props中会包含state的内容
    return state
    return {
        ...state,
        // 会重复的属性使用props
		name: props.name
        // 都进行保留
        name: [state.name, props.name]
    }
}, {
	// 当做组件的一部分，用props访问使用
    // 参数自定义
    setName(name) {
    	// 必须return，返回值为action，在reducer中
        return {
			type: 'set_name',
             name
        }
	}
})(App)
// reducer
function reducer1(state={xxx}, action) {
    if(action.type === 'set_name') {
        return {
            ...state,
            name: action.name
        }
    }
    // 要返回一个新的state
    return state
}

```

优化

```js
// 优化
// 单独的actions.js，找不到时会报错
export const SET_NAME = 'set_name'
// 单独的store.js
// 多个reducer
import {combineReducers} from 'redux'
let reducers = combineReducers({
    user: reducer1,
    comp: reducer2
})
export default createStorer(reducers)
// 修改相应的映射，修改时会触发所有的reducer
// 分模块，分成单独的文件
```

## 路由

react-router-dom

```js
import {BrowserRouter as Router, Route, Link} from 'react-router-dom'
...
```

```jsx
import React from 'react'
// BrowserRouter，以path为键，需要服务器支持，刷新会请求服务器
// HashRouter，以哈希值为键，路由根容器，所有与路由相关的东西都包裹在它里面，一个网站只需要一个
// MemoryRouter，路由信息保存在内存中，刷新后状态不会保留，应用：RN
// Route，表示路由规则，重要的属性path， component
// Link，路由链接，有to属性
// redirect 和link类似也是一个标签，会自动跳转，可以用三目控制
import {HashRouter, Route, Link} from 'react-router-dom'

export default class app extends React.Component{
    constructor(props) {
        super(props)
        this.state = {}
    }
    render() {
        // 使用HashRouter包裹表示使用路由，路径中多了＃，只需要使用一次
        // HashRouter中只能有一个根元素
        return
        <HashRouter>
            <div>
            	<Link to="/home"></h1>
            	<Link to="/movie"></h1>
            	<Link to="/about"></h1>
            </div>
            <hr/>
        	{/* 路由规则以及组件位置占位符 */}
            {/* 默认的路由匹配是模糊匹配，部分匹配也可以成功，加上exact属性表示精确匹配,精确匹配也会从上到下依次匹配 */}
            <Route path="/home" component={Home}></Route>
            {/* 使用:匹配参数 */}
            <Route path="/movie/:type/:id" component={Movie} exact></Route>
            <Route path="/about" component={About}></Route>
        </HashRouter>
    }
}
```

route：表示路由规则，自带三个 render method 和三个 props 。 

`<Route component> `

`<Route render> `

`<Route children> `

```
match
location
history
```

### 路由传参

使用:匹配参数 

`<Route path="/movie/:type/:id" component={Movie} exact></Route>`

获取参数，可以把路由参数保存到state中去，但是参数改变不会让组件销毁重新渲染，需要在componentDidUpdate中更新，由于state，props更新都会update，会导致重复更新，直接使用props更新不会有这个问题

`{this.props.match.params.type}`

```js
componentDidUpdate(old_props, old_state){
    // 判断是否更新
    if (old_state.id === this.props.match.params.id) {
        // 一般是获取数据，更新数据
        this.setState({
            // 设置状态也会导致update
            // props.location.params也行
            id: this.props.match.params.id
        })
    }
}
```

不提供query的传参可以自己解析，一般不会用，会导致页面刷新

### 嵌套路由

在组件中继续添加路由path需要包含父级路由，直接写不好维护，可以使用this.props.match.path

在父级设置默认路由：直接修改path

```jsx
render() {
    const path = this.props.match.path

    return (
        <div>
            {/* 嵌套路由 */}
            <Link to={`${path}/inter`}>国际</Link>
            <Link to={`${path}/society`}>社会</Link>

            <Route path={`${path}/inter`} componet={inter}></Route>
            <Route path={`${path}/society`} componet={society}></Route>
        </div>
	)
}
```

### 应用

通过路由跳转的方式显示模态框，防止刷新关闭，如果还想保存数据，可以写到localstorage里。

问题：跳转时也会请求数据，解决：将数据放到redux中

利用ref获取表单数据

问题：提交数据时如果使用原来的：window.location='xxx'，会导致页面刷新重新访问接口，解决：使用Link，但是处理失败有问题（不能阻止跳转）；使用编程式导航

删除：封装提示框，不用使用路由跳转，使用状态

封装数据通信

### 编程式导航 

需要用到withRouter：`import {withRouter} from 'reacte-router-dom' ... export default withRouter(Component)`

`this.props.hisory.push('')`

### switch组件

```jsx
import {HashRouter, Route, Link, Switch} from 'react=router-dom'

// 表示已经匹配到一个路由的情况下不再继续匹配
<Switch>
    <Route exact path="" component={}></Route>
    <Route exact path="" component={}></Route>
    <Route exact path="" component={}></Route>
</Switch>
```

## AntDesign框架UI

electron使用js，html，css的跨平台桌面应用

1. 运行`npm install antd --save`安装ant design
2. 导入相关组件：

```
import { DatePicker } from 'antd';
```

1. 导入样式：

```
import 'antd/dist/antd.css';
```

### 实现ANT组件的按需加载

1. 运行`cnpm i babel-plugin-import --save-dev`
2. 修改`.babelrc`文件：

```
{
    "presets":["es2015", "stage-0", "react"],
    "plugins":[
        "transform-runtime",
        ["import", { "libraryName": "antd", "style": "css" }]
        ]
}
```

1. 然后只需从 antd 引入模块即可，**无需单独引入样式**。等同于下面手动引入的方式。

### 组件

分页

## Redux

provider：包在最外面

connect：状态映射，合并冲突

reducer：状态对象

状态更新：action

npm i redux react-redux -D

```js
import {createStore} from 'redux'
import {Provider} from 'react-redux'

// 初始化和每次更新状态对象都会执行
function reducer1(state, action) {
    if(!state) {
        // 初始化
    }
    return state
}
// 简写
// 传入旧状态返回新状态
function reducer1(state={xxx}, action) {
    return state
}
// 创建存储对象
const store = createStore(reducer1)
// 用<Provider>包装根组件传入store对象store = {store}
// 使用
import {connect} from 'react-redux'
// export default App
// state来自reducer，props来自组件
// 只能接收不能修改，单向数据流，组件内也不能赋值
export default connect(function(state, props){
    // 混合，解决冲突
    // 使用state，组件props中会包含state的内容
    return state
    return {
        ...state,
        // 会重复的属性使用props
		name: props.name
        // 都进行保留
        name: [state.name, props.name]
    }
}, {
	// 当做组件的一部分，用props访问使用
    // 参数自定义
    setName(name) {
    	// 必须return，返回值为action，在reducer中
        return {
			type: 'set_name',
            name
        }
	}
})(App)
// reducer
function reducer1(state={xxx}, action) {
    if(action.type === 'set_name') {
        return {
            ...state,
            name: action.name
        }
    }
    // 要返回一个新的state
    return state
}
// 优化
// 单独的actions.js，找不到时会报错
export const SET_NAME = 'set_name'
// 单独的store.js
// 多个reducer
import {combineReducers} from 'redux'
let reducers = combineReducers({
    user: reducer1,
    comp: reducer2
})
export default createStorer(reducers)
// 修改相应的映射，修改时会触发所有的reducer
// 分模块，分成单独的文件

```

基本思想：单向数据流

state-》（component）props-》action-》state

## React-Server

# 豆瓣电影案例

## Node.js设置跨域

```js
app.use('*', function (req, res, next) {
	// 设置请求头为允许跨域
    res.header("Access-Control-Allow-Origin", "*");
    // 设置服务器支持的所有头信息字段
    res.header("Access-Control-Allow-Headers", "Content-Type,Content-Length, Authorization, Accept,X-Requested-With");
    // 设置服务器支持的所有跨域请求的方法
    res.header("Access-Control-Allow-Methods", "POST,GET");
    // next()方法表示进入下一个路由
    next();
});
```

## ES6基于Promise的fetch使用

受跨域限制

```js
fetch('')
    // 第一个then中获取不到数据，得到response对象，可以通过res.json()返回一个promise对象
    .then(res => {
    return res.json()
	})
 	// 第二个then返回的data就是获得的数据
    .then(data => {
    console.log(data)
})
```

## 第三方fetch-jsonp

和fetch使用是一样的

```js
import fetchJSONP from 'fetch-jsonp'
fetchJSONP('')
    // 第一个then中获取不到数据，得到response对象，可以通过res.json()返回一个promise对象
    .then(res => {
    return res.json()
	})
 	// 第二个then返回的data就是获得的数据
    .then(data => {
    console.log(data)
})
```

## react-router-dom路由跳转

- HashRouter：是一个路由的跟容器，一个应用程序中，一般只需要唯一的一个HashRouter容器即可！将来，所有的Route和Link都要在HashRouter中进行使用

- 注意：HashRouter中，只能有唯一的一个子元素

- Link：是相当于超链接一般的存在；点击Link，跳转到相应的路由页面！负责进行路由地址的切换！
- Route：是路由匹配规则，当路由地址发生切换的时候，就会来匹配这些定义好的Route规则，如果有能匹配到的路由规则，那么，就会展示当前路由规则所对应的页面！
- Route：除了是一个匹配规则之外，还是一个占位符，将来，此Route所匹配到的组件页面，将会展示到Route所在的这个位置！

```
// 其中path指定了路由匹配规则，component指定了当前规则所对应的组件
<Route path="" component={}></Route>
```

- 注意：react-router中的路由匹配，是进行模糊匹配的！可以通过`Route`身上的`exact`属性，来表示当前的`Route`是进行精确匹配的
- 可以使用`Redirect`实现路由重定向

```
    // 导入路由组件
    import {Route, Link, Redirect} from 'react-router-dom'
    <Redirect to="/movie/in_theaters"></Redirect>
```

## 相关文章

- [ANT DESIGN 一个 UI 设计语言](https://ant.design/index-cn)
- [react-router-dom](https://reacttraining.com/react-router/web/guides/quick-start)
- [豆瓣电影API地址](https://developers.douban.com/wiki/?title=api_v2)

- [正在热映 - in_theaters](https://api.douban.com/v2/movie/in_theaters)
- [即将上映 - coming_soon](https://api.douban.com/v2/movie/coming_soon)
- [top250](https://api.douban.com/v2/movie/top250)
- [电影详细信息 - subject](https://api.douban.com/v2/movie/subject/26309788)

- [跨域资源共享 CORS 详解 - 阮一峰](http://www.ruanyifeng.com/blog/2016/04/cors.html)
- [Request - Simplified HTTP client](https://github.com/request/request)
- [CSS3 transform 属性](http://www.w3school.com.cn/cssref/pr_transform.asp)
- [ES6 - Promise规范 - 阮一峰](http://es6.ruanyifeng.com/#docs/promise)
- [刘龙彬 - 博客园 - Javascript中Promise的简单使用](http://www.cnblogs.com/liulongbinblogs/p/6731288.html)
- [Javascript 中的神器——Promise](http://www.jianshu.com/p/063f7e490e9a)
- [MDN - Fetch API](https://developer.mozilla.org/zh-CN/docs/Web/API/Fetch_API)
- [MDN - Response](https://developer.mozilla.org/zh-CN/docs/Web/API/Response)
- [fetch-jsonp - 支持JSONP的Fetch实现](https://www.npmjs.com/package/fetch-jsonp)

- http://blog.csdn.net/u013531824/article/details/51003775)