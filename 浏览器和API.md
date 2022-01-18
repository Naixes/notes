# 常见浏览器介绍

```
浏览器是网页运行的平台，五大浏览器：IE、火狐（Firefox）、谷歌（Chrome）、Safari和Opera。
```

## 浏览器内核 

```
浏览器内核又可以分成两部分：渲染引擎(layout engineer 或者 Rendering Engine)和 JS 引擎。

渲染引擎 它负责取得网页的内容（HTML、XML、图像等等）、整理讯息（例如加入 CSS 等），以及计算网页的显示方式，然后会输出至显示器或打印机。浏览器的内核的不同对于网页的语法解释会有不同，所以渲染的效果也不相同。

JS 引擎 则是解析 Javascript 语言，执行 javascript语言来实现网页的动态效果。

最开始渲染引擎和 JS 引擎并没有区分的很明确，后来 JS 引擎越来越独立，内核就倾向于只指渲染引擎。有一个网页标准计划小组制作了一个 ACID 来测试引擎的兼容性和性能。内核的种类很多，但是常见的浏览器内核可以分这四种：Trident、Gecko、Blink、Webkit。
五大浏览器采用的都是单内核，而随着浏览器的发展现在也出现了双内核。像360浏览器、QQ浏览器都是采用双内核。

四大内核分别是：Trident（也称IE内核）、webkit、Blink、Gecko
```

- IE浏览器内核：Trident内核，也是俗称的IE内核；
- Chrome浏览器内核：统称为Chromium内核或Chrome内核，以前是Webkit内核，现在是Blink内核；
- Firefox浏览器内核：Gecko内核，俗称Firefox内核；
- Safari浏览器内核：Webkit内核；
- Opera浏览器内核：最初是自己的Presto内核，后来是Webkit，现在是Blink内核；

## 移动端的浏览器内核

主要说的是系统内置浏览器的内核。

iPhone 和 iPad 等苹果 iOS 平台主要是 WebKit

Android 4.4 之前的 Android 系统浏览器内核是 WebKit，Android4.4 系统浏览器切换到了Chromium，内核是 Webkit 的分支 Blink

Windows Phone 8 系统浏览器内核是 Trident。

# Web标准

## Web 标准构成

 Web标准不是某一个标准，而是由W3C和其他标准化组织制定的一系列标准的集合。主要包括结构（Structure）、表现（Presentation）和行为（Behavior）三个方面。

```
结构标准：结构用于对网页元素进行整理和分类，主要包括XML和XHTML两个部分。
样式标准：表现用于设置网页元素的版式、颜色、大小等外观样式，主要指的是CSS。
行为标准：行为是指网页模型的定义及交互的编写，主要包括DOM和ECMAScript两个部分
```

理想状态我们的源码： .HTML    .css   .js 

# Web存储

## cookie，localStorage，sessionStorage，indexDB，indexDB

### 对比

| 特性         | cookie                                     | localStorage             | sessionStorage | indexDB                  | Web SQL      |
| ------------ | ------------------------------------------ | ------------------------ | -------------- | ------------------------ | ------------ |
| 数据生命周期 | 一般由服务器生成，可以设置过期时间         | 除非被清理，否则一直存在 | 页面关闭就清理 | 除非被清理，否则一直存在 |              |
| 数据存储大小 | 4K                                         | 2.5-10M（根据浏览器）    | 5M             | 大于250M、无限           | 50M          |
| 与服务端通信 | 每次都会携带在 header 中，对于请求性能影响 | 不参与，同步             | 不参与         | 异步读取数据             | 异步读取数据 |
|              |                                            |                          |                | 关系型数据库             | 关系型数据库 |

从上表可以看到，`cookie` 已经不建议用于存储。如果没有大量数据存储需求的话，可以使用 `localStorage` 和 `sessionStorage` 。对于不怎么改变的数据尽量使用 `localStorage` 存储，否则可以用 `sessionStorage` 存储。

**sessionStorage/localStorage**：将数据存储到本地

API：

```js
window.sessionStorage.setItem('name',name)
window.sessionStorage.getItem('name')
window.sessionStorage.removeItem('name')
window.sessionStorage.clear()
```

### sessionStorage

1. 存储在当前页面内存中
2. 5M左右

### localStorage

1. 同一个浏览器可以共享
2. 永久存储，存储在硬盘
3. 支持get和post请求，存储在2.5-10M左右，所以超过2.5M时会有性能问题
4. 移动端的一些离线异步js可能会放到这里
5. 不提供搜索功能不能建立自定义索引

### cookie

只有4k大小，服务端和浏览器端；没法送一个新的页面都会发送，形成宽带浪费；需要指定作用域，不可跨域

对于 **`cookie`** 来说，我们还需要注意安全性。

| 属性      | 作用                                                         |
| --------- | ------------------------------------------------------------ |
| value     | 如果用于保存用户登录态，应该将该值加密，不能使用明文的用户标识 |
| http-only | 不能通过 JS 访问 Cookie，减少 XSS 攻击                       |
| secure    | 只能在协议为 HTTPS 的请求中携带                              |
| same-site | 规定浏览器不能在跨域请求中携带 Cookie，减少 CSRF 攻击        |

### indexDB

参考：<http://www.ruanyifeng.com/blog/2018/07/indexeddb.html>

特点：

**（1）键值对储存。** IndexedDB 内部采用对象仓库（object store）存放数据。所有类型的数据都可以直接存入，包括 JavaScript 对象。对象仓库中，数据以"键值对"的形式保存，每一个数据记录都有对应的主键。

**（2）异步。** IndexedDB 操作时不会锁死浏览器，用户依然可以进行其他操作，这与 LocalStorage 形成对比，后者的操作是同步的。为了防止大量数据的读写，拖慢网页的表现。

**（3）支持事务。** IndexedDB 支持事务（transaction），这意味着一系列操作步骤之中，只要有一步失败，整个事务就都取消，数据库回滚到事务发生之前的状态。

**（4）同源限制** IndexedDB 受到同源限制，每一个数据库对应创建它的域名。网页只能访问自身域名下的数据库，而不能访问跨域的数据库。

**（5）储存空间大** IndexedDB 的储存空间比 LocalStorage 大得多，一般来说不少于 250MB，甚至没有上限。

**（6）支持二进制储存。** IndexedDB 不仅可以储存字符串，还可以储存二进制数据（ArrayBuffer 对象和 Blob 对象）。

### Web SQL

参考：<https://www.cnblogs.com/ljwsyt/p/9760266.html>

## Service Worker

Service Worker 是运行在浏览器背后的**独立线程**，一般可以用来实现缓存功能。使用 Service Worker的话，传输协议必须为 **HTTPS**。因为 Service Worker 中涉及到请求拦截，所以必须使用 HTTPS 协议来保障安全。

Service Worker 实现缓存功能一般分为三个步骤：首先需要先注册 Service Worker，然后监听到 `install` 事件以后就可以缓存需要的文件，那么在下次用户访问的时候就可以通过拦截请求的方式查询是否存在缓存，存在缓存的话就可以直接读取缓存文件，否则就去请求数据。以下是这个步骤的实现：

```js
// index.js
if (navigator.serviceWorker) {
  navigator.serviceWorker
    .register('sw.js')
    .then(function(registration) {
      console.log('service worker 注册成功')
    })
    .catch(function(err) {
      console.log('servcie worker 注册失败')
    })
}
// sw.js
// 监听 `install` 事件，回调中缓存所需文件
self.addEventListener('install', e => {
  e.waitUntil(
    caches.open('my-cache').then(function(cache) {
      return cache.addAll(['./index.html', './index.js'])
    })
  )
})

// 拦截所有请求事件
// 如果缓存中已经有请求的数据就直接用缓存，否则去请求数据
self.addEventListener('fetch', e => {
  e.respondWith(
    caches.match(e.request).then(function(response) {
      if (response) {
        return response
      }
      console.log('fetch source')
    })
  )
})
```

打开页面，可以在开发者工具中的 `Application` 看到 Service Worker 已经启动了

