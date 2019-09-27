# Webpack

## 概述

### 常见的静态资源

- JS
  - .js  .jsx  .coffee（需要编译）  .ts（TypeScript  类 C# 语言，需要编译）
- CSS
  - .css  .less   .sass  .scss
- Images
  - .jpg   .png   .gif   .bmp   .svg
- 字体文件（Fonts）
  - .svg   .ttf   .eot   .woff   .woff2
- 模板文件
  - .ejs   .jade  .vue

### 引入的静态资源多的问题

1. 网页加载速度慢， 因为 我们要发起很多的二次请求；
2. 要处理错综复杂的依赖关系

### 解决上述两个问题

1. 合并、压缩、精灵图、图片的Base64编码（将图片编码和代码一起下载存储到客户端减少请求）
2. 可以使用webpack可以解决各个包之间的复杂依赖关系；

### 如何实现上述2种解决方案

1. 使用Gulp， 是基于 task 任务的；
2. 使用Webpack， 是基于整个项目进行构建的；

-   借助于webpack这个前端自动化构建工具，可以完美实现资源的合并、打包、压缩、混淆等诸多功能。
- 根据官网的图片介绍webpack打包的过程
- [webpack官网](http://webpack.github.io/)

### webpack

webpack 是前端的一个项目构建工具，它是基于 Node.js 开发出来的一个前端工具；

可以代码转换，文件优化，代码分割，模块合并，自动刷新，代码校验，自动发布

#### 安装的两种方式

1. 运行`npm i webpack -g`全局安装webpack，这样就能在全局使用webpack的命令
2. 在项目根目录中运行`npm i webpack webpack-cli --save-dev`安装到项目开发依赖中
3. `npx webpack`运行，5.2支持，默认找node_module中bin中的webpack.cmd文件执行，执行过程中用到webpack-cli，cli会查找配置文件

#### 0配置

打包：支持js的模块化（require）

## 使用webpack打包构建

列表隔行变色案例

1. 运行`npm init`初始化项目，使用npm管理项目中的依赖包
2. 创建项目基本的目录结构
3. 使用`cnpm i jquery --save`安装jquery类库
4. 创建`main.js`并书写各行变色的代码逻辑：

```javascript
// 导入jquery类库
import $ from 'jquery'

// 设置偶数行背景色，索引从0开始，0是偶数
$('#list li:even').css('backgroundColor','lightblue');
// 设置奇数行背景色
$('#list li:odd').css('backgroundColor','pink');
```

1. 直接在页面上引用`main.js`会报错，因为浏览器不认识`import`这种高级的JS语法，需要使用webpack进行处理，webpack默认会把这种高级的语法转换为低级的浏览器能识别的语法；
2. 运行`webpack 入口文件路径 输出文件路径`对`main.js`进行处理：

```
webpack src/js/main.js dist/bundle.js
```

### `webpack.config.js`配置文件

1. 在项目根目录中创建`webpack.config.js`
2. 由于运行webpack命令的时候，webpack需要指定入口文件和输出文件的路径，所以，我们需要在`webpack.config.js`中配置这两个路径：

#### entry和output

**基本配置**：

```javascript
// webpack是基于node的
// 导入处理路径的模块
let path = require('path');

// 导出一个配置对象，将来webpack在启动的时候，会默认来查找webpack.config.js或者webpackfile.js（cli的config-yargs中判断），并读取这个文件中导出的配置对象，来进行打包处理
module.exports = {
	// production(默认) development
	mode: 'development',
    entry: path.resolve(__dirname, 'src/js/main.js'), // 项目入口文件，默认./src/index.js
    output: { // 配置输出选项
        path: path.resolve(__dirname, 'dist'), // 配置输出的路径
        filename: 'bundle.js' // 配置输出的文件名，默认main.js
    }
}
```

**两种形式**：导出对象（上例），导出函数

```js
modile.exports = function(env, argv) {
    // env:环境对象,scripts中可以设置
    env = env || {} 
    return {
        // 通用的设置    
    }
}
```

**打包结果**：由`console.log('hello')`打包

```js
(function (modules) { // webpackBootstrap 启动函数
	// The module cache  定义一个缓存
	var installedModules = {}; // "./src/index.js": 对象

	// The require function 实现了require
	function __webpack_require__(moduleId) {

		// Check if module is in cache 检查是否缓存过
		if (installedModules[moduleId]) {
			return installedModules[moduleId].exports;
		}
		// Create a new module (and put it into the cache) 
		var module = installedModules[moduleId] = {
			i: moduleId,
			l: false,
			exports: {}
		};

		// Execute the module function
		modules[moduleId].call(module.exports, module, module.exports, __webpack_require__);

		// Flag the module as loaded
		module.l = true;

		// Return the exports of the module
		return module.exports;

	}

	// expose the modules object (__webpack_modules__)
	__webpack_require__.m = modules;

	// expose the module cache
	__webpack_require__.c = installedModules;

	// define getter function for harmony exports
	__webpack_require__.d = function (exports, name, getter) {
		if (!__webpack_require__.o(exports, name)) {
			Object.defineProperty(exports, name, { enumerable: true, get: getter });

		}

	};

	// define __esModule on exports
	__webpack_require__.r = function (exports) {
		if (typeof Symbol !== 'undefined' && Symbol.toStringTag) {
			Object.defineProperty(exports, Symbol.toStringTag, { value: 'Module' });

		}
		Object.defineProperty(exports, '__esModule', { value: true });

	};

	__webpack_require__.t = function (value, mode) {
		if (mode & 1) value = __webpack_require__(value);
		if (mode & 8) return value;
		if ((mode & 4) && typeof value === 'object' && value && value.__esModule) return value;
		var ns = Object.create(null);
		__webpack_require__.r(ns);
		Object.defineProperty(ns, 'default', { enumerable: true, value: value });
		if (mode & 2 && typeof value != 'string') for (var key in value) __webpack_require__.d(ns, key, function (key) { return value[key]; }.bind(null, key));
		return ns;

	};

	// getDefaultExport function for compatibility with non-harmony modules
	__webpack_require__.n = function (module) {
		var getter = module && module.__esModule ?
			function getDefault() { return module['default']; } :
			function getModuleExports() { return module; };
		__webpack_require__.d(getter, 'a', getter);
		return getter;

	};

	// Object.prototype.hasOwnProperty.call
	__webpack_require__.o = function (object, property) { return Object.prototype.hasOwnProperty.call(object, property); };

	// __webpack_public_path__
	__webpack_require__.p = "";


	// Load entry module and return exports 调用require
	return __webpack_require__(__webpack_require__.s = "./src/index.js"); // 入口模块

})
	({
		// 传入到webpack启动函数中的参数
		"./src/index.js": // 模块路径
			(function (module, exports) { // 函数
				eval("console.log('hello')\n\n//# sourceURL=webpack:///./src/index.js?");
			})
	});
```

**手动指定配置文件**：

直接执行：`npx webpack --config webpack.config.my.js`

可以通过脚本配置

```json
"scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "build": "webpack --config webpack.config.js"
},
```

在命令行传参：`npm run build -- --config webpack.config.my.js // --后面会当做字符串`

**多入口**  ：

```js
var path = require('path');
const HtmlWebpackPlugin = reuqire('html-webpack-plugin')

module.exports = {
    entry: {
        'index': path.resolve(__dirname, 'src/js/main.js'),
        'admin': path.resolve(__dirname, 'src/js/admin.js')
    },
    output: { // 配置输出选项
        path: path.resolve(__dirname, 'build'), // 配置输出的路径
        filename: '[name].min.js' // name对应上面的名称index和admin
    },
    plugins: [
        new HtmlWebpackPlugin({
            template: './src/index.html',
            filename: 'home.html',
            chunks: ['home']
        }),
        new HtmlWebpackPlugin({
            template: './src/index.html',
            filename: 'other.html',
            chunks: ['other']
        })
    ]
}
```

#### mode

 none|development|production：优化级别的区别

### loader

预处理js以外的文件

#### 使用webpack打包css文件

webpack不能处理js以外的文件，会去配置文件查找第三方loader进行匹配，然后调用loader处理文件，注意：**从右到左**依次处理。处理完成后交给webpack打包合并，最后输出到bundle.js中

1. 运行`cnpm i style-loader css-loader --save-dev`
2. 修改`webpack.config.js`这个配置文件：

```javascript
module: { // 用来配置第三方loader模块的
    rules: [ // 文件的匹配规则，从右到左依次处理
	    // loader功能单一，可以叠加使用
        // css-loader： 加载css文件，成为js的一部分（读取成字符串），可以解析@import这种语法
        // style-loader： 使css有作用，让样式字符串变成style标签输出到页面，header标签的最后，可能会覆盖之前的样式
        // 一个loader写成字符串，顺序：从右向左，从下到上
        // { test: /\.css$/, use: ['style-loader', 'css-loader'] }//处理css文件的规则
        // 对象形式：可以传多个参数
        { test: /\.css$/, use: [{
        	loader: 'style-loader',
        	options: {
                // 让样式字符串变成style标签输出到页面，header标签的顶部，不会覆盖自定义样式
                insertAt: 'top'
            }
        }, 'css-loader'] }
    ]
}
```

1. 注意：`use`表示使用哪些模块来处理`test`所匹配到的文件；`use`中相关loader模块的调用顺序是从后向前调用的；

#### 打包less文件-less-loader

1. 运行`cnpm i less-loader less -D`
2. 修改`webpack.config.js`这个配置文件：

```
// less自带postcss的功能
{ test: /\.less$/, use: ['style-loader', 'css-loader', 'less-loader'] }
```

#### 打包sass文件-url-loader

1. 运行`cnpm i sass-loader node-sass --save-dev`
2. 在`webpack.config.js`中添加处理sass文件的loader模块：

```
{ test: /\.scss$/, use: ['style-loader', 'css-loader', 'sass-loader'] }
```

#### file-loader

加载任何类型文件，并形成一个文件模块

```js
{ test: /\.(png|jpg|gif|jpeg|bmp)$/i, use: {
    loader: 'file-loader',
    options: {
        // 会在打包目录新建这个目录
		outputPath: 'images/'
    }
}},
```

#### 处理图片

1. js中创建图片：import或者require

   file-loader在内部生成一张图片，返回名字

2. css中引入background

   file-loader也可以处理

3. html中的img

   html-withimg-loader

#### 处理css中的路径-url-loader

根据限制读取并输出成base64（减少请求但是图片大小会增大原来的三分之一）

1. 运行`cnpm i url-loader file-loader --save-dev`
2. 在`webpack.config.js`中添加处理url路径的loader模块：

```
{ test: /\.(png|jpg|gif|jpeg|bmp)$/, use: 'url-loader' } // file-loader是url-loader内部依赖，这里不需要配置
```

1. 可以通过`limit`指定进行base64编码的图片大小；只有小于指定字节（byte）的图片才会进行base64编码；
2. `[hash:8]-[name].[ext]`可以对图片的名称进行规定：

```javascript
{ test: /\.(png|jpg|gif|jpeg|bmp)$/, use: 'url-loader?limit=43960&[path]-[name].[ext]'},
// 另一种写法    
{ test: /\.(png|jpg|gif|jpeg|bmp)$/, use: {
    loader: 'url-loader',
    options: {
        outputPath: 'images/',
        // 小于这个大小会进行base64编码直接写到css文件，否则使用file-loader产生真实文件
        limit: 43960,
	    name: '[hash:8]-[name].[ext]'
    }
},
```

注意：引入时的node_models可以省略

1. 处理字体文件

```javascript
{ test: /\.(ttf|eot|svg|woff|woff2)$/, use: 'url-loader'},
```

#### postcss-loader和autoprefixer

用于添加css前缀

postcss-loader：加载css并解析样式

autoprefixer：根据浏览器兼容表添加前缀

```js
{ test: /\.css$/, use: ['style-loader', 'css-loader', 'postcss-loader'] } // 配置less时加在css-loader的后面
// postcss.config.js文件，也可以写在webpack.config.js中postcss-loader的options里，要配置alias
module.exports = {
    plugins: [
        require('autoprefixer')
    ]
}

// 注意！！！如果以上配置不起作用
module.exports = {
    plugins: [
        require('autoprefixer')({
            // 必须设置支持的浏览器才会自动添加添加浏览器兼容
            "overrideBrowserslist": [
                "defaults",
                "not ie < 11",
                "last 2 versions",
                "> 1%",
                "iOS 7",
                "last 3 iOS versions"
            ]
        })
    ]
}
```

注意：在`import {xx, xx} from xx`时只是解构赋值不会按需导入，按需导入是`import xx from xx`，除非使用有简写功能的loader

#### 处理 JS语法-babel-loader

将高版本js转换为低版本

1. 运行`cnpm i babel-loader @babel/core --save-dev`安装babel的相关loader包

2. 运行`cnpm i @babel/preset-env --save-dev`安装babel转换的语法

3. 在`webpack.config.js`中添加相关loader模块，其中需要注意的是，一定要把`node_modules`文件夹添加到排除项：

```js
{ test: /\.js$/, use: {
	loader: 'babel-loader',
	options: {
		presets: [
            '@babel/preset-env'
        ]
	}
}, exclude: /node_modules/ }
```

1. presets的配置也可以在项目根目录中添加`.babelrc`文件，并修改这个配置文件如下：

```
{
    "presets":["@babel/preset-env"]
}
```

##### source-map

参考：<https://www.cnblogs.com/tugenhua0707/p/9464984.html>

**eval** 会将每一个module模块，执行eval，执行后不会生成sourcemap文件，仅仅是在每一个模块后，增加sourceURL来关联模块处理前后对应的关系。

**优点是：**打包速度非常快，因为不需要生成sourcemap文件。
**缺点是：**由于会映射到转换后的代码，而不是映射到原始代码，所以不能正确的显示行数。

**source-map** 在webpack中配置加上 devtool: 'source-map' 配置完成后，source-map会为每一个打包后的模块生成独立的sourcemap文件

**inline（比如 inline-source-map）** 该属性不会生成独立的 .map文件，而是将 .map文件以dataURL的形式插入。

**缺点：**它会使得bundle.js文件变得非常大，因为它需要把 sourceMappingURL 以dataurl的形式插入到bundle.js里面去。

**cheap(如：cheap-source-map)** 该属性在打包后同样会为每一个文件模块生成 .map文件，但是与source-map的区别在于cheap生成的 map文件会忽略原始代码中的列信息

使用cheap属性后，也不会有loader模块之间对应的sourcemap，因为webpack打包最终会将所有的非js资源，通过loader形式转换成js资源，比如 vue 中的文件，xx.vue -> vue-loader转换 -> js -> 压缩 -> 压缩后的js

所以说如果没有loader之间的sourcemap文件的话，那么在debug的时候，定义到压缩前的js中的时候，不能跟踪到vue中。

**module(如：cheap-module-source-map)** 该属性的配置也是生成一个没有列的信息的sourceMaps文件，同时loader的sourcemap也被简化成为只包含对应行的。

```js
// webpack.config.js
// 可以直接使用 SourceMapDevToolPlugin/EvalSourceMapDevToolPlugin 来替代使用 devtool 选项，它有更多的选项。切勿同时使用 devtool 选项和 SourceMapDevToolPlugin/EvalSourceMapDevToolPlugin 插件。
// source-map源码映射，单独生成一个文件，编译报错时可以查看原始写法，但是js会很大
devtool: 'source-map'
// eval-source-map源码映射，不会单独生成一个文件，打包到打包文件中，报错会显示行列
devtool: 'eval-source-map'
// cheap-module-source-map源码映射，单独生成一个文件，不会显示列
devtool: 'cheap-module-source-map'
// cheap-module-eval-source-map源码映射，不会单独生成一个文件，不会显示列
devtool: 'cheap-module-eval-source-map'
```

**开发环境和线上环境如何选择**

**1. 源代码中的列信息是没有任何作用，因此我们打包后的文件不希望包含列相关信息，只有行信息能建立打包前后的依赖关系。因此不管是开发环境或生产环境，我们都希望添加cheap的基本类型来忽略打包前后的列信息。**

**2. 不管是开发环境还是正式环境，我们都希望能定位到bug的源代码具体的位置，比如说某个vue文件报错了，我们希望能定位到具体的vue文件，因此我们也需要module配置。**

**3. 我们需要生成map文件的形式，因此我们需要增加 source-map属性。**

**4. 我们介绍了eval打包代码的时候，知道eval打包后的速度非常快，因为它不生成map文件，但是可以对eval组合使用 eval-source-map使用会将map文件以DataURL的形式存在打包后的js文件中，比如如下：**

![img](https://images2018.cnblogs.com/blog/561794/201808/561794-20180812212332038-199268065.png)

它的效果类似于inline的效果，因此在正式环境中不要使用 eval-source-map, 因为它会增加文件的大小，但是在开发环境中，可以试用下，因为他们打包的速度很快。

**在开发环境中我们可以使用** 

```
module.exports = {
  devtool: 'cheap-module-eval-source-map'
}
```

**在正式环境中我们可以使用**  

```
module.exports = { 
  devtool: 'cheap-module-source-map';
}
```

##### ES7的语法不支持

比如class的属性

1. 添加提案中语法，安装 `@babel/plugin-proposal-class-properties`
2. 在`webpack.config.js`中

```js
{ test: /\.js$/, use: {
	loader: 'babel-loader',
	options: {
		presets: [
            '@babel/preset-env'
         ],
         plugins: [
            '@babel/plugin-proposal-class-properties'
         ]
	}
}, exclude: /node_modules/ }
```

有不支持的语法时会报错提示，按照提示去babel官网寻找配置，比如装饰器@xxx

##### 存在重复的公共校验，generator或promise等会报错

需要代码运行时的包：@babel/plugin-transform-runtime @babel/runtime(上线后也需要：--save)

##### 实例上的高级方法不支持

**！！已弃用↓**

@babel/polyfill(--save) 

在代码中引入：`require('@babel/polyfill')`

**！！已弃用↑**

<https://babeljs.io/docs/en/babel-plugin-transform-runtime#docsNav>

### 代码质量-eslint

 `npm i eslint eslint-loader -D`

```js
module: {
    rules: [
        {
            test: /\.js$/,
            // loader: 'eslint-loader',
            use: {
                loader: 'eslint-loader',
                options: {
                	// 强制在普通loader之前执行
                	enforce: 'pre' // post
                }
            }
            exclude: /node_modules/
        }
    ]
}
```

.eslintrc配置文件，在官网配置下载配置文件，或者`eslint --init` 可以初始化

```js
{
    // 解析
    "parserOptions": {
        // 版本
        "ecmaVersion": 6,
        "sourceType": "module",
        // 某些特性是否启用
        "ecmaFeatures": {
            "jsx": true
        }
    },
    "rules": {
        "indent": ["error", 2],
        // Unix格式的换行/n
        "linebreak-style": ["error", "windows"], // /r/n
        // 双引号
        "quotes": ["error", "double"]
        // 结尾的分号
        "semi": ["error", "always"]
    }
}
```

### 全局变量引入

1. 引入jquery，安装，引入，引入后不会暴露在window中

   `import $ from 'jquery'; $; // 有 window.$ // 没有`

   **expose-loader** // 全局的loader。其他的还有pre前置loader，normal普通loader，内联loader，post后置loader

   安装loader

   `import $ from 'expose-loader?$!jquery'`

   或者在配置文件中配置

```js
rules: [
    {
        test: require.resolve('jquery'),
    	use: 'expose-loader?$'
    }
]
```

2. 不引入不通过window直接使用$：给每个模块注入$（注释掉之前的配置）

 ```js
let webpack = require('webpack')
...
plugins: [
    new webpack.ProvidePlugin: ({
    	$: 'jquery'
    })
]
 ```

3. 通过cnd引入的jquery

   可以直接使用window.$或$

   可以配置忽略防止重复引入

```js
externals: {
	jquery: "$"
}
```

   

### 测试

#### 单元测试

jest

`npm i jest jest-webpack -D`

package.json

```js
"scripts": {
    ...
    "test": "jest-webpack"
}
```

测试用例

 ```js
const mod = require('xxx')

test('testName', () => {
    expect(mod.fab(7)).toBe(13)
})
 ```



## 相关文章

[babel-preset-env：你需要的唯一Babel插件](https://segmentfault.com/p/1210000008466178)

## webpack的发布策略 

1. 在实际开发中，一般会有两套项目方案：

- 一套是开发期间的项目，包含了测试文件、测试数据、开发工具、测试工具等相关配置，有利于项目的开发和测试，但是这些文件仅用于开发，发布项目时候需要剔除；
- 另一套是部署期间的项目，剔除了那些客户用不到的测试数据测试工具和文件，比较纯净，减少了项目发布后的体积，有利于安装和部署！

1. 为了满足我们的发布策略，需要新建一个配置文件，命名为`webpack.publish.config.js`，将`webpack.config.js`的配置拷贝过去，剔除一些开发配置项即可：

- 将`devServer`节点删掉：

```
 devServer: {
        hot: true,
        open: true,
        port: 4321
    }
```

- 将`plugins`节点下的热更新插件删掉：

```
 new webpack.HotModuleReplacementPlugin()
```

1. 修改`url-loader`，将图片放入统一的images文件夹之下：

```
{ test: /\.(png|jpg|gif)$/, use: 'url-loader?limit=43959&name=images/[name].[ext]' }
```

或者使用`img-`前缀加上`7位的hash名称`：

```
{ test: /\.(png|jpg|gif)$/, use: 'url-loader?limit=43959&name=images/img-[hash:7].[ext]' }
```

1. 在`package.json`中的script节点下新增`dev`命令，通过`--config`指定webpack启动时要读取的配置文件：

```
"pub": "webpack --config webpack.publish.config.js"
```

## 插件

### `webpack-dev-server`实时构建

1. 由于每次重新修改代码之后，都需要手动运行webpack打包的命令，比较麻烦，所以使用`webpack-dev-server`来实现代码实时打包编译，当修改代码之后，会自动进行打包构建。
2. 运行`cnpm i webpack-dev-server --save-dev`安装到开发依赖
3. `webpack-dev-server`依赖`webpack和webpack-cli`，需要在本地安装
4. mode要是development
5. 安装完成之后，在命令行直接运行`npx webpack-dev-server`来进行打包

- 还可以使用`package.json`文件中的指令，来进行运行`webpack-dev-server`命令，在`scripts`节点下新增`"dev": "webpack-dev-server"`指令后使用`npm run dev`可以进行实时打包，但是dist目录下并没有生成`bundle.js`文件，这是因为`webpack-dev-server`将打包好的文件放在了内存中
- 把`bundle.js`放在内存中的好处是：由于需要实时打包编译，所以放在内存中速度会非常快
- 这个时候访问webpack-dev-server启动的`http://localhost:8080/`网站，发现是一个文件夹的面板，需要点击到src目录下，才能打开我们的index首页，此时引用不到bundle.js文件，需要修改index.html中script的src属性为:`<script src="../bundle.js"></script>`
- 为了能在访问`http://localhost:8080/`的时候直接访问到index首页，可以使用`--contentBase src`指令来修改dev指令，指定启动的根目录：

```
 "dev": "webpack-dev-server --contentBase src" // 将index和bundle都配置到内存后就不需要设置contentBase了
```

 	或者在webpack.config.js中添加配置

```json
module.exports = {
	// 开发服务器配置，webpack-dev-server
	devServer: {
		port: 3000,
		// 显示进度条
		progress: true,
		// 从dist目录开始执行
		contentBase: "./dist"
        // 压缩
        compress: true
	},
	...
}
```

同时修改index页面中script的src属性为`<script src="bundle.js"></script>`

#### 常用命令参数

**注意：**`package.json`JSON文件中不能写注释

方式1：

- 修改`package.json`的script节点如下，其中`--open`表示自动打开浏览器，`--port 4321`表示打开的端口号为4321，`--hot`表示启用浏览器热更新，只更新改动过的模块，保存后修改部分代码更新，不使用会全部更新，无刷新重载：

```
"dev": "webpack-dev-server --hot --port 4321 --open"
```

方式2：

1. 修改`webpack.config.js`文件，新增`devServer`节点如下：

```
devServer:{
        hot: true,
        open: true,
        port: 4321,
        contentBase: 'src'
}
```

1. 要启用热更新还要在头部引入`webpack`模块：

```
var webpack = require('webpack');
```

1. 在`plugins`节点下新增：

```
plugins: [
	new webpack.NamedModulesPlugin(), // 打印更新的模块
	new webpack.HotModuleReplacementPlugin() // 热更新插件 
]
```

​	这样配置过后页面是强制更新会刷新页面，可以使用require改为热更新

```js
// index.js
if(module.hot) {
    // 指定文件更新时的回调
    module.hot.accept('./source', () => {
        require('./source')
    })
}
```



### html-webpack-plugin`配置index页面

由于使用`--contentBase`指令的过程比较繁琐，需要指定启动的目录，同时还需要修改index.html中script标签的src属性，所以推荐大家使用`html-webpack-plugin`插件配置启动页面.

作用：在内存中生成index.html页面，并自动引用

1. 运行`cnpm i html-webpack-plugin --save-dev`安装到开发依赖
2. 修改`webpack.config.js`配置文件如下：

```javascript
// 导入处理路径的模块
var path = require('path');
// 导入自动生成HTMl文件的插件
var HtmlWebpackPlugin = require('html-webpack-plugin');
module.exports = {
    ...
    plugins:
		new HtmlWebpackPlugin({
			// 指定模板
			template: './src/index.html',
			// 打包后的名字
			filename: 'index.html',
			// 压缩html
			minify: {
				// 删除双引号
				removeAttributeQuotes: true,
				// 折叠空行
				collapseWhitespace: true

			},
			// 增加hash戳
			hash: true
		})
	]
}
```

1. 修改`package.json`中`script`节点中的dev指令如下：

```
"dev": "webpack-dev-server"
```

1. 将index.html中script标签注释掉，因为`html-webpack-plugin`插件会自动把bundle.js注入到index.html页面中！

### clean-webpack-plugin

每次重新构建时候删除dist目录

1. 运行`npm i clean-webpack-plugin --save-dev`
2. 在头部引入这个插件：

```
var {cleanWebpackPlugin} = require('clean-webpack-plugin')
```

1. 在`plugins`节点下使用这个插件：

```
new cleanWebpackPlugin()
```

### copy-webpack-plugin

将一些数据信息和代码打包到一起

1. 运行`npm i copy-webpack-plugin --save-dev`
2. 在头部引入这个插件：

```
var copyWebpackPlugin = require('copy-webpack-plugin')
```

1. 在`plugins`节点下使用这个插件：

```
new copyWebpackPlugin([{from: './doc', to: './'}])
```

### banner-plugin

内置，版权说明插件

1. 在头部引入webpack：

```
var webpack = require('webpack')
```

1. 在`plugins`节点下使用这个插件：

```
new webpack.BannerPlugin('make 2019') // 打包到打包结果头部
```

### 分离第三方包改造`webpack.publish.config.js`

1. 改造entry节点如下：

```js
entry: {
        app: path.resolve(__dirname, 'src/js/main.js'), // 自己代码的入口
        vendors: ['jquery'] // 要分离的第三方包的入口
    }
```

1. 在plugins节点下新增插件：

```js
new webpack.optimize.CommonsChunkPlugin({ // 抽离第三方包的插件
        name:'vendors', // 指定抽离第三方包的入口名称
        filename:'vendors.js' // 抽离出的公共模块的名称
})
```

1. `html-webpack-plugin`在生成`index.html`文件的时候，会自动将抽离的第三方包引入进去！

### [优化压缩JS](https://webpack.js.org/configuration/plugins/#plugins)

在plugins数组中添加：

```js
new webpack.optimize.UglifyJsPlugin({ // 优化压缩JS
    compress:{ // 配置压缩选项
        warnings:false // 移除警告
    }
}),
new webpack.DefinePlugin({ // 设置为产品上线环境，进一步压缩JS代码
    'process.env.NODE_ENV': '"production"'
})
```

### 优化压缩HTML文件

在`plugins`节点下的`htmlWebpackPlugin`插件中，添加`minify`子节点：

```js
minify:{// 压缩HTML代码
    collapseWhitespace:true, // 合并空白字符
    removeComments:true, // 移除注释
    removeAttributeQuotes:true // 移除属性上的引号
}
```

其他优化项请参考：[html-minifier - github](https://github.com/kangax/html-minifier#options-quick-reference)

### [抽取CSS文件](https://github.com/webpack-contrib/extract-text-webpack-plugin)

默认的打包css都在页面的style标签中

**已废弃↓**

####  extract-text-webpack-plugin

1. 运行`npm install --save-dev extract-text-webpack-plugin`安装抽取CSS文件的插件。
2. 在配置文件中导入插件：

```
const ExtractTextPlugin = require("extract-text-webpack-plugin");
```

1. 修改CSS和Sass的loader如下：

```js
{
    test: /\.css$/, use: ExtractTextPlugin.extract({
        fallback: "style-loader",
        use: ["css-loader"],
        publicPath: '../' // 抽取时自动给路径加上../设置图片路径
    })
},
{
    test: /\.scss$/, use: ExtractTextPlugin.extract({
        fallback: "style-loader",
        use: ['css-loader', 'sass-loader'],
        publicPath: '../' // 设置图片路径
    })
}
```

1. 在plugins节点下新增插件：

```
new ExtractTextPlugin("css/styles.css"), // 抽取CSS文件的插件
```

**已废弃↑**

#### mini-css-extract-plugin

webpack4使用

1. 运行`npm install --save-dev mini-css-extract-plugin`安装抽取CSS文件的插件。
2. 修改`webpack.config.js`配置文件如下：

```javascript
// 导入处理路径的模块
const path = require('path');
// 导入抽取css文件的插件
const MiniCssExtractPlugin = require('mini-css-extract-plugin');
// 可以使用多个
const LessMiniCssExtractPlugin = require('mini-css-extract-plugin');
module.exports = {
    ...
    // 将style-loader改为MiniCssExtractPlugin.loader
    rules: [
        { test: /\.css$/, use: [
            MiniCssExtractPlugin.loader,
            'css-loader'] }
        ...
    ]
    plugins:
		new MiniCssExtractPlugin({
			// 打包后的名字
			filename: 'main.css',
	]
}
```

#####  压缩css

参考npm文档

1. 安装optimize-css-assets-webpack-plugin
2. 修改`webpack.config.js`配置文件如下：

```javascript
// 导入处理路径的模块
const path = require('path');

const OptimizeCss = require('optimize-css-assets-webpack-plugin');

module.exports = {
    ...
    optimization: {
        // 优化项
        minimizer: [
            // 压缩了css后js没有压缩
            new OptimizeCss()
        ]
    }
}
```

3. 压缩js
   1. 安装**uglifyjs-webpack-plugin**（uglifyjs-webpack-plugin现在又改成了**terser-webpack-plugin**，参考：https://www.npmjs.com/package/mini-css-extract-plugin）
   2. 修改`webpack.config.js`配置文件如下：

```javascript
// uglifyjs-webpack-plugin
// 导入处理路径的模块
const path = require('path');
const UglifyjsWebpackPlugin = require('uglifyjs-webpack-plugin');

module.exports = {
    ...
    optimization: {
        // 优化项
        minimizer: {
            [
            	// 压缩了css后js没有压缩
            	new OptimizeCss()
            	// 压缩了js
            	new UglifyjsWebpackPlugin({
            		// 缓存
            		cache: true,
            		// 并发打包
            		paralle: true,
            		// 源码映射
            		sourceMap: true
        		})
            ]
        }
    }
}

// terser-webpack-plugin
// 压缩js，生产环境下起作用
const TerserJSPlugin = require('terser-webpack-plugin')
optimization: {
    // 压缩css和js
    minimizer: [ 
        new TerserJSPlugin({
            terserOptions: {
                output: {
                    // 去除注释
                    comments: false,
                },
            },
        }),
        new OptimizeCss({}) ]
}
```

#### 自动添加前缀

参考loader中的autoprefixer

### 其他

#### 实时打包

```js
watch: true
watchOptions: {
    poll: 1000, // 每秒询问1000次
    aggregateTimeout: 500, // 防抖：500毫秒
    ignored: /node_modules/
}
```

#### 跨域问题

```js
devServer: {
    proxy: {
        // 1
        // 将前端服务器请求代理到3000
        // '/api': 'http://localhost:3000'
        '/api': {
            target: 'http://localhost:3000',
            pathRewrite: {'api': ''}
        }
    }
    // 2模拟数据
    before(app) {
        app.get('/user', (req, res) => {
            res.json({name: 'sin'})
        })
    }
}

// 3有服务端，不使用代理，在服务端启动webpack，端口使用服务端端口
let express = require('express')
let app = express()

app.get('/user', (req, res) => {
    res.json({name: 'sin'})
})

app.listen(8080)
```

#### resolve配置

```js
resolve: { // 解析 第三方包 common
    // 第三方包的查找路径
    modules: [path.resolve('node_modules')],
    // 别名
    alias: {
        // 1.bootstrap: 'bootstrap/dist/css/bootstrap.css'
    },
    // 2.先找style，再找main
    mainFields: ['style', 'main'],
    // 入口文件的名字，默认index.js
    mainFiles: []
    // 后缀，从左往右
    extensions: ['.js', '.css', 'json']
}
```

#### 定义环境变量

内置插件：

```js
plugins: [
    new webpack.DefinePlugin({
        // DEV: "'dev'" // 定义了一个DEV = 'dev'的环境变量可以判断当前环境
        DEV: JSON.stringify('dev')
    })
]
```

区分不同的环境：三个配置文件（webpack.base.js/webpack.dev.js/webpack.prod.js）

包： webpack-merge

```js
let {smart} = require('webpack-maege')
let base = require('./webpack.base.js')

module.exports = smart(base, {
    mode: 'development',
    dev...
})

// prod
let {smart} = require('webpack-maege')
let base = require('./webpack.base.js')

module.exports = smart(base, {
    mode: 'product',
    // 优化
})

// 执行npm run build -- --config webpack.dev.js
```

### Webpack 性能优化

- 有哪些方式可以减少 Webpack 的打包时间
- 有哪些方式可以让 Webpack 打出来的包更小

#### 减少 Webpack 打包时间

##### 优化 Loader

对于 Loader 来说，影响打包效率首当其冲必属 Babel 了。因为 Babel 会将代码转为字符串生成 AST，然后对 AST 继续进行转变最后再生成新的代码，项目越大，**转换代码越多，效率就越低**。当然了，我们是有办法优化的。

首先我们可以**优化 Loader 的文件搜索范围**

```js
module.exports = {
  module: {
    rules: [
      {
        // js 文件才使用 babel
        test: /\.js$/,
        loader: 'babel-loader',
        // 只在 src 文件夹下查找
        include: [resolve('src')],
        // 不会去查找的路径
        exclude: /node_modules/
      }
    ]
  }
}
```

对于 Babel 来说，我们肯定是希望只作用在 JS 代码上的，然后 `node_modules` 中使用的代码都是编译过的，所以我们也完全没有必要再去处理一遍。

当然这样做还不够，我们还可以将 Babel ，下次只需要编译更改过的代码文件即可，这样可以大幅度加快打包时间

```
loader: 'babel-loader?cacheDirectory=true'
```

##### HappyPack

包名：happypack

受限于 Node 是单线程运行的，所以 Webpack 在打包的过程中也是单线程的，特别是在执行 Loader 的时候，长时间编译的任务很多，这样就会导致等待的情况。小项目不需要。

**HappyPack 可以将 Loader 的同步执行转换为并行的**，这样就能充分利用系统资源来加快打包效率了，小项目不需要。

```js
module: {
  rules: [
    {
      test: /\.js$/,
      include: [resolve('src')],
      exclude: /node_modules/,
      // id 后面的内容对应下面
      loader: 'happypack/loader?id=happybabel'
    }
  ]
},
plugins: [
  new HappyPack({
    id: 'happybabel',
    use: {
	    loader: 'babel-loader?cacheDirectory',
        options: {
            preset: [
                '@babel/preset-env',
                '@babel/preset-react'
            ]
        }
    }
    // 开启4个线程，默认3
    threads: 4
  })
]
```

##### DllPlugin

<https://www.cnblogs.com/tugenhua0707/p/9520780.html>

<https://gitee.com/mr-hu-pan/codes/hznjc518abmxtp6k34uor79>

动态链接库

**DllPlugin 可以将特定的类库提前打包然后引入**。这种方式可以极大的减少打包类库的次数，只有当类库更新版本才有需要重新打包，并且也实现了将公共代码抽离成单独文件的优化方案。

比如抽离react

@babel/preset-react // 解析react

```js
// 单独配置在一个文件中
// webpack.dll.conf.js
const path = require('path')
const webpack = require('webpack')
module.exports = {
    mode: 'development',
  entry: {
    // 想统一打包的类库，键对应下面的name
    react: ['react', 'react-dom']
  },
  output: {
    path: path.join(__dirname, 'dist'),
    filename: '[name].dll.js', // 产生的文件名
    library: '[name]-[hash]', // 导出的变量名
    libraryTarget: 'var' // 导出方式，默认是var，commonjs、umd、this。。。
  },
  plugins: [
    new webpack.DllPlugin({
      // name 必须和 output.library 一致
      name: '[name]-[hash]',
      // manifest文件中请求的上下文，默认为该webpack文件上下文。该属性需要与 DllReferencePlugin 中一致
      context: __dirname,
      // 产生的一个清单，里面有对应的路径
      path: path.join(__dirname, 'dist', '[name]-manifest.json')
    })
  ]
}
```

html中需要引入打包后的[name].dll.js，找到变量名。由于动态链接库我们一般只编译一次，除非依赖的三方库更新，之后就不用编译，因此入口的 index.js 文件中不包含这些模块，所以要在 index.html 中单独引入。

然后我们需要执行这个配置文件生成依赖文件，接下来我们需要使用 `DllReferencePlugin` 将依赖文件引入项目中

```js
// webpack.conf.js
module.exports = {
  // ...省略其他配置
  plugins: [
    new webpack.DllReferencePlugin({
      context: __dirname,
      // manifest 就是之前打包出来的 json 文件
      // 会先去查找清单如果没有才进行打包
      manifest: require('./dist/vendor-manifest.json'),
    })
  ]
}
```

#### 代码压缩

在 Webpack3 中，我们一般使用 `UglifyJS` 来压缩代码，但是这个是单线程运行的，为了加快效率，我们可以使用 `webpack-parallel-uglify-plugin` 来并行运行 `UglifyJS`，从而提高效率。

在 Webpack4 中，我们就不需要以上这些操作了，只需要将 `mode` 设置为 `production` 就可以默认开启以上功能。代码压缩也是我们必做的性能优化方案，当然我们不止可以压缩 JS 代码，还可以压缩 HTML、CSS 代码，并且在压缩 JS 代码的过程中，我们还可以通过配置实现比如删除 `console.log` 这类代码的功能。

#### 一些小的优化点

我们还可以通过一些小的优化点来加快打包速度

- `resolve.extensions`：用来表明文件后缀列表，默认查找顺序是 `['.js', '.json']`，如果你的导入文件没有添加后缀就会按照这个顺序查找文件。我们应该尽可能减少后缀列表长度，然后将出现频率高的后缀排在前面
- `resolve.alias`：可以通过别名的方式来映射一个路径，能让 Webpack 更快找到路径
- `module.noParse`：如果你确定一个文件下没有其他依赖，就可以使用该属性让 Webpack 不扫描该文件，这种方式对于大型的类库很有帮助

##### noParse

用到三方库比如jquery时webpack会去寻找它的依赖包，给没有依赖包的库配置该项可以减少打包时间

```js
module: {
	noParse: /jquery/
}
```

#### 减少 Webpack 打包后的文件体积

##### 按需加载

想必大家在开发 SPA 项目的时候，项目中都会存在十几甚至更多的路由页面。如果我们将这些页面全部打包进一个 JS 文件的话，虽然将多个请求合并了，但是同样也加载了很多并不需要的代码，耗费了更长的时间。那么为了首页能更快地呈现给用户，我们肯定是希望首页能加载的文件体积越小越好，**这时候我们就可以使用按需加载，将每个路由页面单独打包为一个文件**。当然不仅仅路由可以按需加载，对于 `loadash` 这种大型类库同样可以使用这个功能。

按需加载的代码实现这里就不详细展开了，因为鉴于用的框架不同，实现起来都是不一样的。当然了，虽然他们的用法可能不同，但是底层的机制都是一样的。都是当使用的时候再去下载对应文件，返回一个 `Promise`，当 `Promise` 成功以后去执行回调。

##### IgnorePlugin

内置插件可以忽略三方库中一些不需要的文件，比如moment库支持多语言，直接使用体积过大

```js
plugins: [
    // 忽略moment中的locale，此时的moment.locale('zh-cn')不会生效需要手动引入，import 'moment/locale/zh-cn'
    new webpack.IgnorePlugin(/\.\/locale/, /moment/)
]
```

##### Scope Hoisting把模块合并到一个函数中

**Scope Hoisting ，直译过来就是「作用域提升」，webpack 会把引入的 js 文件“提升到”它的引入者顶部。会分析出模块之间的依赖关系，尽可能的把打包出来的模块合并到一个函数中去。**

比如我们希望打包两个文件

```js
// test.js
export const a = 1
// index.js
import { a } from './test.js'
```

对于这种情况，我们打包出来的代码会类似这样

```js
[
  /* 0 */
  function (module, exports, require) {
    //...
  },
  /* 1 */
  function (module, exports, require) {
    //...
  }
]
```

但是如果我们使用 Scope Hoisting 的话，代码就会尽可能的合并到一个函数中去，也就变成了这样的类似代码

```js
[
  /* 0 */
  function (module, exports, require) {
    //...
  }
]
```

它的好处是：

- 代码体积更小，因为函数申明语句会产生大量代码；
- 代码在运行时因为创建的函数作用域更少了，内存开销也随之变小。

如果在 Webpack4 中你希望开启这个功能，只需要启用 `optimization.concatenateModules` 就可以了。

```js
module.exports = {
  optimization: {
    concatenateModules: true
  }
}
```

##### Tree Shaking删除未被引用的代码

**Tree Shaking 可以实现删除项目中未被引用的代码（import引入，require不支持，require会把引用到的结果放到default中）**，比如

```js
// test.js
export const a = 1
export const b = 2
// index.js
import { a } from './test.js'
```

对于以上情况，`test` 文件中的变量 `b` 如果没有在项目中使用到的话，就不会被打包到文件中。

如果使用 Webpack 4 的话，开启生产环境就会自动启动这个优化功能。

##### 提取公共代码

<https://www.cnblogs.com/kwzm/p/10314438.html>

之前会用到插件：commonChunkPlugin，webpack4不需要

多个文件引用到同样的代码时使用，可以缓存代码

```js
optimization: {
    splitChuncks: {
        // cacheGroups其实是splitChunks里面最核心的配置，splitChunks就是根据cacheGroups去拆分模块的，包括chunks属性等属性其实都是对缓存组进行配置的。splitChunks默认有两个缓存组：vender和default
        cacheGroups: { // 缓存组
            commom: {
                // 'async':只拆分动态引入的，'all':所有引入
                chunks: 'initial', // 从入口处开始
                minSize: 0, // 文件大于0字节
                minChunks: 2, // 使用2次及以上
            },
            // vendors的test默认设置为 /[\\/]node_modules[\\/]/ 表示只筛选从node_modules文件夹下引入的模块，所有第三方模块会被拆分出来。
            // default缓存组，minChunks: 2，它的权重小于vendors
            vendors: {
                // 由于从上到下执行，可能会和自定义的通用模块抽取到一起，增加权重
                priority: 1,
                test: /node_modules/,
                chunks: 'initial',
                miniSize: 0,
                minChunks: 2
            }
        }
    }
}
```

参考：

```js
// splitChuncks的默认配置
module.exports = {
  //...
  optimization: {
    splitChunks: {
      // 动态引入的模块
      chunks: 'async',
      minSize: 30000,
      minChunks: 1,
      // 用来限制异步模块内部的并行最大请求数的，可以理解为是每个import()它里面的最大并行请求数量
      maxAsyncRequests: 5,
      // 它表示允许入口并行加载的最大请求数，为了对拆分数量进行限制，不至于拆分出太多模块导致请求数量过多而得不偿失。
      // 如果同时又两个模块满足cacheGroup的规则要进行拆分，但是maxInitialRequests的值只能允许再拆分一个模块，那尺寸更大的模块会被拆分出来
      maxInitialRequests: 3,
      automaticNameDelimiter: '~',
      name: true,
      cacheGroups: {
        vendors: {
          test: /[\\/]node_modules[\\/]/,
          priority: -10
        },
        default: {
          minChunks: 2,
          priority: -20,
          reuseExistingChunk: true
        }
      }
    }
  }
};
```

#### 懒加载

```js
// es6草案语法，jsonp实现动态加载文件
// vue，react的懒加载也是同样的方式
import('./source.js').then(data => {
    console.log(data)
})
```

插件：@babel/plugin-syntax-dynamic-import，在js的rules中的plugins中声明

#### 相关文章

1. [Sass 基础教程](http://www.sasschina.com/guide/)
2. [webpack-dev-server](https://github.com/webpack/webpack-dev-server/releases)
3. [You have not accepted the license agreements of the following ](http://majing.io/questions/804)

### tapable

webpack本质上是一种事件流的机制，它的工作流核心就是将各个插件串联起来，实现的核心就是tapable，有点类似node的events库，核心原理也是发布订阅模式

compile.js核心模块引用了tapable

应用tapable：

安装tapable

