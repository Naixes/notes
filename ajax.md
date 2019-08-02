# Ajax
## 概念
在此之前，我们可以通过以下几种方式让浏览器发出对服务端的请求，获得服务端的数据：

- 地址栏输入地址，回车，刷新
- 特定元素的 href 或 src 属性
- 表单提交

这些方案都是我们无法通过或者很难通过代码的方式进行编程（对服务端发出请求并且接受服务端返回的响应）。

AJAX（Asynchronous JavaScript and XML），最早出现在 2005 年的 GoogleSuggest，是在浏览器端进行网络编程（发送请求、接收响应）的技术方案，它使我们可以通过 JavaScript 直接获取服务端最新的内容而不必重新加载页面。让 Web 更能接近桌面应用的用户体验。

说白了，A JAX 就是浏览器提供的一套 API，可以通过 JavaScript 调用，从而实现通过代码控制请求与响应。实现网络编程。

## 快速上手

``````javascript
// 1. 创建一个 XMLHttpRequest 类型的对象 —— 相当于打开了一个浏览器
var xhr = new XMLHttpRequest()
// 2. 打开与一个网址之间的连接 —— 相当于在地址栏输入访问地址
xhr.open('GET', './time.php', true)// true表示异步，默认
// 3. 通过连接发送一次请求 —— 相当于回车或者点击访问发送请求
xhr.send(null)
// 4. 指定 xhr 状态变化事件处理函数 —— 相当于处理网页呈现后的操作
xhr.onreadystatechange = function () {
    // 通过 xhr 的 readyState 判断此次请求的响应是否接收完成
    if (this.readyState === 4) {
    // 通过 xhr 的 responseText 获取到响应的响应体
    console.log(this)
    }
}
``````

### readyState

由于 readystatechange 事件是在 xhr 对象状态变化时触发（不单是在得到响应时），也就意味着这个事件会被触发多次，所以我们有必要了解每一个状态值代表的含义：

| readyState | 状态描述         | 说明                                                    |
| ---------- | ---------------- | ------------------------------------------------------- |
| 0          | UNSENT           | 代理（XHR）被创建，但尚未调用 open() 方法。             |
| 1          | OPENED           | open() 方法已经被调用，建立了连接。                     |
| 2          | HEADERS_RECEIVED | send() 方法已经被调用，并且已经可以获取状态行和响应头。 |
| 3          | LOADING          | 响应体下载中， responseText 属性可能已经包含部分数据。  |
| 4          | DONE             | 响应体下载完成，可以直接使用 responseText 。            |

``````javascript
var xhr = new XMLHttpRequest()
console.log(xhr.readyState)
// => 0
// 初始化 请求代理对象
xhr.open('GET', 'time.php')
console.log(xhr.readyState)
// => 1
// open 方法已经调用，建立一个与服务端特定端口的连接
xhr.send()
xhr.addEventListener('readystatechange', function () {
    switch (this.readyState) {
        case 2:
        // => 2
        // 已经接受到了响应报文的响应头
        // 可以拿到头
        // console.log(this.getAllResponseHeaders())// 获取响应头所有内容
        console.log(this.getResponseHeader('server'))// 获取响应头特定所有内容
        // 但是还没有拿到体
        console.log(this.responseText)
        break
        case 3:
        // => 3
        // 正在下载响应报文的响应体，有可能响应体为空，也有可能不完整
        // 在这里处理响应体不保险（不可靠）
        console.log(this.responseText)
        break
        case 4:
        // => 4
        // 一切 OK （整个响应报文已经完整下载下来了）
        // 这里处理响应体
        console.log(this.responseText)
        break
	}
})
``````

通过理解每一个状态值的含义得出一个结论：一般我们都是在 readyState 值为 4 时，执行响应的后续逻辑。

``````javascript
xhr.onreadystatechange = function () {
    if (this.readyState === 4) {
    // 后续逻辑......
    }
}
``````

### 遵循HTTP

