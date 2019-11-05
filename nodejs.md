Node.js

## 概述

### Node.js 是什么

- 基于 Chrome V8 引擎的JavaScript 运行时环境
  - 既不是语言，也不是框架，它是一个平台
  - 可以解析执行js代码，完全脱离浏览器执行

- **Node.js中的 JavaScript**
  - 没有 BOM、DOM
  - EcmaScript 基本的 JavaScript 语言部分
  - 在 Node 中为 JavaScript 提供了一些服务器级别的 API
    - 文件操作的能力
    - http 服务的能力
- event-driven **事件驱动**、non-blocking I/O model **非阻塞io模型**（异步）
  - 轻量高效
- 基于node开发的npm是世界上最大的开源库生态系统

### Node.js 能做什么

- Web服务器后台
  - 中间层
    - 在客户端和服务端中间
    - 安全，可以用来提高性能
    - 降低服务器复杂度
  - 小型服务器

- 工具
  - 命令行工具
    - npm
    - hexo
    - 案例：项目初始化工具
  - 命令行工具的使用
    - webpack
    - npm
    - glup

### 优势

1. 便于入手
2. 性能高
3. 利于和前台整合

### Node中的JavaScript

- EcmaScript
  - 没有BOM，DOM
- 核心模块
  - Node 中为 JavaScript 提供了一些服务器级别的 API，大多数都被包装到一个具名的核心模块中
  - fs，http，os，path等
  - 使用前必须引入`var fs = require('fs')`
- 第三方模块
- 自定义模块
  - 模块加载：`require('./xxx') //js后缀可以不加 `
  - **Node中没有全局作用域只有模块作用域**
  - 模块之间通信：`exports.xx //默认是一个空对象 `

### 代码风格

