## 小程序

### 底层架构

![img](Naixes阶段性学习笔记2.assets/a21d58af7cd648648c856764fc0928b3.jpeg)

#### 渲染层

wxml ==> js，因为需要动态渲染

wxss ==> js，处理rpx

渲染层，iframe，webview，容器，一个页面对应一个

> 调试微信开发者工具
>
> 微信开发者工具使用NW（类似electron）
>
> document.querySelectorAll('webview')[0].showDevTools(true, null) // 页面渲染时的渲染层
>
> 基于web component实现了一套组件，比如：wx-view
>
> 视图层基础库：WAWebview，提供事件监听处理，通信，

#### 逻辑层

js，

逻辑层，v8，jscore，webview，一个应用对应一个

> 调试工具输入document，会显示逻辑层，自己写的所有页面的js
>
> 基础库：WAService

两个不同的线程，不会相互阻塞，跨线程通讯



![小程序运行环境](Naixes阶段性学习笔记2.assets/小程序运行环境.png)

> 5个页面，1个逻辑层，5个渲染层

### 通信

### 上传编译

上线之前都编译成js，上线时发到微信服务器，用户点击应用：

准备运行环境，构建基础库（渲染层和逻辑层）

渲染层加载初始化配置的首页js，逻辑层加载应用代码

开始通信

> wxappUnpacker库：可以反编译

**渲染层基础库：**

加载基础库

> 基础库：
>
> foundation 基础模块 发布订阅 EventEmit env
>
> jsbridge（消息模块），on监听native，publish发布消息（兼容处理），invoke调用原生方法，subscribe逻辑层消息，消息订阅转发：invokeCallbackHandler，subscribeHandler
>
> exparser 组件系统，基于web component，衔接原生组件，将自定义组件的功能抛出
>
> \__VirtualDOM__，构建虚拟dom，调用组件系统进行页面渲染
>
> 
>
> 监听了generateFuncReady事件，保存generateFunc函数，判断WeixinJSBridge是否准备完毕，触发WeixinJSBridge发布消息给逻辑层，publish

加载wxmljs，wxssjs

路由改为当前组件路由，加载当前页面config合并全局config，

执行wxssjs（将style插入头部）

执行wxmljs，生成渲染器generateFunc，等待逻辑层数据到达后执行（基础库监听逻辑层）

派发事件generateFuncReady传递generateFunc

> 自定义事件，CustomEvent

**逻辑层基础库：**

> 基础库：foundation 基础模块 发布订阅 EventEmit env
>
> jsbridge（消息模块）
>
> app实例
>
> 生命周期
>
> setData，调用节流

### 事件接收

### app/page/wx

基础库提供

### setData

### 基础库

提供了以上所有东西，运行环境

可以基于虚拟dom构建视图

dom diff

> console: 
>
> help > // 查看客户端暴露出来的方法
>
> openVender() > // 打开基础库，wcc，WXML Compile，编译WXML；wcsc，WeChat Stylesheet Complier
>
> // WXML编译成js，要处理动态属性
>
> // 编译后的js是一个函数$gwx
>
> // 执行这个函数，返回一个函数（渲染器）
>
> // 继续执行（传入数据，动态构建，数据从逻辑层来），返回虚拟dom对象，会给到基础库
>
> 
>
> // WXSS编译成j
>
> // 处理适配
>
> // 处理rpx，其他都是字符串
>
> ​	// 创建style，makeup计算px替换rpx，插入
>
> 
>
> 逻辑层基础库：WAService
>
> 视图层基础库：WAWebview

## v8和Linux异步机制

### nodejs系统体系

nodejs是c/c++和js写的

nodejs不是单线程，js是单线程语言，js没有创建多线程的机制

#### 运作机制

<img src="Naixes阶段性学习笔记2.assets/截屏2021-06-17 上午10.06.38.png" alt="截屏2021-06-17 上午10.06.38" style="zoom:40%;" />

体系结构和运作机制图

根据上图，Node.js的运行机制如下：