本质上 XMLHttpRequest 就是 JavaScript 在 Web 平台中发送 HTTP 请求的手段，所以我们发送出去的请求任然是HTTP 请求，同样符合 HTTP 约定的格式：

``````javascript
// 设置请求报文的请求行
xhr.open('GET', './time.php')
// 设置请求头
xhr.setRequestHeader('Accept', 'text/plain')
// 设置请求体
// 默认表单格式（enctype）form提交的数据为Form Data
// 表单格式为：multipart/form-dataform；text/plain提交的数据为Request Payload
// 所以以'key1=value1&key2=value2'传递POST请求体数据时应该设置请求头Content-Type为application/x-www-form-urlencoded
xhr.send(null)
xhr.onreadystatechange = function () {
    if (this.readyState === 4) {
    // 获取响应状态码，200成功
    console.log(this.status)
    // 获取响应状态描述
    console.log(this.statusText)
    // 获取响应头信息
    console.log(this.getResponseHeader('Content‐Type')) // 指定响应头
    console.log(this.getAllResponseHeader()) // 全部响应头
    // 获取响应体
    console.log(this.responseText) // 文本形式
    console.log(this.responseXML) // XML 形式，了解即可不用了
    }
}
``````

参考链接：
https://developer.mozilla.org/zh-CN/docs/Web/API/XMLHttpRequest
https://developer.mozilla.org/zh-CN/docs/Web/API/XMLHttpRequest/Using_XMLHttpRequest

### 数据接口

返回数据的地址

##  具体用法

### GET请求

通常在一次 GET 请求过程中，参数传递都是通过 URL 地址中的 ? 参数传递。

``````javascript
var xhr = new XMLHttpRequest()
// GET 请求传递参数通常使用的是问号传参
// 这里可以在请求地址后面加上参数，从而传递数据到服务端
xhr.open('GET', './delete.php?id=1')
// 一般在 GET 请求时无需设置响应体，可以传 null 或者干脆不传
xhr.send(null)
xhr.onreadystatechange = function () {
    if (this.readyState === 4) {
    // 返回值为字符串，需要转换，如json：JSON.parse(this.responseText)
    console.log(this.responseText)
    }
}
// 一般情况下 URL 传递的都是参数性质的数据，而 POST 一般都是业务数据
``````

### POST请求

POST 请求过程中，都是采用请求体承载需要提交的数据。

``````javascript
var xhr = new XMLHttpRequest()
// open 方法的第一个参数的作用就是设置请求的 method
xhr.open('POST', './add.php')
// 设置请求头中的 Content‐Type 为 application/x‐www‐form‐urlencoded
// 标识此次请求的请求体格式为 urlencoded 以便于服务端接收数据
xhr.setRequestHeader('Content‐Type', 'application/x‐www‐form‐urlencoded')
// 需要提交到服务端的数据可以通过 send 方法的参数传递
// 格式：key1=value1&key2=value2
xhr.send('key1=value1&key2=value2')
xhr.onreadystatechange = function () {
    if (this.readyState === 4) {
    console.log(this.responseText)
    }
}
``````

### 同步与异步

xhr.open() 方法第三个参数async要求传入的是一个 bool 值，其作用就是设置此次请求是否采用异步方式执行，默认为 true ，如果需要同步执行可以通过传递 false 实现：

``````javascript
console.log('before ajax')
var xhr = new XMLHttpRequest()
// 默认第三个参数为 true 意味着采用异步方式执行
xhr.open('GET', './time.php', true)
xhr.send(null)
xhr.onreadystatechange = function () {
    if (this.readyState === 4) {
    // 这里的代码最后执行
    console.log('request done')
    }
}
console.log('after ajax')
``````

如果采用同步方式执行，则代码会卡死在 xhr.send() 这一步：