当代码以[、(、`开头时要在前面加分号

### debug

vscode左侧的debug图标

### 与前端开发的区别

服务稳定性

- 可能遭受到恶意攻击和误操作
- 服务端不能意外挂掉
- PM2做进程守候（挂掉后自动重启）

考虑内存和cpu（优化，扩展）

- 客户端独占一个浏览器，内存和cpu不是大问题，服务端的cpu和内存都是稀缺资源
- stream写日志，使用redis存session

日志记录

- 前端也会参与，但只是发起方

- 服务端要记录，存储，分析日志

安全

- 接收各种恶意攻击
- 越权操作，数据库攻击等
- 防止xss攻击和sql注入

集群和服务拆分

- 流量增加，利用扩展机器和服务拆分来承载大流量

## 模块系统

### 模块化

- 文件作用域
- 通信规则
  - 加载
  - 导出

### commonJS规范

Node中

- 模块作用域

- require加载

  `var 变量 = require('模块标识符')`

  - 作用：执行模块代码；得到导出接口对象

  - 加载规则

    - 优先从缓存加载：加载过的会缓存起来，不会重复执行，只会得到接口对象

    - 判断模块标识：

      核心模块（名称）

      第三方模块（node_modules/xx/package.json=>main属性=>xx.js，都没有时会向上查找，直到根目录，根目录也没有会报错）

      自定义模块（路径形式）

- exports导出成员

  - exports是module.exports的引用

  - 导出多个成员（对象）

    ```javascript
    exports.a = '1'
    ```

  - 到处单个成员

    ```javascript
    module.exports = fn
    ```



## npm

注意卸载时清理掉安装目录下的node_modules和用户文件夹下的node_modules，删除nodejs目录

### 包管理

yarn：`npm iyarn -g`

bower：前端包管理，`npm i bower -g`

### 包说明文件

快速生成：`npm init -y`

-S：开发依赖

-D：运行依赖

新版本npm5以后的还会生成package-lock文件

- package-lock文件会保存所有的包信息（版本，下载地址等）
  - 重新install时速 度会提升
  - 可以锁定版本，不会重新下载最新版

### 命令行

- 升级npm`npm i -g npm`
- 删除包：`npm un 包名 -S` 
- 帮助：`npm help`
- 查看配置：`npm config list`

### cnpm

安装：`npm i cnpm -g`

切换npm地址

- `npm i jquery --registry=https://registry.npm.taobao.org`
- `npm config set registry https://registry.npm.taobao.org`

### nodemon工具自动重启

安装：`npm i -g nodemon`

使用：`nodemon app.js // 使用nodemon启动`

## 全局对象global

在REPL环境中，默认的所有的变量、函数、对象都会默认的挂载到global对象上

在文件中，声明的变量，如果你没有显示的指定，那么它是属于当前文件的

### 全局函数

`setTimeout,setInterval, clearTimeout, clearInterval, require, Buffer`

### 伪全局变量

`__dirname, __filename`

## 原理解析

### 多线程和单线程

进程：每个正在运行的应用程序，本质上是操作系统给一个应用程序分配资源的最小单位。可以隔离应用程序与应用程序之间的资源，每个进程都有一个processid。进程是给应用程序提供一个执行环境

`process.pid`

`process.kill(pid)`

时间片轮转调度算法

线程：一个进程可以有多个线程，一个线程同时只能做一件事，是一个代码流。可以相互通信

多线程弊端：状态同步问题，对高并发程序支持不好

传统的web服务器给每个用户创建一个线程处理请求（比如apache），对高并发程序支持不好

### 事件驱动

![1543473740973](.\media\1543473740973.png)

node.js收到请求后会把请求添加到事件队列中

node.js中所有的异步代码会在同步代码都执行完之后才执行，即执行完同步代码后循环执行队列中的事件

如果是I/O操作会在线程池中选取一个有效线程执行I/O操作，不会影响队列的循环执行，通过回调函数将数据返回给事件队列继续循环执行，最终返回响应

线程池：提前申请好的几个内存空间，不需要开发人员管理线程

## 启动器

npm i forever -g

forever start xxx

forever list

forever restart xxx

forever stop xxx

forever stopall



forever start xxx.js -l c:/a.log -e c:/err.log -a

## 核心模块

### http模块

```javascript
// 一个简单的服务器
var http = require('http')
var server = http.createServer()
server.on('request', function(req, res){
    // 请求路径，端口号之后的部分，以/开头
	req.url
})
// 监听，等待客户端的连接
server.listen('3000', fn)

// 更简单的写法
var http = require('http')
http
  .createServer(function(req, res){
      // 请求路径，端口号之后的部分，以/开头
      req.url
  })
  .listen('3000', fn)
  // 关闭服务器
  .close()
```

#### 请求对象

获取请求头

`var headers = req.headers`

- message.headers

- message.httpVersion
- message.method
- message.url

##### 解析post请求的数据

request对象本身是一个数据流，所以可以通过监视request对象的data事件，将数据拼接到自定义的变量中，接收完毕后，会触发end事件

```javascript
var queryStr = require('querystring')
function bodyParser(req, next) {
    // post请求判断是否有请求参数
    if('content-length' in req.headers) {
        let data = ''
        req.on('data', function(chunck) {
            data += chunck
        })
        req.on('end', function() {
            req.body = queryStr.parse(data)
            next()
        })
    }else {
        req.body = {}
        next()
    }
}
```

#### 响应对象

- 发送响应

`res.write()` 可以使用多次，也可以用append追加内容，但是一定要用`res.end()`来结束，否则客户端会一直等待，也可以用`res.end()`直接发送响应

**响应内容必须是字符串或者二进制数据**

将数组或者对象转换为字符串：`JSON.stringify(arr)`

将字符串转换为数组或者对象：`JSON.parse('str')`

- 响应内容类型

`res.setHeader('Content-Type', 'text/plain; charset=utf-8') //响应类型为普通文本 `，也可以使用html的meta元数据指定编码格式`<meta charset="UTF-8" />`

[在线工具](tool.oschina.net)

- 设置响应头

`res.writeHead(200, {'Set-Cookie':'isVisited=true'})`

#### 客户端重定向

- 设置状态码为302临时重定向，客户端发现状态码为302时会去找响应头的Location
  - `res.statusCode = 302`
  - 301：永久重定向，浏览器会记住。第二次请求时，会直接请求重定向后的路径
  - 302：临时重定向，浏览器不会记住
- 在响应头中通过Location重定向
  - `res.setHeader('Location', '/')`
- 结束响应
  - `res.end()`

### url模块

```javascript
// 接受表单提交的数据
// true表示将查询字符串转为对象
url.parse('url', true) // 返回对象，包含：search、query、hash、path、href、pathname等
```

- search：包含？及后面的部分
- query：？后面的部分
- pathname：？前面的部分

### path路径模块

```javascript
path.basename('c:/a/c/index.js') // 'index.js'
path.basename('c:/a/c/index.js', '.js') // 'index'
path.dirname('c:/a/c/index.js') // 'c:/a/c'
path.extname('c:/a/c/index.js') // '.js'
path.isAbsolute('c:/a/c/index.js') // true
path.parse('c:/a/c/index.js') // {root: 'c:/', dir: 'c:/a/c', base: 'index.js', ext: '.js', name: 'index'}

path.join('c:/', 'b') // 'c:\\a\\b' 根据系统 将路径片段使用特定的分隔符（window：\）连接起来形成路径d，并规范化生成的路径。
path.resolve('/foo/bar', './baz') // '/foo/bar/baz'把一个路径或路径片段的序列解析为一个绝对路径。/被解析为根目录。
```

### querystring

```js
const querystr = quire("querystring")
querystr.parse("a=1&b=2&c=3") // 解析为json
querystr.stringify(json) // 解析为json

const http = require('http')
const querystr = quire("querystring")
const server = http.createServer((req, res) => {
    const url = req.url
    req.query = querystring.parse(url.split('?')[1])
    res.end(JSON.stringify(req.query))
})
server.listen(8000)
```

### assert

```js
const assert = require("assert")
assert(5>3, 提示消息)
assert.deepEqual(变量， 预期值， 消息) // 比较成员
assert.deepStrictEqual(变量， 预期值， 消息) // 比较成员和类型
```

### net

网络通信，不是http协议时用到

OSI七层参考模型：物理---数据链路层---网络层（IP）---传输层（保证传输质量，TCP）---会话层（计算机之间保留通信的基本信息）---表现层（屏蔽各个网络之间的不同）---应用层（HTTP）

五层参考模型：物理---数据链路层---网络层（IP）---传输层（保证传输质量，TCP，UDP）---应用层（HTTP）

net属于传输层，对TCP的实现

### 文件模块

#### POST文件处理原理理解

```js
const http = require('http')

http.createServer((req, res)=>{
	console.log(req.headers)

	let arr = [] // 实际情况下不应该所有的都放在这里
	req.on('data', buffer=>{
		arr.push(buffer)
	})
	req.on('end', ()=>{
		let buffer = Buffer.concat(arr)
		console.log(buffer.toString())
		// ------WebKitFormBoundaryWZBe3Az77qpZZ48e
		// Content-Disposition: form-data; name="username"

		// naixes
		// ------WebKitFormBoundaryWZBe3Az77qpZZ48e
		// Content-Disposition: form-data; name="file"; filename="test.txt" // 原始文件名
		// Content-Type: text/plain

		// test
		// 000000
		// ------WebKitFormBoundaryWZBe3Az77qpZZ48e--
	})
}).listen(8080)
```

包：multiparty

```js
const http = require('http')
// 文件上传
const multiparty = require('multiparty')

http.createServer((req, res) => {
	let form = new multiparty.Form({
		// 上传路径
		uploadDir: './upload'
	})
	form.parse(req)
	// 普通字段
	form.on('field', (name, value) => {
		console.log(name, value)
	})
	// 文件
	form.on('file', (name, file) => {
		console.log(name, file)
	})
	form.on('close', () => {
		console.log("解析完成")
	})
}).listen(8080)
```

实际项目使用框架

#### 同步与异步文件系统调用

文件模块的所用操作几乎都分为异步与同步

例如：readFile()和readFileSync()

区别：

- 异步函数需要回调函数作为额 外的参数，通常包含一个错误作为回调函数的第一个参数
- 同步函数会阻塞当前线程
- 异步函数会进入事件队列不会阻塞当前线程，直到事件循环线程将他提取出来时才会执行
- 异步通过判断第一个参数处理异常，同步必须使用try/catch处理异常

#### 读取文件

将文件读取到内存中

`fs.readFile('路径', 'utf8', fn(err, data){}) // 中间是可选参数,utf-8可以让输出格式变为string`

err：错误对象，没错时返回null

data：文件中储存二进制数据，返回16进制数据，可以使用`toString()`或传入可选参数`utf8`，失败返回undefined

#### 写入文件

`fs.writeFile('路径', 文件内容, fn(err){})`

err：错误对象，没错时返回null

向文件中添加内容

`fs.appendFile('路径', 文件内容, fn(err){})`

#### 其他文件操作

- 验证路径

`fs.exists(path, fn(exists)) // 返回布尔类型`

- 获取文件信息

`fs.stat(path, fn(err, stats)) // 返回stats对象`

返回stats对象中有一些常用方法，例如

`fs.statSync('').isFile() // 判断是否是文件`

- 删除文件移动文件

`fs.unlink(path, fn(err))`

- 重命名文件或目录

`fs.rename(old, new, fn())`

- 移动文件

#### 目录操作

- 创建目录

`fs.mkdir(path, fn) // 不能创建多级目录`

- 删除目录

`fs.rmdir(path, fn) // 只能删除空目录`

- 读取目录

`fs.readdir('路径', function(err, files) {}) // 返回数组 `

#### 监视文件变化

`fs.watchFile(filenanme, [option], listen(curr, prev))`

options：persistent指是否持续监视默认true；interval监视间隔时间默认5007

监视保存后的变化

#### 文件流操作

对超大文件进行操作

读取流

```javascript
var rs = fs.createReadStream('path')
var ws = fs.createWriteStream('path')

// data事件不断被触发
rs.on('data', function(trunk) {
    // 如果写入速度跟不上读取速度还是会占用很大内存
    writeSream.write(trunk)
})
rs.on(s'end', function(trunk) {
    ...
})

//另一种方法
readStream.pipe(writeSream)
    
// 一些常用事件
rs.on('error', err => {})
ws.on('finish', () => {})

// 一句代码写法
fs.createReadStream(path).pipe(fs.createWriteStream(path))
```

读写流

应用：压缩，加密

```js

```

 

### 文件操作扩展包

fs-extra

#### 文件编码扩展包

iconv-lite

`iconv.decode(data, 'gbk')`

### readline模块

逐行读取，针对文本文件

```javascript
const readline = require('readline')
const rl = readline.creatInterface({
    input: fs.createReadStream('./xx'),
    // output: process.stdout
})
// line为当前行内容
rl.on('line', function(line) {})
```

### process模块

```js
// config/index.js
let process = require('process')
// 环境变量
process.env
// 可以用来获取命令行 -- 后面的参数，使用不同的配置文件
console.log(process.argv)
```

### 实现简单的原生服务器

<https://github.com/Naixes/demo-collection/tree/master/learnNode/native-project>

```js
config:  config.dev.js
	     config.prod.js
libs:    database.js
	     http.js
         router.js
routers: ...
server.js
static:  css/html/js...
```

<http://verymuch.site/2017/12/12/escape%E3%80%81encodeURI%E5%92%8CencodeURIComponent%E7%9A%84%E5%8C%BA%E5%88%AB%E4%B8%8E%E4%BD%BF%E7%94%A8/>
`encodeURLComponent('xxxxx')`

## node中的非模块成员

`__dirname`：**动态获取**当前文件所属目录的绝对路径

`__filename`：**动态获取**当前文件的绝对路径改成绝对路径

node中文件操作中的相对路径是相对执行node命令的路径，不可靠。应该使用`__dirname`和`join`方法

`path.join(__dirname, '')`

## 数据通信

### ajax

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<meta http-equiv="X-UA-Compatible" content="ie=edge">
	<title>Document</title>
	<script>
		window.onload = function() {
			let btn = document.getElementById('btn')
			btn.onclick = function() {
				let ajax = new XMLHttpRequest()
				// true指异步
				ajax.open('GET', 'http://localhost:8080/a', true)
				ajax.send()
				ajax.onreadystatechange = function() {
					if(ajax.readyState === 4) {
						if(ajax.status >= 200 && ajax.status < 300 || ajax.status === 304) {
							alert("请求成功")
							let json = JSON.parse(ajax.responseText)
							console.log(json)
						}else {
							alert("请求失败")
						}
					}
				}
			}
		}
	</script>
</head>
<body>
	<input type="button" value="请求" id="btn">
</body>
</html>
```

```js
const http = require('http')

http.createServer((req, res) => {
	let allowOrigin = {
		"http://localhost": true
	}
	// SOP:同源策略
	// 设置CROS
	const {origin} = req.headers
	if(allowOrigin[origin]) {
		res.setHeader('access-control-allow-origin', '*')
	}

	res.write('{"a": "12", "name": "j"}')
	res.end()
}).listen(8080)
```

### fetch

#### 获取解析二进制数据

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<meta http-equiv="X-UA-Compatible" content="ie=edge">
	<title>Document</title>
	<script>
		window.onload = function() {
			let btn = document.getElementById('btn')
			let img = document.getElementById('img')
			btn.onclick = async function() {
				// 请求
				let res = await fetch('data/f0.png')
				// 解析数据
				// 二进制数据
				let data = await res.blob()
				// 将二进制数据转换为url
				let url = URL.createObjectURL(data)
				img.src = url
			}
		}
	</script>
</head>
<body>
	<input type="button" value="获取数据" id="btn">
	<img src="" alt="" id="img">
</body>
</html>
```

### jsonp

不安全，使用变少

### FormData

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<meta http-equiv="X-UA-Compatible" content="ie=edge">
	<title>Document</title>
	<script>
		window.onload = function() {
			let oForm = document.querySelector("#form")

			oForm.onsubmit = function() {
				let formdata = new FormData(oForm)

				// 脱离表单使用formdata
				// formdata.append("username", document.querySelector("#user"))

				let xhr = new XMLHttpRequest()

				// 这里使用form中的数据
				xhr.open(oForm.method, oForm.action, true)

				// 脱离表单使用formdata
				// xhr.open("post", "http://localhost:8080", true)

				xhr.send(formdata)

				xhr.onreadystatechange = function() {
					if(xhr.readyState == 4) {
						if(xhr.status >= 200 && xhr.status < 300 || xhr.status === 304) {
							alert("成功")
						}else {
							alert("失败")
						}
					}
				}

				return false
			}
		}
	</script>
</head>
<body>
	<form action="http://localhost:8080" method="POST" id="form">
		账号：<input type="text" name="account" id="user"><br/>
		<input type="file" name="file"><br/>
		<input type="submit" id="submit" value="提交">
	</form>
</body>
</html>
```

### webSocket

- 性能高，对比ajax，基于http协议（建立连接阶段）二进制协议
- 双向通信
- 没有同源限制
- 安全

库：socket.io

- 简单方便
- 兼容IE5
- 自动数据解析

```js
const http  = require('http')
const io = require('socket.io')

// 建立普通的http
let server = http.createServer((req, res) => {})
server.listen(8080)

// 建立ws
let wsServer = io.listen(server)
// sock建立好的连接
wsServer.on('connection', sock => {
	// sock.emit('name', 数据) // 发送数据
	// sock.on('name', (数据)=>{})
	sock.on('aaa', (a, b) => {
		console.log(a+b)
	})

	setInterval(function() {
		sock.emit('timer', new Date().getTime())
	}, 1000)
})
```

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<meta http-equiv="X-UA-Compatible" content="ie=edge">
	<title>Document</title>
	<!-- socket.io库中的文件 -->
	<script src="http://localhost:8080/socket.io/socket.io.js"></script>
	<script>
		let sock = io.connect('ws://localhost:8080/')

		// sock.emit
		// sock.on
		sock.emit('aaa', 1, 2)

		sock.on('timer', time => {
			console.log(time)
		})
	</script>
</head>
<body>
	
</body>
</html>
```

## 模板引擎

### art-template

- 在浏览器中使用

  引入

  写一个模板

  用数据替换模板中的标记`template('tpl', data)`

- 在服务器中使用

  安装：`npm i art-template -S`

  加载：`var artTemplate = 'art-template'`

  使用：`artTemplate.render('模板字符串', data)`

#### include-extend-block语法

子模板

引入子模块`{{include '路径'}}`

模板继承

被继承模板`公共内容...{{block 'name'}} <h3>默认内容</h3> {{/block}}...公共内容`

继承`{{extend '路径'}} {{block 'name'}} <h3>替换内容</h3> {{/block}}`

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Document</title>
  {{block 'head'}}{{/block}}
</head>
<body>
  {{include './header.html'}}

  {{block 'conten'}}
    <h3></h3>
  {{/block}}
    
  {{include './footer.html'}}

  {{block 'script'}}{{/block}}
</body>
</html>

// 继承模块
{{extend './layout.html'}}
{{block 'conten'}}
  <style>...</style>
{{/block}}
{{block 'conten'}}
  <h3></h3>
{{/block}}
{{block 'script'}}
  <script></script>
{{/block}}
```

### 客户端渲染和服务端渲染

- 服务端渲染
  - 减少请求次数，直接响应最终结果，数据多的情况下页面响应速度慢，服务器压力大
  - 会刷新整个页面，在源代码中可以查到数据
  - 利于SEO，兼容，安全性高
- 客户端渲染
  - 最少请求两次（页面和数据），页面响应速度快，用户体验好，数据多的情况下内容显示速度慢
  - 不会刷新整个页面，在源代码中查不到数据
  - 浏览器的前进和后退都会重新请求，没有合理利用缓存
  - 无法记住滚动的位置
  - 异步渲染，不利于SEO

## 统一管理静态资源

``````javascript
// 将public目录开放
if (req.url.indexOf('/public/')===0) {
    let fullPath = path.join(__dirname, req.url)
    fs.readFlie(fullPath, function(err, data) {
        if(err) {
            res.writeHead(404)
            return err.message
        }
        let mimeType = mime.lookup(fullPath)
        if(mimeType.startsWith('text/')) {
            mimeType += '; charset=utf8'
        }
        req.writeHeader(200, {'Content-Type': mimeType})
        req.end(data)
    })
}else {
    // 非静态资源的处理
}
// 网站中的静态资源都应该使用url来指定
``````

包：mime 根据后缀名获取类型

引入

`mime.lookup('后缀或者包含后缀的文件或路径') // 返回mime类型`

## express

Web开发框架

``````javascript
var express = require('express')
var app = express()
app.get('/', function(req, res) {
    res.send('hello')
})
app.listen(3000, function() {})
``````

### 静态服务

一般放在最后防止与接口同名

```java
app.use('/public/', express.static('./public/')) // 可以通过/public/访问资源
app.use(express.static('./public/')) // 没有第一个参数时，可省略/public/直接访问
```

### 基本路由

```javascript
// get
app.get('/', function(req, res) {
    // send没有格式的限制
    res.send('hello')
})
// post
app.post('/', function(req, res) {
    res.send('hello')
})
// all
app.all('/', function(req, res, next) {
    next()
})
```

#### 路由路径

路由路径包含正则字符

```javascript
app.get('/ab?cd', function (req, res) {
  res.send('ab?cd')
})
app.get('/ab+cd', function (req, res) {
  res.send('ab+cd')
})
app.get('/ab*cd', function (req, res) {
  res.send('ab*cd')
})
app.get('/ab(cd)?e', function (req, res) {
  res.send('ab(cd)?e')
})
```

路由路径是正则

```javascript

app.get(/.*fly$/, function (req, res) {
  res.send('/.*fly$/')
})
```

#### 路由句柄

使用多个回调函数用逗号隔开，记得使用next()

`app.get('', function(req, res, next){next()}, function(req, res){})`

将多个回调函数放在数组里

`app.get('', [cb1, cb2, cb3])`

也可以混合使用函数和函数组

app.route()创建链式路由句柄

```javascript
app.route('/')
	.get()
	.post()
```

#### 路由实例

```javascript
var express = require('express')
var router = express.Router()

// define the home page route
router.get('/', function (req, res) {
  res.send('Birds home page')
})
// define the about route
router.get('/about', function (req, res) {
  res.send('About birds')
})

module.exports = router
```

### 请求处理

#### get请求获取参数

- 查询字符串形式传递的参数

内置API，获取查询字符串：`req.qurey // 对象`

- ：形式传递参数

```javascript
router.get('/user/:uid', function(req, res) {
    console.log(req.params.uid)
})
```

#### post获取参数

利用中间件body-parser

安装

引入配置：

``````javascript
var express = require('express')
var bodyParser = require('body-parser')

var app = express()

// 配置过后就可以直接使用req.body获取请求体了
// parse application/x-www-form-urlencoded
// extended，是否开启扩展模式
app.use(bodyParser.urlencoded({ extended: false }))
// parse application/json
app.use(bodyParser.json())

// 使用
app.use(function (req, res) {
  res.setHeader('Content-Type', 'text/plain')
  res.write('you posted:\n')
  res.end(JSON.stringify(req.body, null, 2))
})
``````

#### 发送响应

- `res.send()`
- `res.status(200).send()`如果接收的数据格式是JSON但响应的不是JSON，客户端就解析不到
- `res.status(200),json()`会把JSON转换为字符串响应给客户端

#### 重定向

`res.redirect('/')`和location的区别：不用手动设置状态码，也可以用第一个参数指定状态码

`res.redirect('back')`路径值**back**具有特殊的意义，这个涉及到请求头`Referer`中指定的URL，如果`Referer`头没有指定，将会设置为'/'。 

#### 表单的同步提交和异步提交

默认的表单提交，a链接是同步的

同步提交send响应会直接把结果显示到页面上，覆盖到当前页面。一般使用`res.redirect('/')`重定向或`res.render('/')`重新渲染页面，服务器操作更加安全，效果统一。

异步提交：页面不会刷新，交互更丰富

服务端重定向对异步请求无效，只能在客户端重定向`location.href = '/'`

#### Session机制

https://www.cnblogs.com/lonelydreamer/p/6169469.html

由于HTTP协议是无状态的，而出于种种考虑也不希望使之成为有状态的，因此，cookie机制和session机制就成为现实的选择。具体来说cookie机制采用的是在客户端保持状态的方案，而session机制采用的是在服务器端保持状态的方案。同时我们也看到，由于采用服务器端保持状态的方案在客户端也需要保存一个标识，所以session机制可能需要借助于cookie机制来达到保存标识的目的，但实际上它还有其他选择。  

利用例子区分cookie和session

cookie机制：发给顾客一张卡片，上面记录着消费的数量，一般还有个有效期限。每次消费时，如果顾客出示这张卡片，则此次消费就会与以前或以后的消费相联系起来。这种做法就是在客户端保持状态。       

 session机制：发给顾客一张会员卡，除了卡号之外什么信息也不纪录，每次消费时，如果顾客出示该卡片，则店员在店里的纪录本上找到这个卡号对应的纪录添加一些消费信息。这种做法就是在服务器端保持状态。  

##### Cookie

正统的cookie分发是通过扩展HTTP协议来实现的，服务器通过在HTTP的响应头中加上一行特殊的指示以提示浏览器按照指示生成相应的cookie。然而纯粹的客户端脚本如JavaScript或者VBScript也可以生成cookie。

而cookie的使用是由浏览器按照一定的原则在后台自动发送给服务器的。浏览器检查所有存储的cookie，如果某个cookie所声明的作用范围大于等于将要请求的资源所在的位置，则把该cookie附在请求资源的HTTP请求头上发送给服务器。

cookie的**内容主要包括：名字，值，过期时间，路径和域。**       

其中域可以指定某一个域比如.google.com。       

路径就是跟在域名后面的URL路径。路径与域合在一起就构成了cookie的作用范围。

如果不设置过期时间，则表示这个cookie的生命期为**浏览器会话期间**，只要关闭浏览器窗口，cookie就消失了。这种生命期为浏览器会话期的cookie被称为会话cookie。会话cookie一般不存储在硬盘上而是**保存在内存**里，当然这种行为并不是规范规定的。如果设置了过期时间，浏览器就会把cookie保存到硬盘上，关闭后再次打开浏览器，这些cookie仍然有效直到超过设定的过期时间。存储在硬盘上的cookie可以在不同的浏览器进程间共享，比如两个IE窗口。而对于保存在内存里的cookie，不同的浏览器有不同的处理方式。

比如在响应头中写入：

`res.writeHead(200, {'Set-Cookie':'isVisited=true；Path=/;Max-Age:;Domain=*.com;HTTP'})`

再次请求时，请求头中就会有：`Cookie:isVisited=true；Path=/;Max-Age:;Domain=*.com;HTTPOnly:true`

获取请求头：`var headers = req.headers`

cookie的值的格式是：key=value

在页面也可以获取到cookie：`document.cookie`

- 保存一些不太敏感的信息，比如：记住用户名，购物车
- express中间件：cookie-parser

```javascript
app.use(cookie-parse())

let name = body.name
// maxAge的单位是毫秒，原生单位是秒
res.cookie('name', name, {option})
```

##### Session

session机制是一种服务器端的机制，服务器使用一种类似于散列表的结构（也可能就是使用散列表）来保存信息。   

当程序需要为某个客户端的请求创建一个session的时候，服务器首先检查这个客户端的请求里是否已包含了一个session标识 - 称为session id，如果已包含一个session id则说明以前已经为此客户端创建过session，服务器就按照session id把这个session检索出来使用（如果检索不到，可能会新建一个），如果客户端请求不包含session id，则为此客户端创建一个session并且生成一个与此session相关联的session id，session id的值应该是一个既不会重复，又不容易被找到规律以仿造的字符串，这个session id将被在本次响应中返回给客户端保存。

保存这个session id的方式可以采用cookie，这样在交互过程中浏览器可以自动的按照规则把这个标识发挥给服务器。一般这个cookie的名字都是类似于SEEESIONID。

由于cookie可以被人为的禁止，必须有其他机制以便在cookie被禁止时仍然能够把session id传递回服务器。经常被使用的一种技术叫做**URL重写**，就是把session id直接附加在URL路径的后面，附加方式也有两种

一种是作为URL路径的附加信息，表现形式为`http://...../xxx;jsessionid=ByOK3vjFD75aPnrF7C2HmdnV6QZcEbzWoWiBYEnLerjQ99zWpBng!-145788764`

另一种是作为查询字符串附加在URL后面，表现形式为`http://...../xxx?jsessionid=ByOK3vjFD75aPnrF7C2HmdnV6QZcEbzWoWiBYEnLerjQ99zWpBng!-145788764`

这两种方式对于用户来说是没有区别的，只是服务器在解析的时候处理的方式不同，采用第一种方式也有利于把session id的信息和正常程序参数区分开来。  为了在整个交互过程中始终保持状态，就必须在每个客户端可能请求的路径后面都包含这个session id。

另一种技术叫做表单隐藏字段。就是服务器会自动修改表单，添加一个隐藏字段，以便在表单提交时能够把session id传递回服务器。这种技术现在已较少应用。

除非程序通知服务器删除一个session，否则**服务器会一直保留**，程序一般都是在用户做log off的时候发个指令去删除session。然而浏览器从来不会主动在关闭之前通知服务器它将要关闭，因此服务器根本不会有机会知道浏览器已经关闭，之所以会有这种错觉，是大部分session机制都使用会话cookie来保存session id，而关闭浏览器后这个session id就消失了，再次连接服务器时也就无法找到原来的session。如果服务器设置的cookie被保存到硬盘上，或者使用某种手段改写浏览器发出的HTTP请求头，把原来的session id发送给服务器，则再次打开浏览器仍然能够找到原来的session。

session默认存储在内存，服务器重启会丢失，一般会对它进行持久化存储

恰恰是由于关闭浏览器不会导致session被删除，迫使服务器为session设置了一个失效时间，当距离客户端上一次使用session的时间超过这个失效时间时，服务器就可以认为客户端已经停止了活动，才会把session删除以节省存储空间。 

- express中间件：express-session

```javascript
// 引入
var session = require('express-session')
// 在路由之前
app.use(session({
  // 加密字符串，在原有的加密基础之上拼接字符串，增加安全性
  secret: 'keyboard cat',
  resave: false,
  // 未初始化保存，true：无论是否使用，都会分配session_id，false：存储时才分配
  saveUninitialized: true
}))
// 通过req.session获取和设置session成员
// 添加req.session.foo = 'bar'
// 访问req.session.foo
```

存在 cookie 里的 session id 也叫 token

### 模板引擎

安装：`express-art-template和art-template`

配置：`app.engin('art', require(art-template)) // 第一个参数为文件后缀`

使用：`res.render('模板', data) //默认去views目录下寻找`

修改默认路径：`app.set('views', 默认路径)`

### express中的中间件

用来处理请求，本质是请求处理方法，把用户的请求到响应分发到多个中间件去处理，提高代码灵活性，动态可扩展性。

从上往下匹配，接受三个参数

- req
- res
- next()，默认不会往后走，参数是固定的，不可以通过next传参，**可以在req上增加属性当做参数**

####  应用程序级别的中间件

不关心路径和请求方法的中间件，任何请求都会进入这个中间件

```javascript
app.use(function(req, res, next) {
    // 所有的请求都会进来
    // 匹配下一个中间件 
    next()
})

// 配置404页面，注意配置到最后，没有被处理的请求都会进来
app.use(function(req, res) {
    res.render('404.html')
})
```

符合路径的请求

```javascript
app.use('/a', function(req, res) {
    console.log(req.url) // url不包括/a
})
```

#### 路由级别的中间件

app.get和app.post是严格匹配路径（可选）和方法的中间件

还有app.put和app.delete

#### 错误处理中间件

注意：配置到最后，参数必须写完整

```javascript
app.use('/', function(req, res) {
    fs.resdFile('', function(err, data) {
        if(err) {
            // 这里会直接进入错误处理中间件，传递错误对象
            next(err)
        }
    })
})
// 参数必须写完整
app.use(function(err, req, res, next) {
    console.error(err.stack)
    res.status(500).json({
        err_code: 500,
        message: err.message
    })
})
```

#### 内置中间件

express.static

express.json

express.urlencoded

#### 第三方中间件

body-parser

##### cookie-parser

```js
const express = require('express')
const cookieParser = require('cookie-parser')

let server = express()
server.listen(8080)
server.use(cookieParser())
server.get('/a', (req, res) => {
    // cookie 不跨域，子级可以访问父级，父级不能访问子级，domain 设为主域名，path 可以往上访问不能向下访问，path 一般设为'/'根
    res.cookie('amount', 99, {
        // domain: 'aaa.com',
        path: '/',
        maxAge: 14*86400*1000
    })
    console.log(req.cookies)
    res.send('ok')
})
```

cookie 签名

```js
const express = require('express')
const cookieParser = require('cookie-parser')

let server = express()
server.listen(8080)
server.use(cookieParser('naixes1995'))
server.get('/a', (req, res) => {
    // cookie 不跨域，子级可以访问父级，父级不能访问子级
    res.cookie('amount', 99, {
        // 通过js脚本将无法读取到cookie信息，这样能有效的防止XSS攻击
        httpOnly: true,
        maxAge: 14*86400*1000,
        // 签名
        signed: true
    })
    console.log('cookies', req.cookies)
    // 签名cookie
    console.log('signedCookies', req.signedCookies)
    
    res.send('ok')
})
```

其他：express-session，express-mysql-session

##### cookie-session

强制加签名

默认保存到系统的临时文件夹，tempt文件夹

循环秘钥，每个用户的每次登录都不同 

```js
const express = require('express')
const cookieSession = require('cookie-session')

let server = express()
server.listen(8080)

// 强制签名
server.use(cookieSession({
    // 循环秘钥，每个用户的每次登录都不同 
    keys: ['naixes1995', 'sartine1995'],
    maxAge: 20*60*1000 // 20分钟
}))

server.get('/a', (req, res) => {
    if(!req.session['view']) {
        req.session['view'] = 1
    }else {
        req.session['view']++
    }
    req.session['amount'] = 99
    res.send(`欢迎你第${req.session['view']}次访问本站，你的余额为${req.session['amount']}`)
})
```

##### multer

处理文件上传

```js
const express = require('express')
const multer = require('multer')
const body = require('body-parser')

let server = express()
server.listen(8080)

let obj = multer({dest: './static/upload'})
server.use(obj.any())

server.use(body.urlencoded({
    extended:false
}))

server.post('/reg', (req, res) => {
    console.log(req.body)
    console.log(req.files)
    res.send('success')
})

server.use(express.static('./static/'))

```

### 常用API

#### express

```javascript
var app = express() // 导出入口
express.static(root, [opt])
```

#### application 

```javascript
app.locals // 一些默认配置
app.all(path, cb)
app.engine(ext, cb)
app.get('', cb)
app.listen('3000', cb)
app.render(views, [data], cb)
app.route(path) // 链式路由
app.set(name, val) //views,可以设置模板引擎默认路径；views cache，模板缓存；views engine，设置模板引擎
app.use() //中间件
```

#### request

```javascript
req.app // 可以访问app上的一些属性
req.baseUrl
req.body // 获取post表单参数
req.cookies
req.hostname
req.id
req.params
req.path // 请求路径部分不
req.protocol // 协议
req.query // 获取get请求参数
```

#### response

```javascript
res.app
res.locals // 可以挂载一些本地信息，在不同的处理中使用
res.download('路径', [name], [fn])
res.json([body])
res.redirect([status], '') // 刷新当前页面back
res.render(views, [data], cb)
res.send() // 发送文本
res.sendStatus(500)
res.status(500)
res.type(json)
```

#### router

router中也可以添加中间件

### 路由模块

将路由提取到一个文件router.js

```javascript
// router.js文件
module.exports = function(app) {
    app.get('', fn)
}

// app.js文件
...
var app = express()
var router = require('./router.js')
router(app)
...
module.exports = app
```

express提供了一种更好的方式，专门包装路由

```javascript
// router.js文件
var express = require('express')
// 创建路由容器
var router = express.Router()
router.get('', fn)
module.exports = router

// app.js文件
...
var app = express()
var router = require('./router.js')
// 把路由挂载到app实例上
app.use(router)
...
module.exports = app
```

入口文件的作用：

- 创建服务
- 服务相关配置
  - 静态服务
  - 模板引擎
  - body-parser请求解析
- 挂载路由
- 监听端口启动

## KOA

express：基于回调，自带路由

koa：基于promise，不带路由

版本：1：generator

   	    2：generator&promise

​	       3：未发布

```js
const Koa = require('Koa')
const Router = require('koa-router')

let server = new Koa()
server.listen(8080)

let router = new Router()
// router.get('/a', (ctx, next) => {
// 	ctx.req
// 	ctx.res
// })
router.get('/a', async ctx => {
	ctx.body = 'aa'
	ctx.body += 'bb'
})
server.use(router.routes())

```

### koa-router

```js
const Koa = require('Koa')
const Router = require('koa-router')

let server = new Koa
server.listen(8080)

let router = new Router
// router.get('/a', (ctx, next) => {
// 	ctx.req
// 	ctx.res
// })
router.get('/a', async ctx => {
	ctx.body = 'aa'
	ctx.body += 'bb'
})

server.use(router.routes())
```

get，post，all（express是use）

#### 嵌套路由 

```js
const Koa = require('Koa')
const Router = require('koa-router')

let server = new Koa()
server.listen(8080)

let router = new Router()
// router.get('/a', (ctx, next) => {
// 	ctx.req
// 	ctx.res
// })
router.get('/a', async ctx => {
	ctx.body = 'aa'
	ctx.body += 'bb'
})

// 嵌套路由
let userRouter = new Router()
userRouter.get('/', async ctx =>{ctx.body = 'user'})
let admin = new Router()
// /user/admin/a
admin.get('/a', async ctx =>{ctx.body = 'admin-a'})
let comp = new Router()
comp.get('/a', async ctx =>{ctx.body = 'comp-a'})

userRouter.use('/admin', admin.routes())
userRouter.use('/comp', comp.routes())

let newsRouter = new Router()

router.use('/user', userRouter.routes())
router.use('/news', newsRouter.routes())

server.use(router.routes())

```

分模块

```js
// server.js
const Koa = require('koa')
const Router = require('koa-router')

let server = new Koa()
server.listen(8080)

let router = new Router()

router.get('/a', ctx => {
    ctx.body = 'aa'
    ctx.body += 'bb'
})
router.use('/user', require('./routers/user'))

server.use(router.routes())
// routers/user/index.js
const Router = require('koa-router')

let router = new Router()
router.get('/', ctx => {
    ctx.body = 'user'
})
router.use('/admin', require('./admin'))
router.use('/comp', require('./comp'))

module.exports = router.routes()
// routers/user/admin.js
const Router = require('koa-router')

let router = new Router()
router.get('/', ctx => {
    ctx.body = 'admin'
})
router.get('/a', ctx => {
    ctx.body = 'admin-a'
})

module.exports = router.routes()
```

#### 参数传递

1. ctx.params
2. ctx.query

```js
// 两种传参方式
// urlencoed：顺序灵活，可省略，不利于SEO
const Koa = require('koa')
const Router = require('koa-router')

let server = new Koa()
server.listen(8080)

let router = new Router()
router.get('/a', ctx => {
    ctx.body = ctx.query.id
})
// 可添加多个
router.get('/a/:id', async (ctx, next) => {
    ctx.body = ctx.params.id
    await next()
})
router.get('/a/123', (ctx, next) => {
    ctx.body += ctx.params.id
})

server.use(router.routes())
```

#### ctx参数

```js
const Koa = require('koa')
const Router = require('koa-router')

let server = new Koa()
server.listen(8080)

// server.context相当于ctx的原型
// 可以放一些全局参数
server.context.a = 12

let router = new Router()
router.get('/a', async (ctx, next) => {
    let {user, pass} = ctx.query
    if(user && pass) {
        ctx.body = user + pass
    }else {
        // ctx.throw(code, msg)
        ctx.throw(400, 'user and pass are required')
    }
    // ctx.assert(condition, code, msg) // 和 throw 类似
    // ctx.assert(user, 400, 'user is required')
    // ctx.assert(pass, 400, 'pass is required')
    

    // ctx.request
    // ctx.response
    // ctx.method
    // ctx.url
    // ctx.path
    // ctx.query
    // 客户端ip
    // ctx.ip                 
    // ctx.headers
    console.log('ctx.url', ctx.url)
    console.log('ctx.method', ctx.method)
    console.log('ctx.path', ctx.path)
    console.log('ctx.ip', ctx.ip)
    console.log('ctx.headers', ctx.headers)
    console.log('ctx.request', ctx.method)
    console.log('ctx.response', ctx.method)
})

server.use(router.routes())

// 设置状态码
// ctx.state = 305
// 重定向
// ctx.redirect()
// 下载文件
// ctx.attachment()       
```

### koa-static

可缓存

```js
const Koa = require('koa')
const Router = require('koa-router')
const static = require('koa-static')

let server = new Koa()
server.listen(8080)

let router = new Router()
server.use(router.routes())

server.use(static('./static', {
    // 缓存时间
    maxage: 86400*1000,
    // 默认访问文件
    index: '1.html'
}))
```

结合路由设置缓存

```js
// 结合路由设置缓存时间
let staticRouter = new Router()
// .表示除换行符以外的单个字符需要转义，i忽略大小写
// 图片资源
staticRouter.all((/(\.jpg|\.png|\.gif)$/i), static('./static', {
    maxage: 60*86400*1000
}))
// 其余资源
staticRouter.all('*', static('./static', {
    maxage: 30*86400*1000
}))

server.use(staticRouter.routes())
```

### koa-better-body

可以处理二进制数据

ctx.request.fields

```js
const Koa = require('koa')
const Router = require('koa-router')
// 会有警告
const body = require('koa-better-body')

let server = new Koa()
server.listen(8080)

let router = new Router()

server.use(body({
    uploadDir: './static/upload'
}))

router.post('/upload', ctx => {
    // 文件和post数据
    console.log(ctx.request.fields)
    ctx.body = 'hhh'
})

server.use(router.routes())
```

### cookie

自带

```js
const Koa = require('koa')
let server = new Koa()
server.listen(8080)
// 滚动密钥
server.keys = [
    '1995-naixes',
    'sd34-naixes',
    '89ss-naixes'
]
server.use(async ctx => {
    ctx.cookies.set('user', 'naixes', {signed: true})
    console.log(ctx.cookies.get('user', {signed: true}))
    ctx.body = 'hhh'
})
```

### koa-session

```js
const Koa = require('koa')
const session = require('koa-session')
let server = new Koa()
server.listen(8080)
// 滚动密钥
server.keys = [
    '1995-naixes',
    'sd34-naixes',
    '89ss-naixes'
]

server.use(session({
    maxAge: 20*60*1000,
    // 自动续期
    renew: true
}, server))

server.use(async ctx => {
    if(!ctx.session['view']) {
        ctx.session['view'] = 0
    }else {
        ctx.session['view']++
    }

    ctx.body = `欢迎你第${ctx.session['view']}次来访`
})
```

### 数据库引入及错误处理

```js
const mysql = require('mysql')
const co = require('co-mysql')

let conn = mysql.createPool({
    host: 'localhost',
    user: 'admin',
    password: 'root',
    database: 'node'
})
let db = co(conn)

module.exports = db
```

```js
const Koa = require('koa')
const Router = require('koa-router')

let server = new Koa()
server.listen(8080)
// 引入数据库
server.context.db = require('./libs/database')
server.use(async (ctx, next) => {
    try {
        await next()
    } catch (error) {
        ctx.body = '程序出错'
    }
})
let router = new Router()
router.all('*', async (ctx, next) => {
    try {
        await next()
    } catch (error) {
        ctx.body = 'router出错'
    }
})
router.get('/a', async ctx => {
    ctx.body = div.title
})
server.use(router.routes())
```

### uuid

token用

`npm i uuid`

```js
const guid = require('uuid/v4')
```



### 服务器渲染

pug(jade)：侵入式

ejs：侵入式

1. 安全

2. 耗费流量

3. 用户体验不好，需要刷新页面

4. 有利于SEO

#### pug

```js
doctype
html
	//- 缩进来表现层级关系
    head
        //- ()属性
        meta(charset='utf-8')
        meta(name='site', content='test')
        //- =赋值
        title=title
        //- .多行代码
        script.
            window.onload = function() {
                let dom = document.getElementById('div')
                dom.onclick = function() {}
            }
    body
        ul
        	//- 循环：each xx in xxs
            each user in users
                li(class='user-item clearfix')
                    span(class='name')=user.name
                    span(class='pass')=user.pass
```

```js
const pug = require('pug')

pug.renderFile('./template/hello.pug', {
    pretty: true,
    title: 'hello',
    users: [
        {name: 'a', pass: '1'},
        {name: 'b', pass: '2'},
        {name: 'c', pass: '3'},
    ]
}, (err, data) => {
    if(err) {
        console.log(err)
    }else {
        console.log(data)
    }
})
```

#### ejs

<%=xxx%>，语法和js一样，<% include 路径 -%>//-减少空行

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title><%=title%></title>
</head>
<body>
    <%for(let i=0;i<users.length;i++){%>
        <div class="">
            name:<%=users[i].name%>
            pass:<%=users[i].pass%>
        </div>
    <%}%>
</body>
</html>
```

```js
// ejs内置
const ejs = require('ejs')

// 和pug一样
ejs.renderFile('./template/hello.ejs', {
    ...
}, (err, data) => {
    ...
})
```

koa-ejs

```js
const Koa = require('koa')
const ejs = require('koa-ejs')
const path = require('path')

let server = new Koa()
server.listen(8080)

ejs(server, {
    // 模板目录
    root: path.resolve(__dirname, 'template'),
    // true会再加一层目录
    layout: false,
    // 扩展名
    viewExt: 'ejs',
    cache: false,
    debug: false
})

server.use(async ctx => {
    await ctx.render('hello', {
        title: 'hello',
        users: [
            {name: 'a', pass: '1'},
            {name: 'b', pass: '2'},
            {name: 'c', pass: '3'},
        ]
    })
})
```

### 案例

**目录结构**

```
node-demo                      #項目目录
│
├── log                        #日志
│
├── lib                        #通用库
│   └── database.js            #数据库配置
│   
├── static                     #静态资源
|   |── upload				  #上传目录
│   └── <other files>          #
│
|── upload                     #
│   └── <other files>          #
|
├── config.js                #全局配置
|
├── node_modules                
└── package.json                
```



加路由的两种方法：/的问题，本质是字符串拼接

统一处理：正常情况的数据处理

管理员使用文件管理

md5：散列算法

crypto

sha1/128/256

await-fs

## Controllers模块

将路由的具体操作按照业务模块进行划分如：user.js

```javascript
exports.doLogin = function(req, res, next) {}
```

## 异步编程

### 并发与并行

并发是宏观概念，我分别有任务 A 和任务 B，在一段时间内通过任务间的切换完成了这两个任务，这种情况就可以称之为并发。

并行是微观概念，假设 CPU 中存在两个核心，那么我就可以同时完成任务 A、B。同时完成多个任务的情况就可以称之为并行。

### 回调函数

字面上的理解，回调函数就是一个参数，将这个函数作为参数传到另一个函数里面，当那个函数执行完之后，再执行传进去的这个函数。这个过程就叫做回调。 

但是回调函数有一个致命的弱点，就是容易写出回调地狱（Callback hell）。假设多个请求存在依赖性，你可能就会写出如下代码：

```js
ajax(url, () => {
    // 处理逻辑
    ajax(url1, () => {
        // 处理逻辑
        ajax(url2, () => {
            // 处理逻辑
        })
    })
})
```

以上代码看起来不利于阅读和维护，当然把函数分开来写会利于阅读，但没有解决根本问题

回调地狱的根本问题就是：

1. 嵌套函数存在耦合性，一旦有所改动，就会牵一发而动全身
2. 嵌套函数一多，就很难处理错误

当然，回调函数还存在着别的几个缺点，比如不能使用 `try catch` 捕获错误，不能直接 `return`。

### 回调封装异步函数

```javascript
function get(url, cb) {
    var xhr = new XMLHttpRequest()
    xhr.onload = function() {
        callback(xhr.responseText)
    }
    xhr.open('get', url, true)
    xhr.send()
}
get('data.json', function(data) {
    console.log(data)
})
```

### 哨兵变量

在多个异步事件结束（或者循环）之后做某件事情，可以使用哨兵变量（计数器）

```javascript
var count = 0
setTimeoute(function() {todo()})
setTimeoute(function() {todo()})
setTimeoute(function() {todo()})
todo() {
    count++
    if(count === 3) {}
}
```

### Promise（ES6）

- 回调地狱：使用回调嵌套的方式保证异步操作的执行顺序

Promise是一个构造函数，用来封装异步函数

### promise封装异步函数

封装Promise版本的readFile()

promise容器一旦创建就开始执行里面的代码，要想按需执行，要把它放到方法中去，由于外面无法访问到promise无法传递回调，所以将promise返回，使用.then给promise绑定回调。因为.then方法先于异步函数执行，回调函数可以正常绑定。

```javascript
var fs = require('fs')
function pReadFile(filePath) {
    return new Promise(function(resolve, reject) {
        fs.readFile(filePath, function(err, data) {
            if(err) {
                reject(err)
            }
            resolve(data)
        })
    })
}

pReadFile.('aa.js')
  .then(function(data) {
    // todo
    return pReadFile.('bb.js')
  })
  .then(function(data) {
    // todo
    return pReadFile.('cc.js')
  })
```

jquery的ajax也支持Promise的方式，返回Promise对象


```javascript
$.get('')
  .then(data => {
  	console.log(data)
    return $.get('')
  })
  .then(...)
```
mongoose所有的API都支持promise

```javascript
// 注册用户
User.findOne({name: 'a'})
  .then(function(data) {
    if(data) {
        console.log('已存在用户')
    }
    return new User({
        name: 'a',
        pw: '123'
    }).save()
  })
  .then(function(ret) {})
```

promise也是存在一些缺点的，比如无法取消 `Promise`，错误需要通过回调函数捕获， 代码冗余 ，原来的任务被 Promise 包装了一下，不管什么操作，一眼看去都是一堆then，原来的语义变得很不清楚。 

### Generator

语法上，首先可以把它理解成，Generator 函数是一个**状态机**，封装了多个内部状态。 

执行 Generator 函数会返回一个遍历器对象，也就是说，Generator 函数除了状态机，还是一个**遍历器对象生成函数**。返回的遍历器对象，可以依次遍历 Generator 函数内部的每一个状态。

形式上，Generator 函数是一个普通函数，但是有两个特征。一是，`function`关键字与函数名之间有一个星号；二是，函数体内部使用`yield`表达式，定义不同的内部状态（`yield`在英语里的意思就是“产出”）。

```js
function* helloWorldGenerator() {
  yield 'hello';
  yield 'world';
  return 'ending';
}

var hw = helloWorldGenerator();
```

Generator 函数的调用方法与普通函数一样。不同的是，调用 Generator 函数后，该函数并不执行，返回的也不是函数运行结果，而是一个**指向内部状态的指针对象**，也就是遍历器对象（Iterator Object）。 

下一步，必须调用遍历器对象的`next`方法，使得指针移向下一个状态。也就是说，每次调用`next`方法，内部指针就从函数头部或上一次停下来的地方开始执行，直到遇到下一个`yield`表达式（或`return`语句）为止。换言之，Generator 函数是分段执行的，`yield`表达式是**暂停执行的标记**，而`next`方法可以恢复执行。 

```js
hw.next() // {value: 'hello', done: false}
hw.next() // {value: 'world', done: false}
hw.next() // {value: 'ending', done: true}
hw.next() // {value: undefined, done: false}
```

总结一下，调用 Generator 函数，返回一个遍历器对象，代表 Generator 函数的内部指针。以后，每次调用遍历器对象的`next`方法，就会返回一个有着`value`和`done`两个属性的对象。`value`属性表示当前的内部状态的值，是`yield`表达式后面那个表达式的值；`done`属性是一个布尔值，表示是否遍历结束。 

#### yield表达式

- 遍历器对象的`next`方法的运行逻辑如下。

（1）遇到`yield`表达式，就暂停执行后面的操作，并将紧跟在`yield`后面的那个表达式的值，作为返回的对象的`value`属性值。

（2）下一次调用`next`方法时，再继续往下执行，直到遇到下一个`yield`表达式。

（3）如果没有再遇到新的`yield`表达式，就一直运行到函数结束，直到`return`语句为止，并将`return`语句后面的表达式的值，作为返回的对象的`value`属性值。

（4）如果该函数没有`return`语句，则返回的对象的`value`属性值为`undefined`。

需要注意的是，`yield`表达式后面的表达式，只有当调用`next`方法、内部指针指向该语句时才会执行，因此等于为 JavaScript 提供了手动的“惰性求值”（Lazy Evaluation）的语法功能。

- `yield`表达式与`return`语句

相似之处在于，都能返回紧跟在语句后面的那个表达式的值。

区别在于每次遇到`yield`，函数暂停执行，下一次再从该位置继续向后执行，而`return`语句不具备**位置记忆**的功能。一个函数里面，只能执行一次（或者说一个）`return`语句，但是可以**执行多次**（或者说多个）`yield`表达式。正常函数只能返回一个值，因为只能执行一次`return`

Generator 函数可以返回一系列的值，因为可以有任意多个`yield`。从另一个角度看，也可以说 Generator 生成了一系列的值，这也就是它的名称的来历（英语中，generator 这个词是“生成器”的意思）。

Generator 函数可以不用`yield`表达式，这时就变成了一个单纯的暂缓执行函数。

- `yield`表达式只能用在 Generator 函数里面，用在其他地方都会报错。 

- `yield`表达式如果用在另一个表达式之中，必须放在圆括号里面。

  ```js
  function* demo() {
    console.log('Hello' + yield); // SyntaxError
    console.log('Hello' + yield 123); // SyntaxError
  
    console.log('Hello' + (yield)); // OK
    console.log('Hello' + (yield 123)); // OK
  }
  ```

  `yield`表达式用作函数参数或放在赋值表达式的右边，可以不加括号。

  ```js
  function* demo() {
    foo(yield 'a', yield 'b'); // OK
    let input = yield; // OK
  }
  ```

- `yield`表达式本身**没有返回值**，或者说总是返回`undefined`。`next`方法可以带一个**参数**，该参数就会被当作上一个`yield`表达式的返回值。 当执行第一次 `next` 时，传参会被忽略。

`Generator` 函数一般见到的不多，其实也于他有点绕有关系，并且一般会配合 co 库去使用。当然，我们可以通过 `Generator` 函数解决回调地狱的问题，可以把之前的回调地狱例子改写为如下代码：

```js
function *fetch() {
    yield ajax(url, () => {})
    yield ajax(url1, () => {})
    yield ajax(url2, () => {})
}
let it = fetch()
let result1 = it.next()
let result2 = it.next()
let result3 = it.next()
```

### Generator的异步应用

#### 协程

传统的编程语言，早有异步编程的解决方案（其实是多任务的解决方案）。其中有一种叫做"程"（coroutine），意思是多个线程互相协作，完成异步任务。

协程有点像函数，又有点像线程。它的运行流程大致如下。

- 第一步，协程`A`开始执行。
- 第二步，协程`A`执行到一半，进入暂停，执行权转移到协程`B`。
- 第三步，（一段时间后）协程`B`交还执行权。
- 第四步，协程`A`恢复执行。

上面流程的协程`A`，就是异步任务，因为它分成两段（或多段）执行。

举例来说，读取文件的协程写法如下。

```js
function* asyncJob() {
  // ...其他代码
  var f = yield readFile(fileA);
  // ...其他代码
}
```

上面代码的函数`asyncJob`是一个协程，它的奥妙就在其中的`yield`命令。它表示执行到此处，执行权将交给其他协程。也就是说，`yield`命令是异步两个阶段的分界线。

协程遇到`yield`命令就暂停，等到执行权返回，再从暂停的地方继续往后执行。它的最大优点，就是代码的**写法非常像同步操作**，如果去除`yield`命令，简直一模一样。

#### 协程的 Generator 函数实现

Generator 函数是协程在 ES6 的实现，最大特点就是可以交出函数的执行权（即暂停执行）。

整个 Generator 函数就是一个封装的异步任务，或者说是异步任务的容器。异步操作需要暂停的地方，都用`yield`语句注明。Generator 函数的执行方法如下。

```js
function* gen(x) {
  var y = yield x + 2;
  return y;
}
var g = gen(1); // 调用 Generator 函数，会返回一个内部指针（即遍历器）g
g.next() // { value: 3, done: false }
g.next() // { value: undefined, done: true }
```

#### Generator 函数的数据交换和错误处理

Generator 函数可以暂停执行和恢复执行，这是它能封装异步任务的根本原因。除此之外，它还有两个特性，使它可以作为异步编程的完整解决方案：函数体内外的数据交换和错误处理机制。

`next`返回值的 value 属性，是 Generator 函数向外输出数据；`next`方法还可以接受参数，向 Generator 函数体内输入数据。

```js
function* gen(x){
  var y = yield x + 2;
  return y;
}
var g = gen(1);
g.next() // { value: 3, done: false }
g.next(2) // { value: 2, done: true }
```

Generator 函数内部还可以部署错误处理代码，捕获函数体外抛出的错误。

```js
function* gen(x){
  try {
    var y = yield x + 2;
  } catch (e){
    console.log(e);
  }
  return y;
}
var g = gen(1);
g.next();
g.throw('出错了'); // 使用指针对象的throw方法抛出的错误，可以被函数体内的try...catch代码块捕获。这意味着，出错的代码与处理错误的代码，实现了时间和空间上的分离，这对于异步编程无疑是很重要的。
// 出错了
```

#### 异步任务的封装

下面看看如何使用 Generator 函数，执行一个真实的异步任务。

```js
var fetch = require('node-fetch');

function* gen(){
  var url = 'https://api.github.com/users/github';
  var result = yield fetch(url);
  console.log(result.bio);
}
```

上面代码中，Generator 函数封装了一个异步操作，该操作先读取一个远程接口，然后从 JSON 格式的数据解析信息。就像前面说过的，这段代码非常像同步操作，除了加上了`yield`命令。

执行这段代码的方法如下。

```js
var g = gen();
var result = g.next();

result.value.then(function(data){ // 由于Fetch模块返回的是一个 Promise 对象，因此要用then方法调用下一个next方法。
  return data.json();
}).then(function(data){
  g.next(data);
});
```

可以看到，虽然 Generator 函数将异步操作表示得很简洁，但是流程管理却不方便（即何时执行第一阶段、何时执行第二阶段）。

#### Thunk 函数

Thunk 函数是自动执行 Generator 函数的一种方法。

##### 参数的求值策略

Thunk 函数早在上个世纪 60 年代就诞生了。

那时，编程语言刚刚起步，计算机学家还在研究，编译器怎么写比较好。一个争论的焦点是"求值策略"，即函数的参数到底应该何时求值。

```js
var x = 1;
function f(m) {
  return m * 2;
}
f(x + 5) // 请问，这个表达式应该何时求值？
```

一种意见是"传值调用"（call by value），即在进入函数体之前，就计算`x + 5`的值（等于 6），再将这个值传入函数`f`。C 语言就采用这种策略。

另一种意见是“传名调用”（call by name），即直接将表达式`x + 5`传入函数体，只在用到它的时候求值。Haskell 语言采用这种策略。

```js
f(x + 5)
// 传名调用时，等同于
(x + 5) * 2
```

传值调用和传名调用各有利弊。传值调用比较简单，但是对参数求值的时候，实际上还没用到这个参数，有可能造成性能损失。

##### Thunk 函数的含义

编译器的“传名调用”实现，往往是将参数放到一个临时函数之中，再将这个临时函数传入函数体。这个临时函数就叫做 Thunk 函数。

```js
function f(m) {
  return m * 2;
}
f(x + 5);
// 等同于
var thunk = function () {
  return x + 5;
};
function f(thunk) {
  return thunk() * 2;
}
```

这就是 Thunk 函数的定义，它是“传名调用”的一种实现策略，用来替换某个表达式。

##### JavaScript 语言的 Thunk 函数

JavaScript 语言是传值调用，它的 Thunk 函数含义有所不同。在 JavaScript 语言中，Thunk 函数替换的不是表达式，而是多参数函数，将其替换成一个**只接受回调函数作为参数的单参数函数。**

```js
// 正常版本的readFile（多参数版本）
fs.readFile(fileName, callback);

// Thunk版本的readFile（单参数版本）
var Thunk = function (fileName) {
  return function (callback) {
    return fs.readFile(fileName, callback);
  };
};

var readFileThunk = Thunk(fileName);
readFileThunk(callback);
```

上面代码中，`fs`模块的`readFile`方法是一个多参数函数，经过转换器处理，它变成了一个单参数函数，只接受回调函数作为参数。这个单参数版本，就叫做 Thunk 函数。

任何函数，只要参数有回调函数，就能写成 Thunk 函数的形式。下面是一个简单的 Thunk 函数转换器。

```js
// ES5版本
var Thunk = function(fn){
  return function (){
    var args = Array.prototype.slice.call(arguments);
    return function (callback){
      args.push(callback);
      return fn.apply(this, args);
    }
  };
};

// ES6版本
const Thunk = function(fn) {
  return function (...args) {
    return function (callback) {
      return fn.call(this, ...args, callback);
    }
  };
};
```

使用上面的转换器，生成`fs.readFile`的 Thunk 函数。

```js
var readFileThunk = Thunk(fs.readFile);
readFileThunk(fileA)(callback);
```

下面是另一个完整的例子。

```js
function f(a, cb) {
  cb(a);
}
const ft = Thunk(f);
ft(1)(console.log) // 1
```

##### Thunkify 模块

生产环境的转换器，建议使用 Thunkify 模块。

首先是安装。

```
$ npm install thunkify
```

使用方式如下。

```js
var thunkify = require('thunkify');
var fs = require('fs');

var read = thunkify(fs.readFile);
read('package.json')(function(err, str){
  // ...
});
```

Thunkify 的源码与上一节那个简单的转换器非常像。

```js
function thunkify(fn) {
  return function() {
    var args = new Array(arguments.length);
    var ctx = this;

    for (var i = 0; i < args.length; ++i) {
      args[i] = arguments[i];
    }

    return function (done) {
      var called; // 变量called确保回调函数只运行一次

      args.push(function () {
        if (called) return;
        called = true;
        done.apply(null, arguments);
      });

      try {
        fn.apply(ctx, args);
      } catch (err) {
        done(err);
      }
    }
  }
};
```

它的源码主要多了一个检查机制。这样的设计与下文的 Generator 函数相关。请看下面的例子。

```js
function f(a, b, callback){
  var sum = a + b;
  callback(sum);
  callback(sum);
}

var ft = thunkify(f);
var print = console.log.bind(console);
ft(1, 2)(print);
// 3
```

上面代码中，由于`thunkify`只允许回调函数执行一次，所以只输出一行结果。

##### Generator 函数的流程管理

Thunk 函数现在可以用于 Generator 函数的自动流程管理。

Generator 函数可以自动执行。

```js
function* gen() {
  // ...
}

var g = gen();
var res = g.next();

while(!res.done){
  console.log(res.value);
  res = g.next();
}
```

上面代码中，Generator 函数`gen`会自动执行完所有步骤。

但是，这不适合异步操作。如果必须保证前一步执行完，才能执行后一步，上面的自动执行就不可行。这时，Thunk 函数就能派上用处。以读取文件为例。下面的 Generator 函数封装了两个异步操作。

```js
var fs = require('fs');
var thunkify = require('thunkify'); // Thunkify 模块
var readFileThunk = thunkify(fs.readFile);

var gen = function* (){
  var r1 = yield readFileThunk('/etc/fstab'); // readFileThunk('/etc/fstab')返回参数为回调的函数
  console.log(r1.toString());
  var r2 = yield readFileThunk('/etc/shells');
  console.log(r2.toString());
};
```

上面代码中，`yield`命令用于将程序的执行权移出 Generator 函数，那么就需要一种方法，将执行权再交还给 Generator 函数。这种方法就是 Thunk 函数，因为它可以在回调函数里，将执行权交还给 Generator 函数。为了便于理解，我们先看如何手动执行上面这个 Generator 函数。

```js
var g = gen();

var r1 = g.next();
r1.value(function (err, data) { // 返回第一步的信息
  if (err) throw err;
  var r2 = g.next(data);
  r2.value(function (err, data) {
    if (err) throw err;
    g.next(data);
  });
});
```

上面代码中，变量`g`是 Generator 函数的内部指针，表示目前执行到哪一步。`next`方法负责将指针移动到下一步，并返回该步的信息（`value`属性和`done`属性）。

仔细查看上面的代码，可以发现 Generator 函数的执行过程，其实是将同一个回调函数，反复传入`next`方法的`value`属性。这使得我们可以用递归来自动完成这个过程。

##### Thunk 函数的自动流程管理

Thunk 函数真正的威力，在于可以自动执行 Generator 函数。下面就是一个基于 Thunk 函数的 Generator 执行器。

```js
function run(fn) {
  var gen = fn();
  // 内部的next函数就是 Thunk 的回调函数。
  function next(err, data) {
    var result = gen.next(data);
    if (result.done) return;
    result.value(next); // 前提是每一个异步操作，都要是 Thunk 函数，也就是说，跟在yield命令后面的必须是 Thunk 函数。
  }
  next();
}
function* g() {
  // ...
}
run(g);
```

上面代码的`run`函数，就是一个 Generator 函数的自动执行器，内部的next函数就是 Thunk 的回调函数。`next`函数先将指针移到 Generator 函数的下一步（`gen.next`方法），然后判断 Generator 函数是否结束（`result.done`属性），如果没结束，就将`next`函数再传入 Thunk 函数（`result.value`属性），否则就直接退出。

有了这个执行器，执行 Generator 函数方便多了。不管内部有多少个异步操作，直接把 Generator 函数传入`run`函数即可。当然，前提是每一个异步操作，都要是 Thunk 函数，也就是说，跟在`yield`命令后面的必须是 Thunk 函数。

```js
var g = function* (){
  var f1 = yield readFileThunk('fileA');
  var f2 = yield readFileThunk('fileB');
  // ...
  var fn = yield readFileThunk('fileN');
};

run(g);
```

上面代码中，函数`g`封装了`n`个异步的读取文件操作，只要执行`run`函数，这些操作就会自动完成。这样一来，异步操作不仅可以写得像同步操作，而且一行代码就可以执行。

Thunk 函数并不是 Generator 函数自动执行的唯一方案。因为自动执行的关键是，必须有一种机制，自动控制 Generator 函数的流程，接收和交还程序的执行权。回调函数可以做到这一点，Promise 对象也可以做到这一点。

#### co 模块

#### 基本用法

[co 模块](https://github.com/tj/co)是著名程序员 TJ Holowaychuk 于 2013 年 6 月发布的一个小工具，用于 Generator 函数的自动执行。

下面是一个 Generator 函数，用于依次读取两个文件。

```js
var gen = function* () {
  var f1 = yield readFile('/etc/fstab');
  var f2 = yield readFile('/etc/shells');
  console.log(f1.toString());
  console.log(f2.toString());
};
```

co 模块可以让你不用编写 Generator 函数的执行器。

```js
var co = require('co');
co(gen); // Generator 函数只要传入co函数，就会自动执行。
```

`co`函数返回一个`Promise`对象，因此可以用`then`方法添加回调函数。

```js
co(gen).then(function (){
  console.log('Generator 函数执行完成');
});
```

上面代码中，等到 Generator 函数执行结束，就会输出一行提示。

##### co 模块的原理

前面说过，Generator 就是一个异步操作的容器。它的自动执行需要一种机制，当异步操作有了结果，能够自动交回执行权。

两种方法可以做到这一点。

（1）回调函数。将异步操作包装成 Thunk 函数，在回调函数里面交回执行权。

（2）Promise 对象。将异步操作包装成 Promise 对象，用`then`方法交回执行权。

co 模块其实就是将两种自动执行器（Thunk 函数和 Promise 对象），包装成一个模块。使用 co 的前提条件是，Generator 函数的`yield`命令后面，只能是 Thunk 函数或 Promise 对象。如果数组或对象的成员，全部都是 Promise 对象，也可以使用 co，详见后文的例子。

##### 基于 Promise 对象的自动执行

还是沿用上面的例子。首先，把`fs`模块的`readFile`方法包装成一个 Promise 对象。

```js
var fs = require('fs');

var readFile = function (fileName){
  return new Promise(function (resolve, reject){
    fs.readFile(fileName, function(error, data){
      if (error) return reject(error);
      resolve(data);
    });
  });
};

var gen = function* (){
  var f1 = yield readFile('/etc/fstab');
  var f2 = yield readFile('/etc/shells');
  console.log(f1.toString());
  console.log(f2.toString());
};
```

然后，手动执行上面的 Generator 函数。

```js
var g = gen();

g.next().value.then(function(data){
  g.next(data).value.then(function(data){
    g.next(data);
  });
});
```

手动执行其实就是用`then`方法，层层添加回调函数。理解了这一点，就可以写出一个自动执行器。

```js
function run(gen){
  var g = gen();

  function next(data){
    var result = g.next(data);
    if (result.done) return result.value;
    result.value.then(function(data){
      next(data);
    });
  }
  next();
}

run(gen);
```

上面代码中，只要 Generator 函数还没执行到最后一步，`next`函数就调用自身，以此实现自动执行。

##### co 模块的源码

co 就是上面那个自动执行器的扩展，它的源码只有几十行，非常简单。

首先，co 函数接受 Generator 函数作为参数，返回一个 Promise 对象。

```js
function co(gen) {
  var ctx = this;

  return new Promise(function(resolve, reject) {
  });
}
```

在返回的 Promise 对象里面，co 先检查参数`gen`是否为 Generator 函数。如果是，就执行该函数，得到一个内部指针对象；如果不是就返回，并将 Promise 对象的状态改为`resolved`。

```js
function co(gen) {
  var ctx = this;

  return new Promise(function(resolve, reject) {
    if (typeof gen === 'function') gen = gen.call(ctx);
    if (!gen || typeof gen.next !== 'function') return resolve(gen);
  });
}
```

接着，co 将 Generator 函数的内部指针对象的`next`方法，包装成`onFulfilled`函数。这主要是为了能够捕捉抛出的错误。

```js
function co(gen) {
  var ctx = this;

  return new Promise(function(resolve, reject) {
    if (typeof gen === 'function') gen = gen.call(ctx);
    if (!gen || typeof gen.next !== 'function') return resolve(gen);

    onFulfilled();
    function onFulfilled(res) {
      var ret;
      try {
        ret = gen.next(res);
      } catch (e) {
        return reject(e);
      }
      next(ret);
    }
  });
}
```

最后，就是关键的`next`函数，它会反复调用自身。

```js
function next(ret) {
  if (ret.done) return resolve(ret.value); // 检查当前是否为 Generator 函数的最后一步，如果是就返回。
  var value = toPromise.call(ctx, ret.value); // 确保每一步的返回值，是 Promise 对象。
  if (value && isPromise(value)) return value.then(onFulfilled, onRejected); // 使用then方法，为返回值加上回调函数，然后通过onFulfilled函数再次调用next函数。
  return onRejected( // 在参数不符合要求的情况下（参数非 Thunk 函数和 Promise 对象），将 Promise 对象的状态改为rejected，从而终止执行。
    new TypeError(
      'You may only yield a function, promise, generator, array, or object, '
      + 'but the following object was passed: "'
      + String(ret.value)
      + '"'
    )
  );
}
```

上面代码中，`next`函数的内部代码，一共只有四行命令。

### 异步函数（ES6）

async 函数是什么？一句话，它就是 Generator 函数的语法糖。function前面有关键字`async`的函数，会返回Promise对象

`async`函数对 Generator 函数的改进，体现在以下四点。

（1）内置执行器。

Generator 函数的执行必须靠执行器，需要调用`next`方法，或者用`co`模块，才能真正执行，得到最后结果，而`async`函数自带执行器。也就是说，`async`函数的执行，与普通函数一模一样，只要一行。

```js
asyncReadFile();
```

（2）更好的语义。

`async`和`await`，比起星号和`yield`，语义更清楚了。`async`表示函数里有异步操作，`await`表示紧跟在后面的表达式需要等待结果。

（3）更广的适用性。

`co`模块约定，`yield`命令后面只能是 Thunk 函数或 Promise 对象，而`async`函数的`await`命令后面，可以是 Promise 对象和原始类型的值（数值、字符串和布尔值，但这时会自动转成立即 resolved 的 Promise 对象）。

（4）返回值是 Promise。

`async`函数的返回值是 Promise 对象，这比 Generator 函数的返回值是 Iterator 对象方便多了。你可以用`then`方法指定下一步的操作。

进一步说，`async`函数完全可以看作多个异步操作，包装成的一个 Promise 对象，而`await`命令就是内部`then`命令的语法糖。

`async`函数返回一个 Promise 对象，可以使用`then`方法添加回调函数。当函数执行的时候，一旦遇到`await`就会先返回，等到异步操作完成，再接着执行函数体内后面的语句。 

- `async`函数内部`return`语句返回的值，会成为`then`方法回调函数的参数。 但如果函数内部抛出错误那么就会调用Promise.reject()返回一个promise 对象。
- `async`函数内部抛出错误，会导致返回的 Promise 对象变为`reject`状态。抛出的错误对象会被`catch`方法回调函数接收到。 
- `async`函数返回的 Promise 对象，必须等到内部所有`await`命令后面的 Promise 对象执行完，才会发生状态改变，除非遇到`return`语句或者抛出错误。也就是说，只有`async`函数内部的异步操作执行完，才会执行`then`方法指定的回调函数。 

await：语法`await expression `，只能用在异步函数中，它后面可以放任何表达式，不过我们更多的是放一个返回promise 对象的表达式。 

- 其中 `expression` 是一个 `Promise` 对象或者任何要等待的值 
- `await` 在等待 Promise 对象时会导致 `async function` 暂停执行, 一直到 Promise 对象决议之后才会 `async function` 继续执行. 
- 任何一个`await`语句后面的 Promise 对象变为`reject`状态，那么整个`async`函数都会中断执行。 有时，我们希望即使前一个异步操作失败，也不要中断后面的异步操作。这时可以将第一个`await`放在`try...catch`结构里面，这样不管这个异步操作是否成功，第二个`await`都会执行。 另一种方法是`await`后面的 Promise 对象再跟一个`catch`方法，处理前面可能出现的错误。 
-  await 的同步只是在 async 函数里同步，但并不会阻塞其他外部代码的执行。而这也是 await 必须放在 async 函数里的原因 

`async` 和 `await` 可以说是异步终极解决方案了，相比直接使用 `Promise` 来说，优势在于处理 `then`的调用链，能够更清晰准确的写出代码，并且也能优雅地解决回调地狱问题。

当然也存在一些缺点，因为 `await` 将异步代码改造成了同步代码，如果多个异步代码没有依赖性却使用了 `await` 会导致性能上的降低。 

https://www.cnblogs.com/SamWeb/p/8417940.html

#### async 函数的实现原理

async 函数的实现原理，就是将 Generator 函数和自动执行器，包装在一个函数里。 

```js
async function fn(args) {
  // ...
}
// 等同于
function fn(args) {
  return spawn(function* () {
    // ...
  });
}
```

所有的`async`函数都可以写成上面的第二种形式，其中的`spawn`函数就是自动执行器。

Async 函数的实现最简洁，最符合语义，几乎没有语义不相关的代码。它将 Generator 写法中的自动执行器，改在语言层面提供，不暴露给用户，因此代码量最少。如果使用 Generator 写法，自动执行器需要用户自己提供。 

## 案例

### 用户注册

发出请求==》服务端收到请求==》执行中间件==》进入路由==》匹配路径==》进入controller处理请求==》根据请求处理数据models==》发出响应==》渲染页面view

## 其他

region注释

### MD5加密

MD5加密，不可逆

包：`npm i blueimp-md5 -D`或者`utility`

引入

`body.psw = md5(md5(body.psw)) // 一般加两次`

`body.psw = utility.md5(utility.md5(body.psw))`

### 图片验证码

包：`ccap`

```javascript
var ccap = require('ccap')

var captcha = ccap();
var ary = captcha.get();//ary[0] is captcha's text,ary[1] is captcha picture buffer.
var text = ary[0]; // 验证码
var buffer = ary[1]; // 图片

res.end(buffer)
```

### 配置文件

`module.exports = {debug: 'true', secret: 'xx'}`

```javascript
var config = require('./config')
app.locals.config = config

//请求中使用
req.app.locals.config.secret
```

### markdown插件

lepture/editor编辑器

```html
<link rel="stylesheet" href="http://lab.lepture.com/editor/editor.css" />
<script type="text/javascript" src="http://lab.lepture.com/editor/editor.js"></script>
<script type="text/javascript" src="http://lab.lepture.com/editor/marked.js"></script>
```

```javascript
var editor = new Editor({
  element: document.getElementById('editor'),
});
editor.render();
// 获取内容
var content = editor.codemirror.getValue();
// 设置内容
editor.codemirror.getValue('xxx	');
```

将内容转换为markdown

插件：markdown-it

引入

```javascript
var markdownIt = require('markdown-it')
var md = new markdownIt()
var result = md.render(content)
// 更简单的方法
var md = require('markdown-it')()
var result = md.render(content)
```

### 处理时间的插件

moment

引入

```javascript
moment().formate('YYYY-MM-DD HH:mm:ss') // 大写的H表示24小时制
```

### 文件上传

H5中FormData，可以异步上传二进制文件，不支持ie10以下

```javascript
// 构建一个表单数据
var formData = new FormData
// file[0]获取该文件的二进制
formData.append('pic', document.querySelector('#pic_file').file[0])
// xhr
...
xhr.send(formData)
```

插件：WebUploader

插件：jQuery-File-Uploade 推荐

插件：formidable，后台解析上传的文件

```javascript
var form = new formidable.IncomingForm();
form.uploadDir = './uploads'; // 指定上传路径，最好写到配置文件中
form.parse(req, function(err, fields, files) {
    if(err) {
        res.json({
            code: '0',
            msg: '上传失败'
        })
    }
    
    let pic = files.pic
    let tmPath = pic.path
    let size = pic.size
    let name = pic.name
    
    let newPath = tmPath + path.extname(name)
    
    fs.rename(tmPath, newPath, function() {
        // 将图片路径响应给客户端
        res.json({
            code: '1',
            msg: `/upload/${path.basename(newPath)}`
        })
    })
});
```

### Underscore工具库

模板

```javascript
var _ = require('underscore')
var compiled = _.template("hello: <%= name %>");
compiled({name: 'moe'});
=> "hello: moe"
```

在`<% 这里可以写原生js %>`

### 权限控制

某些操作需要登陆才能执行，所以要在操作之前检查是否登陆

```javascript
router.get('/register', [checklogin, userController.showRegister])

function checkLogin(req, res, next) {
    if(req.session.user) {
        return res.redirect('/')
    }
    next()
}
```

### 分页

#### 异步无刷新分页

twbsPagination插件

```javascript
<ul id="pagination-demo" class="pagination-sm"></ul>

$('#pagination-demo').twbsPagination({
    totalPages: 35,
    visiblePages: 7,
    first: '<<',
    last: '>>',
    prev: '<',
    next:'>',
    onPageClick: function (event, page) {
        $('#page-content').text('Page ' + page);
    }
});
```

### nginx部署

ngnix反向代理服务器：用户没有直接和node进行交互，而是通过nginx分发给node

使用

conf目录==》nginx.conf

## nodejs应用

**前端常用模式**

spa：vue-cli，nginx处理跨域；nodejs处理跨域：路由冲突问题（koa.history-fallback解决）

mpa+vue+swg：没有跨域问题

mpa+swg

同构化

**应用**

1. node前端：proxy，自己提供api

2. vue同构化，ssr+nodejs
3. proxy代理，削减api
4. 跨端

### 异 步IO原理浅析 

#### 异步IO

优点：

- 前端通过异步IO可以消除UI堵塞。
- 假设请求资源A的时间为M,请求资源B的时间为N.那么同步的请求耗时为M+N.如果采用异步方式占用时间为Max(M,N)。
- 随着业务的复杂，会引入分布式系统，时间会线性的增加，M+N+...和Max(M,N…)，这会放大同步和异步之间的差异。
- I/O是昂贵的，分布式I/O是更昂贵的。
  - CPU时钟周期： 1/cpu主频 -> 1s/3.1 GHz
  - 同步和异步没有绝对的好坏
- NodeJS 适用于IO密集型（读写）不适用CPU密集型（计算）
  - 操作系统对计算机进行了抽象，将所有输入 输出设备抽象为文件。内核在进行文件I/O操作时，通过文件描述符进行管理。应用程序如果需要进行IO需要打开文件描述符，在进行文件和数据的读写。异步IO不带数据直接返回，要获取数据还需要通过文件描述符再次读取。 
  - nodejs多线程不如Java等，nodejs是解释性语言所以不适用CPU密集型

##### Node对异步IO的实现

完美的异步IO应该是应该是应用程序发起非阻塞调用，无需通过遍历或者事件循环等方式轮询。 

LIBUV：负责管理通知

##### 几个特殊的API

1. SetTimeout和SetInterval 线程池不参与LIBUV
2. process.nextTick() 实现类似SetTimeout(function(){},0);每次调用放入队列中，在下一轮循环中取出。
3. setImmediate();比process.nextTick()优先级低
4. Node如何实现一个Sleep? 