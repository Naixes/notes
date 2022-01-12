## V8

根据机器cpu架构编译，最终会编译成机器码，前几年会将js全部直接编译为机器码，现在会先编译成字节码

libuv，事件循环原理while（蹦床函数优化递归，async/await，dom diff，koa中间件都用到while）。独立线程辅助V8

在node.js启动时，创建了一个类似while(true)的循环体，每次执行 一次循环体称为一次**tick**，类似于饭店的厨师。每个tick的过程就是查看是否有事件等待处理，如果有，则取出事件极及其相关的回调函数并执行，然后执行下一次tick。它的执行逻辑是，先询问**事件观察者**当前是否有任务需要执行?观察者回答“有”，于是取出A执 行，A是否有回调函数?如果有(如果没有则继续询问当前是否有任务需要执行)，则取出回调函数并执行(注意:**回调函数的执行基本都是异步的**，可能不止一个回调)，执行完回调后通过某种方式**通知调用者**（事件循环是一个典型的生产消费模型），我执行完了，并把执行结果给你，主函数不需要不断询问回调函数执行结果，回调函数会以通知的方式告知调用者我执行 完了，而这个过程主线程并不需要等待回调函数执行完成，它会继续向前执行，直到观察者回答没有了，线程结束。

事件循环是一个典型的生产者、消费者模型。异步IO、网络请求等 则是事件的生产者，源源不断为Node提供不同类型事件，这些事 件被传到观察者哪里，事件则从观察者哪里取出事件并处理。

### 观察者

负责将事件分类

idle观察者，process.nextTick()，效率最高，消费资源小， 但会阻塞CPU的后续调用

IO观察者，类似setTimeout()，精确度不高，可能有延迟执行 的情况发生，且因为动用了红黑树，所以消耗资源大，node中尽量不使用

check观察者，setImmediate()，消耗的资源小，也不会造成阻塞，但效率也是最低

idle观察者>Promise.then>io观察者>check观察者

macro-task: script (整体代码)，setTimeout, setInterval, setImmediate, I/O, UI rendering. micro-task: process.nextTick, Promise(原生)，Object.observe，MutationObserver

事件循环什么时候开始？

在所有同步操作之前

### 事件循环

7个阶段

1. 【update_time】为了获取一下系统时间，以保证之后的timer有个计时的标。避免过多的系统调用影响性能。 

2. 【run_timers】要检查是否有到期的timer，也就是setTimeout和setInterval这种类型的timer

3. 【I/O callbacks(epool、kqueue、IOCP)】I/O异步事件的回调，比如网络I/O，比如文件读取I/O。当这些I/O动作都结束的时候调用(比如TCP socket ECONNREFUSED在尝 试connect时receives，则某些* nix系统希望等待报告错误)

   > Easy-monitor，node监控平台
   >
   > GC后内存不变说明发生了内存泄漏
   >
   > CPU
   >
   > Heap
   >
   > 诊断报告中可以看到libuv的七个阶段

4. 【idle, prepare】这个阶段内部做一些动作，如果节点处理avtive状态，每次事件循环都会被执行。nexttick

5. 【I/O poll阶段】 调用各平台提供的io多路复用接口，执行I/O回调、处理轮询队列中的事件。如果poll队列不为空，则事件循环将遍历其同步执行它们的callback队列，直到队 列为空。如果poll队列为空，有setImmediate()立即进入,没有就等着callback被添加到队 列中，然后立即执行。当然有timer的话如果超时会回到timer

6. 【check】执行setImmediate操作
7. 【close callbacks】闭I/O的动作，比如文件描述符的关闭，链接断开，等等等

> timer和setImmediate在IO回调中，setImmediate优先，在外面不一定，受到进程性能的限制

与浏览器区别

浏览器的eventloop是浏览器自己实现的，node是基于libuv，js在浏览器中的单线程是ui渲染进程，如果被js阻塞会造成卡顿，react-fiber就是利用时间碎片解决了主线任务的穿插，浏览器中的eventloop由messagePump和messageLoop组成，浏览器为了防止多线程之间传递数据，将每一个任务封装成task，messageLoop是运行的task，messagePump是用来接收和控制messageLoop中传递的task

node中libuv实现了eventloop，libuv封装了系统中windows的LCP和linux异步？？query，libuv辅助js单线程，libuv执行时核心分为7个阶段，负责通信的是三大观察者，维护微任务和宏任务



为了实现多线程，Chrome思路是简单且尽可能的少用锁，相比平时的消息循环(如:Windows的消息 循环，Linux中的epoll模型)，它唯一增加的功能就是可以运行自定义的任务:Task。如果在一个线程 里面需要访问另一个线程的数据，则把接下来要运行的函数和参数包装成一个Task，并将其传递给另外 一个线程，由另外一个线程来执行这个Task。

Chrome将其线程分为了三类：普通线程，UI线程和IO线程。他们之间的区别是:

普通线程:只能执行Task，没有其他的功能。

UI线程:所有的窗口都需要跑在UI线程上，它除了能执行Task以外，还能执行和界面相关的消息循环。

IO线程:和本地文件读写，或者网络收发相关的操作都运行在这个线程上，它除了能执行Task以外，还 能执行和IO操作相关的事件回调。