``````javascript
console.log('before ajax')
var xhr = new XMLHttpRequest()
// 同步方式
xhr.open('GET', './time.php', false)
// 同步方式 执行需要 先注册事件再调用 send，否则 readystatechange 无法触发
xhr.onreadystatechange = function () {
    // 如果在Chrome中查看this，展开后readyState都是4，因为控制台打开时显示即时数据
    if (this.readyState === 4) {
    // 这里的代码最后执行
    console.log('request done')
    }
}
xhr.send(null)
console.log('after ajax')
``````

一定在发送请求 send() 之前注册 readystatechange （不管同步或者异步）

- 为了让这个事件可以更加可靠（一定触发），一定是先注册了解同步模式即可，切记不要使用同步模式。

#### 进程与线程

进程：运行中的程序	

线程：cpu中的最小执行单元

​	js是单线程技术

多线程技术：

### 响应数据格式

this.response 获取响应提体的结果根据this.responseType的变化而变化

- responseType 是客户端自己手动设置的属性

```javascript
var xhr = new XMLHttpRequest()
xhr.open('POST', './add.php')
xhr.setRequestHeader('Content‐Type', 'application/x‐www‐form‐urlencoded')
// responseType 是客户端自己手动设置的属性，默认为空和text相同:json，text，document等，可以在MDN中查看，ie9不兼容，一般不用
xhr.responseType = 'json'
xhr.send('key1=value1&key2=value2')
xhr.onreadystatechange = function () {
    if (this.readyState === 4) {
    console.log(this.responseText)
    }
}
```

this.responseText 获取字符串类型的响应提体，不能获取二进制数据

**兼容性不好，ie9不兼容**



服务端应该设置合理的响应头header的Content-Type，如application/json，默认为text/html格式

XML

一种数据描述手段，淘汰的原因：数据冗余太多

服务端设置响应头header的Content-Type为application/xml，客户端使用xhr.responseXML接收

JSON

也是一种数据描述手段，类似于 JavaScript 字面量方式
服务端采用 JSON 格式返回数据，客户端按照 JSON 格式解析数据。

### 处理响应数据渲染

模板引擎：
artTemplate：https://aui.github.io/art-template/

#### artTemplate

script标签的特点：

1. innerHTML不会显示到界面上
2. 如果type不是text/javascript时不会作为javascript执行

所以我们一般使用script标签写模板内容，并将type改为text/x-art-template

`<script id='templ' type='text/x-art-template'>`

`</script>`

- 遍历

  {{each arr}}{{/each}}  

  {{$value}} 是指被循环的元素

  {{$index}} 是指被循环的元素的索引

``````javascript
var html = template('id',data)
document.getElementById('id').innerHTML = html 
``````

### 兼容方案

XMLHttpRequest 在老版本浏览器（IE5/6）中有兼容问题，可以通过另外一种方式代替

``````javascript
var xhr = window.XMLHttpRequest ? new XMLHttpRequest() : new ActiveXObject('1 Microsoft.XMLHTTP')
``````

## 封装

### AJAX请求封装

``````javascript
/**
* 发送一个 AJAX 请求
* @param {String} method 请求方法
* @param {String} url 请求地址
* @param {Object} params 请求参数
* @param {Function} done 请求完成过后需要做的事情（委托/回调）
*/
function ajax (method, url, params, done) {
    // 统一转换为大写便于后续判断
    method = method.toUpperCase()
    // 对象形式的参数转换为 urlencoded 格式
    if(typeof params === 'object') {
        var pairs = []
        for (var key in params) {
            pairs.push(key + '=' + params[key])
        }
        params = pairs.join('&')
    }
    var xhr = window.XMLHttpRequest ? new XMLHttpRequest() : new
    ActiveXObject('Microsoft.XMLHTTP')
    xhr.addEventListener('readystatechange', function () {
        if (this.readyState !== 4) return
        // 尝试通过 JSON 格式解析响应体
        try {
            done(JSON.parse(this.responseText))
        } catch (e) {
            done(this.responseText)
        }
   	})
    // 如果是 GET 请求就设置 URL 地址 问号参数
    if (method === 'GET') {
        url += '?' + params
    }
    xhr.open(method, url)
    // 如果是 POST 请求就设置请求体
    var data = null
    if (method === 'POST') {
        xhr.setRequestHeader('Content‐Type', 'application/x‐www‐form‐urlencoded')
        data = params
    }
    xhr.send(data)
}