![img](https://user-gold-cdn.xitu.io/2018/3/28/1626b1e8eba68e1c?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

在 Cache 中也可以发现我们所需的文件已被缓存

![img](https://user-gold-cdn.xitu.io/2018/3/28/1626b20dfc4fcd26?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

当我们重新刷新页面可以发现我们缓存的数据是从 Service Worker 中读取的

![img](https://user-gold-cdn.xitu.io/2018/3/28/1626b20e4f8f3257?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

## 应用缓存ApplicationCache

指定缓存文件，5M左右

```html
<html lang='en' manifest='demo.appcache'>
...
</html>
```

manifest=应用程序缓存清单路径，文件扩展名建议为appcache

appcache文件内容：

```config
#第一句
CACHE MANIFEST
#需要缓存的清单列表
CACHE:
../01.jpg
#*代表所有文件
#每次请求都需要重新获取的清单列表
NETWORK：
../02.jpg
#没找到时的替代文件
FALLBACK:
#被替代文件 替代文件
../03.jpg ../04.jpg
#/代表所有文件
```

不起作用时要配置IIS管理器（服务器）里的的MIME类型：text/cache-manifest

根据官方文档，AppCache 已经不推荐使用了，标准也不会再支持。 

## 多媒体标签

- embed：标签定义嵌入的内容
- audio：播放音频
- video：播放视频

### 多媒体 embed

embed可以用来插入各种多媒体，格式可以是 Midi、Wav、AIFF、AU、MP3等等。url为音频或视频文件及其路径，可以是相对路径或绝对路径。

```html
<embed src="http://player.youku.com/player.php/sid/XMTI4MzM2MDIwOA==/v.swf" allowFullScreen="true" quality="high" width="480" height="400" align="middle" allowScriptAccess="always" type="application/x-shockwave-flash"></embed>
```

### 多媒体 audio

```
<audio controls>
  <source src="horse.ogg" type="audio/ogg">
  <source src="horse.mp3" type="audio/mpeg">
您的浏览器不支持 audio 元素。
</audio>
```

**autoplay**：autoplay自动播放

**controls**：controls是否显示默认播放控件

**loop**：loop循环播放，loop='2'，-1为循环播放

目前<audio>元素支持三种音频格式文件: MP3, Wav, 和 Ogg由于版权等原因，不同的浏览器可支持播放的格式是不一样的

| 浏览器               | MP3  | Wav  | Ogg  |
| -------------------- | ---- | ---- | ---- |
| Internet Explorer 9+ | YES  | NO   | NO   |
| Chrome 6+            | YES  | YES  | YES  |
| Firefox 3.6+         | YES  | YES  | YES  |
| Safari 5+            | YES  | YES  | NO   |
| Opera 10+            | YES  | YES  | YES  |

多浏览器支持的方案，如下图

```
<audio src="" controls autoplay>
  <source src="bgs.mp3" />
  <source src="bgs.wav" />
  <source src="bgs.ogg" />
  你的浏览器不支持该audio音频播放
</audio>
```

### 多媒体 video

```
<video width="320" height="240" controls>
  <source src="movie.mp4" type="video/mp4">
  <source src="movie.ogg" type="video/ogg">
  您的浏览器不支持Video标签。
</video>
```

**autoplay** 自动播放

**controls** 是否显示默认播放控件

**loop** 循环播放

**width** 设置播放窗口宽度

**height**设置播放窗口的高度

当前， <video> 元素支持三种视频格式： MP4, WebM, 和 Ogg ，由于版权等原因，不同的浏览器可支持播放的格式是不一样的，如下图供参考

| 浏览器            | MP4                  | WebM | Ogg  |
| ----------------- | -------------------- | ---- | ---- |
| Internet Explorer | YES                  | NO   | NO   |
| Chrome            | YES                  | YES  | YES  |
| Firefox           | YES                  | YES  | YES  |
| Safari            | YES                  | NO   | NO   |
| Opera             | YES (从 Opera 25 起) | YES  | YES  |

**多浏览器支持的方案同音频**

## DOM操作

### 获取元素

document.getElementByClassName('class')类数组

document.getElementByTagName('tag')类数组

document.querySelector('')返回第一个匹配的元素

document.querySelectorAll('')类数组

### 类名操作

Node.classLisht.add('')

Node.classLisht.remove('')

Node.classLisht.toggle('')

Node.classLisht.contains('')

### 自定义属性

1. 在HTML5中我们可以自定义属性，其格式如下`data-*=""`，例如：`data-info="我是自定义属性"`，通过`Node.dataset['info']` 我们便可以获取到自定义的属性值。
2. 当我们如下格式设置时，则需要以驼峰格式才能正确获取：`data-my-name="itcast"`，获取`Node.dataset['myName']

# 浏览器缓存机制

缓存可以说是性能优化中**简单高效**的一种优化方式了，它可以**显著减少网络传输所带来的损耗**。

对于一个数据请求来说，可以分为发起网络请求、后端处理、浏览器响应三个步骤。浏览器缓存可以帮助我们在第一和第三步骤中优化性能。比如说直接使用缓存而不发起请求，或者发起了请求但后端存储的数据和前端一致，缓存会根据请求保存输出内容的副本，例如html页面，图片，文件，当 下一个请求来到的时候：如果是相同的URL，缓存直接使用副本响应访问请求，而不是向源服务器再次发送请求。那么就没有必要再将数据回传回来，这样就减少了响应数据。

1. 减少响应延迟
2. 减少网络带宽消耗

## 缓存位置

从缓存位置上来说分为四种，并且各自有**优先级**，当依次查找缓存且都没有命中的时候，才会去请求网络

1. Service Worker
2. Memory Cache
3. Disk Cache
4. Push Cache
5. 网络请求

### Service Worker

Service Worker 的缓存与浏览器其他内建的缓存机制不同，它可以让我们**自由控制**缓存哪些文件、如何匹配缓存、如何读取缓存，并且**缓存是持续性的**。

当 Service Worker 没有命中缓存的时候，我们需要去调用 `fetch` 函数获取数据。也就是说，如果我们没有在 Service Worker 命中缓存的话，会根据缓存查找优先级去查找数据。**但是不管我们是从 Memory Cache 中还是从网络请求中获取的数据，浏览器都会显示我们是从 Service Worker 中获取的内容。**

### Memory Cache

Memory Cache 也就是内存中的缓存，读取内存中的数据肯定比磁盘快。**但是内存缓存虽然读取高效，可是缓存持续性很短，会随着进程的释放而释放。** 一旦我们关闭 Tab 页面，内存中的缓存也就被释放了。

当我们访问过页面以后，再次刷新页面，可以发现很多数据都来自于内存缓存

![img](https://user-gold-cdn.xitu.io/2018/12/5/1677db8003dc8311?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)从内存中读取缓存

那么既然内存缓存这么高效，我们是不是能让数据都存放在内存中呢？

先说结论，这是**不可能**的。首先计算机中的内存一定比硬盘容量小得多，操作系统需要精打细算内存的使用，所以能让我们使用的内存必然不多。内存中其实可以存储大部分的文件，比如说 JSS、HTML、CSS、图片等等。但是浏览器会把哪些文件丢进内存这个过程就很**玄学**了，我查阅了很多资料都没有一个定论。

当然，我通过一些实践和猜测也得出了一些结论：

- 对于大文件来说，大概率是不存储在内存中的，反之优先
- 当前系统内存使用率高的话，文件优先存储进硬盘

### Disk Cache

Disk Cache 也就是存储在硬盘中的缓存，读取速度慢点，但是什么都能存储到磁盘中，比之 Memory Cache **胜在容量和存储时效性上。**

在所有浏览器缓存中，Disk Cache 覆盖面基本是最大的。它会**根据 HTTP Herder 中的字段判断**哪些资源需要缓存，哪些资源可以不请求直接使用，哪些资源已经过期需要重新请求。**并且即使在跨站点的情况下，相同地址的资源一旦被硬盘缓存下来，就不会再次去请求数据。**

### Push Cache

Push Cache 是 HTTP/2 中的内容，当以上三种缓存都没有命中时，它才会被使用。**并且缓存时间也很短暂，只在会话（Session）中存在，一旦会话结束就被释放。**

Push Cache 在国内能够查到的资料很少，也是因为 HTTP/2 在国内不够普及，但是 HTTP/2 将会是日后的一个趋势。这里推荐阅读 [HTTP/2 push is tougher than I thought](https://link.juejin.im/?target=https%3A%2F%2Fjakearchibald.com%2F2017%2Fh2-push-tougher-than-i-thought%2F) 这篇文章，但是内容是英文的，我翻译一下文章中的几个结论，有能力的同学还是推荐自己阅读

- 所有的资源都能被推送，但是 Edge 和 Safari 浏览器兼容性不怎么好
- 可以推送 `no-cache` 和 `no-store` 的资源
- 一旦连接被关闭，Push Cache 就被释放
- 多个页面可以使用相同的 HTTP/2 连接，也就是说能使用同样的缓存
- Push Cache 中的缓存只能被使用一次
- 浏览器可以拒绝接受已经存在的资源推送
- 你可以给其他域名推送资源

### 网络请求

如果所有缓存都没有命中的话，那么只能发起请求来获取资源了。

那么为了性能上的考虑，大部分的接口都应该选择好缓存策略，接下来我们就来学习缓存策略这部分的内容。

## 缓存策略

通常浏览器缓存策略分为两种：**强缓存**和**协商缓存**，并且缓存策略都是通过设置 HTTP Header 来实现的，强缓存优先于协商缓存。

HTTP缓存都是从第二次开始

- 第一次服务器返回资源并在reaponse header中回传缓存策略
- 第二次浏览器判断参数，强缓存直接200，否则把参数添加到request header传给服务器判断是否协商缓存，是返回304，否返回资源

![浏览器的缓存机制-无缓存](\media\浏览器的缓存机制-无缓存.png)

![浏览器的缓存机制-有缓存](\media\浏览器的缓存机制-有缓存.png)

![浏览器的缓存机制-完整流程](\media\浏览器的缓存机制-完整流程.png)

### 强缓存

强缓存可以通过设置两种 HTTP Header 实现：`Expires` 和 `Cache-Control` 。**强缓存表示在缓存期间不需要请求**，不在期间执行比较缓存策略，`state code` 为 200。

直接读取本地资源，network显示from memory 或from disk

缺点：存在版本问题，到期之前的修改不可知

#### Expires

绝对时间

```
Expires: Wed, 22 Oct 2018 08:41:00 GMT
```

`Expires` 是 HTTP/1 的产物，表示资源会在 `Wed, 22 Oct 2018 08:41:00 GMT` 后过期，需要再次请求。

缺点：**受限于本地时间**，如果修改了本地时间，和服务端时间不一致，可能会造成缓存失效。

#### Cache-control

相对时间

```
Cache-control: max-age=30
```

`Cache-Control` 出现于 HTTP/1.1，**优先级高于 Expires** 。该属性值表示资源会在 30 秒后过期，需要再次请求。

`Cache-Control` **可以在请求头或者响应头中设置**，并且可以组合使用多种指令，达到多个目的。比如说我们希望资源能被缓存下来，并且是客户端和代理服务器都能缓存，还能设置缓存失效时间等等。

![img](https://user-gold-cdn.xitu.io/2018/12/6/1678234a1ed20487?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

多种指令配合流程图

常见指令的作用：

<img src="浏览器和API.assets/截屏2022-01-13 上午10.43.08.png" alt="截屏2022-01-13 上午10.43.08" style="zoom:50%;" />

> no-cache：不使用强缓存
>
> no-store：不缓存

### 协商缓存

无版本问题

如果缓存过期了，就需要发起请求验证资源是否有更新。协商缓存可以通过设置两种 HTTP Header 实现：`Last-Modified` 和 `ETag` 。

当浏览器发起请求验证资源时，如果资源没有做改变，那么服务端就会返回 304 状态码，并且更新浏览器缓存有效期。

![img](https://user-gold-cdn.xitu.io/2018/12/6/16782357baddf1c6?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)协商缓存

1. **Last-Modified 和 If-Modified-Since**

`Last-Modified` 表示本地文件最后修改日期，`If-Modified-Since` 会将 `Last-Modified` 的值发送给服务器，询问服务器在该日期后资源是否有更新，有更新的话就会将新的资源发送回来，否则返回 304 状态码。

但是 `Last-Modified` 存在一些**弊端**：

- 如果本地**打开**缓存文件，即使没有对文件进行修改，但还是会造成 `Last-Modified` 被修改，服务端不能命中缓存导致发送相同的资源
- 因为 `Last-Modified` 只能**以秒计时**，如果在不可感知的时间内修改完成文件，那么服务端会认为资源还是命中了，不会返回正确的资源
- 某些服务器不能精确的得到最后修改时间
- 文件时服务器动态生成时，更新时间永远是生成时间，其不到缓存作用

因为以上这些弊端，所以在 HTTP / 1.1 出现了 `ETag` 。

2. **ETag 和 If-None-Match**

`ETag` 类似于文件指纹，`If-None-Match` 会将当前 `ETag` 发送给服务器，询问该资源 `ETag` 是否变动，有变动的话就将新的资源发送回来。并且 `ETag` **优先级**比 `Last-Modified` **高**。准确性较高。

弊端：

- 计算ETag需要性能损耗
- 分布式服务器存储时，计算ETag的算法如果不同，从一台服务器上获得的页面到另一台服务器上验证时出现ETag不匹配的现象

以上就是缓存策略的所有内容了。**如果什么缓存策略都没设置，那么浏览器会怎么处理？**

对于这种情况，浏览器会采用一个**启发式的算法**，通常会取响应头中的 `Date` 减去 `Last-Modified` 值的 10% 作为缓存时间。

## 实际场景应用缓存策略

单纯了解理论而不付诸于实践是没有意义的，接下来我们来通过几个场景学习下如何使用这些理论。

### 频繁变动的资源

对于频繁变动的资源，首先需要使用 `Cache-Control: no-cache` 使浏览器每次都请求服务器，然后配合 `ETag` 或者 `Last-Modified` 来验证资源是否有效。这样的做法虽然不能节省请求数量，但是能显著减少响应数据大小。

### 代码文件

这里特指除了 HTML 外的代码文件，因为 HTML 文件一般不缓存或者缓存时间很短。

一般来说，现在都会使用工具来打包代码，那么我们就可以对文件名进行哈希处理，只有当代码修改后才会生成新的文件名。基于此，我们就可以给代码文件设置缓存有效期一年 `Cache-Control: max-age=31536000`，这样只有当 HTML 文件中引入的文件名发生了改变才会去下载最新的代码文件，否则就一直使用缓存。

# 浏览器渲染原理

学习浏览器渲染原理更多的是为了解决性能的问题，如果不了解这部分的知识，你就不知道什么情况下会对性能造成损伤。

我们知道执行 JS 有一个 JS 引擎，那么执行渲染也有一个渲染引擎。同样，渲染引擎在不同的浏览器中也不是都相同的。比如在 Firefox 中叫做 **Gecko**，在 Chrome 和 Safari 中都是基于 **WebKit** 开发的。以下是关于 **WebKit** 的渲染引擎内容。

## HTML 转换为 DOM 树

- **字节流解码**

当我们打开一个网页时，浏览器都会去请求对应的 HTML 文件。但是计算机硬件是不理解这些字符串的，所以在网络中传输的内容其实都是 `0` 和 `1` 这些**字节数据**。当浏览器得到字节数据后，通过“**编码嗅探算法**”来**确定字符编码**，然后根据字符编码将字节流数据进行**解码**，生成**字符数据**，也就是我们编写的代码。

这个把字节数据解码成字符数据的过程称之为“**字节流解码**”。

- **输入流预处理**

通过上一步解码得到的字符流数据在进入解析环节之前还需要进行一些预处理操作。比如将换行符转换成统一的格式，最终生成**规范化的字符流数据**，这个把字符数据进行统一格式化的过程称之为“**输入流预处理**”。

![img](https://user-gold-cdn.xitu.io/2018/11/27/16754281e59587f3?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

- **解析：令牌化/标记化**

解析包含两步，第一步是将**字符数据转化成令牌**（Token），第二步是解析 **HTML 生成 DOM 树**。

当数据转换为字符串以后，浏览器会先将这些**字符串通过词法分析转换为标记**（token），这一过程在词法分析中叫做**标记化**（tokenization）。

![img](https://user-gold-cdn.xitu.io/2018/11/27/16754288f37a5347?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

那么什么是标记呢？这其实属于编译原理这一块的内容了。简单来说，标记还是字符串，是构成代码的**最小单位**。这一过程会将代码分拆成一块块，并给这些内容打上标记，便于理解这些最小单位的代码是什么意思。

其过程是使用了一种类似状态机的算法，即每次接收一个或多个输入流中的字符；然后根据当前状态和这些字符来更新下一个状态，也就是说在不同的状态下接收同样的字符数据可能会产生不同的结果，比如当接收到“body”字符串时，在标签打开状态会解析成标签，在标签关闭状态则会解析成文本节点。

> **遇到 script 标签时的处理**
>
> HTML中往往会引入一些额外的资源，图片、CSS、js等，图片，CSS需要通过网络下载或从缓存中直接加载，不会阻塞HTML解析，但是如果在 HTML 解析过程中遇到 script 标签，则会发生一些变化。
>
> 如果遇到的是内联代码，也就是在 script 标签中直接写代码，那么解析过程会暂停，执行权限会转给 JavaScript 脚本引擎，待 JavaScript 脚本执行完成之后再交由渲染引擎继续解析。但是如果脚本内容中调用了改变 DOM 结构的 document.write() 函数，此时渲染引擎会回到第二步，将这些代码加入字符流，重新进行解析。
>
> 如果遇到的是外链脚本，那么渲染引擎会根据标签属性来执行对应的操作，比如 async 或 defer 异步加载js

![img](https://user-gold-cdn.xitu.io/2018/11/27/167540a7b5cef612?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

- **解析：构建 DOM 树**

浏览器在创建**解析器**的同时会创建一个 **Document 对象**。在树构建阶段，Document 会作为根节点被不断地修改和扩充。标记步骤产生的令牌会被送到树构建器进行处理。HTML 5 标准中定义了每类令牌对应的 DOM 元素，当树构建器接收到某个令牌时就会创建该令牌对应的 DOM 元素并将该元素插入到 DOM 树中。

为了纠正元素标签嵌套错位的问题和处理未关闭的元素标签，树构建器创建的新 DOM 元素还会被插入到一个开放元素栈中。

![img](https://user-gold-cdn.xitu.io/2018/11/27/1675416cbea98c3c?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

以上就是浏览器从网络中接收到 HTML 文件然后一系列的转换过程。

![img](https://user-gold-cdn.xitu.io/2018/11/27/167542b09875a74a?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

当然，在解析 HTML 文件的时候，浏览器还会遇到 CSS 和 JS 文件，这时候浏览器也会去下载并解析这些文件。

## CSS 文件转换为 CSSOM 树

其实转换 CSS 解析的过程和 HTML 解析的过程是极其类似的，最终也会生成树状结构。

与 DOM 树不同的是，CSSOM 树的节点具有**继承特性**，也就是会先继承父节点样式作为当前样式，然后再进行补充或覆盖。

![img](https://user-gold-cdn.xitu.io/2018/11/27/167542a9af5f193f?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

在这一过程中，浏览器会确定下每一个节点的**样式**到底是什么，并且这一过程其实是**很消耗资源**的。因为样式你可以自行设置给某个节点，也可以通过继承获得。在这一过程中，浏览器得**递归** CSSOM 树，然后确定具体的元素到底是什么样式。

如果你有点不理解为什么会消耗资源的话，我这里举个例子

```html
<div>
  <a> <span></span> </a>
</div>
<style>
  span {
    color: red;
  }
  div > a > span {
    color: red;
  }
</style>
```

对于第一种设置样式的方式来说，浏览器只需要找到页面中所有的 `span` 标签然后设置颜色，但是对于第二种设置样式的方式来说，浏览器首先需要找到所有的 `span` 标签，然后找到 `span` 标签上的 `a` 标签，最后再去找到 `div` 标签，然后给符合这种条件的 `span` 标签设置颜色，这样的递归过程就很复杂。所以我们**应该尽可能的避免写过于具体的 CSS 选择器**，然后对于 HTML 来说也**尽量少的添加无意义标签**，保证**层级扁平**。

## 渲染

- **构建渲染树（render tree）**

当我们生成 DOM 树和 CSSOM 树以后，就需要将这两棵树**组合为渲染树**。

![img](https://user-gold-cdn.xitu.io/2018/11/27/16754488529c48bd?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

在这一过程中，不是简单的将两者合并就行了。这个过程会从 DOM 树的根节点开始遍历，然后在 CSSOM 树上找到每个节点对应的样式。

遍历过程中会自动忽略那些不需要渲染的节点（比如脚本标记、元标记等）以及不可见的节点（比如设置了“display:none”样式），同时也会将一些需要显示的伪类元素加到渲染树中，所以dom tree和render tree并不是一一对应的。

- **布局（layout tree）**

当浏览器生成渲染树以后，就会根据渲染树来进行**布局**（也可以叫做回流），就是通过遍历dom和计算元素的大小及位置来生成layout tree。layout tree每个节点都记录了x，y坐标和边框尺寸。

计算元素布局是一个比较复杂的操作，因为需要考虑的因素有很多。

布局完成后会**输出对应的“盒模型”**，它会精确地捕获每个元素的确切位置和大小，将所有相对值都转换为屏幕上的绝对像素。

- **绘制**

绘制和栅格化就是将layout tree中的**每个节点转换成屏幕上的实际像素**的过程。

渲染引擎现在知道了元素的大小形状和位置，但是还不知道绘制顺序，如果按照dom层级结构绘制，很可能会导致页面被错误地渲染。例如，对于使用 z-index 属性的元素。所以绘制过程中的第一步就是遍历布局树，**生成绘制记录（paint record）**，然后渲染引擎会根据绘制记录去绘制相应的内容。

- **栅格化**

将所有的信息转换成像素点显示到屏幕上的行为称为栅格化（rastering）

chrome最早使用了一种简单方式，只栅格化用户可视区域的内容，滚动页面时再栅格化更多的内容，缺点是会导致延迟，现在chrome进行了优化使用了一种更为复杂的栅格化流程叫做**合成（compositing）**，合成是将页面各个部分分成多个图层，分别进行栅格化，并在合成器线程中（compositor thread）中单独进行合成，简单来说就是页面所有元素按照某种规则划分图层并栅格化好了，然后把可视区的内容组成一帧显示给用户。

- **layer tree**

遍历layout tree生成layer tree以及绘制顺序确定后，将这些信息传递给合成器线程，合成器线程将每个图层栅格化，由于一层可能像整张页面那么大，因此合成器将他们切分为许多图块（tiles），然后将每个图块发送给栅格化线程（raster thread），栅格化每个图块，并存储在GPU中，栅格化完成之后，合成器将它们收集成为 draw quads 信息，记录了图块在内存中的位置和在页面上的位置，根据这些信息合成器线程生成一个合成器帧（compositor frame）然后合成器帧通过IPC传递给浏览器进程，浏览器进程传送给GPU，GPU渲染到页面上

![html渲染流程](E:\Jennifer\other\notes\images\html渲染流程.png)

> GPU与CPU：
>
> CPU，大脑，负责处理各种任务，现在支持多核心多线程，运算能力大大增强
>
> GPU，更擅长多核心处理单一任务，最初被用于处理图像，所以用来渲染页面内容，随着GPU发展，也承担了越来越多的计算任务

（对于无动画效果的情况，只需要考虑空间维度，生成不同的图层，然后再把这些图层进行合成，最终成为我们看到的页面。当然这个绘制过程并不是静态不变的，会随着页面滚动不断合成新的图形）

总结：具体来说数据的变化过程为：字节 → 字符 → 令牌 → node → dom树/css树 → render树（处理样式） →layout树（计算大小形状位置） → layer树（绘制顺序） → 栅格化之后的图块 → GPU渲染页面

## 为什么操作 DOM 慢

想必大家都听过操作 DOM 性能很差，但是这其中的原因是什么呢？

因为 DOM 是属于渲染引擎中的东西，而 JS 又是 JS 引擎中的东西。当我们**通过 JS 操作 DOM 的时候，其实这个操作涉及到了两个线程之间的通信，操作系统在进行线程切换的时候需要保存上一个线程执行时的状态信息并读取下一个线程的状态信息，俗称上下文切换。而这个操作相对而言是比较耗时的。那么势必会带来一些性能上的损耗。**操作 DOM 次数一多，也就等同于一直在进行线程之间的通信，并且操作 DOM **可能还会带来重绘回流**的情况，所以也就导致了性能上的问题。

> 经典面试题：插入几万个 DOM，如何实现页面不卡顿？

对于这道题目来说，首先我们肯定不能一次性把几万个 DOM 全部插入，这样肯定会造成卡顿，所以解决问题的重点应该是如何分批次部分渲染 DOM。大部分人应该可以想到通过 `requestAnimationFrame`（计时器）的方式去循环的插入 DOM，其实还有种方式去解决这个问题：**虚拟滚动**（virtualized scroller）。

**这种技术的原理就是只渲染可视区域内的内容，非可见区域的那就完全不渲染了，当用户在滚动的时候就实时去替换渲染的内容。**

![img](https://user-gold-cdn.xitu.io/2018/12/15/167b1c6887ecbba7?imageslim)

从上图中我们可以发现，即使列表很长，但是渲染的 DOM 元素永远只有那么几个，当我们滚动页面的时候就会实时去更新 DOM，这个技术就能顺利解决这道经典面试题。如果你想了解更多的内容可以了解下这个 [react-virtualized](https://link.juejin.im/?target=https%3A%2F%2Fgithub.com%2Fbvaughn%2Freact-virtualized)。

## 什么情况阻塞渲染

首先渲染的前提是生成渲染树，所以 **HTML 和 CSS 肯定会阻塞渲染**。如果你想渲染的越快，你越应该降低一开始需要渲染的文件**大小**，并且**扁平层级，优化选择器**。

然后当浏览器在**解析到 `script` 标签时，会暂停构建 DOM**，完成后才会从暂停的地方重新开始。也就是说，如果你想首屏渲染的越快，就越**不应该在首屏就加载 JS 文件，这也是都建议将 `script` 标签放在 `body` 标签底部的原因。**

当然在当下，并不是说 `script` 标签必须放在底部，因为你可以给 `script` 标签添加 `defer` 或者 `async` 属性。

当 `script` 标签加上 `defer` 属性以后，表示该 JS 文件会并行下载，但是会放到 HTML 解析完成后顺序执行，所以对于这种情况你可以把 `script` 标签放在任意位置。

对于没有任何依赖的 JS 文件可以加上 `async` 属性，表示 JS 文件下载和解析不会阻塞渲染。

## 重绘（Repaint）和回流（Reflow）

重绘和回流会在我们设置节点样式时频繁出现，同时也会很大程度上影响性能。

- 重绘是当节点需要更改外观而不会影响布局的，比如改变 `color` 就叫称为重绘
- 回流是布局或者几何属性需要改变就称为回流。

回流**必定**会发生重绘，重绘**不一定**会引发回流。回流所需的成本比重绘高的多，改变父节点里的子节点很可能会导致父节点的一系列回流。

以下几个动作可能会导致性能问题：

- 改变 `window` 大小
- 改变字体
- 添加或删除样式
- 文字改变
- 定位或者浮动
- 盒模型

并且很多人不知道的是，重绘和回流其实也和 Eventloop 有关。

1. 当 Eventloop 执行完 Microtasks 后，会判断 `document` 是否需要更新，因为浏览器是 60Hz 的刷新率，每 16.6ms 才会更新一次。
2. 然后判断是否有 `resize` 或者 `scroll` 事件，有的话会去触发事件，所以 `resize` 和 `scroll` 事件也是至少 16ms 才会触发一次，并且自带节流功能。
3. 判断是否触发了 media query
4. 更新动画并且发送事件
5. 判断是否有全屏操作事件
6. 执行 `requestAnimationFrame` 回调
7. 执行 `IntersectionObserver` 回调，该方法用于判断元素是否可见，可以用于懒加载上，但是兼容性不好
8. 更新界面
9. 以上就是一帧中可能会做的事情。如果在一帧中有空闲时间，就会去执行 `requestIdleCallback`回调。

以上内容来自于 [HTML 文档](https://link.juejin.im/?target=https%3A%2F%2Fhtml.spec.whatwg.org%2Fmultipage%2Fwebappapis.html%23event-loop-processing-model)。

### 减少重绘和回流

- 使用 `transform` 替代 `top`

```js
<div class="test"></div>
<style>
  .test {
    position: absolute;
    top: 10px;
    width: 100px;
    height: 100px;
    background: red;
  }
</style>
<script>
  setTimeout(() => {
    // 引起回流
    document.querySelector('.test').style.top = '100px'
  }, 1000)
</script>
```

- 使用 `visibility` 替换 `display: none` ，因为前者只会引起重绘，后者会引发回流（改变了布局）

- 在循环外操作元素，当然即使在循环外也要尽量减少操作元素，因为不知道他人调用你的代码时是否处于循环中。

  ```js
  const times = 10000;
  console.time('switch')
  for (let i = 0; i < times; i++) {
    document.body === 1 ? console.log(1) : void 0;
  }
  console.timeEnd('switch') // 1.873046875ms
  var body = JSON.stringify(document.body)
  console.time('batch')
  for (let i = 0; i < times; i++) {
    body === 1 ? console.log(1) : void 0;
  }
  console.timeEnd('batch') // 0.846923828125ms
  ```

  ```js
  for(let i = 0; i < 1000; i++) {
      // 获取 offsetTop 会导致回流，因为需要去获取正确的值
      console.log(document.querySelector('.test').style.offsetTop)
  }
  ```

- 批量操作元素

  比如说要创建 1 万个 div 元素，在循环中直接创建再添加到父元素上耗时会非常多。如果采用字符串拼接的形式，先将 1 万个 div 元素的 html 字符串拼接成一个完整字符串，然后赋值给 body 元素的 innerHTML 属性就可以明显减少耗时。

  ```js
  const times = 10000;
  console.time('createElement')
  for (let i = 0; i < times; i++) {
    const div = document.createElement('div')
    document.body.appendChild(div)
  }
  console.timeEnd('createElement')// 54.964111328125ms
  console.time('innerHTML')
  let html=''
  for (let i = 0; i < times; i++) {
    html+='<div></div>'
  }
  document.body.innerHTML += html // 31.919921875ms
  console.timeEnd('innerHTML')
  ```

  虽然通过修改 innerHTML 来实现批量操作的方式效率很高，但它并不是万能的。比如要在此基础上实现事件监听就会略微麻烦，只能通过事件代理或者重新选取元素再进行单独绑定。批量操作除了用在创建元素外也可以用于修改元素属性样式，比如下面的例子。

  创建 2 万个 div 元素，以单节点树结构进行排布，每个元素有一个对应的序号作为文本内容。现在通过 style 属性对第 1 个 div 元素进行 2 万次样式调整。下面是直接操作 style 属性的代码：

  ```js
  const times = 20000;
  let html = ''
  for (let i = 0; i < times; i++) {
    html = `<div>${i}${html}</div>`
  }
  document.body.innerHTML += html
  const div = document.querySelector('div')
  for (let i = 0; i < times; i++) {
    div.style.fontSize = (i % 12) + 12 + 'px'
    div.style.color = i % 2 ? 'red' : 'green'
    div.style.margin = (i % 12) + 12 + 'px'
  }
  ```

  如果将需要修改的样式属性放入 JavaScript 数组，然后对这些修改进行 reduce 操作，得到最终需要的样式之后再设置元素属性，那么性能会提升很多。代码如下：

  ```js
  const times = 20000;
  let html = ''
  for (let i = 0; i < times; i++) {
    html = `<div>${i}${html}</div>`
  }
  document.body.innerHTML += html
  
  let queue = [] //  创建缓存样式的数组
  let microTask // 执行修改样式的微任务
  const st = () => {
    const div = document.querySelector('div')
    // 合并样式
    const style = queue.reduce((acc, cur) => ({...acc, ...cur}), {})
    for(let prop in style) {
      div.style[prop] = style[prop]
    }
    queue = []
    microTask = null
  }
  const setStyle = (style) => {
    queue.push(style)
    // 创建微任务
    if(!microTask) microTask = Promise.resolve().then(st)
  }
  for (let i = 0; i < times; i++) {
    const style = {
      fontSize: (i % 12) + 12 + 'px',
      color: i % 2 ? 'red' : 'green',
      margin:  (i % 12) + 12 + 'px'
    }
    setStyle(style)
  }
  ```

- 缓存元素集合

  ```js
  for (let i = 0; i < document.querySelectorAll('div').length; i++) {
    document.querySelectorAll(`div`)[i].innerText = i
  }
  
  // 优化后
  const divs = document.querySelectorAll('div')
  for (let i = 0; i < divs.length; i++) {
    divs[i].innerText = i
  }
  ```

- 不要使用 `table` 布局，可能很小的一个小改动会造成整个 `table` 的重新布局

- 动画实现的速度的选择，动画速度越快，回流次数越多，也可以选择使用 `requestAnimationFrame`

- CSS 选择符**从右往左**匹配查找，避免节点层级过多，尽量不要使用复杂的匹配规则和复杂的样式，从而减少渲染引擎计算样式规则生成 CSSOM 树的时间；

- 尽量减少重排和重绘影响的区域；

- 使用 CSS3 特性来实现动画效果。

- 将频繁重绘或者回流的节点设置为图层，图层能够阻止该节点的渲染行为影响别的节点。比如对于 `video` 标签来说，浏览器会自动将该节点变为图层。

  

  ![img](https://user-gold-cdn.xitu.io/2018/3/29/1626fb6f33a6f9d7?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

  

  设置节点为图层的方式有很多，我们可以通过以下几个常用属性可以生成新图层

  - `will-change`
  - `video`、`iframe` 标签

## 思考题

> 思考题：在不考虑缓存和优化网络协议的前提下，考虑可以通过哪些方式来最快的渲染页面，也就是常说的关键渲染路径，这部分也是性能优化中的一块内容。

首先你可能会疑问，那怎么测量到底有没有加快渲染速度呢

![img](https://user-gold-cdn.xitu.io/2018/11/27/16754b5a3511198f?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

当发生 `DOMContentLoaded` 事件后，就会生成渲染树，生成渲染树就可以进行渲染了，这一过程更大程度上和硬件有关系了。

**提示如何加速：**

1. 从文件大小考虑
2. 从 `script` 标签使用上来考虑
3. 从 CSS、HTML 的代码书写上来考虑
4. 从需要下载的内容是否需要在首屏使用上来考虑





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

# 同源策略

参考：<http://www.ruanyifeng.com/blog/2016/04/same-origin-policy.html>

## 含义

- 协议相同
- 域名相同
- 端口相同

目的，是为了保证用户信息的安全，防止恶意的网站窃取数据。

**img，iframe，script(jsonp)，link(css:url)不受同源策略限制**

## 限制范围

（1） Cookie、LocalStorage 和 IndexDB 无法读取。

（2） DOM 无法获得。

（3） AJAX 请求不能发送。

## domain

两个网页一级域名相同，只是二级域名不同，浏览器允许通过设置`document.domain`共享 Cookie。

举例来说，A网页是`http://w1.example.com/a.html`，B网页是`http://w2.example.com/b.html`，那么只要设置相同的`document.domain`，两个网页就可以共享Cookie。

```javascript
// A
document.domain = 'example.com';
document.cookie = "test1=hello";
// B
var allCookie = document.cookie;
```

注意，这种方法只适用于 Cookie 和 iframe 窗口，LocalStorage 和 IndexDB 无法通过这种方法，规避同源政策，要使用PostMessage API。

另外，服务器也可以在设置Cookie的时候，指定Cookie的所属域名为一级域名，比如`.example.com`。

```http
Set-Cookie: key=value; domain=.example.com; path=/
```

这样的话，二级域名和三级域名不用做任何设置，都可以读取这个Cookie。

## 跨域

### jsonp

利用script标签没用跨域限制的特点，向服务端发送一个带有回调函数名称和参数的请求，服务端根据参数获取数据后将数据作为参数，返回一个回调函数的调用脚本。

### CORS（跨域资源共享）

需要前后端同时支持，主要是在服务端配置access-control-allow-origin

分为两种请求简单请求和复杂请求，复杂请求会先发一个预检请求，服务端允许后响应会多几条access-control-allow-origin相关字段，不允许会正常返回但不包含这些字段

### hash

hash改变不会刷新页面

在A页面包含跨域页面B时，获取B页面改变hash传递参数，在B页面监听hash的改变

### postMessage

H5类似于hash，利用window.postMessage传递参数，在另一个页面监听message事件执行回调

### webSocket

应对HTTP协议只能客户端发起请求效率低的缺陷一种网络通信协议，客户端服务端都能发送请求，不受同源限制



把代码压缩成图片？？？

# 前端优化

压力

速度

成本

回退：减小系统不正常造成的影响

## 通用优化

### 开发阶段：

文件/请求数量 ---》   合并打包webpack/合并请求
文件体积   ---》   压缩，比如接口的url；减少html代码（利用伪元素等）
合理缓存   ---》   考虑缓存文件，更新，时间
异步请求   ---》   比如图片懒加载，复杂的逻辑，不能过度使用，会让请求增加，需要数据做参考
增加数据请求量   ---》   一个请求32k（包括头），比如翻页，如果一页的数据少可以同时请求多页，如果数据处理复杂有可能得不偿失，需要综合考虑
预加载数据   ---》   增加用户体验

具体的优化方法参考监控数据，用户访问习惯等

监控数据来源：
日志，数据库日志
埋点，前端，服务器获取不到的信息
统计

### 部署阶段：本质是省钱

// 服务器负载，uptime命令

CDN   ---》   变动不大，体积较大的数据，优点：安全，节约带宽
P2P ---》   对等网络，客户端也可以当作服务器，比如百度网盘，腾讯视频，讯雷客户端等，利用用户缓存
静态化，缓存
异构计算   ---》   

### **找出性能瓶颈**

找出瓶颈，内存？cpu？数据库？

**工具：**阿里云pts，百度apm，webpagetest.org，tools.pingdom.com，gtmetrix.com，network，yslow

**network：**

waterflow（瀑布流）：Stalled：开始连接，和服务器负载有关；Request sent：发送请求的时间；waiting：等待响应，和服务器负载有关；content download：下载数据时间

**数据库：**

**测试工具：**数据库管理工具中的性能监测工具，high cost SQL statements 监测sql执行的时间

NoSQL：redis，内存型分布式

浏览器---》服务器---》redis---》数据库---》服务器---》redis---》浏览器

解决问题















react-native build android

























## 图片优化

### 计算图片大小

对于一张 100 * 100 像素的图片来说，图像上有 10000 个像素点，如果每个像素的值是 **RGBA** 存储的话，那么也就是说每个像素有 4 个通道，每个通道 1 个字节（8 位 = 1个字节），所以该图片大小大概为 39KB（10000 * 1 * 4 / 1024）。

但是在实际项目中，一张图片可能并不需要使用那么多颜色去显示，我们可以通过减少每个像素的调色板来相应缩小图片的大小。

了解了如何计算图片大小的知识，那么对于如何优化图片，想必大家已经有 2 个思路了：

- **减少像素点**
- **减少每个像素点能够显示的颜色**

### 图片加载优化

1. 不用图片。很多时候会使用到很多修饰类图片，其实这**类修饰图片**完全可以用 **CSS 去代替**。
2. 对于**移动端**来说，屏幕宽度就那么点，完全没有必要去加载原图浪费带宽。**一般图片都用 CDN 加载**，可以计算出适配屏幕的宽度，然后去请求相应裁剪好的图片。
3. **小图使用 base64 格式**
4. 将多个图标文件整合到一张图片中（**雪碧图**）
5. 选择正确的图片格式：
   - 对于能够显示 WebP 格式的浏览器尽量使用 WebP 格式。因为 WebP 格式具有更好的图像数据压缩算法，能带来更小的图片体积，而且拥有肉眼识别无差异的图像质量，缺点就是兼容性并不好
   - 小图使用 PNG，其实对于大部分图标这类图片，完全可以使用 SVG 代替
   - 照片使用 JPEG

## DNS 预解析

DNS 解析也是需要时间的，可以通过预解析的方式来预先获得域名所对应的 IP。

```html
<link rel="dns-prefetch" href="//yuchengkai.cn">
```

## 节流

考虑一个场景，滚动事件中会发起网络请求，但是我们并**不希望用户在滚动过程中一直发起请求，而是隔一段时间发起一次**，对于这种情况我们就可以使用节流。

理解了节流的用途，我们就来实现下这个函数

```js
const throttle = (func, wait = 0, execFirstCall) => {
  let timeout = null
  let args
  let firstCallTimestamp


  function throttled(...arg) {
    if (!firstCallTimestamp) firstCallTimestamp = new Date().getTime()
    if (!execFirstCall || !args) {
      console.log('set args:', arg)
      args = arg
    }
    if (timeout) {
      clearTimeout(timeout)
      timeout = null
    }
    // 以Promise的形式返回函数执行结果
    return new Promise(async(res, rej) => {
      if (new Date().getTime() - firstCallTimestamp >= wait) {
        try {
          const result = await func.apply(this, args)
          res(result)
        } catch (e) {
          rej(e)
        } finally {
          cancel()
        }
      } else {
        timeout = setTimeout(async () => {
          try {
            const result = await func.apply(this, args)
            res(result)
          } catch (e) {
            rej(e)
          } finally {
            cancel()
          }
        }, firstCallTimestamp + wait - new Date().getTime())
      }
    })
  }
  // 允许取消
  function cancel() {
    clearTimeout(timeout)
    args = null
    timeout = null
    firstCallTimestamp = null
  }
  // 允许立即执行
  function flush() {
    cancel()
    return func.apply(this, args)
  }
  throttled.cancel = cancel
  throttled.flush = flush
  return throttled
}
```

## 防抖

考虑一个场景，有一个按钮点击会触发网络请求，但是我们并不希望每次点击都发起网络请求，而是**当用户点击按钮一段时间后没有再次点击的情况才去发起网络请求**，对于这种情况我们就可以使用防抖。

理解了防抖的用途，我们就来实现下这个函数

```js
// func是用户传入需要防抖的函数
// wait是等待时间
const debounce = (func, wait = 50) => {
  // 缓存一个定时器id
  let timer = 0
  // 这里返回的函数是每次用户实际调用的防抖函数
  // 如果已经设定过定时器了就清空上一次的定时器
  // 开始一个新的定时器，延迟执行用户传入的方法
  return function(...args) {
    if (timer) clearTimeout(timer)
    timer = setTimeout(() => {
      func.apply(this, args)
    }, wait)
  }
}

// 优化：将原函数作为参数传入 debounce() 函数中，同时指定延迟等待时间，返回一个新的函数，这个函数包含 cancel 属性，用来取消原函数执行。flush 属性用来立即调用原函数，同时将原函数的执行结果以 Promise 的形式返回。
const debounce = (func, wait = 0) => {
  let timeout = null
  let args
  function debounced(...arg) {
    args = arg
    if(timeout) {
      clearTimeout(timeout)
      timeout = null
    }
    // 以Promise的形式返回函数执行结果
    return new Promise((res, rej) => {
      timeout = setTimeout(async () => {
        try {
          const result = await func.apply(this, args)
          res(result)
        } catch(e) {
          rej(e)
        }
      }, wait)
    })
  }
  // 允许取消
  function cancel() {
    clearTimeout(timeout)
    timeout = null
  }
  // 允许立即执行
  function flush() {
    cancel()
    return func.apply(this, args)
  }
  debounced.cancel = cancel
  debounced.flush = flush
  return debounced
}
```

## 预加载

在开发中，可能会遇到这样的情况。**有些资源不需要马上用到，但是希望尽早获取，这时候就可以使用预加载。**

预加载其实是声明式的 `fetch` ，强制浏览器请求资源，并且不会阻塞 `onload` 事件，可以使用以下代码开启预加载

```html
<link rel="preload" href="http://example.com">
```

预加载可以一定程度上降低首屏的加载时间，因为可以将一些不影响首屏但重要的文件延后加载，唯一缺点就是兼容性不好。

## 预渲染

可以通过预渲染将下载的文件预先在后台渲染，可以使用以下代码开启预渲染

```html
<link rel="prerender" href="http://example.com"> 
```

预渲染虽然可以提高页面的加载速度，但是要确保该页面大概率会被用户在之后打开，否则就是白白浪费资源去渲染。

## 懒执行

懒执行就是将**某些逻辑延迟到使用时再计算**。该技术可以用于首屏优化，对于某些耗时逻辑并不需要在首屏就使用的，就可以使用懒执行。懒执行需要唤醒，一般可以通过定时器或者事件的调用来唤醒。

## 懒加载

懒加载就是**将不关键的资源延后加载**。

懒加载的原理就是只加载自定义区域（通常是可视区域，但也可以是即将进入可视区域）内需要加载的东西。对于图片来说，先设置图片标签的 `src` 属性为一张占位图，将真实的图片资源放入一个自定义属性中，当进入自定义区域时，就将自定义属性替换为 `src` 属性，这样图片就会去下载资源，实现了图片懒加载。

懒加载不仅可以用于图片，也可以使用在别的资源上。比如进入可视区域才开始播放视频等等。

## CDN

CDN 的原理是尽可能的在各个地方分布机房缓存数据，这样即使我们的根服务器远在国外，在国内的用户也可以通过国内的机房迅速加载资源。

因此，我们可以将静态资源尽量使用 CDN 加载，由于浏览器对于单个域名有并发请求上限，可以考虑使用多个 CDN 域名。并且对于 CDN 加载静态资源需要注意 CDN 域名要与主站不同，否则每次请求都会带上主站的 Cookie，平白消耗流量。

- 减少重绘避免重排，本质是合并修改

  1. css操作合并到一个类中，一次性修改
  2. 将Dom操作合并，一次性插入

- 减少DNS查找

  网页的呈现过程：域名解析 --> 发起TCP的3次握手 --> 建立TCP连接后发起http请求 --> 服务器响应http请求，浏览器得到html代码 --> 浏览器解析html代码，并请求html代码中的资源（如js、css、图片等） --> 浏览器对页面进行渲染呈现给用户 

  域名解析过程：浏览器DNS缓存-->系统DNS缓存-->host文件-->向DNS服务器发起域名解析请求...

  减少主机名的数量就可以减少DNS查找的数量。 

- 使用DNS预解析DNS（Domain Name System 域名系统）

  - DNS解析：通过主机名，最终得到该主机名对应的IP地址的过程。 DNS解析时间可能导致大量用户感知延迟，DNS解析所需的时间差异非常大，延迟范围可以从1ms（本地缓存结果）到普遍的几秒钟时间。所以利用DNS预解析是有意义的。 

  - DNS预解析是浏览器试图在用户访问链接之前解析域名，域名解析后，如果用户确实访问该域名，那么DNS解析时间将不会有延迟。 

  - DNS预解析在某个页面中包含非常多的域名非常有效，如搜索结果页。 

  - 遇到网页中的超链接，`DNS prefetching`从中提取域名并将其解析为IP地址，这些工作在用户浏览网页时，使用最少的CPU和网络在后台进行解析。

    当用户点击这些已经预解析的域名，可以平均减少200毫秒耗时（假设用户最近还未访问过该域名），更重要的是用户不会遇到DNS解析最坏的情况（往往超过1秒）。

    https://www.xuanfengge.com/dns-prefetching-analysis.html

- 压缩合并资源，减少请求

- 使用浏览器缓存

  Cache-Control 用于控制文件在本地缓存有效时长。最常见的，比如服务器回包：Cache-Control:max-age=600 表示文件在本地应该缓存，且有效时长是600秒（从发出请求算起）。在接下来600秒内，如果有请求这个资源，浏览器不会发出 HTTP 请求，而是直接使用本地缓存的文件。

  Last-Modified 是标识文件在服务器上的最新更新时间。下次请求时，如果文件缓存过期，浏览器通过 If-Modified-Since 字段带上这个时间，发送给服务器，由服务器比较时间戳来判断文件是否有修改。如果没有修改，服务器返回304告诉浏览器继续使用缓存；如果有修改，则返回200，同时返回最新的文件。

  Expires 是 HTTP1.0 标准中的字段，Cache-Control 是 HTTP1.1 标准中新加的字段，功能一样，都是控制缓存的有效时间。Expires 的值一个绝对的时间点，如：Expires: Thu, 10 Nov 2015 08:45:11 GMT，表示在这个时间点之前，缓存都是有效的。 当这两个字段同时出现时，Cache-Control 是高优化级的。

  Etag 也是和 Last-Modified 一样，对文件进行标识的字段。不同的是，Etag 的取值是一个对文件进行标识的特征字串。在向服务器查询文件是否有更新时，浏览器通过 If-None-Match 字段把特征字串发送给服务器，由服务器和文件最新特征字串进行匹配，来判断文件是否有更新。没有更新回包304，有更新回包200。Etag 和 Last-Modified 可根据需求使用一个或两个同时使用。两个同时使用时，只要满足基中一个条件，就认为文件没有更新。

  还有一些应用层的缓存机制比如：DOMStorage和appstorage等

- 非核心代码异步加载

- 使用CDN

  内容分发网络（Content delivery network或Content distribution network，缩写：CDN）。简单来说它主要的工作是把我们需要被分发的内容分发到世界各地的各个节点上，让世界各地的人都可以在距离最近的网络节点拿到想要拿到的内容，减少网络传输距离从而达到加速的目的。

  CDN的本质仍然是一个缓存，而且将数据缓存在里用户最近的地方，使用户以最快的速度获取数据，即网络访问第一跳。 

  适用于静态资源

- 减少DOM嵌套

- 将样式表放在头部，脚本放在底部

# 安全防范

## XSS

> 涉及面试题：什么是 XSS 攻击？如何防范 XSS 攻击？什么是 CSP？

XSS 简单点来说，就是攻击者想尽一切办法将**可以执行的代码注入到网页中**。

XSS 可以分为多种类型，但是总体上我认为分为两类：**持久型和非持久型**。

持久型也就是攻击的代码被服务端写入进**数据库**中，这种攻击危害性很大，因为如果网站访问量很大的话，就会导致大量正常访问页面的用户都受到攻击。

举个例子，对于评论功能来说，就得防范持久型 XSS 攻击，因为我可以在评论中输入以下内容

![img](https://user-gold-cdn.xitu.io/2018/12/2/1676a843648d488c?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

这种情况如果前后端没有做好防御的话，这段评论就会被存储到数据库中，这样每个打开该页面的用户都会被攻击到。

非持久型相比于前者危害就小的多了，一般通过**修改 URL 参数**的方式加入攻击代码，诱导用户访问链接从而进行攻击。

举个例子，如果页面需要从 URL 中获取某些参数作为内容的话，不经过过滤就会导致攻击代码被执行

```html
<!-- http://www.domain.com?name=<script>alert(1)</script> -->
<div>{{name}}</div>                                                  
```

但是对于这种攻击方式来说，如果用户使用 Chrome 这类浏览器的话，浏览器就能自动帮助用户防御攻击。但是我们不能因此就不防御此类攻击了，因为我不能确保用户都使用了该类浏览器。

![img](https://user-gold-cdn.xitu.io/2018/12/2/1676d5e1a09c8367?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

对于 XSS 攻击来说，通常有两种方式可以用来防御。

### 转义字符

首先，**对于用户的输入应该是永远不信任的**。最普遍的做法就是转义输入输出的内容，对于引号、尖括号、斜杠进行转义

```js
function escape(str) {
  str = str.replace(/&/g, '&amp;')
  str = str.replace(/</g, '&lt;')
  str = str.replace(/>/g, '&gt;')
  str = str.replace(/"/g, '&quto;')
  str = str.replace(/'/g, '&#39;')
  str = str.replace(/`/g, '&#96;')
  str = str.replace(/\//g, '&#x2F;')
  return str
}
```

通过转义可以将攻击代码 `<script>alert(1)</script>` 变成

```js
// -> &lt;script&gt;alert(1)&lt;&#x2F;script&gt;
escape('<script>alert(1)</script>')
```

但是对于显示富文本来说，显然不能通过上面的办法来转义所有字符，因为这样会把需要的格式也过滤掉。对于这种情况，通常采用**白名单过滤**的办法，当然也可以通过黑名单过滤，但是考虑到需要过滤的标签和标签属性实在太多，更加推荐使用白名单的方式。

```js
const xss = require('xss')
let html = xss('<h1 id="title">XSS Demo</h1><script>alert("xss");</script>')
// -> <h1>XSS Demo</h1>&lt;script&gt;alert("xss");&lt;/script&gt;
console.log(html)
```

以上示例使用了 `js-xss` 来实现，可以看到在输出中保留了 `h1` 标签且过滤了 `script` 标签。

### CSP

CSP **本质上就是建立白名单**，开发者明确告诉浏览器哪些外部资源可以加载和执行。我们只需要配置规则，如何拦截是由浏览器自己实现的。我们可以通过这种方式来尽量减少 XSS 攻击。

通常可以通过两种方式来开启 CSP：

1. 设置 HTTP Header 中的 `Content-Security-Policy`
2. 设置 `meta` 标签的方式 `<meta http-equiv="Content-Security-Policy">`

这里以设置 HTTP Header 来举例

- 只允许加载本站资源

  ```
  Content-Security-Policy: default-src ‘self’
  ```

- 只允许加载 HTTPS 协议图片

  ```
  Content-Security-Policy: img-src https://*
  ```

- 允许加载任何来源框架

  ```
  Content-Security-Policy: child-src 'none'
  ```

当然可以设置的属性远不止这些，你可以通过查阅 [文档](https://link.juejin.im/?target=https%3A%2F%2Fdeveloper.mozilla.org%2Fen-US%2Fdocs%2FWeb%2FHTTP%2FHeaders%2FContent-Security-Policy) 的方式来学习，这里就不过多赘述其他的属性了。

对于这种方式来说，只要开发者配置了正确的规则，那么即使网站存在漏洞，攻击者也不能执行它的攻击代码，并且 CSP 的兼容性也不错。

![img](https://user-gold-cdn.xitu.io/2018/12/2/1676d8215a3d1f5b?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

## CSRF

> 涉及面试题：什么是 CSRF 攻击？如何防范 CSRF 攻击？

CSRF 中文名为**跨站请求伪造**。原理就是攻击者构造出一个后端请求地址，诱导用户点击或者通过某些途径自动发起请求。如果用户是在登录状态下的话，后端就以为是用户在操作，从而进行相应的逻辑。

举个例子，假设网站中有一个通过 `GET` 请求提交用户评论的接口，那么攻击者就可以在钓鱼网站中加入一个图片，图片的地址就是评论接口

```
<img src="http://www.domain.com/xxx?comment='attack'"/>
```

那么你是否会想到使用 `POST` 方式提交请求是不是就没有这个问题了呢？其实并不是，使用这种方式也不是百分百安全的，攻击者同样可以诱导用户进入某个页面，在页面中通过表单提交 `POST` 请求。

### 如何防御

防范 CSRF 攻击可以遵循以下几种规则：

1. Get 请求不对数据进行修改
2. 不让第三方网站访问到用户 Cookie
3. 阻止第三方网站请求接口
4. 请求时附带验证信息，比如验证码或者 Token

#### SameSite

可以对 Cookie 设置 `SameSite` 属性。该属性表示 **Cookie 不随着跨域请求发送**，可以很大程度减少 CSRF 的攻击，但是该属性目前并不是所有浏览器都兼容。

#### 验证 Referer

对于需要防范 CSRF 的请求，我们可以通过验证 Referer 来判断该请求是否为第三方网站发起的。

#### Token

服务器下发一个随机 Token，每次发起请求时将 Token 携带上，服务器验证 Token 是否有效。

## 点击劫持

> 涉及面试题：什么是点击劫持？如何防范点击劫持？

点击劫持是一种视觉欺骗的攻击手段。攻击者将需要攻击的网站通过 `iframe` 嵌套的方式嵌入自己的网页中，并将 `iframe` 设置为透明，在页面中透出一个按钮诱导用户点击。

![img](https://user-gold-cdn.xitu.io/2018/12/1/16768734d57c5f47?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

对于这种攻击方式，推荐防御的方法有两种。

### X-FRAME-OPTIONS

`X-FRAME-OPTIONS` 是一个 HTTP 响应头，在现代浏览器有一个很好的支持。这个 HTTP 响应头 就是为了防御用 `iframe` 嵌套的点击劫持攻击。

该响应头有三个值可选，分别是

- `DENY`，表示页面不允许通过 `iframe` 的方式展示
- `SAMEORIGIN`，表示页面可以在相同域名下通过 `iframe` 的方式展示
- `ALLOW-FROM`，表示页面可以在指定来源的 `iframe` 中展示

### JS 防御

对于某些远古浏览器来说，并不能支持上面的这种方式，那我们只有通过 JS 的方式来防御点击劫持了。

```html
<head>
  <style id="click-jack">
    html {
      display: none !important;
    }
  </style>
</head>
<body>
  <script>
    if (self == top) {
      var style = document.getElementById('click-jack')
      document.body.removeChild(style)
    } else {
      top.location = self.location
    }
  </script>
</body>
```

以上代码的作用就是当通过 `iframe` 的方式加载页面时，攻击者的网页直接不显示所有内容了。

## 中间人攻击

> 涉及面试题：什么是中间人攻击？如何防范中间人攻击？

中间人攻击是**攻击方同时与服务端和客户端建立起了连接，并让对方认为连接是安全的，但是实际上整个通信过程都被攻击者控制了。攻击者不仅能获得双方的通信信息，还能修改通信信息。**

通常来说不建议使用公共的 Wi-Fi，因为很可能就会发生中间人攻击的情况。如果你在通信的过程中涉及到了某些敏感信息，就完全暴露给攻击方了。

当然防御中间人攻击其实并不难，只需要增加一个安全通道来传输信息。**HTTPS** 就可以用来防御中间人攻击，但是并不是说使用了 HTTPS 就可以高枕无忧了，因为如果你没有完全关闭 HTTP 访问的话，攻击方可以通过某些方式将 HTTPS 降级为 HTTP 从而实现中间人攻击。

# 从 V8 中看 JS 性能优化

> 注意：该知识点属于性能优化领域。

## 测试性能工具

Chrome 已经提供了一个大而全的性能测试工具 **Audits**

![img](https://user-gold-cdn.xitu.io/2018/12/3/16772c479b194d48?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)Audits 所处位置

点我们点击 Audits 后，可以看到如下的界面

![img](https://user-gold-cdn.xitu.io/2018/12/3/16772c52e83d97c7?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)Audits 界面

在这个界面中，我们可以选择想测试的功能然后点击 **Run audits** ，工具就会自动运行帮助我们测试问题并且给出一个完整的报告

![img](https://user-gold-cdn.xitu.io/2018/12/3/16772ca3d13a68ab?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)Audits 工具给出的报告

上图是给掘金首页测试性能后给出的一个报告，可以看到报告中分别为**性能、体验、SEO** 都给出了打分，并且每一个指标都有详细的**评估**

![img](https://user-gold-cdn.xitu.io/2018/12/3/16772cae50f7eb81?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)指标中的详细评估

评估结束后，工具还提供了一些**建议**便于我们提高这个指标的分数

![img](https://user-gold-cdn.xitu.io/2018/12/3/16772cbdcdaccf15?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)优化建议

我们只需要一条条根据建议去优化性能即可。

除了 **Audits** 工具之外，还有一个 **Performance** 工具也可以供我们使用。

![img](https://user-gold-cdn.xitu.io/2018/12/3/16772cf78a4fa18f?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)Performance 工具给出的报告

在这张图中，我们可以详细的看到每个**时间段**中浏览器在处理什么事情，哪个过程最消耗时间，便于我们更加详细的了解性能**瓶颈**。

## JS 性能优化

JS 是编译型还是解释型语言其实并不固定。首先 JS 需要有引擎才能运行起来，无论是浏览器还是在 Node 中，这是解释型语言的特性。但是在 V8 引擎下，又引入了 `TurboFan` 编译器，他会在特定的情况下进行优化，将代码编译成执行效率更高的 **Machine Code**，当然这个编译器并不是 JS 必须需要的，只是为了提高代码执行性能，所以总的来说 JS 更偏向于解释型语言。

那么这一小节的内容主要会针对于 Chrome 的 **V8** 引擎来讲解。

在这一过程中，JS 代码首先会解析为**抽象语法树**（AST），然后会通过解释器或者编译器转化为 **Bytecode** 或者 **Machine Code**

![img](https://user-gold-cdn.xitu.io/2018/12/3/167736409eebe688?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)V8 转化代码的过程

从上图中我们可以发现，JS 会首先被解析为 AST，解析的过程其实是略慢的。代码越多，解析的过程也就耗费越长，这也是我们需要压缩代码的原因之一。另外一种减少解析时间的方式是预解析，会作用于未执行的函数，这个我们下面再谈。

![img](https://user-gold-cdn.xitu.io/2018/12/3/1677468f20b62240?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)2016 年手机解析 JS 代码的速度

这里需要注意一点，对于函数来说，应该**尽可能避免声明嵌套函数**（类也是函数），因为这样会造成函数的重复解析。

```js
function test1() {
  // 会被重复解析
  function test2() {}
}
```

然后 **Ignition** 负责将 AST 转化为 Bytecode，**TurboFan** 负责编译出优化后的 Machine Code，**并且 Machine Code 在执行效率上优于 Bytecode**

![img](https://user-gold-cdn.xitu.io/2018/12/3/16773b904cfb732f?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

那么我们就产生了一个疑问，**什么情况下代码会编译为 Machine Code？**

JS 是一门**动态类型**的语言，并且还有一大堆的规则。简单的加法运算代码，内部就需要考虑好几种规则，比如数字相加、字符串相加、对象和字符串相加等等。这样的情况也就势必导致了内部要增加很多判断逻辑，降低运行效率。

```js
function test(x) {
  return x + x
}

test(1)
test(2)
test(3)
test(4)
```

对于以上代码来说，如果一个函数被**多次调用**并且参数一直传入 `number` 类型，那么 V8 就会认为该段代码可以编译为 Machine Code，因为你**固定了类型**，不需要再执行很多判断逻辑了。

但是如果一旦我们传入的参数**类型改变**，那么 Machine Code 就会被 **DeOptimized** 为 Bytecode，这样就有性能上的一个损耗了。所以如果我们希望代码能多的编译为 Machine Code 并且 DeOptimized 的次数减少，就应该尽可能保证传入的**类型一致**。

那么你可能会有一个疑问，到底优化前后有多少的提升呢，接下来我们就来实践测试一下到底有多少的提升。

```js
const { performance, PerformanceObserver } = require('perf_hooks')

function test(x) {
  return x + x
}
// node 10 中才有 PerformanceObserver
// 在这之前的 node 版本可以直接使用 performance 中的 API
const obs = new PerformanceObserver((list, observer) => {
  console.log(list.getEntries())
  observer.disconnect()
})
obs.observe({ entryTypes: ['measure'], buffered: true })

performance.mark('start')

let number = 10000000
// 不优化代码
%NeverOptimizeFunction(test)

while (number--) {
  test(1)
}

performance.mark('end')
performance.measure('test', 'start', 'end')
```

以上代码中我们使用了 `performance` API，这个 API 在性能测试上十分好用。不仅可以用来测量代码的执行时间，还能用来测量各种网络连接中的时间消耗等等，并且这个 API 也可以在浏览器中使用。

![img](https://user-gold-cdn.xitu.io/2018/12/4/16778338eb8b7130?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)优化与不优化代码之间的巨大差距

从上图中我们可以发现，优化过的代码执行时间只需要 9ms，但是不优化过的代码执行时间却是前者的二十倍，已经接近 200ms 了。在这个案例中，我相信大家已经看到了 V8 的性能优化到底有多强，**只需要我们符合一定的规则书写代码，引擎底层就能帮助我们自动优化代码。**

另外，编译器还有个骚操作 **Lazy-Compile**，当函数没有被执行的时候，会对函数进行一次预解析，直到代码被执行以后才会被解析编译。对于上述代码来说，`test` 函数需要被预解析一次，然后在调用的时候再被解析编译。**但是对于这种函数马上就被调用的情况来说，预解析这个过程其实是多余的**，那么有什么办法能够让代码不被预解析呢？

其实很简单，我们只需要给函数**套上括号**就可以了

```
(function test(obj) {
  return x + x
})
```

但是不可能我们为了性能优化，给所有的函数都去套上括号，并且也不是所有函数都需要这样做。我们可以通过 [optimize-js](https://link.juejin.im/?target=https%3A%2F%2Fgithub.com%2Fnolanlawson%2Foptimize-js) 实现这个功能，这个库会分析一些函数的使用情况，然后给需要的函数添加括号，当然这个库很久没人维护了，如果需要使用的话，还是需要测试过相关内容的。

## 小结

- 可以通过 **Audit** 工具获得网站的多个指标的性能报告
- 可以通过 **Performance** 工具了解网站的性能瓶颈
- 可以通过 **Performance** API 具体测量时间
- 为了减少编译时间，我们可以采用**减少代码文件的大小**或者**减少书写嵌套函数**的方式
- 为了让 V8 优化代码，我们应该尽可能保证传入参数的**类型一致**。这也给我们带来了一个思考，这是不是也是使用 TypeScript 能够带来的好处之一`

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

`console.log()`：在控制台输出信息。

`console.warn()`：将警告消息打印到控制台。

`console.error()`：将错误消息打印到控制台。

`console.table()`：接受一些能够以表格形式展示的数据并输出。

`console.group` 和 `console.groupEnd` 是可以将许多 console.log 逻辑分组的方式。然后，你可以在需要时通过折叠组以将其隐藏。

`console.dir()`：可以显示一个对象所有的属性和方法。 

`console.trace()`：用来追踪函数的调用轨迹。 

`console.dirxml()`：用来显示网页的某个节点(node)所包含的html/xml代码) 。

`console.assert()`：用来判断一个表达式或变量是否为真，只有表达式为false时，才输出一条相应作息，并且抛出一个异常 。

```js
const obj = { restaurantName: 'Pizza Planet' };
console.assert(obj.restaurantName === 'Pizza Palace', 'The name of the restaurant is not "Pizza Palace"');
```

`console.time()`和`console.timeEnd()`：用来显示代码的运行时间，传入计时器标志

性能分析：就是分析程序各个部分的运行时间，找出瓶颈所在，使用的方法是`console.profile()`和`console.proileEnd()`; 

`console.count()`：统计代码被执行的次数 ，计数器

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
- 节点：网页中的所有内容都是节点（元素/标签、属性、文本、注释等）
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
// 方式1
<div id="box" onclick="click()"/>
// 方式2
var box = document.getElementById('box');
// onclick方式只能绑定1个事件
box.onclick = function () {
  console.log('点击后执行');
};
box.onclick = null;
// 方式3
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

方式 1 和方式 2 同属于 DOM0 标准，通过这种方式进行事件监会覆盖之前的事件监听函数。

方式 3 属于 DOM2 标准，推荐。同一元素上的事件监听函数互不影响，而且可以独立取消，调用顺序和监听顺序一致。

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

另一个例子：

```html
<ul class="list">
  <li class="item" id="item1">项目1<span class="edit">编辑</span><span class="delete">删除</span></li>
  <li class="item" id="item2">项目2<span class="edit">编辑</span><span class="delete" >删除</span></li>
  <li class="item" id="item3">项目3<span class="edit">编辑</span><span class="delete">删除</span></li>
  ...
</ul>
```

```js
const ul = document.querySelector('.list')
ul.addEventListener('click', e => {
  const t = e.target || e.srcElement
  if (t.classList.contains('item')) {
    getInfo(t.id)
  } else {
    id = t.parentElement.id
    if (t.classList.contains('edit')) {
      edit(id)
    } else if (t.classList.contains('delete')) {
      del(id)
    }
  }
})
```

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