由于这三类线程中Task的执行部分基本是一样的，而其他的功能却完成不同，为了实现这不同的三类线 程，Chrome将消息循环分成了两个部分:**MessageLoop**和**MessagePump**。chrome-thread-and- messageloop(如下图)

MessagePump被提取出来负责执行Task的时机和处理线程本身的消息，如:UI线程的Windows消息， IO线程的IO事件。

MessageLoop则仅仅是做Task的管理，它实现了MessagePump的Delegate的接口，这样MessagePump 就可以告诉MessageLoop何时应该处理Task了。

MessagePump通知，MessageLoop循环，完成对外的代理对接

另外实现上虽然Chrome为这三种线程实现了三套MessageLoop，但是它们之间的区别，也仅限于暴露 出现的MessagePump的接口不同而已。

<img src="Naixes阶段性学习笔记2.assets/截屏2021-08-06 上午10.44.10.png" alt="截屏2021-08-06 上午10.44.10" style="zoom:50%;" />

<img src="Naixes阶段性学习笔记2.assets/截屏2021-08-06 上午10.44.47.png" alt="截屏2021-08-06 上午10.44.47" style="zoom:50%;" />

### 性能优化

**JIT**，Just-In-Time，即时编译，编译的结果直接是机器语言，而不是字节码。大大提高了JS的执行效率。

**GC**，Garbage collection，V8的垃圾回收借鉴了Java VM的精确垃圾回收管理，而其他语言用的还是保守的垃圾管理。独立的

**内联缓存**，Inline Cache，this.a没有内存缓存的时候，每次取a都会对哈希表进行一次寻址。加入了之后V8能⻢上知道这个属性的偏移量。

**隐藏类**，Hidden Class，隐藏类和内联缓存这两把 技术合起来是V8性能高效一个非常重要的原因。

> --max_old_space_size + 数字 设置老生代内存单位 MB 
>
> --max_new_space_size + 数字 设置新生代内存单位 KB

#### 类型检查、优化与去优化

二元运算符可以收集函数的 type feedback 信息。

1. 使用 type feedback 做动态检查

2. 一般而言，在编译阶段提前检查 

3. 检查之后，使用该类型作为动态类型 

4. 如果检查失败，去优化(deoptimize) （改变类型，突出了ts的优势，ts已经做了此时就不会发生去优化）

5. 去优化之后，可能会使用解释器运行中间码（去优化非常消耗内存（已经优化的机器码会被浪费），尽量避免）

#### 隐藏类与内联缓存

同一个class，new的实例在V8是同一个，所有的对象形成一个栈

破坏结构会变成不同的隐藏类

<img src="Naixes阶段性学习笔记2.assets/截屏2021-07-15 上午11.58.23.png" alt="截屏2021-07-15 上午11.58.23" style="zoom:50%;" />

back pointer可以往回找，最好不要破坏back pointer

有三种不同的命名属性类型:对象内，快速和慢速/词典。 

1.对象内属性直接存储在对象本身上，并提供最快的访问权限。 

2.快速属性位于属性存储中，所有元信息都存储在HiddenClass的描述符数组中。 

3.慢速属性存在于独立的属性字典中，不再通过HiddenClass共享元信息。 慢速属性允许高效地删除和添加属性，但访问速度比其他两种类型慢。

V8利用了另一种优化动态类型语言的技术，称为**内联缓存**。 内联缓存依赖于这样一种观察，即对同一方法的重复调用往往发生在同一类型的对 象上。 那么隐藏类和内联缓存的概念如何相关呢?无论何时在特定对象上调用方法时，
 V8 引擎都必须执行对该对象的隐藏类的查找，以确定访问特定属性的偏移量。在同一个隐藏类的两次成功的调用之后，V8 省略了隐藏类的查找，并简单地将该属 性的偏移量添加到对象指针本身。如果你创建两个相同类型和不同隐藏类的对象， V8将无法使用内联缓存，因为即使这两个对象属于同一类型，它们对应的隐藏类 为其属性分配不同的偏移量。

### DSL NLP AST

1. 领域特定语言指的是专注于某个应用程序领域的计算机语言。  

   外部DSL:宿主应用的代码采用文本解析技术对外部DSL编写 的脚本进行解析。如:正则表达式、SQL、配置文件、koa- swig 模板引擎如 mustache 以及 React、Vue 支持的 JSX 语 法都属于外部 DSL等

   内部DSL:通用语言的特定语法，用内部DSL写成的脚本是一段合法的程序。比如PHP C# Java、 jQuery 就可以认为是针对 DOM 操作的一种内部DSL。

   语法噪音:(2).weeks().ago() -> (2).weeks.ago ，(Lambda 表达式本质上是一种直观易读且延迟执行的逻辑表达能力，从而避免额外的解析工作，不过它强依托宿主的语言特性支持 (匿名函数 + 箭头表示)，并且也会引入一定的语法噪音)

2. 抽象语法树(abstract syntax tree或者缩写为AST)，或者 语法树(syntax tree)，是DSL的抽象语法结构的树状表现形 式。

3. NLP自然语言处理用于对代码分词