ajax('get', './get.php', { id: 123 }, function (data) {
	console.log(data)
})
ajax('post', './post.php', { foo: 'posted data' }, function (data) {
	console.log(data)
})
``````

### jQuery中的AJAX

参考：
http://www.jquery123.com/category/ajax/
http://www.w3school.com.cn/jquery/jquery_ref_ajax.asp

#### $.ajax

``````javascript
$.ajax({
    url: './get.php',
    type: 'get',
    // 指定响应数据类型
    dataType: 'json',
    data: { id: 1 },
    // open之前的操作
    beforeSend: function (xhr) {
    	console.log('before send')
    },
    // 只有状态码为200时执行
    success: function (data) {
        // data会根据服务端响应的content-type自动转换类型，jquery提供
        // 指定了响应数据类型，就不用关心服务端响应的content-type
    	console.log(data)
    },
    error: function (err) {
    	console.log(err)
    },
    complete: function () {
    	console.log('request completed')
    }
})
``````

常用选项参数介绍：
url：请求地址

type：请求方法，默认为 get

dataType：服务端响应数据类型

contentType：请求体内容类型，默认 application/x-www-form-urlencoded

data：需要传递到服务端的数据，如果 GET 则通过 URL 传递，如果 POST 则通过请求体传递

timeout：请求超时时间

beforeSend：请求发起之前触发

success：请求成功之后触发（响应状态码 200）

error：请求失败触发

complete：请求完成触发（不管成功与否）

#### $.get

``````javascript
$.get('url', {}, fn)
$.getJSON('url', {}, fn)
``````

#### $.post

``````javascript
$.post('url', {}, fn)
$.postJSON('url', {}, fn)
``````

#### 全局事件处理

http://www.jquery123.com/category/ajax/global-ajax-event-handlers/

``````javascript
// 只要有ajax发生就会执行
$(document).ajaxStart(fn)
$(document).ajaxStop(fn)
``````

Nprogress库（加载进度条）

​	Nprogress.start()

​	Nprogress.set(0.4)

​	Nprogress.done()

#### 其他方法

$(selector).load(url, data, fn)

​	用返回的url内容代替选择器区域，url中可以包括选择器用空格隔开

$.getScript()

$('form').serialize()：输出序列化表单值的结果

```html
<form>
  <div><input type="text" name="a" value="1" id="a" /></div>
  <div><input type="text" name="b" value="2" id="b" /></div>
  <div><input type="hidden" name="c" value="3" id="c" /></div>
  <div>
    <textarea name="d" rows="8" cols="40">4</textarea>
  </div>
  <div><select name="e">
    <option value="5" selected="selected">5</option>
    <option value="6">6</option>
    <option value="7">7</option>
  </select></div>
  <div>
    <input type="checkbox" name="f" value="8" id="f" />
  </div>
  <div>
    <input type="submit" name="g" value="Submit" id="g" />
  </div>
</form>

```
.serialize() 方法可以操作已选取个别表单元素的 jQuery 对象，比如 `<input>, <textarea>`以及 `<select>`。不过，选择` <form>`标签本身进行序列化一般更容易些：
```javascript
$('form').submit(function() {
  alert($(this).serialize()); // a=1&b=2&c=3&d=4&e=5
  return false;
});
// 注释：只会将”成功的控件“序列化为字符串。如果不使用按钮来提交表单，则不对提交按钮的值序列化。如果要表单元素的值包含到序列字符串中，元素必须使用 name 属性。 
```

## 跨域

https://segmentfault.com/a/1190000015597029

### 概念 