1. 写的JavaScript脚本会交给V8引擎解析
2. V8只负责解析，解析后的代码，调用Node API，Node会交给 [Libuv库](https://link.juejin.im/?target=https%3A%2F%2Fgithub.com%2Fjoyent%2Flibuv) 处理
3. [Libuv库](https://link.juejin.im/?target=https%3A%2F%2Fgithub.com%2Fjoyent%2Flibuv) 将不同的任务分配给不同的线程，形成一个Event Loop（事件循环），以异步的方式将任务的执行结果返回给V8引擎
4. V8引擎再将结果返回给用户 

NodeBindings就像一个交换机，V8要调用更底层的东西需要穿过NodeBindings

#### **Event Loop**

有请求时，将响应事件放到事件序列（关联了回调函数），调用更底层的东西，由工作线程线程控制（文件系统，网络，进程）调用操作系统的系统调用发送http请求（操作系统的网络调用栈），发出请求到远程服务器返回的这段时间较长，程序不会阻塞，响应回来之后，再进行回调，工作线程中有一个独立的线程，这个线程会等待响应，但是不能直接跨线程回调，要把响应数据交回给事件循环统一调度，事件循环找到事件，执行回调函数

程序执行时依赖nodejs主线程，主线程包括应用程序，V8，NodeBindings，事件队列和事件循环。事件循环和工作线程之间的调用通过线程间通信，比如消息传递，共享内存等

<img src="Naixes阶段性学习笔记2.assets/截屏2021-06-17 上午10.57.56.png" alt="截屏2021-06-17 上午10.57.56" style="zoom:40%;" />

数据流向图（非阻塞事件驱动）

同步异步：运作机制

阻塞非阻塞：调用机制

#### nodejs结构

从代码层面

<img src="Naixes阶段性学习笔记2.assets/截屏2021-06-17 上午11.02.16.png" alt="截屏2021-06-17 上午11.02.16" style="zoom:50%;" />

nodejs包括：

API，nodejs+库，js写的

NodeBindings，nodejs自己的核心，c/c++写的

Add-One，插件，功能性，不参与机制，c/c++写的

其他的都是别人的

### 异步IO和事件循环

本质上是调用的操作系统

#### 用户态和内核态

Linux程序执行时的用户态（自己写的代码）和内核态（调用API）

为什么要区分？保证代码执行时的安全，防止互相干扰

用户不能直接调用内核（二进制），以库的形式调用

比如输入a，b，计算a+b，保存c，会多次切换用户态和内核态

怎么从用户空间进入内和空间？系统调用

nodejs用户和内核的切换在工作线程

#### Linux的信号机制

软中断信号(signal，又简称为信号)用来通知进程发生了异步事件。进程之间可以互相通过系统调用kill发送软中断信号。 内核也可以因为内部事件而给进程发送信号，通知进程发生了某个事件。信号只是用来通知某进程发生了什么事件，并不给该进程传递任何数据。

对信号的处理方法:

1、对于需要处理的信号，进程可以指定处理函数，由该函数来处 理。

2、忽略某个信号，对该信号不做任何处理，就象未发生过一样。其中，有两个信号不能忽略:SIGKILL及SIGSTOP;

3、对该信号的处理保留系统的默认值，这种缺省操作，对大部分的信 号的缺省操作是使得进程终止。进程通过系统调 用signal来指定进程对某个信号的处理行为。

内核处理一个进程收到的信号的时机是在一个进程从内核态返回用户态时。所以，当一个进程在内核态下运行时，软中断信 号并不立即起作用，要等到将返回用户态时才处理。进程只有处理完信号才会返回用户态，进程在用户态下不会有未处理完 的信号。

可使用 linux 命令 kill -l 查看所有信号的定义

linux：unix有前31个

<img src="Naixes阶段性学习笔记2.assets/截屏2021-06-17 下午2.31.37.png" alt="截屏2021-06-17 下午2.31.37" style="zoom:50%;" />信号是进程间通信的唯一一个异步通信机制

进程和操作系统之间通过操作系统和其他进程，通过操作系统调用操作系统的系统调用的一种异步通信机制，唯一的异步通信机制

信号是最简单的信息载体，一个状态/动作/指令

信号只是通知不发送数据

进程一和进程二的通信：

不能直接发送数据，会混乱

进程一准备好数据放到共享内存，发信号给进程二，进程二去共享内存拿数据，这就是一种异步机制，后面的异步IO模型都用到了信号，不用主动处理，底层已经封装了

在程序内部，通过回调函数通知信号（参数）

信号由内核产生

#### linux的4种IO模型

**同步和异步**，流程上

同步：调用别人时需要等待

**阻塞和非阻塞**，操作上

属于两个维度

每一个模型都有应用场景

<img src="Naixes阶段性学习笔记2.assets/截屏2021-06-17 下午2.44.47.png" alt="截屏2021-06-17 下午2.44.47" style="zoom:50%;" />

##### 同步阻塞IO

同步阻塞I/O模型是最常见的模型之一

用户空间的应用程序在执行系统调用 之后会被阻塞，直到系统调用完成 (数据传输完成或者出现错误)。此 时应用程序只是处于简单的等待响应状态不会消耗CPU

站在CPU的角度他是高效的。

<img src="Naixes阶段性学习笔记2.assets/截屏2021-06-18 上午9.46.20.png" alt="截屏2021-06-18 上午9.46.20" style="zoom:50%;" />

##### 同步非阻塞

同步阻塞I/O的一种变体是效率较 低的同步非阻塞I/O。

非阻塞意味着如果I/O操作不能立即完成，则需要应用程序多次调用直到任务完成。

这可能非常低效，因为大多数时候应用程序必须忙等待或者尝试做其他事情直到数据可用。

<img src="Naixes阶段性学习笔记2.assets/截屏2021-06-18 上午9.47.29.png" alt="截屏2021-06-18 上午9.47.29" style="zoom:50%;" />

比较低效的调用方式

调用时进入内核态，内核继续往下安排任务并且返回状态，切换到用户态

二次调用询问，还没完成，返回状态

三次调用，完成，返回结果

被分割了很多时间间隙

很少用

##### 异步阻塞

设备以非阻塞方式打开，然后应用程序阻塞 在select系统调用中，用它来监听可用的I/ O操作。

select系统调用最大的好处是可以监听多个 描述符，而且可以指定每个描述符要监听的 事件:可读事件、可写事件和发生错误事件

select系统调用的主要问题是效率不高。虽 然它是一个非常方便的异步通知模型，但不 建议将其用于高性能I/O中。

高性能场景一般使用epoll系统调用

<img src="Naixes阶段性学习笔记2.assets/截屏2021-06-18 上午9.48.09.png" alt="截屏2021-06-18 上午9.48.09" style="zoom:50%;" />

调用阻塞api

select，操作系统提供，统一进行等待

linux将硬件操作当作文件操作，会给一个文件描述符，select帮我们维护文件描述符，同步阻塞式程序维护

select属于异步模型，内部反复询问，效率不高，并发上限是固定的，1000多个，定义在内核中不好改

##### select

select模型的关键是使用一种有序的方式，对多个套接字进行统一管 理与调度

select模型的缺点:

- 单个进程能够监视的文件描述符的数量存在最大限制，通常是 1024，当然可以更改数量，但由于select采用轮询的方式扫描 文件描述符，文件描述符数量越多，性能越差;(在linux内核 头文件中，有这样的定义:#define __FD_SETSIZE 1024)

- 内核/用户空间内存拷贝问题，select需要复制大量的句柄数据 结构，产生巨大的开销;

- select返回的是含有整个句柄的数组，应用程序需要遍历整个 数组才能发现哪些句柄发生了事件;

- select的触发方式是水平触发，应用程序如果没有完成对一个 已经就绪的文件描述符进行IO操作，那么之后每次select调用 还是会将这些文件描述符通知进程。

<img src="Naixes阶段性学习笔记2.assets/截屏2021-06-18 上午9.52.29.png" alt="截屏2021-06-18 上午9.52.29" style="zoom:50%;" />

##### 异步非阻塞

异步非阻塞I/O模型是可以并行处理I/O的 模型

异步非阻塞I/O模型的读请求会立即返 回，表明读操作成功启动。然后应用程 序就可以在读操作完成之前做其他的事 情。当读操作完成时，内核可以通过信 号或者基于线程的回调函数来通知应用 程序读取数据。

在单个进程可以并行执行多个I/O请求是 因为CPU的处理速度要远大于I/O的处理 速度。 当一个或多个I/O请求在等待处理 时，CPU可以处理其他任务或者处理其他 已完成的I/O请求。

<img src="Naixes阶段性学习笔记2.assets/截屏2021-06-18 上午9.48.51.png" alt="截屏2021-06-18 上午9.48.51" style="zoom:50%;" />

进行多任务

用户空间分了三段，调用非阻塞api时，主线程将工作交给其他过程在另外的线程/进程里，帮我们等待，回来之后交给主过程处理

效率高，资源消耗多

#### 事件驱动

linux内部没有提供，第三方库libuv

nginx复合式，用到了事件循环和异步非阻塞的多工作进程，一个进程里面一个循环

#### epoll模型

epoll模型的优点: 支持一个进程打开大数目的socket描述符 IO效率不随FD数目增加而线性下降 使用mmap加速内核与用户空间的消息传递

高并发解决方案

用到了多进程，没用到时间循环，每个进程都有一个连接池，不够时新开进程，还用到了分层

关键在分层上，每一层负责不同工作，比如负责连接，收到数据后向下一层传递，用到了mmap（高效率内存复制模式）

连接层

数据存储层

数据处理层

epoll 的两种工作模式:

LT(level triggered，水平触发模式)是缺省的工作方式，并且同时支持 block 和 non-block socket。在这种做法中，内核告诉你一个文件描述符是否就绪了，然后你可以对这个就绪的fd 进行IO操作。如果你不作任何操作，内核还是会继续通知你的，所以，这种模式编程出错误可 能性要小一点。比如内核通知你其中一个fd可以读数据了，你赶紧去读。你还是懒懒散散，不 去读这个数据，下一次循环的时候内核发现你还没读刚才的数据，就又通知你赶紧把刚才的 数据读了。这种机制可以比较好的保证每个数据用户都处理掉了。

ET(edge-triggered，边缘触发模式)是高速工作方式，只支持no-block socket。在这种模式 下，当描述符从未就绪变为就绪时，内核通过epoll告诉你。然后它会假设你知道文件描述符 已经就绪，并且不会再为那个文件描述符发送更多的就绪通知，等到下次有新的数据进来的 时候才会再次出发就绪事件。简而言之，就是内核通知过的事情不会再说第二遍，数据错过 没读，你自己负责。这种机制确实速度提高了，但是风险相伴而行。

#### iocp模型

windows的高效IO模型

层次不清

1:创建一个完成端口。 2:创建一个线程A。

3:A线程循环调用GetQueuedCompletionStatus()函数来得到IO操作结果，这个 函数是个阻塞函数。

4:主线程循环里调用accept等待客户端连接上来。

5:主线程里accept返回新连接建立以后，把这个新的套接字句柄用 CreateIoCompletionPort关联到完成端口，然后发出一个异步的 WSASend或者 WSARecv调用，因为是异步函数，WSASend/WSARecv会马上返回，实际的发 送或者接收数据的操作由WINDOWS系统去做。

6:主线程继续下一次循环，阻塞在accept这里等待客户端连接。 7:WINDOWS系统完成WSASend或者WSArecv的操作，把结果发到完成端口。

8:A线程里的GetQueuedCompletionStatus()马上返回，并从完成端口取得刚完 成的

9:在A线程里对这些数据进行处理(如果处理过程很耗时，需要新开线程处 理)，然后接着发

#### libuv

很多底层机制的封装，两大块，异步驱动模型和io操作，还有进程管理等

官网：http://docs.libuv.org/en/v1.x/

代码：

两大平台，unix和win，为了统一接口

libuv 是用 C 写的，因此，它具有很高的可移植性，非常适用嵌 入到像 JavaScript 和 Python 这样的高级语言中。

libuv使用异步，事件驱动的编程方式，核心是提供 i/o 的事件循 环和异步回调。

libuv的API包含有时间，非阻塞的网络，异步文件操作，子进程 等等。

当程序在等待i/o完成的时候，我们希望cpu不要被这个等待中的 程序阻塞，libuv提供的编程方式使我们开发异步程序变得简单。

### V8源码

#### 渲染引擎

渲染引擎 - 能够能够将HTML/ CSS/JavaScript文本及相应的资 源文件转换成图像结果.

渲染引擎的种类：

Tridend(IE)

Gecko(FF)

WebKit(Safari,Chrome,Andrio d浏览器)等，处于独立的进程中，现都浏览器都是多进程

#### webkit体系结构

<img src="Naixes阶段性学习笔记2.assets/截屏2021-06-18 上午10.18.52.png" alt="截屏2021-06-18 上午10.18.52" style="zoom:50%;" />

#### JavaScript引擎与渲染引擎

渲染引擎（css解析器也能处理部分逻辑）使用JS引擎的接口来处理逻辑代码并获取结果

JS引擎通过桥接接口访问渲染引擎中的DOM及CSSOM

> js引擎处理渲染引擎逻辑时如何调取dom？
>
> 不是直接调用渲染引擎接口，会造成调用环路产生死锁
>
> 此时用到桥接接口，相当于发一个消息：
>
> js调用时发一个数据包给消息传递的框架然后发到webkit进行处理避免死锁，数据包包括事件名称（指令）和数据
>
> 渲染引擎提供桥接API

<img src="Naixes阶段性学习笔记2.assets/截屏2021-06-18 上午10.23.01.png" alt="截屏2021-06-18 上午10.23.01" style="zoom:40%;" />

html解析和js解析在不同线程，不能同时工作

#### JavaScript引擎工作流程

<img src="Naixes阶段性学习笔记2.assets/截屏2021-06-18 上午10.38.59.png" alt="截屏2021-06-18 上午10.38.59" style="zoom:40%;" />

V8源码，谷歌的开发者网站下载

src：编译器，解释源代码变成抽象语法树，再转成字节码（都是属于预处理，把文本形式的源码转换成更加高效的形式），解析器，处理代码执行代码，同时还需要内存管理（垃圾回收和内存分析），现在V8多了一个JIT用来提高效率，just in time，即时编译，转换成二进制代码，不依赖解析器，解析器会将频繁执行的代码会交给JIT（JIT处理全部代码还是挺久的），JIT处理成本地代码（直接跑在cpu不通过解释器，效率高）交然后给解析器一个调用方式

JIT：最早从c#和java来的，python和ruby也引入了

字节码：来源于js引擎的虚拟机化，对比java的jvm，跨平台

抽象语法树，有一条主干

#### V8 与 JavaScript Core

JavaScript Core 引擎是WebKit中默认的JavaScript引擎，也是苹果开源的一个项 目，应用较为广泛。最初，性能不是很好，从2008年开始了一系列的优化，重新实 现了编译器和字节码解释器，使得引擎的性能有较大的提升。随后内嵌缓存、基于正 则表达式的JIT、简单的JIT及字节码解释器等技术引入进来，JavaScriptCore引擎也 在不断的迭代和发展。

JavaScriptCore与V8有一些不同之处，其中最大的不同就是新增了字节码的中间表 示，并加入了多层JIT编译器(如:简单JIT编译器、DFG JIT编译器、LLVM等)优化 性能，不停的对本地代码进行优化。

v8倾向于减少资源占用

jscore倾向于增加处理层次，增加执行效率

文章：js引擎是怎样将var转换为JIT的

> 确定频繁执行的代码：两套分析模式，快粗略，慢精细，先用快的分析，保存到内存区域，统计使用频率，然后交给慢的然后转换为JIT，做一个映射替换代码

#### 源码分析

文档:https://v8.dev/docs 

源码:https://cs.chromium.org/chromium/src/v8/ 

通过源码可以学到的东西：

增强对JavaScript的理解

前端算法

内存管理与CG算法

编译原理、操作系统等知识

面试装逼的高级方式

V8 引擎源码都看什么

工作过程

数据表示

类型

内存管理 绑定机制与扩展机制 字节码与JIT

##### libuv

c语言

入口在头文件（.h）include，uv.h

先看头文件，公共的函数声明，让其他文件引入的

事件循环的实现：

queue.h

使用宏编写，可以使生成的二进制代码更加紧凑，防止过多的函数调用栈，不能断点调试

strcpy.h

复制字符串

loop.h

##### V8

heap

内存管理，基于链表实现的堆

##### node

c++

lib，js层面上实现的api

src，运行机制，核心node bindings

sample，例子，嵌入v8

shell

## WASM

webAssembly

参考：webAssembly正式成为web的第四种语言

严格来说不是一种语言，是一套标准，机制

**依赖低层基础架构的高性能应用程序**

**核心是一种虚拟指令集体系结构**（类似于虚拟机，不是直接给cpu的，跨平台），可在web上运行高性能应用程序，随着运算量的增大，运行时间可以减少一半，比js快一倍，并可在其他许多环境中使用。WebAssembly 的实现有多种，包括浏览器和独立系统。WebAssembly 可用于视频和音频编解码器，图形和 3D，多媒体和游戏，密码计算或便携式语言实现等领域。

**WebAssembly 增强 Web 性能**

WebAssembly 是虚拟机和执行环境，可以让加载的页面作为本机编译代码运行，从而提高了 Web 性能和功耗。换句话说，WebAssembly 可以实现接近本机的性能以及优化的加载时间，并且最重要的是可以为现有的代码库提供编译目标。

尽管本机类型的数量很少，但相对于 JavaScript 而言，性能的提高大部分归功于其对一致类型的使用。WebAssembly 对编译语言进行了几十倍的优化，针对其字节码的紧凑性和流传输进行了优化。在下载其余代码时，网页就可以开始执行。网络与 API 访问通过随附的 JavaScript 库进行。它的安全模型与 JavaScript 相同。

现在还没有很成熟，但也好用

**未来版本已经在开发中**

其中包括：

- 线程

线程提供了共享内存多线程和原子内存访问的诸多好处。

- **Fixed-width** SIMD

并行执行循环中的向量操作（物理，人工智能）。

- 引用类型

允许 WebAssembly 代码直接引用宿主对象。

- 尾调用

能够使用额外的栈空间去调用函数。

- ECMAScript 模块集成

通过将 WebAssembly 可执行文件加载为 ES6 模块来与 JavaScript 进行交互。

### WASM 的特点

高效

WebAssembly 有一套完整的语义，实际上 wasm 是体积小且加载快的**二进制格式**， 其目标就是充分发挥硬件能力以达到原生执行效率

> 用c写，编译完成后cpu可以直接执行，但是浏览器要跑的时候，还要进行转换，转换成虚拟容器可以执行的二进制代码

安全

WebAssembly 运行在一个**沙箱化**的执行环境中（现代浏览器也是一种沙箱，不会影响到操作系统），甚至可以在现有的 JavaScript 虚拟机中实现。在web环境中， WebAssembly将会严格遵守**同源策略以及浏览器安全策略**。

开放

WebAssembly 设计了一个非常规整的文本格式用来、调试、测试、实验、优化、学习、教学或者编写程序。可以 以这种文本格式在web页面上查看wasm模块的源码。可以反编译

标准

WebAssembly 在 web 中被设计成**无版本、特性可测试、向后兼容**的。WebAssembly 可以被 JavaScript 调用，进入 JavaScript 上下文，也可以像 Web API 一样调用浏览器的功能。当然，WebAssembly 不仅可以运行在浏览器 上，也可以运行在非web环境下。

c go rust ts等语言都可以写，都有对应的编译工具

### 执行过程对比

<img src="Naixes阶段性学习笔记2.assets/截屏2021-06-19 上午11.12.04.png" alt="截屏2021-06-19 上午11.12.04" style="zoom:50%;" />

js性能较低，预处理阶段比较长（前三个阶段，执行之前都是预处理），GC也会影响一些

wasm：解码（load二进制文件，js是文本，处理二进制更快），编译+优化（解码出来的内容进行转化，优化），执行，无GC（wasm和js内存是分开的，wasm有独立内存区域，没有动态内存管理，手动管理，将时间平摊到运行时期）

WebAssembly版本和原生JavaScript版本的递归无优化的Fibonacci函数，下图是这两个函数在值是45、48、50的时候的性能对比。

<img src="Naixes阶段性学习笔记2.assets/截屏2021-06-19 上午11.23.06.png" alt="截屏2021-06-19 上午11.23.06" style="zoom:50%;" />

### WASM 的工具

AssemblyScript:支持直接将 TypeScript 编译成 WebAssembly。这对于前端来 说，入门的门槛很低的。

**Emscripten**:可以说是 WebAssembly 的灵魂工具。将其他的高级语言，编译成 WebAssembly。

> Emscripten 相对复杂，需要配置
>
> https://emscripten.org/docs/getting_started/downloads.html
>
> 还需要其他语言的编译器，会调用到，c用到gcc，mac的xcode自带
>
> 参考文档：clone 克隆 emsdk，更新版本，激活，激活环境变量（一次性，关闭会话后失效，每次都要激活）
>
> 在线版
>
> https://wasdk.github.io/WasmFiddle/

WABT:将 WebAssembly在字节码和文本格式相互转换的一个工具，方便开发者去理解这个 wasm 到底是在做什么事。反编译，有点像汇编指令

WebAssembly 中文网：只供参考

http://webassembly.org.cn

w3c官网

### 运作机制

无论用什么写的最终都要用js调用的

#### jsAPI

所有的，已经固定：

方法

1.WebAssembly.validate() // 验证二进制字节码是否合法

2.WebAssembly.compile() // 把二进制代码编译成虚拟指令

3.WebAssembly.instantiate() // 代码实例化，变成一个进程

类

1.WebAssembly.Module // 导入

2.WebAssembly.Instance // 函数导出

3.WebAssembly.Memory // 创建内存，管理内存。wasm需要初始内存，没执行时将代码放进去，执行时需要的内存变大需要申请内存，一次申请一个单元（页面，一个64k）

4.WebAssembly.Table // 专门提供给js的包装，是一个映射表，连接js和wasm。要进行数据交换时，简单变量直接传参，复杂变量需要Memory参与

5.WebAssembly.CompileError // 编译期错误

6.WebAssembly.LinkError // 关联错误，错误位置

7.WebAssembly.RuntimeError // 运行时错误

123导入-12使用-34运行，数据交换-567异常

引入模块

```js
const importObject = { 
  func: {
		log: (num)=> document.write(num) 
  }
}
fetch('test.wasm')
.then(response=>response.arrayBuffer()) 
.then(types=>WebAssembly.instantiate(bytes, importObject)) 
.then(({instance}) => window.test = instance.exports.test)
```

webpack提供的wasm-loader可以使用import导入不需要123

使用 文本格式 编写 WebAssembly

文本格式 基于S-表达式

可以用于调试、学习、手写WebAssembly

文章参考：用WebAssembly在浏览器对视频进行转码 使用FFmpeg

> 视频的编码格式，怎么压缩，H.264（视频），ACC（音频）
>
> 视频的封装格式，网络传输，mp4

### 实践

xx.c

emac xx.c -o xx.js --xx.js/xx.wasm，js是给nodejs调的，js调wasm

生成的js代码很多，做了很多容错

emac xx.c -o xx.html--xx.html/xx.js/xx.wasm，js，wasm和node生成的是一样的

浏览器执行不能是本地代码，需要服务器

html中的脚本是给js准备环境的，页面上显示的类似终端的东西

编译库和程序不一样

## webpack优化

开发时优化：版本升级

构建时：prepack

从两个层面：

编译速度，loader，plugin，babel-loader换成swc-loader

文件大小

### 版本升级

4

> speed-measure-webpack-plugin 打包速度分析，包裹一下配置
>
> // 4中的很多优化插件5用不了
>
> thread-loader慎用，消耗系统资源，js线程通信，不一定会更快，大项目可以试
>
> cache：
>
> cache-loader，webpack5已经自己实现了一套cache的体系
>
> hard-source-webpack-plugin，全局缓存
>
> 5里中设置一下cache就可以
>
> terser-webpack-plugin // 并行压缩，开启压缩缓存，5可用，不如esbuild

5，编译出来比4小很多，少了很多polyfill，使用箭头函数（babel不能编译，webpack的template），有的浏览器会挂掉

内置很多loader，静态资源指定一下type就可以

#### Prepack

深层次执行代码，自己有一个代码解释器

对静态代码进行执行

webpack5模拟了一部分

> webpack为什么慢？
>
> 他是js运行到V8，要经过JIT，要转化
>
> esbuild，go写的，直接编译成bin（二进制，字节码），vite就是基于esbuild，esbuild+koa
>
> swc，rust写的，直接编译成bin，对标babel和esbuild

### 5优化

cache设置

terser-webpack-plugin // 并行压缩，开启压缩缓存，5可用，不如esbuild

esbuild-loader // 有自己的一套，可以只使用压缩工具，swc-loader对标babel-loader速度对标esbuild，迁移成本小；也可以使用esbuild+prepack替代webpack

#### 工程上的优化

构建配置设计成一个库，比如:hjs-webpack、Neutrino、webpack-blocks

抽成一个工具进行管理，比如:create-react-app, kyt, nwb

更多的快速构建工具:lerna 、brunch、 rome 、snowpack (过往Browserify、 Rollup.js、Gulp、Parcel、Microbundle)

更友好的提示错误 

friendly-errors-webpack-plugin 

webpack-build-notifier 

set-iterm2- badge && node-bash-title 标题和窗口内容修改

使用动态 polyfill

它会根据你的浏览器 UA 头，判断你是否支持某些特性，从而返回给你一个合适的polyfill。

### dist分析

## 小程序基础架构

双线程，逻辑线程（jscore或v8，执行js逻辑接收数据处理数据）和视图线程（web view或iframe，接收事件渲染页面），基于基础库，视图层基础库，组件系统，事件系统，虚拟dom，渲染；逻辑层基础库，jsbridge，page实例，app实例，setData，微信sdk

工程化，复用 --> 框架，脚手架

编译时

js运行时

1. page实例 data event 生命周期 配置
2. app实例 data event 生命周期 配置

### 多端

完全编译时框架，上线之前，自定义语法，vue - template，react - jsx都会编译成js，taro 类jsx，编译成wxml，wxss，js

分析打包出的代码，taro的createComponent，初始化，更新

运行时：

基于vue，生命周期，事件代理，数据同步，维护两个运行时

template作用1构建wxml，2构建render

重写patch，构建虚拟dom和setData

页面挂载时构建page实例

框架，mpvue，uniapp

基于react，没有模版，自定义模版，通过给的动态数据结构和一套基础模版，嵌套解析

其他和基于vue一样

remax

## 微前端

来源于微服务，微服务是独立服务，微前端是独立模块

<img src="Naixes阶段性学习笔记2.assets/截屏2021-06-25 上午9.55.08.png" alt="截屏2021-06-25 上午9.55.08" style="zoom:50%;" />

eventBus，跨技术栈通信，xstate

微前端(Micro-Frontend)，是将微服务(Micro-Services)理念应用于前端技术后的 相关实践，使得一个前端项目能够经由多个团队独立开发以及独立部署。

### 特性

技术无关，各个开发团队都可以自行选择技术栈，不受同一项目中其它团队影响; 

代码独立，各个交付产物都可以被独立使用，避免和其它交付产物耦合;

样式隔离，各个交付产物中的样式不会污染到其它组件; 

原生支持，各个交付产物都可以自由使用浏览器原生 API，而非要求使用封装后的 API;

### 微前端核心解决问题和步骤

传统开发模式，巨石应用(Frontend Monolith)

⻚面加载 动态的分发路由

服务发现 客户端服务发现、服务端服务发现、分自注册和第三方注册。自注册不言而喻。第三方注册就是 一个保活机制，定期检查服务状态。

根据服务发现结果加载资源 

iframe是一种微前端

改造成本低，可以快速上线

不可控制
 iframe嵌入的显示区大小不容易控制，存在一定局限性。

bfcache! URL的记录完全无效，⻚面刷新不能够被记忆，刷新会 返回首⻚，iframe功能之间跳转也无效

兼容性坑 iframe的样式显示、兼容性等都具有局限性

性能开销 iframe 阻塞 onload、占用连接池、多层嵌套⻚ 面崩溃。。

### 必须要解决的问题

一个前端需要对应多个后端

提供一套应用注册机制，完成应用的无缝整合

在应用之前团队开发者要制定好使 用CSR或SSR的技术方案

构建时集成应用和应用独立发布部署

微前端具体要解决好的 10 个问题

### 微应用的注册、异步加载和生命周期管理;

微应用之间、主从之间的消息机制;

微应用之间的安全隔离措施;

微应用的框架无关、版本无关;

微应用之间、主从之间的公共依赖的库、业务逻辑(utils)以及版本怎么管理;

微应用独立调试、和主应用联调的方式，快速定位报错(发射问题);

微应用的发布流程;

微应用打包优化问题;

微应用专有云场景的出包方案;

渐进式升级:用微应用方案平滑重构老项目。

<img src="Naixes阶段性学习笔记2.assets/截屏2021-06-25 上午10.21.40.png" alt="截屏2021-06-25 上午10.21.40" style="zoom:50%;" />

### 微前端交付产物

发布静态资源+后台路由和服务

发布组件启动时机全由父级决定

发布局部应用配置过程由自身决定

前端静态+后端

每个项目独立通过代码版本管理库独立分组、统一技术方案，合成整体技术架构。 https://micro-frontends.org/

常见的部署方式

大仓库拆分独立的模块，统一构建

大仓库通过 monorepo methodology 做成npm包，集成主项目

大仓库拆分子仓库，构建应用出独立的服务/应用

大仓库拆分多仓库，构建后集成到主应用

### mpa解决方案-yog2

2012年的技术栈

实战

新建项目yog2 init project，mpa，主站，基座

app放路由，子项目

新建子项目yog2 init app，可以直接放进主站的app，可以独立运行

fis-conf维护了namespace

有两份代码

release --dest debug，后代码自动发送到主站

再新建一个子项目

可以跨项目使用组件，修改路径即可

可以新建一个公共项目common

bigpipe让后台以chunk形式输出

lazyload管理静态资源，并发，缓存

mod模块化

page管理容器，spa，融合了单页和多页

listenerjs通讯（或者xstate，都是全局变量）

### spa解决方案

基座，systemjs解决模块，listenerjs通讯

子项目

远程组件（在别的地方使用该组件），方法一快速原型开发（vue-cli），方法二webpack的entry，方法三rollup

方法一：

vue serve 单页.vue 报错。。。

方法二：

entry，编译，主站复制文件component直接引入，两份代码，不能显示，js没有执行

使用systemjs，安装webpack-system-register，编译时包裹一下，包裹成systemjs可以使用的模块，在基座中使用systemjs引入

方法三：

rollup

安装rollup，rollup-plugin-vue@next，rollup-plugin-css-only，编译出来比较纯净

缺点：还是单页

维护映射表

#### 乾坤

核心是自己实现了一套沙盒机制

子项目修改较复杂，侵入性较强

破坏html结构规范

### 基于web components

custom elements

HTML imports，废弃

HTML template，存放暂时不需要渲染的HTML

shadow dom

### 基于webpack5

#### 联邦模块

csr

使用lerna管理项目

lerna init

参考demo代码

#### 原理

<img src="Naixes阶段性学习笔记2.assets/截屏2021-06-25 下午9.54.29.png" alt="截屏2021-06-25 下午9.54.29" style="zoom:50%;" />

```js
import('aa.js') // chunk，异步，可以then
import 'aa.js' // 直接引入到当前文件
```

4，index.js - a.js - b.js --> main.js - 0.js - 1.js     index.js - b.js --> main.js - 0.js

5，index.js - a.js - b.js --> main.js - src_a_js.js - src_b_js.js，上线环境main.js - md5.js

模块固定：trunkIds和moduleIds配置，4中需要在注释中写webpackChunkName

4

```js
异步模块
window["webpackJsonp"]中push数组
[['filename'], {'/.src/data.js': function(){}}]
不能共享出去，模块名是0，同名会使顺序错乱，依赖关系紊乱

// 总结
// 异步a.js
// e，load文件，创建script，src为这个文件
// 返回状态，成功后放入modules
```

5

```js
异步模块
self['webpackChunkProjectName']，为联邦模块做的一些准备
main：
// 找到对应模块，返回promise
.e('./src/data.js')
// 重新二次bind
.then(__webpack_require__.bind(__webpack_require__, './src/data.js'))
.then((_) => {...})
// 模块缓存
// 加载模块
// polyfill
// __webpack_require__.e加载异步chunk专用
// __webpack_require__.f遍历所有异步模块，最后执行
// 加载异步模块
// 重写push
// 判断超时和出错，4判断状态

// 总结和4类似
// timeout不太一样，之前是回调，现在bind一个函数
```



### 沙箱环境