DSL执行要经过两步：词法分析，语法分析

<img src="Naixes阶段性学习笔记2.assets/截屏2021-08-06 上午11.06.58.png" alt="截屏2021-08-06 上午11.06.58" style="zoom:50%;" />

<img src="Naixes阶段性学习笔记2.assets/截屏2021-08-06 上午11.09.52.png" alt="截屏2021-08-06 上午11.09.52" style="zoom:50%;" />

1.词法分析

2.确定语法语义 

3.扫面分词结果 

4.根据语法定义 转换成AST

词法分析是由词法分析器完成的,词法分析器会扫描(scanning)代码,提 取词法单元token。

V8有编译器和解释器

相关概念：

闭包

一等公民

惰性解析

在 C/C++ 中，你不可以在一个函数中定义另外一个函数，JavaScript中函数是一等公⺠，本质是因 为JavaScript 函数在 V8 中是 JSFunction 的实例，它实际是 V8 中的一个 C++ 对象。C++ 对象是 C++ 世界中当之无愧的一等公⺠，JavaScript 函数当然也是。(你可以在函数中声明一个变量，当然你也可以 在函数中声明一个函数。C 语言编译器把 C 语言函数编译成机器码，V8 把 JavaScript 函数编译成 C++ 对象)

**惰性解析**是指解析器在解析的过程中，如果遇到函数声明，那么会跳过函数内部的代码，并不会为 其生成 AST 和字节码，而仅仅生成顶层代码的 AST 和字节码。利用惰性解析可以加速 JavaScript 代码的启动速度，如果要将所有的代码一次性解析编译完成，那么会大大增加用户的等待时间。

> 之前直接编译成机器码，第二次执行比第一次执行还要久，因为反序列化太久了

JavaScript 是一⻔天生支持闭包的语言，闭包会引用当前函数作用域之外的变量，所以当 V8 解析一 个函数的时候，还需要判断该函数的内部函数是否引用了当前函数内部声明的变量，如果引用了， 需要将该变量存放到堆中，即便当前函数执行结束之后，也不会释放该变量(称**预解析**)。

V8 第一次执行一段代码时，会编译源 JavaScript 代码，并将编译后的二进制代码缓存在内存中，**内存缓存**(in-memory cache)。然后通过 JavaScript 源文件的字符串在内存中查找对应的编译后的二进制代码。V8 除了采用将代码缓存在内存中策略之外，还会将代码缓存到硬盘上。

> 缓存出现了一些问题，模块化
>
> 他们的作用只是注册、初始化各个模块，一旦初始化完成便不会再执行。由于机器码占空间大，这些只执行一次的代码也会在内存中长期占用空间且缓存作用就只能作用在最外层的 __d() 代码上，而内部的真正的逻辑根本没有被缓存。

在 V8 的 5.9 版本出来之前，V8 引擎使用了两个编译器:v8 5.9(2017年4月底) 发布以后，重新回归了字节码: 

(1)full-codegen — 一个简单和非常快的编译器，产生简单和相对较慢的机器码。

(2)Crankshaft (2010年) 一种更复杂(Just-In-Time)的优化编译器，生成高度优化的代码。
 V8 5.9之前:
当第一次执行 JavaScript 代码时，V8 利用 full-codegen 编译器，直接将解析的 JavaScript 翻译成机器代码而不进行任何转换。 这使得它可以非常快速地开始执行机器代码。请注意这里V8 不使用中间字节码，从而不需要解释器。当代码已经运行一段时间主线程执行你所期望的操作后还有一个 Profiler 线程，它会告诉运行时我 们花了很多时间，让 Crankshaft 可以优化它们一些线程处理垃圾 收集器后，分析线程已经收集了足够的数据来判断应该优化哪个方法。

5.9 发布以后，其中的 Ignition 字节码解释器将默认启动，v8 自此回到了字节码的怀抱。这次 V8 引入字节码却是向着 相反的方向后退。因为之前所有 js 代码编译成机器码缓存下来，因为这样不仅缓存占用的内存、磁盘空间很大，而且退 出 Chrome 再打开时序列化、反序列化缓存所花费的时间也很长，时间、空间成本都接受不了。所以V8 退而求其次， 只编译最外层的 js 代码，也就是下图这个例子里面绿色的部分。那么内部的代码(如下图中的黄色、红色的部分)是什 么时候编译的呢?v8 推迟到第一次被调用的时候再编译。这时间上的推导致被解析多次——绿色的代码一次、黄色的代 码再解析一次(当 new Person 被调用)、红色的代码再解析一次(当 doWork() 被调用)。因此，如果你的 js 代码 的闭包套了 n 层，那么最终他们至少会被 v8 解析 n 次。所以http://crbug.com/593477第二次执行时间会变长(发 现第一次加载时 v8.CompileScript 花费了 165 ms，再次加载加入 V8.ParseLazy 居然依然花费了 376 ms。)

<img src="Naixes阶段性学习笔记2.assets/截屏2021-08-06 上午11.37.26.png" alt="截屏2021-08-06 上午11.37.26" style="zoom:50%;" />



1.(主要动机)减轻机器码占用的内存空间，即牺牲时间换空间，通过恰当地设计字节码的编码方式，字节码可以做到比机器码紧凑很多。 