同源策略是浏览器的一种安全策略，所谓同源是指域名，协议，端口完全相同，只有同源的地址才可以相互通过AJAX 的方式请求。

**那么是出于什么安全考虑才会引入这种机制呢？** 其实主要是用来防止 CSRF 攻击的。简单点说，CSRF 攻击是利用用户的登录态发起恶意请求。

也就是说，没有同源策略的情况下，A 网站可以被任意其他来源的 Ajax 访问到内容。如果你当前 A 网站还存在登录态，那么对方就可以通过 Ajax 获得你的任何信息。当然跨域并不能完全阻止 CSRF。

**然后我们来考虑一个问题，请求跨域了，那么请求到底发出去没有？** 请求必然是发出去了，但是浏览器拦截了响应。你可能会疑问明明通过表单的方式可以发起跨域请求，为什么 Ajax 就不会。因为归根结底，跨域是为了阻止用户读取到另一个域名下的内容，Ajax 可以获取响应，浏览器认为这不安全，所以拦截了响应。但是表单并不会获取新的内容，所以可以发起跨域请求。同时也说明了跨域并不能完全阻止 CSRF，因为请求毕竟是发出去了。

同源或者不同源说的是两个地址之间的关系，不同源地址之间请求我们称之为跨域请求

什么是同源？例如：http://www.example.com/detail.html 与一下地址对比

| 对比地址                                 | 是否同源 | 原因           |
| ---------------------------------------- | -------- | -------------- |
| http://api.example.com/detail.html       | 不同源   | 域名不同       |
| https://www.example.com/detail.html      | 不同源   | 协议不同       |
| http://www.example.com:8080/detail.html  | 不同源   | 端口不同       |
| http://api.example.com:8080/detail.html  | 不同源   | 域名、端口不同 |
| https://api.example.com/detail.html      | 不同源   | 协议、域名不同 |
| https://www.example.com:8080/detail.html | 不同源   | 端口、协议不同 |
| http://www.example.com/other.html        | 同源     | 只是目录不同   |

### 解决方案

现代化的 Web 应用中肯定会有不同源的现象，所以必然要解决这个问题，从而实现跨域请求。

参考：http://rickgray.me/solutions-to-cross-domain-in-browser

#### JSONP

JSON with Padding，是一种借助于 script 标签发送跨域请求的技巧。

其原理就是在客户端借助 script 标签请求服务端的一个动态网页（php 文件），服务端的这个动态网页返回一段带有函数调用的 JavaScript 全局函数调用的脚本，将原本需要返回给客户端的数据传递进去。

```html
<script src="http://domain/api?param1=a&param2=b&callback=jsonp"></script>
<script>
    function jsonp(data) {
    	console.log(data)
	}
</script>    
```

客户端 http://www.zce.me/users-list.html

`<script src="http://api.zce.me/users.php?callback=foo"></script>`

服务端 http://api.zce.me/users.php?callback=foo 返回的结果

