# React.js

声明式，组件化，一次学习随处编写

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

  ![Diff算法图](../media/Diff.png)

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

特点：只有一个依赖，不需要配置，可自定义

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