2.提高代码的启动速度。内存占用过大的问题消除了，就可以提前编译所有代码了。第二次启动就会变快

3.对v8 的代码进行重构，降低 v8 的代码复杂度。有了字节码，v8 可以朝着简化的架构方向发展，消除 Cranshaft 这 个旧的编译器，并让新的 Turbofan 直接从字节码来优化代码，并当需要进行反优化的时候直接反优化到字节码，而不需要再考虑 JS 源代码。Ignition + TurboFan 的组合，就是字节码解释器 + JIT 编译器的黄金组合。

<img src="Naixes阶段性学习笔记2.assets/截屏2021-08-06 上午11.37.51.png" alt="截屏2021-08-06 上午11.37.51" style="zoom:50%;" />

> 分两步：通过lgnition，通过优化程序监听所有代码的热执行，使用Turbofan做反向做优化，把一部分可以做优化的字节码转换成机器码

V8引擎由两个主要部件组成: 1、emory Heap(内存堆) — 内存分配 地址的地方
 2、Call Stack(调用堆栈) — 代码执行的地方

有些浏览器的 API 经常被使用到(比如 说:setTimeout)，但是，这些 API 却 不是引擎提供的。所以说我们还有很多引擎之外的 API，我们把这些称为 浏览器提供 API 称为 Web API，比如 说 DOM、AJAX、setTimeout等等。

webpack优化问题？

慢是因为本身是js，单线程

webpack执行在JIT之内的，js第一次执行时v8进行了缓存编译（字节码要经过），第二次执行时字节码用turbofan编译成机器码，需要通过一系列类型检查等机制，可以使用swc，esbuild可以直接构建机器码，使用js-cache，更新nodejs版本