`foo(['我', '是', '你', '原', '本', '需', '要', '的', '数', '据'])

问题：

1. JSONP 需要服务端配合，服务端按照客户端的要求返回一段 JavaScript 调用客户端的函数
2. 只能发送 GET 请求

注意：JSONP 用的是 script 标签，更 AJAX 提供的 XMLHttpRequest 没有任何关系！！！
jQuery 中使用 JSONP 就是将 dataType 设置为 jsonp

在开发中可能会遇到多个 JSONP 请求的回调函数名是相同的，这时候就需要自己封装一个 JSONP，以下是简单实现

```js
function jsonp(url, jsonpCallback, success) {
  let script = document.createElement('script')
  script.src = url
  script.async = true
  script.type = 'text/javascript'
  window[jsonpCallback] = function(data) {
    success && success(data)
  }
  document.body.appendChild(script)
}
jsonp('http://xxx', 'callback', function(value) {
  console.log(value)
})
```

其他常见的 AJAX 封装库：

- Axios

#### CORS

Cross Origin Resource Share，跨域资源共享

```javascript
// 允许远端访问
header('Access‐Control‐Allow‐Origin: *');
```

CORS 需要浏览器和后端同时支持。IE 8 和 9 需要通过 `XDomainRequest` 来实现。

浏览器会自动进行 CORS 通信，实现 CORS 通信的关键是后端。只要后端实现了 CORS，就实现了跨域。

在被请求的服务端响应的时候添加一个 Access-Control-Allow-Origin 的响应头，表示这个资源是否允许指定域请求，如果设置通配符则表示所有网站都可以访问资源。`Access-Control-Allow-Origin:*`

虽然设置 CORS 和前端没什么关系，但是通过这种方式解决跨域问题的话，会在发送请求时出现两种情况，分别为**简单请求和复杂请求**。

- 简单请求

以 Ajax 为例，当满足以下条件时，会触发简单请求

1. 使用下列方法之一：
   - `GET`
   - `HEAD`
   - `POST`
2. `Content-Type` 的值仅限于下列三者之一：
   - `text/plain`
   - `multipart/form-data`
   - `application/x-www-form-urlencoded`

请求中的任意 `XMLHttpRequestUpload` 对象均没有注册任何事件监听器； `XMLHttpRequestUpload` 对象可以使用 `XMLHttpRequest.upload` 属性访问。

- 复杂请求

那么很显然，不符合以上条件的请求就肯定是复杂请求了。

对于复杂请求来说，首先会发起一个预检请求，该请求是 `option` 方法的，通过该请求来知道服务端是否允许跨域请求。

对于预检请求来说，如果你使用过 Node 来设置 CORS 的话，可能会遇到过这么一个坑。

以下以 express 框架举例：

```js
app.use((req, res, next) => {
  res.header('Access-Control-Allow-Origin', '*')
  res.header('Access-Control-Allow-Methods', 'PUT, GET, POST, DELETE, OPTIONS')
  res.header(
    'Access-Control-Allow-Headers',
    'Origin, X-Requested-With, Content-Type, Accept, Authorization, Access-Control-Allow-Credentials'
  )
  next()
})
```

该请求会验证你的 `Authorization` 字段，没有的话就会报错。

当前端发起了复杂请求后，你会发现就算你代码是正确的，返回结果也永远是报错的。因为预检请求也会进入回调中，也会触发 `next` 方法，因为预检请求并不包含 `Authorization` 字段，所以服务端会报错。

想解决这个问题很简单，只需要在回调中过滤 `option` 方法即可

```js
res.statusCode = 204
res.setHeader('Content-Length', '0')
res.end()
```

#### document.domain

该方式只能用于**二级域名相同**的情况下，比如 `a.test.com` 和 `b.test.com` 适用于该方式。

只需要给页面添加 `document.domain = 'test.com'` 表示二级域名都相同就可以实现跨域

#### postMessage

这种方式通常用于获取嵌入页面中的第三方页面数据。一个页面发送消息，另一个页面判断来源并接收消息

```js
// 发送消息端
window.parent.postMessage('message', 'http://test.com')
// 接收消息端
var mc = new MessageChannel()
mc.addEventListener('message', event => {
  var origin = event.origin || event.originalEvent.origin
  if (origin === 'http://test.com') {
    console.log('验证通过')
  }
})
```

## XMLHttpRequest 2.0	

### onload / onprogress

``````javascript
var xhr = new XMLHttpRequest()
xhr.open('GET', './time.php')
xhr.onload = function () {
    // onload readyState === 4
    console.log(this.readyState)
}
xhr.onprogress = function () {
    // onload readyState === 3
    console.log(this.readyState)
}
xhr.send(null)
``````

### FormData

FormData以前 AJAX 只能提交字符串，现在可以提交二进制的数据

### 案例

异步上传文件

### 参考链接

http://www.w3school.com.cn/ajax/index.asp
https://aui.github.io/art-template/zh-cn