> V8在21年5月份发布了Sparkplug，介于lgnition和turbofan之间。lgnition有一些不可避免的固定开销，在turbofan优化之前，Sparkplug做了一些辅助工作，可以尽快编译成机器码
>
> Sparkplug 编译器运行快：
>
> 首先，它作弊；它编译的函数已经编译成字节码，字节码编译器已经完成了大部分艰苦的工作，比如变量解析、确定括号是否实际上是箭头函数、解构语句的脱糖等等。Sparkplug **从字节码**而不是从 JavaScript 源代码编译。
>
> 第二个技巧是 Sparkplug **不会**像大多数编译器那样**生成**任何**中间表示 (IR)**。相反，Sparkplug 在字节码的单个线性传递中直接编译为机器代码，发出与该字节码的执行相匹配的代码。事实上，整个编译器是一个[循环](https://source.chromium.org/chromium/chromium/src/+/main:v8/src/baseline/baseline-compiler.cc;l=290;drc=9013bf7765d7febaa58224542782307fa952ac14)内的[`switch`语句](https://source.chromium.org/chromium/chromium/src/+/main:v8/src/baseline/baseline-compiler.cc;l=465;drc=55cbb2ce3be503d9096688b72d5af0e40a9e598b)，分派到固定的每个字节码机器代码生成函数。[`for`](https://source.chromium.org/chromium/chromium/src/+/main:v8/src/baseline/baseline-compiler.cc;l=290;drc=9013bf7765d7febaa58224542782307fa952ac14)

entry过多，使用npm私仓，微前端

接口过多，webpack集群编译，scripty的shell，ssh免密连接到三个linux机器共同编译

整个生命周期如图：（加上GC）

<img src="Naixes阶段性学习笔记2.assets/截屏2021-08-06 下午12.29.25.png" alt="截屏2021-08-06 下午12.29.25" style="zoom:50%;" />

<img src="Naixes阶段性学习笔记2.assets/截屏2021-08-06 下午12.33.20.png" alt="截屏2021-08-06 下午12.33.20" style="zoom:50%;" /><img src="Naixes阶段性学习笔记2.assets/截屏2021-08-06 下午12.33.48.png" alt="截屏2021-08-06 下午12.33.48" style="zoom:50%;" />

 调试参数

<img src="Naixes阶段性学习笔记2.assets/截屏2021-08-06 下午2.22.15.png" alt="截屏2021-08-06 下午2.22.15" style="zoom:50%;" />

实践

```js
//整数相加
//node --trace-opt-verbose
function add(obj) {
    return obj.prop + obj.prop;
}

const length = 1000 * 1000;

const o = { prop: 1 };

for (let i = 0; i < length; i++) {
    add(o);
}
```

没有优化，没有足够的ticks，还没到一轮ticks，还没等到turbofan参与进来（在cli等短期会话的场景下，turbofan优化没有很大作用，因为还没有稳定的对象形状反馈，Sparkplug对此进行了优化，更早的开始了优化）

开始编译优化add

使用turbofan编译

开始编译优化fn

add已经在优化队列

使用turbofan编译fn

优化add

优化fn

完成优化add



<img src="Naixes阶段性学习笔记2.assets/截屏2021-08-06 下午2.56.45.png" alt="截屏2021-08-06 下午2.56.45" style="zoom:50%;" />

反优化

```js
//node --trace-opt-verbose
function test( obj ) {
  return obj.prop + obj.prop;
}

let a = { prop: 'a' }, b = { prop: [] }, i = 0;

while ( i++ < 10000) {
  test( i !== 8000 ? a : b );
}
```

<img src="Naixes阶段性学习笔记2.assets/截屏2021-08-06 下午4.16.57.png" alt="截屏2021-08-06 下午4.16.57" style="zoom:50%;" />

GC

```js
//node --trace-gc 
function strToArray( str ) {
  let i = 0,
    len = str.length,
      // 频繁调动scavenger
    arr = new Uint16Array(str.length);
  for ( ; i < len; ++i ) {
    arr[ i ] = str.charCodeAt( i );
  }
  return arr;
}

let i = 0, str = 'V8 is the coolest';

while ( i++ < 1e5 ) {
  strToArray( str );
}
```

一直失败，没有机会GC

<img src="Naixes阶段性学习笔记2.assets/截屏2021-08-06 下午4.21.37.png" alt="截屏2021-08-06 下午4.21.37" style="zoom:50%;" />

```js
//node --trace-gc 
function strToArray( str, bufferView ) {
  let i = 0,
    len = str.length;
  for ( ; i < len; ++i ) {
    bufferView[ i ] = str.charCodeAt( i );
  }
  return bufferView;
}
//改善代码
let i = 0,
  str = 'V8 is the coolest',
  buffer = new ArrayBuffer( str.length * 2 ),
  bufferView = new Uint16Array( buffer );

while ( i++ < 1e5 ) {
  strToArray( str, bufferView );
}
```

<img src="Naixes阶段性学习笔记2.assets/截屏2021-08-06 下午4.47.43.png" alt="截屏2021-08-06 下午4.47.43" style="zoom:50%;" />

```js
//强制触发GC
function strToArray(str) {
    var i = 0,
        len = str.length,
        arr = new Uint16Array(str.length);
    for (; i < len; ++i) {
        arr[i] = str.charCodeAt(i);
    }
    return arr;
}

var i = 0,
    str = 'V8 is the coolest',
    arr = [];

while (i++ < 1e6) {
    strToArray(str);
    if (i % 100000 === 0) {
        // 数组里面存放大对象 huge object
        arr.push(new Uint16Array(100000000));
        // 5% 概率释放数组
        Math.random() > 0.95 && (arr.length = 0);
    }
}
```

<img src="Naixes阶段性学习笔记2.assets/截屏2021-08-06 下午4.53.44.png" alt="截屏2021-08-06 下午4.53.44" style="zoom:50%;" />

```js
//node --allow-natives-syntax --trace-gc
function factorial( n ) {
  return n === 1 ? n : factorial( --n );
}

var i = 0;

while ( i++ < 1e8 ) {
  factorial( 10 );
  i % 1e7 === 0 && %CollectGarbage(null);
}
```

<img src="Naixes阶段性学习笔记2.assets/截屏2021-08-06 下午5.00.06.png" alt="截屏2021-08-06 下午5.00.06" style="zoom:50%;" />

ast

```js
var test = 'laoyuan'

function init(str){
	//console.log(str)
}

for(var i=0;i<10000;i++){
   init(test);
}
```

<img src="Naixes阶段性学习笔记2.assets/截屏2021-08-06 下午5.16.03.png" alt="截屏2021-08-06 下午5.16.03" style="zoom:50%;" />

## node性能优化

### 内存泄漏

运行内存需要内存，必须释放不再用到的内存否则影响系统性能，可能导致程序崩溃。

没有用的内存没有及时释放就叫做内存泄漏

<img src="Naixes阶段性学习笔记2.assets/截屏2021-08-09 下午5.49.32.png" alt="截屏2021-08-09 下午5.49.32" style="zoom:50%;" />

锯齿状是由scavenge创建的，向下的跳跃是由mark-sweep产生的

浏览器端的内存泄漏会造成网页卡顿

### 压力测试

node压力测试寻找内存泄漏WRK，jmeter

<img src="Naixes阶段性学习笔记3.assets/截屏2021-08-10 上午9.05.30.png" alt="截屏2021-08-10 上午9.05.30" style="zoom:50%;" />

node自带process.memoryUsage，判断泄漏以heapUsed为准

rss：所有

heapTotal：堆

heapUsed：使用的堆

external：v8内部引擎的c++对象占用的内存

memwatch+heapdump

easy-monitor，node监控平台

### 原因

使用js全局变量当作缓存必然会发生内存泄漏，可以使用redis

队列消费不及时，消费生产者模型中，生产大于消费会产生堆积，容易产生内存泄漏，比如收集日志，产生速度大于文件写入速度（事件循环也是一个典型的生产消费模型）

闭包，最小化闭包

**浏览器中**

全局变量大

原型链，vue2的插件在原型链上挂载过多的东西，new Vue是一个全局变量，with的虚拟dom也在内存中，vuex的对象使用Object.create创建，慢对象

游离Dom，dom内存泄漏

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>dom内存泄漏</title>
  </head>
  <body>
    <!--只有同时满足 DOM 树和 JavaScript 代码都不引用某个 DOM 节点，该节点才会被作为垃圾进行回收。 
        如果某个节点已从 DOM 树移除，但 JavaScript 仍然引用它，我们称此节点为“detached ”。
        因为 DOM 元素依然会呆在内存中。
        “detached ”节点是 DOM 内存泄漏的常见原因。-->
    <script>
      //万万记得避免全局变量 "use strict"
      //同时也要避免在函数内部不使用var的声明
      let detachedTree;
      function create() {
        var ul = document.createElement('ul');
        for (var i = 0; i < 100; i++) {
          var li = document.createElement('li');
          ul.appendChild(li);
        }
        detachedTree = ul;
      }
      create();
      detachedTree = null;
    </script>
  </body>
</html>

<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>游离的DOM元素2</title>
  </head>
  <body>
    <script>
      function createElement() {
        const div = document.createElement('div');
        div.id = 'yideng';
        return div;
      }
      // this will keep referencing the DOM element even after deleteElement() is called
      // 放在函数里执行完后可以回收
      // function appendElement() {
      const detachedDiv = createElement();
      document.body.appendChild(detachedDiv);
      // }
      // appendElement();
      // 在页面上删除没有用，js中还存在
      function deleteElement() {
        document.body.removeChild(document.getElementById('detached'));
      }
      deleteElement(); // Heap snapshot will show detached div#detached
    </script>
  </body>
</html>

```

> 控制台：performance
>
> hs Heap
>
> memory中有detached HTMLElement
>
> vue的虚拟dom不能回收，因为用了with，react双缓存也一样

事件绑定，使用事件具柄（不要使用匿名函数），记得移除

清除定时器

delete和修改对象

统计代码运行时间，避免逻辑过于复杂没有GC的机会

学会查看控制台的memory快照

compiled code和string太大说明js文件太大了

node内存泄漏监控：

使用memeye监控，简陋，node启动demo，再使用wrk进行压力测试

```js
const http = require('http');
const memeye = require('memeye');
memeye();
// 泄漏，使用redis代替变量缓存
let leakArray = [];
const server = http.createServer((req, res) => {
  if (req.url == '/') {
    // const wm = new WeakMap();
    leakArray.push(Math.random());
    // wm.set(leakArray, leakArray);
    // console.log(wm.get(leakArray));
    console.log(leakArray);
		// 使用null也不能明显解决，因为不会马上进行回收，也不一定会回收（还有其他强引用的情况下）
    // leakArray = null;
    res.end('hello world');
  }
});
server.listen(4000);
```

demo1

```js
//node --expose-gc
const format = (bytes) => {
  return (bytes / 1024 / 1024).toFixed(2) + 'MB';
};
//手动GC
global.gc();
// 返回 Nodejs 的内存占用情况，单位是 bytes
const mem = process.memoryUsage();
console.log(format(mem.heapUsed));

// let map = new Map();
// let key = new Array(5 * 1024 * 1024);
// map.set(key, 1);
// //注意要先删除依赖关系，再置空，否则删除后，gc也毫无用处
// map.delete(key);
// key = null;

// global.gc();
// const mem2 = process.memoryUsage();
// null没用
// console.log('对象占用之后🐻', format(mem2.heapUsed));

const wm = new WeakMap();
let key = new Array(5 * 1024 * 1024);
wm.set(key, 1);
// console.log(%DebugPrint(wm));
//不用做无谓的挣扎
key = null;
global.gc();
const mem3 = process.memoryUsage();
console.log('使用Weakmap以后🐻', format(mem3.heapUsed));

```

demo2，buffer的性能优于string，bigpipe的应用

```js
const http = require('http');
const memeye = require('memeye');
memeye();
let s = '';
for (let i = 0; i < 1024 * 10; i++) {
  s += 'a';
}

const str = s;
const bufStr = Buffer.from(s);
const server = http.createServer((req, res) => {
  if (req.url == '/buffer') {
    res.end(bufStr);
  } else if (req.url == '/string') {
    res.end(str);
  }
});
server.listen(3000);

```

buffer需要处理大量的二进制数据，用一点就去向系统申请就会造成频繁的内存调用申请，所以buffer的内存不由V8分配，而是在c++层面完成，这部分内存称为堆外内存

nodejs采用了slob机制进行预先申请，事后分配

nodejs以8kb为界限区分小对象和大对象

## serverless

FAAS

函数即服务，每一个函数都是一个服务，函数可以由任何语言编写，除此 之外不需要关心任何运维细节，比如:计算资源、弹性扩容，而且可以按 量计费，且支持事件驱动。业界大云厂商都支持 FAAS，各自都有一套工 作台、或者可视化工作流来管理这些函数。

BAAS

后端及服务，就是集成了许多中间件技术，可以无视环境调用服 务，比如数据即服务(数据库服务)，缓存服务等。虽然下面还 有很多 XASS，但组成 Serverless 概念的只有 FAAS + BAAS。

PAAS

平台即服务，用户只要上传源代码就可以自动持续集成并享受高 可用服务，如果速度足够快，可以认为是类似 Serverless。但随 着以 Docker 为代表的容器技术兴起，以容器为粒度的 PASS 部 署逐渐成为主流，是最常用的应用部署方式。比如中间件、数据 库、操作系统等。

DAAS

数据即服务，将数据采集、治理、聚合、服务打包起来提供出 去。DASS 服务可以应用 Serverless 的架构。

<img src="Naixes阶段性学习笔记3.assets/截屏2021-08-10 上午9.58.34.png" alt="截屏2021-08-10 上午9.58.34" style="zoom:50%;" />

国内为数不多的实践ServerLess的云平 台，但是现阶段开发体验相对较差。

亚马逊云，开发体验更好。有更完整的 Demo和实际的代码

让前后端链接在一起真正的云化，利用 Service Worker部署到边缘服务器上

https://www.aliyun.com

https://serverless.com

https://www.cloudflare.com/zh-cn/

原理

docker+k8s

<img src="Naixes阶段性学习笔记3.assets/截屏2021-08-10 上午10.00.26.png" alt="截屏2021-08-10 上午10.00.26" style="zoom:50%;" />

<img src="Naixes阶段性学习笔记3.assets/截屏2021-08-10 上午10.03.47.png" alt="截屏2021-08-10 上午10.03.47" style="zoom:50%;" />

FaaS 推荐无状态的函数。就是函数不可改变 Immutable。就是说一个函数只要参数固定，返回的结果也必须是固定的。

状态交给数据库

<img src="Naixes阶段性学习笔记3.assets/截屏2021-08-10 上午10.04.49.png" alt="截屏2021-08-10 上午10.04.49" style="zoom:50%;" />

FaaS 就像高铁的⻋头 Bass就是⻋厢

<img src="Naixes阶段性学习笔记3.assets/截屏2021-08-10 上午10.05.20.png" alt="截屏2021-08-10 上午10.05.20" style="zoom:50%;" />

DDD

领域驱动模型

<img src="Naixes阶段性学习笔记3.assets/截屏2021-08-10 上午10.05.37.png" alt="截屏2021-08-10 上午10.05.37" style="zoom:50%;" />

......

## Electron

1 Electron = Chromium + Node.js+Native API,我们每天使 用的VsCode就是使用它开发的。

2 我们学习他的收益:自己造工具、拓展技术的广度

3 它没有跨域问题、最新浏览器的Feature、没有PolyFill

4 node.js add-on、node-ffi可以调用原生模块

5 系统OS能力WinRT、AppleScript、Shell

6 同类对比:Native( C++/C#/Objective-C)、QT(基于C++)

Wps就是基于QT的、NW、Flutter、PWA、WPF等。

能力：

<img src="Naixes阶段性学习笔记3.assets/截屏2021-08-10 下午4.08.09.png" alt="截屏2021-08-10 下午4.08.09" style="zoom:50%;" />

对比：

<img src="Naixes阶段性学习笔记3.assets/截屏2021-08-10 下午4.08.27.png" alt="截屏2021-08-10 下午4.08.27" style="zoom:50%;" />

原理：

Node.js与Chromiums整合

难点:Node.js事件循环基于libuv，但Chromium基于 Message pump

1. Chromium集成到Node.js 用libuv实现Message pump(nw) 

2. Node.js集成到Chromium 

3. libuv引入了backend_fd（事件通知机制，监控node eventloop，送回chrome）的概念右侧如图，libuv轮询事件的 文件描述符，我们通过Elector起了一个新的安全线程去轮询 这个backend_fd，可以知道libuv的一个新事件，通过 postTask转发到Chromium MesssageLoop中。

4. 资料:

https://www.electronjs.org/blog/electron-internals-node-integration 

https://www.youtube.com/watch?v=OPhb5GoV8Xk 

https://github.com/electron/electron/blob/master/shell/common/node_bindings.cc

PrepareMessageLoop->独立线程(uv_thread_create)-> EmbedThreadRunner(轮询)->有消息WakeupMainThread唤起主线程 ->PostTask 转发到Chromium事件循环

准备事件循环，如果node有返回，拉起独立线程，开始轮询，有消息时唤醒主线程，把当前PostTask 转发到Chromium事件循环

<img src="Naixes阶段性学习笔记3.assets/截屏2021-08-10 下午4.37.01.png" alt="截屏2021-08-10 下午4.37.01" style="zoom:50%;" />

Chromium架构

<img src="Naixes阶段性学习笔记3.assets/截屏2021-08-10 下午5.03.52.png" alt="截屏2021-08-10 下午5.03.52" style="zoom:50%;" />

<img src="Naixes阶段性学习笔记3.assets/截屏2021-08-10 下午5.06.57.png" alt="截屏2021-08-10 下午5.06.57" style="zoom:50%;" />

<img src="Naixes阶段性学习笔记3.assets/截屏2021-08-10 下午5.07.13.png" alt="截屏2021-08-10 下午5.07.13" style="zoom:50%;" />

Package.json中启动的就是主进程，展示Web页面的进程称为渲染进程(有多个可以)

<img src="Naixes阶段性学习笔记3.assets/截屏2021-08-10 下午5.08.01.png" alt="截屏2021-08-10 下午5.08.01" style="zoom:50%;" />

Electron提供了IPC通信模块，主进程的ipcMain和渲染进程的ipcRender都是EventEmitter对象

......

## PWA

Progressive Web Apps 是 Google 提出的用前沿的 Web 技术为网页 提供 App 般使用体验的一系列方案。但是作为一个 web 应用，它可以 断网使用、推送消息、发送通知、从桌面启动，当然还包括 Web 应 用的优势:免安装、快速开发、依赖浏览器跨平台(支持包括Edge在内的 各种主流PC/手机浏览器)。

响应式: 用户界面可以兼容多种设备，比如: 桌面，移动端，平板。

应用化: 交互体验接近native应用。

网络低依赖: 无网络或者低速网络下依然可以 使用。

延续性: 借助推送功能，能够维持用户粘性。

可安装: 可以被安装到主屏，这样用户随时可 以从主屏启动应用。

可被发现: 被视为一个独立应用，而且可以被 搜索.

可更新: 当用户重新联网时，可以更新内容.

安全: 可以使用HTTPS来防止内容伪造和中间 人攻击。

渐进性: 所有用户都可以使用，浏览器无关。 

兼容url: 可以通过url传播。

不兼容苹果

利用“App Shell”方法设计和构建应用、应用能够离线工 作、存储供稍后离线使用的数据、代理的https服务器、 Chrome 52 或更高版本

<img src="Naixes阶段性学习笔记3.assets/截屏2021-08-10 下午5.55.38.png" alt="截屏2021-08-10 下午5.55.38" style="zoom:50%;" />

**Service worker** 它是一个在浏览器后台运行的脚本，与网页不相干，专注于那些不需要网页或用户互动就能完成的功能。它主要用于操作离线缓存。

**前端缓存介质**，利用orm操作缓存的库? **offline.js**实现数据的互通

**App Shell**，顾名思义，就是“壳”的意思， 也可以理解为“骨架屏”，说白了就是在内容 尚未加载完全的时候，优先展示页面的结构、 占位图、主题和背景颜色等，它们都是一些被 强缓存的 html，css和javascript。

**测试环境&开发环境** http-server -c-1 # 注意设置 关闭缓存 ngrok http 8080

### service work

存储机制

通过拦截网络请求，使得网站运行得更快，或者在离线情况下，依然可以执行。也作为其他后台功能的基础，比如消息推送和背景同步。

属于JavaScript Worker，不能直接接触DOM，通过 postMessage接口与页面通信。

不用的时候会终止执行，需要的时候又重新执行，即它是事 件驱动的。

只在**HTTPs协议下可用**，这是 因为它能拦截网络请求，所以必须保证请求是安全的。

有一个精心定义的升级策略，内部大量使用Promise。

#### 生命周期

**INSTALLING 正在安装阶段** 此阶段处于Service Worker被注册的 时候。在这个阶段，Service Worker 的install() 方法将会被执行，声明的资 源即将被加入缓存。

**INSTALLED 安装完成阶段** 当 Service Worker 完成其初始化安装 之后就会进入到这个阶段。在这个阶 段，它是一个“有效但尚未激活的 worker ”，等待着客户端对其进行激活 使用。我们可以在这个阶段告知用户， PWA 已经可以进行升级了。

**ACTIVATING 正在激活阶段**当客户端已无其它激活状态的 Service Worker、或者脚本中的skipWaiting() 方 法被调用、或者用户关闭了该 Service Worker 作用域下的所有页面时，就会触 发 ACTIVATING 阶段。在这个阶段中，Service Worker脚本中的activate() 事件 会被执行，此时可以清除掉过期的资源，并将进入下一个“激活完成阶段”。

**ACTIVETED 激活完成阶段**此时 Service Worker 已经被激活并生效，可以开 始控制网站的资源请求了。此时 Service Worker 内的fetch 和message 事件已经可以被监听。

**REDUNDANT 废弃阶段** 当安装失败，激活失败或者当前 Service Worker 被其他 Service Worker 替换时，就会进入这个阶 段，此时 Service Worker 将失去对页面的控制。

第一次安装，第二次激活，原子操作



PWA 的核心可谓是 Service Worker，任何一个PWA都有 且只有一个service-worker.js 文件，用于为Service Worker添加资源列表，进行注册、激活等生命周期操作。 但是在webpack构建的项目中，生成一个service- worker.js 可能会面临很多的问题。 							 					 				

文件的版本戳

webpack生成的资源多会生成一串hash，Service Worker的 资源列表里面需要同步更新这些带hash的资源;

sw.js文件的版本号

每次更新代码，都需要通过更新service-worker.js 文件版本号 来通知客户端对所缓存的资源进行更新，(但使用明确的版本 号会更加合适)。

#### offline-plugin PK Worker-precache-webpack-plugin

配置 

更多的可选配置项，满足更加细致的配置要 求;

社区

更新频率相对更高，star数更多;

文档

更为详细的文档和例子。

自动

自动处理生命周期，用户无需纠结生命周期 的坑;

#### Workbox

workbox这个库和构建工具的集合使用了servicework 的 fetch event 和cache API，可以很容易地在用户的设备上本地存储您的网站文件。

让您的网站离线访问。

提高重复访问的负载性能，即使您不想完全离线，也可以使用 workbox 在本地存储和提供常用文件，而不是从网络中存储和提供。

迅速集成进**workbox-webpack-plugin**

