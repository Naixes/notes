····

## html

1. html布局元素分类有哪些？应用场景都是什么？

有行内元素，块状元素，行内块状元素

行内元素从左向右显示，宽高由内容决定不能直接控制，只能嵌套行内元素，常见的有span a textarea，display: inline

块状元素独占一行，宽度默认父元素宽度，高度默认本身内容高度，常见的div h1-6 ul li p form，display: block

行内块状元素，集合了两种特性，不自动换行并且可以设置宽高，display: inline-block



2. b和strong区别

效果一样，目的不一样，b注重样式，strong表示强调，即样式标签和语义化标签的区别

语义化标签优势在于便于理解，结构明确，利于seo，一个重要场景就是无障碍阅读



3. 减少dom数量的办法？怎么优化大量的dom

不使用无意义标签，使用伪元素代替，比如阴影，清除浮动

按需加载，减少不必要渲染

结构合理，语义化标签

优化：

缓存dom对象，比如在循环遍历之前先获取到主节点

合并操作：使用文档片段，`document.createDocumentFragment()`操作文档片段不会影响真实dom，做完所有操作后一次性更新到dom；进行复杂的dom操作时（删减或添加子节点），先删除或者复制元素，操作完成后再更新

使用innerHtml代替频繁的appendChild

虚拟dom+diff



5. SEO

seo优化就是提高网站在搜索引擎的权重，重点就是提高搜索引擎对网站的理解

最基础的方法就是title，description，keywords，语义化标签，图片的alt，唯一的h1，页面扁平，flash/图片/视频/iframe/异步加载抓取不到，优先加载重要内容，提高速度，友情链接

- 网站结构布局：

控制首页链接数量，扁平化跳转层次，导航尽量文字，

头部包括logo主导航用户信息，使用面包屑导航，右相关连接，底部版权信息和友情链接，分页使用页码

优先加载重要内容

控制页面大小，减少请求，提高速度

- 代码优化：

合理的title，description，keywords

语义化标签

a，内部链接加title，外部链接加el="nofollow"，只能抓取href，不要带参数

唯一的h1

图片添加alt

表格标题使用caption

不会执行js，重要内容不要使用js输出

会过滤display: none，只能抓取get请求

减少iframe

使用robots.txt



6. meta标签

提供页面的元信息，属性：charset，content，http-equiv，name

http-equiv，http头部某些作用，可以改变服务器和用户代理行为，模拟http头字段

content与http-equiv，name配合

name定义元数据不和charset，http-equiv共存

常用：声明字符集，viewport，优先使用的浏览器版本



7. async和defer

都是为了加载文件时不阻塞页面渲染，对内联脚本不起作用，脚本中不能调用document.write

defer立即下载，延迟到页面解析完成之后执行，规范要求按照出现顺序执行并且先于DOMContentLoaded执行，实际上都并不一定，所以最好只包含一个延迟脚本，async不保证执行先后顺序，模块脚本默认defer

async允许脚本异步执行，在下载完成后立即执行，window的load之前执行，是html5定义，浏览器支持不同，同时存在时只触发async

## css

1. 移动端适配方案和对比

**媒体查询**，简单方便，响应式，代码量大，有资源浪费

**flex**

**rem+viewport**，根据rem将页面放大dpr倍，viewport设为1/dpr，在 scale 为 1 的情况下，`device-width（设备逻辑像素大小） = 设备的物理分辨率/devicePixelRatio（物理像素分辨率与CSS像素分辨率之比）`

**rem**，根据屏幕宽度设置`html`标签的`font-size`，在布局时使用 **rem** 单位布局，达到自适应的目的。需要内嵌js，浏览器渲染整数，可能不准确

```js
!(function (d) {
  var c = d.document;
  var a = c.documentElement;
  var b = d.devicePixelRatio;
  var f;
  function e() {
    var h = a.getBoundingClientRect().width,
      g;
    if (b === 1) {
      h = 720;
    }
    if (h > 720) h = 720; //设置基准值的极限值
    g = h / 7.2;
    a.style.fontSize = g + "px";
  }
  if (b > 2) {
    b = 3;
  } else {
    if (b > 1) {
      b = 2;
    } else {
      b = 1;
    }
  }
  a.setAttribute("data-dpr", b);
  d.addEventListener(
    "resize",
    function () {
      clearTimeout(f);
      f = setTimeout(e, 200);
    },
    false
  );
  e();
})(window);
```

**vh，vw**

**百分比**，有可能拉伸变形，字体不能动态变化



2. 伪元素和伪类

伪类用来选择dom树之外的信息，添加一些特殊效果，`:active :hover​ :link :visited`等，与class类似

伪元素dom树没有定义的虚拟元素，是基于元素的抽象

都不会出现在源文件或者dom树中，伪元素需要添加元素



3. link和@import区别

link使用在html头部，引入外部css文件，也可以引入别的文件，在页面载入时同时加载

@import在css中引入外部css文件，在页面载入之后加载，页面会有闪烁，有兼容问题



4. flex

flex属性是 `flex-grow、flex-shrink、flex-basis` 的简写，默认值为`0，1，auto。`

- flex-grow 定义项目的放大比例，默认为0，即如果存在剩余空间，也不放大
- flex-shrink 定义了项目的缩小比例，默认为1，即如果空间不足，该项目将缩小
- flex-basis 给上面两个属性分配多余空间之前, 计算项目是否有多余空间, 默认值为 auto, 即项目本身的大小

flex = 1，1 1 0%



5. 盒模型

IE：width=content+padding+border

标准：width=content

相对定位，相对自己；绝对定位，脱离文档流，相对定位的父元素；浮动，脱离文档流



6. 动画实现

transition

animation，更加强大



7. 浮动

脱离文档流，移动到指定的相对于父元素的位置

清除浮动本质是避免浮动元素对其他元素产生影响

额外标签 `<div style="clear:both"></div>`

BFC，父元素添加overflow:hidden

伪元素

```js
 .clearfix:after {  
     content: "";
     display: block;
     height: 0;
     clear: both;
     visibility: hidden;
}
```

8. 使用transform和margin，top，left改变位置的区别

transform生成独立的层不会造成整个页面重绘回流，GPU直接渲染，但会占用多余的内存



9. px和em

em相对父元素的字体大小，使用起来复杂，会有很多小数，不精确

px绝对长度单位



10. inherit，initial，unset区别

继承，默认值，不设置默认继承不可继承就默认



11. 超出省略

```css
.single-ellipsis{
  width: 500px;
  overflow: hidden;
  white-space: nowrap;
  text-overflow: ellipsis;
}

.multiline-ellipsis {
  display: -webkit-box;
  word-break: break-all;
  -webkit-box-orient: vertical;
  -webkit-line-clamp: 3; //需要显示的行数
  overflow: hidden;
  text-overflow: ellipsis;
}
```



## js

执行流程

分为编译阶段和执行阶段

**编译阶段：**

1. 生成执行上下文和变量对象：在执行上下文栈ECS创建一个全局执行上下文GC其中包含了变量对象VO，在编译阶段js引擎会对声明进行处理，对于通过var声明的变量，js引擎会在环境对象中创建名为变量名的属性，初始化为undefined，对于函数，会将函数的定义部分存到堆中，并在环境对象中创建一个名为方法名的属性指向堆中函数的地址。
2. 将声明之外的代码编译成可执行代码（字节码），然后进入执行阶段

一段代码经过编译后会生成两部分内容执行上下文和可执行代码。

执行上下文EC就是执行代码时的运行环境，调用一个函数时就会进入这个函数的执行上下文，决定了这个函数执行期间用到的变量。执行上下文中存在一个变量对象，变量提升就保存在这个对象中

**执行阶段：**

顺序执行可执行代码，每调用一个函数就会**创建一个新的EC**，并在ECS中压入这个函数的EC，调用完成之后会销毁，并回到上一个执行上下文，直到栈中的代码全部执行完毕。

如果出现相同的变量或函数时会怎样？

```js
a(); // 1
var a = "hello world"; //2 a -> undefined
console.log(a); // 3
function a() {
  // 4
  console.log("inner a function 1");
}

var a = "hello, tomorrow"; // 5 a -> function

console.log(a); // 6
function a() {
  // 7 a -> function2
  console.log("inner a function 2");
}
a(); // 8
/* 
inner a function 2
hello world
hello, tomorrow

报错 a is not a function
*/
```

其中**ESP**永远指向栈顶也就是this的指向

**变量对象VO**，EC中的特殊变量，用来存储函数声明，函数形参和变量。**作用域链**就是依靠VO维持的

**活动对象AO**，函数**执行时创建**，包含了普通参数和具有所有属性的参数映射表（arguments），VO是不能直接访问的，所以需要AO来管理内部变量，通过VO来与外部进行联系。

**AO分为创建阶段和执行阶段**

函数执行时创建函数执行上下文，包含scopeChain（指向scope），AO，VO，scope: [AO, VO, GO]，在创建阶段会发生属性名称的定义但不会赋值，**变量提升**就是在这个阶段。创建阶段结束就到了运行阶段，运行阶段执行内部代码，**确定this指向**，执行变量赋值等

如果发生**闭包**，执行完成后会被存储到堆区，不会进行回收。

new Function创建函数，scope绑定全局作用域，不会回收，eval也类似，可能造成**内存泄漏**

**ES5+**的执行上下文发生了变化包含**词法环境和变量环境**和ThisBinding，this在一开始就确定了。词法环境中的**环境记录**包含了外部引用和内部变量以及函数声明，而变量环境是用来兼容之前使用var创建的变量。在创建阶段let，const声明的变量没有绑定任何值，这也是造成暂时性死区TDZ的原因

无论是ES多少，上下文的生命周期都是三个阶段：**创建阶段-执行阶段-回收阶段**



1. 原型链继承和class继承

ES5 prototype 继承

子类的 prototype 为父类对象的一个实例，实质是先创造子类的实例对象`this`，然后再将父类的方法添加到`this`上面（`Parent.apply(this)`）

ES6 class 继承

子类没有自己的 this 对象，因此必须在 constructor 中通过 super 继承父类的 this 对象，而后对此 this 对象进行加工。`super`关键字在构造函数中表示父类的构造函数，用来新建父类的`this`对象。实质是先创造父类的实例对象`this`（所以必须先调用`super`方法），然后再用子类的构造函数修改`this`。

super 可作为函数和对象使用。当作为函数使用时，只可在子类的构造函数中使用，表示父类的构造函数，但是 super 中的 this 指向的是子类的实例，`因此在子类中super()表示的是Parent.prototype.constructor.call(this)`。当作为对象使用时，super 表示父类原型对象，即 Parent.prototype。

区别和不同

- 类内部定义的方法都是不可枚举的
- 类不存在变量提升（hoist）
- 类相当于实例的原型，所有在类中定义的方法，都会被实例继承。静态方法直接通过类来调用。
- ES5 的继承，实质是先创造子类的实例对象 this，然后再将父类的方法添加到 this 上面（Parent.apply(this)）。ES6 的继承机制完全不同，实质是先创造父类的实例对象 this（所以必须先调用 super 方法），然后再用子类的构造函数修改 this。



2. Reflect.ownKeys和Object.keys

获取对象的属性，以数组的形势返回

前者所有属性包括不可枚举属性和symbol属性，不包括原型

后者可枚举属性，不包括symbol和原型属性



3. Promise

Promise 对象是 JavaScript 的异步操作解决方案，为异步操作提供统一接口。它起到代理作用（proxy），充当异步操作与回调函数之间的中介，使得异步操作具备同步操作的接口。Promise 可以让异步操作写起来，就像在写同步操作的流程，而不必一层层地嵌套回调函数。

有三个状态：pending，fulfilled，rejected，只能从pending到fulfilled，rejected

通过catch捕获到reject之后，在catch后面还可以继续顺序执行then方法，但是只执行then的第一个回调(resolve回调)

```js
Promise.reject(2)
    .catch(r => {
        // 捕获到错误，执行
        console.log('catch1');
    })
    // 错误已经被捕获，后边的`then`都顺序执行，且只执行`then`的第一个回调（resolve的回调）
    .then(v => {
        console.log('then1');
    }, r => {
        console.log('catch2');
    })
    .catch(r => {
        // 前边没有未捕获的错误，不执行
        console.log('catch3');
    })
    .then(v => {
        console.log('then2');
    }, r => {
        console.log('catch4');
});
// 结果会打印：catch1、then1、then2
```



4. 大数计算

因为 JavaScript 的 Number 类型是遵循 IEEE 754 规范表示的，能精确表示的数字是有限的，可以精确到个位的最大整数是 2 的 53 次方，超过这个范围就会精度丢失，造成 JavaScript 无法判断大小

常用的一中方案是将 Number 转为 String，然后将 String 转为 Array，并且注意补齐较短的数组，将他们每一位一一相加得到一个新数组，再将和组成的新数组转为数字就可以了。也可以引用第三方库 bignumber.js，原理也是把所有数字当作字符串



5. 文件上传

每一个input标签都会创建一个FileUpload对象，使用form的submit可以实现最简单的上传，但是会刷新页面

使用XMLHttpRequest2和FormData对象可以无刷新上传

```js
let xhr = new XMLHttpRequest();
let formData = new FormData();
let fileInput = document.querySelector("#myFile");
let file = fileInput.files[0];
formData.append("myFile", file);
xhr.open("POST", "/upload.php");
xhr.onload = function () {
  if (this.status === 200) {
    // 对请求成功处理
  }
};
// 进度监听
xhr.upload.onprogress = function (event) {
  const { loaded, total, lengthComputable } = event;
  // lengthComputable 代表文件总大小是否可知
  if (lengthComputable) {
    let percentComplete = (loaded / total) * 100;
    // 对进度处理
  }
};
xhr.send(formData);
xrh = null;
```

图片预览

一般实现预览的方式是，等待文件上传成功后，后台返回上传文件的url，然后把预览图片的img元素的src指向该url。

但是还有更好的实现方式。就是使用HTML5提供的 FileReader API。

```js
function handleImageFile(file){
  let previewArea = document.querySelector("#previewArea");
  let img = document.createElement('img');
  let fileInput = document.querySelector('#myFile');
  let file = fileInput.files[0];
  img.file = file;
  previewArea.appendChild(img);
  let reader = new FileReader();
  reader.onload = (function(aImg){
    return function(e){
      aImg.src = e.target.result;
    }
  })(img)
  reader.readAsDataURL(file);
}
```

这里使用FileReader来处理图片的异步加载。在创建新的FileReader对象之后，我们建立了onload函数，然后调用readAsDataURL()开始在后台进行读取操作。当图像文件加载后，转换成一个 data: URL，并传递到onload回调函数中设置给img的src。

另外还可以使用对象URL来实现预览

```js
let img = document.createElement("img");
img.src = window.URL.createObjectURL(file);
img.onload = function(){
  window.URL.revokeObjectURL(this.src);
}
previewArea.appendChild(img);
```

多文件

```js
let fileInput = document.querySelector('#myFile');
let files = fileInput.files;
let formData = new FormData();
for(let i = 0;i<files.length;i++){
  let file = files[i];
  formData.append('files[]',file,file.name);
}
```

二进制上传

有了FileReader 其实还有一种上传的途径，读取文件内容后可以直接二进制格式上传。

```js

let reader = new FileReader();
reader.onload = function(){
  xhr.sendAsBinary(this.result);
}
// 把input里读取的文件内容，放到fileReader的result字段里
reader.readAsBinaryString(file);
// 但是这里有个问题，查看MDN文档，可以看到XMLHttpRequest的sendAsBinary方法已经移除了，所以需要自己实现一个

XMLHttpRequest.prototype.sendAsBinary = function(text){
  let data = new ArrayBuffer(text.length);
  let ui8a = new Unit8Array(data,0);
  for(let i =0;i<text.length;i++){
    ui8a[i] = (text.charCodeAt(i) & 0xff);
  }
  this.send(ui8a);
}
// 这段代码将字符串转成8位无符号整型，然后存放到一个8位无符号整型数组里面，再把整个数组发送出去。
```

拖拽

```js
let dropArea;
dropArea = document.querySelector("#dropArea");
dropArea.addEventListener('dragenter',handleDragenter,false);
dropArea.addEventListener('dragover',handleDragover,false);
dropArea.addEventListener('drop',handleDrop,false);

// 阻止dragenter和dragover的默认行为，这样才能使drop事件被触发
function handleDragenter(e) {
    e.stopPropagation();
    e.preventDefault();
}

function handleDragover(e) {
    e.stopPropagation();
    e.preventDefault();
}

function handleDrop(e) {
    e.stopPropagation();
    e.preventDefault();

    let dt = e.dataTransfer;
    let files = dt.files;

    // handle files ...
}
```

### 数据结构

1. weakMap和weakSet为什么键只能是对象？

为了保证只能通过键对象的引用来获取值，由于基本数据类型在传递时，传递的是值，而不是引用，没办法区分是否初始化时的键。

不支持迭代以及keys，values，entries方法，因为回收的时间是不确定的，不知道有没有被回收

```js
const m = new WeakMap();
m.set({}, 100);
// 由于 {} 没有在其他地方引用，所以在垃圾回收时，这个值也会被回收。

// 在创建对象时，分配了一块内存，并把这块内存的地址传给 a
const a = {};
// 执行 set 操作时，实际上是将 a 指向的内存地址和 100 关联起来
m.set(a, 100);
// 如果使用这种方式，则不会被回收。因为 {} 有 a 变量在引用它。

a = null;
// 将 a 置为空后，m 里的值 100 在垃圾回收时将会被回收。如果是Map类型不会被回收，需要手动清空 m

const a = "abc";
// 由于基本数据类型在传递时，传递的是值，而不是引用。
m.set(a, 100);
// 所以执行 set 操作时，实际上是将新的 'abc' 和 100 关联起来，而不是原来 a 变量指向的那个。
// 那这样就会有问题，m 里存储的永远是没有被引用的键，随时都会被回收。
```

使用场景：

**缓存计算结果**，使用完成后将键置为null，键回收时，缓存也会被回收

**关联数据**，当作为键的对象消失时对应的数据也会被回收



2. Reflect和元编程

**Reflect**不是构造函数，所有属性和方法都是静态的

作用：

- 整合一些语言内部方法，统一命名空间
- 函数化一些对象操作
- 修改了Object一些方法的返回结果，用boolean代替抛出异常
- Proxy可以改写原生api，reflect可以起到备份作用，proxy可以代理的13种拦截，reflect中都有对应方法

**元编程**

借助Proxy和Reflect允许拦截并定义语言操作的自定义行为

应用：

- **数据劫持，验证操作**

- **函数节流**

```js
const createThrottleProxy = (fn, rate) => {
  let lastClick = Date.now() - rate;
  return new Proxy(fn, {
    apply(target, context, args) {
      if (Date.now() - lastClick >= rate) {
        fn.bind(target)(args);
        lastClick = Date.now();
      }
    },
  });
};
const handler = () => console.log("do something");
const handlerProxy = createThrottleProxy(handler, 1000);
document.addEventListener("scroll", handlerProxy);
```

- **图片懒加载**：通过proxy构造Image对象，加载完成时替换默认图片

```js
const IMG_URL =
  "http://img-static.yidengxuetang.com/wxapp/github-img/javascript1.png";
const imageProxy = (loadImage) => {
  return new Proxy(Image, {
    construct(target, args) {
      const instance = Reflect.construct(target, args);
      instance.src = loadImage;
      return instance;
    },
  });
};
const ImageProxy = imageProxy(IMG_URL);

const createImageProxy = (realImg) => {
  const img = new ImageProxy();
  const virtualImg = new Image();
  virtualImg.src = realImg;
  virtualImg.onload = () => {
    hasloaded = true;
    img.src = realImg;
  };
  return img;
};

const img = createImageProxy(
  "http://img-static.yidengxuetang.com/wxapp/issue-img/wxqr-github.png"
);
document.body.appendChild(img);
```

- **单例模式**

```js
function makeSingleton(func) {
  let instance,
    handler = {
      construct: function (target, args) {
        if (!instance) {
          instance = new func();
        }
        return instance;
      },
    };
  return new Proxy(func, handler);
}

// 以这个constructor为例
function Test() {
  this.value = 0;
}

// 普通创建实例
const t1 = new Test(),
  t2 = new Test();
t1.value = 123;
console.log(t2.value); // 0 因为 t1、t2 是不同的实例

// 使用proxy
const TestSingleton = makeSingleton(Test),
  s1 = new TestSingleton(),
  s2 = new TestSingleton();
s1.value = 123;
console.log(s2.value); // 123 现在 s1、s2 是相同的实例。
```

- **观察者模式**

```js
let hero = {
  name: "赵云",
  hp: 100,
  sp: 100,
  equipment: ["马", "长枪"],
};

const handler = {
  set(target, key, value, receiver) {
    //内部调用对应的 Reflect 方法
    const result = Reflect.set(target, key, value, receiver);
    //执行观察者队列
    observableArray.forEach((item) => item());
    return result;
  },
};

//初始化Proxy对象，设置拦截操作
const createProxy = (obj) => new Proxy(obj, handler);

//初始化观察者队列
const observableArray = new Set();

const heroProxy = createProxy(hero);

//将监听函数加入队列
observableArray.add(() => {
  console.log(heroProxy.name);
});

heroProxy.name = "黄忠";
// --> 黄忠
```

- 对象多重继承

```js
const people = {
  name: "people",
  run() {
    console.log("people.run:", this.name);
  },
};

const powerMan = {
  name: "powerMan",
  run() {
    console.log("powerMan.run:", this.name);
  },
  fight() {
    console.log("powerMan.fight:", this.name);
  },
};

const handler = {
  get(target, name, receiver) {
    if (Reflect.has(target, name)) {
      return Reflect.get(target, name, receiver);
    } else {
      for (let P of target[Symbol.for("[[Prototype]]")]) {
        if (Reflect.has(P, name)) {
          return Reflect.get(P, name, receiver);
        }
      }
    }
  },
};

const hero = new Proxy(
  {
    name: "hero",
    strike() {
      this.run();
      this.fight();
    },
  },
  handler
);

hero[Symbol.for("[[Prototype]]")] = [people, powerMan];
hero.strike();
// --> people.run:hero
// --> powerMan.fight:hero
```

## ts

### 高级类型

改为选填Partial<User>

改为必填Required<User>

过滤Pick<User, 'age'>

排除Omit<User, 'age'>

排除Exclude<'a' | 'b', 'b' | 'c'>

交集Extract<'a'|'b', 'a'|'y'|'z'>

参数类型的元祖Parameters

Record<K, V>，将V作为整体当成value，key类型为K，生成新的类型，对象嵌套对象

ConstructorParameters，构造函数参数类型的元组

NonNullable<T>，从类型T中剔除null和undefined，然后构造一个类型。

ReturnType<T>，由函数类型T的返回值类型构造一个类型。

infer：表示待推断的类型变量

// 由函数类型T的返回值类型构造一个类型。

其他技巧：

合并 &

[K in keyof Modules]

typeof

### 常用技巧

```js
interface NewAble<T> {
  new (...args: any[]): T;
}
```

## 浏览器

功能检测：通过判断浏览器是否支持某段代码来决定运行不同的代码

功能推断：也是对代码可用性的检查，检查过后还会使用其他功能，不推荐

UA字符串：可以让对方识别请求用户代理的类型，navigator.userAgent可以获取，但是很难解析，并且具有欺骗性

### 事件流

DOM事件的处理级别

DOM0行内模型和脚本模型，跨浏览器，绑定速度最快，只能绑定一个函数，只支持冒泡

DOM2addEventListener，参数3true表示捕获false冒泡（默认），都存在先捕获后冒泡，可以绑定多个函数

### http

1. 浏览器工作过程

简单版：

输入网址回车，先做一些准备工作，检查能不能访问互联网--通过DNS服务器解析域名得到ip地址？-- 建立TCP连接 -- 发送http请求，用到了路由技术找到机房--通过反向代理发送到对应服务器，服务器处理请求--原路返回html响应 -- 解析数据处理html页面--请求其他资源--绘制界面

http工作过程：

一次http操作是一次事务，首先客户机和服务器要建立一个tcp连接，连接建立后客户机开始给服务端发送请求，请求的格式为请求行，请求头和请求体，请求行包括请求方法名、统一资源标识符(URI)、协议版本号，请求头：头字段，MIME信息，包括请求修饰符、客户机信息等，服务器返回响应信息，格式为响应行，响应头和响应体，响应行包括信息的协议版本号、响应状态代码和文本描述，响应头：头字段，MIME信息，包括服务器信息，客户端收到响应展示页面，最后断开连接

以上是短连接请求过程，长连接包括多次请求和响应

详细版：

浏览器标准处理流程，从请求发出到响应回来渲染到浏览器navigation timing，api用来分析性能，通过每个过程上面的标签来计时

浏览器处理

1提示卸载，卸载上一页，可以看作初始化，navigationStart

2本地重定向（查看本地缓存），没有跳过，redirectStart/redirectEnd，同时并发执行卸载上一页unloadStart/unloadEnd，可能出现性能瓶颈的位置，unload事件中执行的事情

3有缓存时获取缓存，读文件，属于IO操作，也是瓶颈位置，fetchStart

网络操作

4DNS，获取ip，标签是domainLookupStart/domainLookupEnd，也是瓶颈位置，底层传输层协议UDP，有不同的镜像服务器有的远有的近，跨网的时候会慢，还有带宽和地理上的影响，通过CDN优化，就近原则

5TCP，建立连接三次握手，connectStart/connectEnd，瓶颈位置，受到网络影响

6请求，发送请求，requestStart，请求结束没办法界定，因为navigation timing跑在客户端，所以这部分包含了服务器响应的时间

7响应，收到响应，responseStart/responseEnd，这里长可能是数据过大或网络链路不好，可以开启压缩或者架设镜像服务器

浏览器

8processing，流转成文本，转成dom，处理dom，domLoading转化/domInteractive处理/domContentLoaded加载/domComplete完成

9触发onLoad事件，loadEventStart/loadEventEnd



2. DNS解析过程

DNS解析会先查找缓存依次是浏览器缓存1000个左右，系统缓存，路由器缓存，ISP（互联网服务提供商）DNS缓存

域名很多为了加快解析，分到了多个服务器，不同等级的域名归不同的服务器管（分治），分根服务器，TLD服务器，名称服务器（负责一级域名以后的），客户端路由器收到DNS解析请求以后会把域名发到DNS服务器（路由器内置，经过路由器中转到DNS服务器），DNS服务器有一个缓存，先查看有没有缓存，没有的话先从根服务器处理顶级域名（全球有13个），查到以给定顶级域名结尾的一级域名归哪个TLD服务器，返回这个服务器ip给DNS服务器，DNS再给TLD服务器发送第二个请求，返回名称服务器ip，DNS再发送第三次请求，名称服务器会找到最终的ip返回。由于通信较多所以没有用TCP

过程中的优化包括，DNS的缓存，还有大数据库的镜像，减少通讯，阿里云等买到域名设置好了ip之后会有一个提示，十分钟之内同步，就是将解析记录主动同步到镜像



3. CDN

解决问题：分散所有客户端请求同一个服务器的数据请求压力，使用镜像服务器，依赖DNS使用就近原则解析到最近的镜像，比如每个区域解析到的ip不是同一个，取决于网络环境



2. HTTP协议

超文本传输协议，为了统一计算机的通信方式而产生的，规定了客户机和服务机之间请求和响应的方法

请求方法：GET，POST，DELETE，PUT，UPDATE，TRACE，HEAD，CONNECT

请求与响应的组成：

请求，请求行（请求方法，资源标识符，协议版本号）请求头（MIME信息）请求体

响应，响应行（协议版本号，状态码，描述文本）响应头（MIME信息）响应体

常用请求头响应头

accept，cookie，referer，authorization，user-agent

connection，cache-control，expire，last-modified

状态码

1xx：请求已经成功接受

2xx：请求成功

3xx：重定向，301永久，302临时，304缓存生效

4xx：客户端错误，400报文语法错误，401没有权限，403服务端拒绝访问，404未找到资源，413请求实体过大（一般出现在上传文件，修改客户端请求大小和缓存大小）

5xx：服务端错误，500执行时出错，502内部网关错误，一般是nginx

早一点的0.9版本已经有了最基本的语义和规则，1.0基本完整稳定，1.1成熟，增加了**长连接**（TCP），2改变了底层机制，TCP的实现层面 ，很多网站已经迁移到了2，看协议头可以看出1和2，带冒号的伪头，重新设计了协议封装

**HTTP1.1**

- keep-alive，长连接

在一定时间内，同一个域名多次请求数据，只建立一次HTTP连接，其他请求复用连接通道，提高效率，一定时间是可以配置的，1.1还存在效率问题，文件的串行传输和浏览器连接数限制，HTTP2的多路复用对此进行了优化

**HTTP2**

语义没有改变，改变了协议的实现

- 改变了数据的封装格式，之前是文本不稳定解析容易出错，改成了二进制形式更紧凑，解析更高效

- 引入分帧层，无法兼容，产生了伪头

将消息分成了更小的消息和帧，比如之前的请求行请求头请求体之间没有明显的区分，现在分成两帧头帧和数据帧，界限明显用了二进制的分割符，头有专门描述头的长度的字段，来计算偏移量。更加的严密了

伪头字段，没有请求行请求头，都封装到头帧里了，但是还得是键值对模式让浏览器进行处理所以使用伪头代替了请求行和请求头，本质是因为数据的封装格式变化了

- **压缩报头**，之前只是压缩报文体，不压缩头

- **多路复用**，一个TCP连接可以并行传输多个文件，之前是串行

之前可以并发发起多个请求，每个请求都需要建立连接，服务器压力变大，需要维护每个连接，HTTP2的多路复用对同一个域名下的所有请求都是**基于流和二进制数据帧**的，帧对数据进行顺序标识，所以只需要一个连接，可以并发传输多个数据，解决了1.1并发连接数的限制。

Apache最大连接数是300。1.1要想在一个连接发送多个数据是串行的，会产生队首阻塞，多路复用会把文件切成小块轮流发送，在另一端重新组装，看起来像是并行传输，也会产生阻塞但是只阻塞了当前文件，其他文件不受影响，有一定的优化。阻塞是由于TCP的特性产生的，在TCP层面是无法解决的。

阻塞的主要原因是基于链路，两层链路TCP和TLS，加密以文件为单位，解密需要等完整的文件传输过来，所以会有当前文件的阻塞问题

HTTP3完全解决了阻塞

- 服务器**主动推送**，减少请求延迟

比websocket轻量，不能完全取代websocket，只是在推送方面取代，websocket是双向的，http是基于请求和响应，相当于一次请求多次响应

- 默认使用加密

**HTTP3**

解决了队首阻塞，发包时没有顺序，有一个编号，**以包为单位**，所有收到以后组装时发现有丢包要求重发，加解密也是以包为单位，不存在阻塞问题

基于QUIC，QUIC基于UDP，为了解决性能问题，同时也很严密，对数据包进行加密，不是链路加密

跨多层实现属于会话层和安全层

- 减少了握手的延迟，一次握手（首次通信，探查服务器在不在）或不握手（1TTR或0TTR），切换网络也不需要重新握手，因为没有链路
- 更灵活的多路复用，没有链路，没有阻塞
- 连接迁移，切换网络时连接不会断开，适用于移动端



3. 反向代理

正向代理，类似代购，反向代理，类似门房

nginx，c语言写的

用途：加密（配置HTTPS）和SSL加速，负载均衡（CDN），缓存静态文件，压缩，减速上传（有选择的丢包，延迟响应），安全，相当于一层堡垒给解决争取时间，外网发布（整合各种服务到同一个端口）



3. TLS握手

主要是协商加密算法，交换证书，交换密钥，切换到加密

TCP握手

客户端发送支持的协议版本，加密算法和压缩方法，和一个随机数

服务端确定协议版本，加密算法和压缩方法，返回给客户端，和一个随机数

服务端发送证书

服务端通知协商结束

客户端通过服务端公钥加密公钥和密钥种子（大随机数）发送给服务端

双方计算密钥（利用三个随机数）

客户端通知切换加密

客户端准备完成

服务端通知切换加密

服务端准备完成

加密通信

通信完成后切断SSL

TCP挥手



使用非对称加密交换密钥，使用对称加密进行通信



3. TCP和UDP

滑动窗口：

TCP的可靠传输是在传输层上完成的，但是发送报文等待确认确认后再发送下一个报文的效率非常低下，滑动窗口是为了解决这个问题

滑动窗口允许发送方连续发送多个报文，根据对方接受窗口大小限制发送方的发送速率，防止拥堵

本质是维护了几个变量，同时在发出或收到报文时对这几个变量进行维护

TCP是双全工，双方都包含了发送窗口和接收窗口



2. HTTP缓存

分为强缓存和协商缓存，都是通过http header实现

强缓存优先于协商缓存

第一次请求没有缓存，服务器设置cache-control和expires或者etag和last-modified并返回资源

再次请求时，先检查强制缓存是否过期未过期不会发起请求直接从缓存中获取，状态为200

强缓存过期后进行协商缓存，依次发送文件上的etag/last-modified，头字段if-none-match/if-modified-since，服务器判断与自己维护的内容md5/时间戳是否相同，相同时使用浏览器缓存时返回304，否则说明资源变化返回最新数据状态200，然后重新进行缓存协商



3. TCP握手/挥手

**三次握手**

不包含数据

客户端发起连接请求，SYN置为1，顺序号seq=x，进入SYN_SEND状态等待服务器确认

服务端响应握手包发送SYN报文，位置为1，顺序号seq=y，应答号ACK=x+1，进入SYN_RECV状态，客户端收到应答号，客户端能确认服务器能收到自己的数据，达到半连接，半连接不能保证服务器能收到客户端的数据

客户端发送应答号ACK=y+1，进入ESTABLISHED状态，服务器收到应答号，服务端能确认客户端能收到自己的数据，达到全连接

三次交互保证对方可以正确得接收自己的数据，防止服务器端收到已经过期的连接请求，进行响应，由于客户端没有发送请求收到响应也不会做出反应，服务端就会一直处于等待状态，浪费资源

两次握手（半连接）的问题：如果客户端不断发起连接请求，服务端需要维护的连接数据越来越多，由于服务器还需要遍历数组，维护连接超时，数据过多时服务器会拒绝服务，这是拒绝服务攻击的一种，半连接攻击，缩短超时间可以缓解但是不能解决问题解决：防火墙，堆硬件

**四次挥手**

一般是客户端发起断开

收到断开请求后马上返回，然后做收尾工作，最后再发送断开请求，所以响应和FIN请求分成两次发送

客户端发送FIN指令，顺序号seq=x+2，应答号ACK=y+1

服务器立刻响应，应答号ACK=x+3

服务器做完收尾工作后发送FIN指令，顺序号seq=y+1

客户端收到后响应，应答号ACK=y+2，至此连接断开



`======其他相关题目======`

1. 图片资源为什么放在不同的域名下面

浏览器对并发请求的数目限制是针对域名的，即针对同一域名（包括二级域名）在同一时间支持的并发请求数量的限制。如果请求数目超出限制，则会阻塞。因此，网站中对一些静态资源，使用不同的一级域名，可以提升浏览器并行请求的数目，加速界面资源的获取速度。



2. 浏览器与服务器建立一个TCP连接后，是否会在完成一个http请求后断开？什么条件下会断开？

`HTTP/1.1`将`Connection`写入了标准，默认值为`keep-alive`。默认情况下建立的TCP连接不会断开，只有在请求头中设置`Connection: close`才会在请求后关闭TCP连接。



3. 一个TCP连接可以同时发送几个HTTP请求？

`HTTP/1.1`中，单个TCP连接，在同一时间只能处理一个http请求，虽然存在Pipelining技术支持多个请求同时发送，但由于实践中存在很多问题无法解决，所以浏览器默认是关闭，所以可以认为是不支持同时多个请求。

`HTTP2`提供了多路传输功能，多个http请求，可以同时在同一个TCP连接中进行传输。



4. 浏览器http请求的并发性是如何体现的？并发请求的数量有没有限制？

页面资源请求时，浏览器会同时和服务器建立多个TCP连接，在同一个TCP连接上顺序处理多个HTTP请求。所以浏览器的并发性就体现在可以建立多个TCP连接，来支持多个http同时请求。

Chrome浏览器最多允许对同一个域名Host建立6个TCP连接，不同的浏览器有所区别。

如果图片都是HTTPS的连接，并且在同一域名下，浏览器会先和服务器协商使用`HTTP2`的`Multiplexing`功能进行多路传输，不过未必所有的挂在这个域名下的资源都会使用同一个TCP连接。如果用不了HTTPS或者HTTP2（HTTP2是在HTTPS上实现的），那么浏览器会就在同一个host建立多个TCP连接，每一个TCP连接进行顺序请求资源。



5. 多个域名存储网站资源的优点

- 动静分离，方便CDN缓存
- 突破浏览器最大并发数，6个左右
- 节约cookie带宽
- 节约主域名连接数，提高客户端带宽利用率，优化页面响应速度
- 避免不必要的安全问题，比如cookie隔离



### 渲染

1. 渲染原理

总体过程：

渲染部分通过html生成dom树，子资源加载，样式表计算，布局，绘制

主要参与模块：html解析器，css解析器，这两个在webcore中，js解释器（jscore或v8）

具体就是浏览器获取到html后，先进行字节流解码把字节数据转换为字符，包括一些字符的预处理，然后通过词法分析将字符串转化为标记同时生成dom树

遇到css时解析css，结构化css，不是树结构，是按照一定的数据结构生成css片段，在dom树上找到对应的节点，与css片段进行关联匹配，生成渲染树

如果遇到js，html解析器会暂停工作，将js给js解释器解析，js可以以桥接机制影响dom树和渲染树，js解析完成后html解析器继续工作

在渲染树的基础上加上布局规则一层一层得叠加生成布局渲染树，就是一个排版的过程

最后进行绘制，将数据显示到显示器上，需要调用显示后端，控件，字体，图形库视频解码库等，将视口里的内容映射到显示器上，就是计算像素点，通过显卡描到显示器上，一个图片就是一帧

以谷歌浏览器为例：

chrome是多进程浏览器，主进程就是浏览器进程，其他为子进程，比如插件进程，渲染由渲染进程负责，有多个一个域名是一个渲染进程，包括主线程和一些工作线程，js就跑在工作线程下，排版和栅格线程也在这个进程内运行

渲染过程：通过网络请求获取资源，html解析器开始解析根据html结构生成dom树，处理css片段生成数据结构，找到对应节点进行匹配关联生成渲染树，接下来进行排版就是计算每个节点的大小坐标和相对位置，基于根节点计算，生成排版树，然后进行一层一层合成生成层树，这些都在在主线程

一旦创建了层树确定了绘制顺序，就开始由GPU生成图，根据层树一个点一个点计算的，这里有一个优化，就是GPU把整个渲染任务进行分解，分成一个个小tile，通过GPU的各个核进行并行计算，计算完成之后将数据集中到显卡的显存里，显存将数据直接显示到显示器上，从屏幕左上角依次排列，速度很快具体取决于刷新率



2. 重绘重排

涉及到渲染的排版和绘制过程：重排 - 重绘 - 合成层

对dom元素进行分层，计算图形样式calculate style，对每个节点计算图形位置layout，将节点绘制填充到图层中paint，将图层作为纹理（CPU给GPU最小的一个bitmap）上传给GPU，GPU做一些旋转缩放什么的

GPU的合成层线程（composite layers）将符合的图层生成屏幕图像，具体工作：

主线程把绘制列表commit到合成线程

合成线程根据视口切成tile，比如256*256

栅格线程将小图块生成位图，也叫栅格化，保存到GPU

合成线程发送一个绘制图块的命令draw quad给浏览器进程

浏览器的viz组件接受命令，最终显示到屏幕上display

对GPU位图进行旋转缩放的时候，首次合成会有一个低分辨率的图，显示的时候会全部显示

可以独立成层的属性：根元素，position，transform，半透明，css滤镜，canvas，video，overflow

GPU可以加速的独立层：css3d，vidoe，webGL，transform，css滤镜，会跳过布局layout和绘制paint阶段（重绘重排）直接进入GPU合成层，比如淘宝轮播图使用translate的translate3d，也叫硬件加速

会造成重排的属性：读offset，scroll，client，width，盒子模型大小变化，浏览器会维护一个重绘重排队列等积累到一定数量或时间会进行批处理，但是遇到这些属性会放弃掉优化队列直接进行重排，box-sizing：border-box也是为了尽量减少外界对盒模型的影响

为了避免频繁的flash，可以将读写分别放在一起，不破坏浏览器的优化，或者使用requestAnimationFrame下一帧再写



### websocket

由于底层依赖TCP的不稳定性，需要设计一整套保活，验活，重连方案

心跳重连，原生的websocket断开连接时不会触发任何事件，前端需要定时发送ping，如果后端没有返回pong，前端就会执行重连

```js
let socket; //websocket的实例
let lockReconnect = false; //避免重复连接

//新建websocket的函数 页面初始化 断开连接时重新调用
const getwebsocket =  ()=> {
    let wsUrl = 'ws://ip';
    socket = new WebSocket(wsUrl);
    // 绑定一些事件，onerror,onclose,onopen，onmessage
    // 如果希望WebSocket 连接一直保持，可以在close或者error上绑定重连方法
    // 这样一般正常情况下失去连接时，触发onclose方法，就能重连了。
    socket.onerror = function(event) {
        console.log('websocket服务出错了');
        reconnect(wsUrl);
    };
    socket.onclose .= function(event) {
        console.log('websocket服务关闭了');
        reconnect(wsUrl);
    };
    socket.onopen = function(event) {
        heartCheck.reset().start(); //传递信息
    };
    socket.onmessage = function(event) {
        //如果获取到消息，心跳检测重置
        //拿到任何消息都说明当前连接是正常的
        console.log('websocket服务获得数据了');
        //接受消息后的UI变化
        doWithMsg(event.data);
        heartCheck.reset().start();
    };
    //收到消息推送
    function doWithMsg(msg) {
        //执行业务代码.....
    }
}

// 重新连接
const  reconnect = (url)=> {
    if (lockReconnect) return;
    lockReconnect = true;
    //没连接上会一直重连，设置延迟避免请求过多
    setTimeout(function() {
        getwebsocket();
        lockReconnect = false;
    }, 2000);
}

//心跳检测
let heartCheck = {
    timeout: 60000, //60秒
    timeoutObj: null,
    serverTimeoutObj: null,
    reset: ()=> {
        clearTimeout(this.timeoutObj);
        clearTimeout(this.serverTimeoutObj);
        return this;
    },
    start: ()=> {
        let _this = this;
        this.timeoutObj = setTimeout(()=> {
            //这里发送一个心跳，后端收到后，返回一个心跳消息，
            //onmessage拿到返回的心跳就说明连接正常
            socket.send("心跳测试");
            //如果超过一定时间还没重置，说明后端主动断开了
            _this.serverTimeoutObj = setTimeout(function() {
              //这里再onclose里执行了reconnect，
              // 所以这里检测到超时之后，执行socket.close()就触发了onclose，进而就执行了reconnect。
              socket.close();
            }, _this.timeout)
        }, this.timeout)
    }
}
```

当连接上时就开始计时，在一定范围内获取到后端信息，重置倒计时，超过60s执行心跳检测



## BFF

主要应用在多端应用，减少前后端协同成本，用于接口的整合编排、字段裁剪，服务端渲染直出提升首屏性能。

日志系统

容错处理

## 工程化

一切以项目的性能，稳定性，可用性，可维护性，注重开发效率，运行效率的同时，保证维护效率为目标的工作都是工程化

包括模块化，组件化，合理地加载静态资源（性能优化），规范化，自动化

典型的工作流：开发，测试，构建，部署，监控

开发阶段：脚手架，公共库，包管理器，编辑器，代码检查，构建工具，调试套件

测试阶段：测试框架，自动化测试工具，性能测试工具

构建阶段：打包构建

部署阶段：发布平台，迭代管理平台

监控阶段：埋点平台

### 进程和线程

进程，进程执行在cpu和内存中，执行一个程序时操作系统将程序文件读取到内存中，操作系统找到程序的执行入口，将指令交给cpu去执行，单个cpu一次只能执行一个程序，所以不会一直执行统一个程序，操作系统会对cpu执行时间进行调度，看起来像是并行。进程代表cpu所能处理的单个任务，好比工程的车间，线程就像车间的工人，协作完成同一个任务。一个进程可以包含多个线程，进程内内存共享，所有线程都可以使用，但不能同时使用，此时的内存管理方法有互斥锁（mutex，一个锁一个钥匙）和信号量（semaphore，一个锁多把钥匙）

进程：线程的容器，资源分配调度的最小单位，程序是指令数据，数据及其组织形式的描述，进程是程序的实体

线程：系统进行运算调度的最小单位，是进程中的实际运作单元，一条线程指进程中的一个单一顺序的控制流

简单来说：

进程指系统运行的一个应用程序，是资源分配的最小单位

线程是系统分配处理器时间单元的基本单位，或者是进程中独立执行的最小单位

### 组件化

尽可能解耦，用多组件组合或HOC的形式

#### AutoComplete组件设计

考虑通用性，可移植性和扩展性，组件粒度要小，还有安全性

由文本框，搜索按钮和扩展区

文本框事件focus，blur，change，按钮事件search，扩展区通过props.children或slot

安全性，将输入进行转义后提交

性能问题通过防抖来限制

其他功能：清空

### CSS组织

cssModule：css-loader配置

postcss：集成模块化，css in js，autoprefix，css-next等众多功能，原理通过ast分析css

less/sass/stylus：css预处理器

模块化的实现：

使用命名规范防止类名污染，比如BEM

使用cssModule，打包时类名转换hash值，书写不变，模块化饮用，难以与外部样式混合使用

使用css in js，css放在组件内部，最有名的是styled-components，css内联在js中书写，不能使用预处理器

### 状态树设计

状态树可以理解为redux中的store，个人理解类似于设计数据库

把相互嵌套又关联的数据视为数据库，将数据按范式化存储，使数据更加扁平

数据项只在一个地方定义，便于更新（避免多次更新同样的数据和更新不必要的数据），然后通过id进行相互关联

### 项目架构

#### CI/CD

必要性：减少人工失误，减少成本

#### next/nuxt同构原理

代理a链接通过header判断是站内切换还是刷新，站内切换的情况下，使用node操作dom实现html的局部更新，关于js，无论之前有没有加载过js，切换到这个页面，js都可能会缺失，可以在webpack插件中给指定的js加上标识，通过自定义插件给业务js添加的lazyload-js标识找到需要的js进行bigpipe输出，还可以在这里做缓存，不通过请求直接从localStorage中拿js，在前端执行

#### vue/react SSR

首屏SSR+内部spa路由跳转

两个入口，服务端和客户端分别打包，服务端bundle返回app，store和router，vue提供createSSRApp方法用来生服务端渲染的应用，服务端获取打包好的服务端代码，注入预加载的数据后替换模版的内容

数据预加载，vue提供serverPrefetch方法，只在服务端执行，用这个方法获取数据，在服务器替换模版时注入全局变量，客户端获取并替换store

### 打包

#### vite

- 和webpack对比：

webpack 先打包，服务器返回打包结果，vite 请求某一模块时才**实时编译**，**利用了现代浏览器es module**自动请求依赖模块的特点，也因为启动时不需要打包，所以不需要分析依赖，不需要编译，速度就很快。

热更新方面当改动了一个模块后，仅需让浏览器重新请求该模块即可，不像 webpack 那样需要把该模块的相关依赖模块全部编译一次，**效率更高**。

当需要打包到生产环境时，vite 使用传统的 **rollup 进行打包**。因此，vite 的主要优势在开发阶段。

实际项目中很少用到vite

- 为什么快：

使用 **esbuild** 进行编译，因为 esbuild 是用 **Golang 编写**的，自然比用 JavaScript 编写的构建工具快很多。同时 esbuild 中的**算法**经过精心设计充分利用 CPU 资源。另外，esbuild **没有使用第三方依赖**，和内存高效利用，也是打包快的原因。

- 为什么用的少：

在生产环境仍然需要使用 Rollup 打包。因为**嵌套 import** 会导致发送大量网络请求，即使使用 HTTP/2.0 ，直接使用未打包的 ESM 仍然效率低下。所以为了在生产环境中获得最佳的加载性能，最好将代码 bundle 一遍（结合 Tree Shaking，lazy-loading 和 common chunk splitting 等技术手段）。

另外，开发环境使用浏览器 ESM 解析模块，而生产环境使用 Rollup 打包，这就导致本地和线上环境跑的**代码不一致**，线上环境出了 bug，本地很难排查。

Vite **更像是一个开发工具**，而不是用于生产环境的构建工具。基本上只有浏览器支持完全和基于 QUIC 协议的 HTTP/3 普及之后才可能大规模使用 ESM 。更何况 Webpack 发展至今 loader 和 plugin 生态已经十分丰富，而 bundleless 构建工具的生态还在起步阶段。

#### webpack 

- 为什么需要打包：

http1.1时期受网络延迟和浏览器**并行请求限制**等原因，将资源合并压缩有助于减少 HTTP 请求从而提升页面性能。

es module之前没用**模块系统**，webpack实现了一套模块系统，提供了 HMR 机制等，极大的提升了开发体验。

- 缺点：主要是慢

打包时需要构建模块依赖图，因此需要**递归遍历**所有的模块，大项目会很慢。

修改文件需要**重新打包**

打包后会对源码进行编译和压缩，可读性大大降低，开发环境下，我们借助 **SourceMap** 进行调试，大大降低打包速度。

过大的包会延长**页面首屏加载时间**，对此 Webpack 也有解决方案，即使用 Tree Shaking、Lazy-loading、CommonsChunkPlugin 等。

- 不打包的趋势

首先主要的原因是 HTTP/2.0 实现了**多路复用和首部压缩**，解决了 HTTP/1.1 中队头阻塞的问题，因此通过资源合并压缩减少了 HTTP 请求对页面加载性能不会有显著提升了。

其次，现在各大浏览器逐一支持 ESM，无需自己再实现模块化优化了。可以实现按需加载，不用打包了，启动很快，只需要启动 devServer 即可。

和 Snowpack 类似，Vite 也是利用浏览器原生的 ESM 去解析 imports，然后向 devServer 请求模块，在服务器端使用 esbuild 对浏览器无法处理的文件模块进行即时编译后返回。

##### 插件

postcss：集成模块化，css in js，autoprefix，css-next等众多功能

##### loader

css：css-loader，可以开启模块化

##### 模块加载原理4.x

代码参考demoCollection/learnWebpack

每个文件都是一个模块，打包后统一使用自定义的模块规范管理

```js
// commonjs规范代码打包
// index.js
const test2 = require("./test");
function test() {}

test();
test2();

// ./test
function test2() {}

module.exports = test2;

// 打包后：一个立即执行函数，传入对象，key是文件路径，value是文件内容
// 简化后：
// (function (modules) {})({
//   path1: function1,
//   path2: fucntion2,
// });

// 1. 定义缓存模块对象
// 2. 实现模块加载函数__webpack_require__
//  	2.1 判断缓存
//  	2.2 新建一个module放入缓存
//  	2.3 执行路径对应的模块函数，参数module，module.exports，__webpack_require__
//  	2.4 模块标识为已加载
//  	2.5 执行完成后返回exports对象
// 3. ...
// 4. 使用__webpack_require__加载入口函数
/******/ (function (modules) {
  // webpackBootstrap
  // The module cache
  //   模块缓存对象
  var installedModules = {};
  // The require function
  //   webpack 实现的require()函数
  function __webpack_require__(moduleId) {
    // Check if module is in cache
    // 如果模块已经加载过，直接返回缓存
    if (installedModules[moduleId]) {
      return installedModules[moduleId].exports;
    }
    // Create a new module (and put it into the cache)
    // 创建一个新模块，并放入缓存
    var module = (installedModules[moduleId] = {
      i: moduleId,
      l: false,
      exports: {},
    });
    // Execute the module function
    // 执行模块函数
    modules[moduleId].call(
      module.exports,
      module,
      module.exports,
      __webpack_require__
    );
    // Flag the module as loaded
    // 将模块标识为已加载
    module.l = true;
    // Return the exports of the module
    return module.exports;
  }
  // expose the modules object (__webpack_modules__)
  // 将所有的模块挂载到 require() 函数上
  __webpack_require__.m = modules;

  // expose the module cache
  // 将缓存对象挂载到 require() 函数上
  __webpack_require__.c = installedModules;
  // define getter function for harmony exports
  __webpack_require__.d = function (exports, name, getter) {
    if (!__webpack_require__.o(exports, name)) {
      Object.defineProperty(exports, name, {
        enumerable: true,
        get: getter,
      });
    }
  };
  // define __esModule on exports
  __webpack_require__.r = function (exports) {
    if (typeof Symbol !== "undefined" && Symbol.toStringTag) {
      Object.defineProperty(exports, Symbol.toStringTag, {
        value: "Module",
      });
    }
    Object.defineProperty(exports, "__esModule", { value: true });
  };
  // create a fake namespace object
  // mode & 1: value is a module id, require it
  // mode & 2: merge all properties of value into the ns
  // mode & 4: return value when already ns object
  // mode & 8|1: behave like require
  __webpack_require__.t = function (value, mode) {
    if (mode & 1) value = __webpack_require__(value);
    if (mode & 8) return value;
    if (mode & 4 && typeof value === "object" && value && value.__esModule)
      return value;
    var ns = Object.create(null);
    __webpack_require__.r(ns);
    Object.defineProperty(ns, "default", {
      enumerable: true,
      value: value,
    });
    if (mode & 2 && typeof value != "string")
      for (var key in value)
        __webpack_require__.d(
          ns,
          key,
          function (key) {
            return value[key];
          }.bind(null, key)
        );
    return ns;
  };
  // getDefaultExport function for compatibility with non-harmony modules
  __webpack_require__.n = function (module) {
    // 判断是否esmodule
    var getter =
      module && module.__esModule
        ? function getDefault() {
            return module["default"];
          }
        : function getModuleExports() {
            return module;
          };
    __webpack_require__.d(getter, "a", getter);
    return getter;
  };
  // Object.prototype.hasOwnProperty.call
  __webpack_require__.o = function (object, property) {
    return Object.prototype.hasOwnProperty.call(object, property);
  };
  // __webpack_public_path__
  __webpack_require__.p = "";
  // Load entry module and return exports
  // 加载入口模块，并返回模块对象
  return __webpack_require__((__webpack_require__.s = "./src/index.js"));
})({
  "./src/index.js": function (module, exports, __webpack_require__) {
    eval(
      // 格式化：对比源代码，require直接改为了__webpack_require__，说明完全适配
      // const test2 = __webpack_require__("./src/test2.js");
			// function test() {}
			// test();
			// test2();
			//# sourceURL=webpack:///./src/index.js?
      'const test2 = __webpack_require__(/*! ./test */ "./src/test.js");\nfunction test() {}\n\ntest();\ntest2();\n\n//# sourceURL=webpack:///./src/index.js?'
    );
  },

  "./src/test.js": function (module, exports) {
    eval(
      "function test2() {}\n\nmodule.exports = test2;\n\n//# sourceURL=webpack:///./src/test.js?"
    );
  },
});

// es6模范打包
// index.js
import test2 from "./test";
function test() {}
test();
test2();

// test.js
export default function test2() {}

// 打包后，基本与上面一样，只有文件代码不同
// 多了__webpack_require__.r(__webpack_exports__); // 给__webpack_exports__加一个属性__esModule为true，__esModule用来处理混合使用commonjs和import的情况
// __webpack_require__.d() // 给__webpack_exports__导出变量用，相当于__webpack_exports__['default'] = test2
{

  /***/
  "./src/index.js":(function (module, __webpack_exports__, __webpack_require__) {
      "use strict";
      eval(
      	// 格式化：
        // __webpack_require__.r(__webpack_exports__);
        // var _test2__WEBPACK_IMPORTED_MODULE_0__ = __webpack_require__("./src/test2.js");
        // function test() {}
        // test();
        // Object(_test2__WEBPACK_IMPORTED_MODULE_0__["default"])();
        //# sourceURL=webpack:///./src/index.js?
        "__webpack_require__.r(__webpack_exports__);\n/* harmony import */ var _test__WEBPACK_IMPORTED_MODULE_0__ = __webpack_require__(/*! ./test */ \"./src/test.js\");\n\nfunction test() {}\ntest();\nObject(_test__WEBPACK_IMPORTED_MODULE_0__[\"default\"])();\n\n//# sourceURL=webpack:///./src/index.js?"
      );

    }),

  "./src/test.js":(function (module, __webpack_exports__, __webpack_require__) {
      "use strict";
      eval(
      	// 格式化：
        // __webpack_require__.r(__webpack_exports__);
				// __webpack_require__.d(__webpack_exports__, "default", function () {
				//   return test2;
				// });
function test2() {}
//# sourceURL=webpack:///./src/test2.js?
        "__webpack_require__.r(__webpack_exports__);\n/* harmony export (binding) */ __webpack_require__.d(__webpack_exports__, \"default\", function() { return test2; });\nfunction test2() {}\n\n//# sourceURL=webpack:///./src/test.js?"
      );
    })
}
```

**按需加载**：webpack使用import和require.ensure来引入需要动态引入的代码

直接使用import引入的代码会单独打包

打包出的代码分析：

installedChunks，缓存动态模块，对象，{id: state}

jsonpScriptSrc，根据ID生成URL

\__webpack_require__.e，import被打包成了这个函数

- 查看缓存对应状态是否为0，0表示加载成功，第一次是undefined
- 不是0或undefined，表示加载中，将这个promise推入promise数组
- undefined，新建promise，用于加载动态引用的模块
- 生成script，使用jsonpScriptSrc生成的url
- 设置2分钟的超时时间，onScriptComplete处理超时错误
- 添加到页面，开始加载模块
- 返回promise数组

window["webpackJsonp"]，存储需要动态导入的模块，包含模块id，路径名和内容，push方法重写为webpackJsonpCallback

当js下载完成后就会自动执行文件内容，即下载完0.bundle.js就会执行window['webpackJsonp'].push()即webpackJsonpCallback

- id对应的promise执行resolve，状态置为0

总体流程：

- 重写push
- 入口模块使用\__webpack_require__.e下载动态资源
- 下载完成后执行window['webpackJsonp'].push()即webpackJsonpCallback
- 执行`__webpack_require__.e`后的then调用`__webpack_require__`真正开始加载代码

#### babel

原理：

解析Parse：将代码经过词法分析和语法分析解析生成抽象语法树，通过babylon

转换Transform：进行一些列变换操作，通过babel-traverse遍历，在这个阶段转换为es5代码

生成Generate：将AST转换为js，使用到babel-generator

#### 其他

npm run start自动更新插件

`"prestart": "npm update a b c" // 注意版本号控制，推荐使用~`



## 性能优化



### 生产环境优化

#### 页面加载

spa/csr，预渲染，mpa/ssr，同构

spa/csr，FP最快，客户端用户体验好，内存数据共享，SEO差，FCP慢，白屏

预渲染，FCP比csr快，客户端用户体验好，内存数据共享，SEO差，FMP慢

mpa/ssr，SEO好，首屏性能高，FMP快，数据共享成本高，模版维护成本高，可见不一定可操作，开发条件受限，资源重复加载，index重，可以使用bigpipe优化

同构，SEO好，首屏性能高，FMP快，用户体验好，数据共享，代码公用，node容易形成性能瓶颈

- 减少请求数量，后台合并接口，合理控制模块的大小，base64
- 减少请求结果的大小，压缩

- 减少白屏时间

白屏时间指的是页面准备加载到收到服务器返回的这段时间，这段时间过长就会产生白屏现象，在spa中尤为明显，以vue为例，浏览器加载完index.html后并不能看到页面，以为它只是一个框架没有实际内容，加下来还要加载vue，相关库，webpack公用文件，mainjs，发送请求，构建虚拟dom，diff，将虚拟dom patch到页面，初始化事件引擎等完成之后才能看到页面进行操作

优化办法：quicklint，guess，骨架屏，HTTP2等

quicklint：

使用ssr

- SSR优化

bigpipe，使用文件/流输出页面而不是传统的render页面，或者将不重要的内容分成task利用流在服务端异步输出都属于bagpipe，响应头Transfer-Encoding: chunked，可以不使用koa-bigpipe等库，可以自己写，很简单

- 预加载/懒加载
- 静态页面预渲染
- CDN

控制模块的拆分和合并，每个页面引用脚本不超过6个，因为网站最多并发请求是6个（受浏览器和http版本影响），要突破限制加CDN，在1.1时是有用的，还有一个好处是CDN可以去cookie，因为每次请求都会带cookie，cookie很长浪费资源，每个CDN不超过6个文件，超过了就新开域名，每个脚本压缩后32kb左右，webpack超过30kb才会提取为单独的文件，不够的话就需要懒加载或者做缓存

- 缓存

合理设置**浏览器缓存**，强缓存一般不会用在业务上，业务上一般会关闭强缓存no-cache使用etag，多用在库上基本不会修改，业务可以使用离线缓存前端就可以管理版本不需要服务端参与，有很多大公司直接将整个网站使用service worker离线缓存，确保用户体验

做**离线缓存**前端有一个localForage库对现有的离线缓存做了封装，百度地图就通过localStorage做了离线缓存js，大概过程就是启动js时有一个全局的md5的表，可以用webpack生成，写一个active.js负责加载js，当加载js时不直接请求js而是现在缓存中查看是否有缓存，缓存中存的是两个键值对，文件名：md5文件和md5文件名：js内容，本地没有缓存时才加载文件，使用eval或者addScript执行，然后再请求一次资源，将它注入缓存。如果缓存过期会进行清理再次注入。在中间加一层版本判断还可以进行版本控制，有5m的限制某些机型是2.5m，超过了也可以使用web SQL或indexedDB，但是这个是异步的，可以用在一些不重要的内容上比如广告位

使用basketjs+localforage做离线缓存库

service worker没有大小限制，可以缓存所有文件

- prerender预渲染

打包工具完成打包后会启动一个server模拟网站运行，用无头浏览器比如puppeteer访问指定路由，得到对应的html结构并输出到指定目录，让用户首次获取html时更快看到内容。prerender-spa-plugin就是一个完成预渲染的插件

主要应用在seo和骨架屏，适用于不经常变化的数据

利于seo和弱网环境白屏，缺点就是打包速度变慢，预渲染的页面永远是上一次打包是生成的

**冷接口缓存**

- 根据网速优化

**检测用户网速**响应不同的图片，`navigator.connection`或者多普勒测速法

多普勒测速法：请求三次0kb图片，一次10k，一次40k，t1为DNS+新建连接+1RTT往返，t2新建连接+1RTT往返，t31RTT往返（三次请求同一个资源时无论是HTTP2还是1.1都会开启多路复用）10k/（t4-t3）就是带宽

- 升级为**HTTP2**
- 图片使用内存较小的格式或使用base64（css体积增大阻塞渲染）

#### 渲染过程优化

- **减少重排**

减少dom操作，使用transform代替直接修改dom

- 减少无用dom节点
- 事件代理

常用性能优化指标：

FP，第一个像素点落点

FCP，首次内容绘制，2s

LCP，最大内容绘制，页面速度指标，2.5s

TTI，可交互时间

FID，首次输入延迟，FCP-TTI之间的时间，交互体验指标，react的fiber专门优化这一点，100ms

CLS，累计位移偏移，页面稳定指标，尤其是移动端，移动距离（%）*影响距离（%）< 0.1

使用PerformanceObserver和performance.timing可以获取或计算这些指标

白屏时间：responseStart - navigationStart

首屏时间：loadEventEnd - navigationStart首次全部完整下载和渲染完页面时间

### 开发过程优化

#### 代码层面优化

节流：确保在一段时间内只执行一次，滚动

防抖：等连续操作后再执行，input

使用requestAnimationFrame优化页面滚动，保证每次重绘只会触发一次事件

```js
(function () {
  const throttle = function (type, name, obj) {
    let obj = obj || window;
    let running = false;
    const func = function () {
      if (running) {
        return;
      } 
      running = true;
      requestAnimationFrame(function () {
        obj.dispatchEvent(new CustomEvent(name));
        running = false;
      });
    };
    obj.addEventListener(type, func);
  };

  // 将 scroll 事件重定义为 optimizedScroll 事件
  throttle("scroll", "optimizedScroll");
})();

window.addEventListener("optimizedScroll", function () {
  console.log("Resource conscious scroll callback!");
});
```

#### webpack优化

### node性能优化

### 体验优化

#### 骨架屏

在进行了CDN和静态代码缓存等优化方式后，还存在首屏加载时间过长问题时，可以使用骨架屏技术提高用户体验

路由切换loading，自己编写骨架屏，推荐react-content-loader/vue-content-loader

首屏渲染优化，如果是基于vue-cli可以使用page-skeleton-webpack-plugin，否则可以使用vue-server-renderer

page-skeleton-webpack-plugin原理，通过puppeteer在服务端操控无头浏览器打开需要骨架屏的页面，在等待页面加载渲染完成后，在保留布局的前提下通过对页面元素进行增删，对已有元素进行样式覆盖，显示为灰色块，然后将修改后的html和css提取出来就是骨架屏了

具体实现：

1. 利用模版，直接在id为app的div中书写骨架屏，加载完成后会被替换，也可以使用base64图片

2. 抽离到vue文件

```js
<!-- skeleton.vue -->
<template>
  <div class="skeleton page">
    <span>骨架屏</span>
  </div>
</template>

<style scoped></style>

// skeleton.entry.js
import Vue from "vue";
import Skeleton from "./skeleton.vue";

export default new Vue({
  // 根实例简单的渲染应用程序组件
  render: (h) => h(Skeleton),
});
```

配合vue-server-renderer专门进行骨架屏的构建成json文件

```js
// webpack.skeleton.conf.js
"use strict";
const path = require("path");
const nodeExternals = require("webpack-node-externals");
const VueSSRServerPlugin = require("vue-server-renderer/server-plugin");

module.exports = {
  target: "node",
  devtool: "#source-map",
  entry: "./src/skeleton/skeleton.entry.js",
  output: {
    path: path.resolve(__dirname, "../dist"),
    publicPath: "/dist/",
    filename: "[name].js",
    libraryTarget: "commonjs2",
  },
  module: {
    noParse: /es6-promise\.js$/, // avoid webpack shimming process
    rules: [
      {
        test: /\.vue$/,
        loader: "vue-loader",
        options: {
          compilerOptions: {
            preserveWhitespace: false,
          },
        },
      },
      {
        test: /\.css$/,
        use: ["vue-style-loader", "css-loader"],
      },
    ],
  },
  performance: {
    hints: false,
  },
  externals: nodeExternals({
    // do not externalize CSS files in case we need to import it from a dep
    whitelist: /\.css$/,
  }),
  plugins: [
    // 这是将服务器的整个输出构建为单个 JSON 文件的插件。
    // 默认文件名为 `vue-ssr-server-bundle.json`
    new VueSSRServerPlugin({
      filename: "skeleton.json",
    }),
  ],
};
```

将json文件插入到模版

```js
// skeleton.js
const fs = require("fs");
const { resolve } = require("path");
const { createBundleRenderer } = require("vue-server-renderer");

function createRenderer(bundle, options) {
  return createBundleRenderer(
    bundle,
    Object.assign(options, {
      // recommended for performance
      // runInNewContext: false
    })
  );
}

const handleError = (err) => {
  console.error(`error during render : ${req.url}`);
  console.error(err.stack);
};

const bundle = require("./dist/skeleton.json");
const templatePath = resolve("./index.html");
const template = fs.readFileSync(templatePath, "utf-8");
const renderer = createRenderer(bundle, {
  template,
});

// console.log(renderer)

/**
 * 说明：
 * 默认的index.html中包含<%= BASE_URL %>的插值语法
 * 我们不在生成骨架屏这一步改变模板中的这个插值
 * 因为这个插值会在项目构建时完成
 * 但是如果模板中有这个插值语法，而我们在vue-server-renderder中使用这个模板，而不传值的话，是会报错的
 * 所以，我们去掉模板中的插值，而使用这个传参的方式，再将这两个插值原模原样返回到模板中
 *
 */
const context = {
  title: "", // default title
  meta: `<meta name="theme-color" content="#4285f4">
    <link rel="icon" href="<%= BASE_URL %>favicon.ico">
    <link rel="stylesheet" href="<%= BASE_URL %>css/reset.css">`,
};

renderer.renderToString(context, (err, html) => {
  if (err) {
    return handleError(err);
  }
  fs.writeFileSync(resolve(__dirname, "./index.html"), html, "utf-8");
});
```

加上注释

```vue
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width,initial-scale=1.0" />
    <title>vue-for-test</title>
  </head>
  <body>
    <div id="app">
      <!--vue-ssr-outlet-->
    </div>
    <!-- built files will be auto injected -->
  </body>
</html>
```

3. 使用插件

page-skeleton-webpack-plugin或者vue-skeleton-webpack-plugin

前者根据项目中不同的路由页面生成相应的骨架屏并通过webpack打包到静态路由页面中

后者将插入骨架屏的方式由手动改为自动，原理在构建时使用预渲染，将骨架屏渲染结果片段插入模版，样式内联到head中

#### 其他

hover

## SOLID

### SOLID

s，单一功能原则，对象应该仅具有一种功能

o，开闭原则，软件应该可扩展而不可修改

l，里氏替换原则，子类可以替换任何基类并且能正常运行

i，接口隔离原则，多个专用接口好过单一的总接口

d，依赖倒置原则，高层模块不应该依赖于低层模块，都应该依赖于抽象

### AOP

AOP是面向切面编程，是一种思想，**是OOP的补充**，旨在通过分离关注点来增加模块化，**通过向现有代码添加额外的行为而不修改当前代码来实现，允许将非核心行为添加到程序中，并且不与核心业务混淆**。可以降低耦合度，提高重用性。比如日志功能它横跨了多个业务，此时就可以将它作为一个切面，然后以某种自动化的方式织入到核心业务逻辑来解耦。

```js
function test() {
    console.log(2);
    return 0
}

Function.prototype.before = function (fn) {
    const _self = this
    return function () {
        // 先执行传入的函数
        // 返回false中断执行
        if(fn.apply(this, arguments) === false) {
            return false
        }
        return _self.apply(_self, arguments)
    }
}
Function.prototype.after = function (fn) {
    const _self = this
    return function () {
        // 获取原本的返回值
        const result = _self.apply(_self, arguments)
        if(result === false) {
            return false
        }
        // 后执行传入的函数
        fn.apply(this, arguments)
        return result
    }
}

// 先挂载self = test
// 执行before，self，after
const a = test.after(function() {
    console.log(3);
}).before(function() {
    console.log(1);
    // return false
})()
console.log(a);
```

### IOC

面向对象编程中的一个设计原则，在对象创建的时候，通过一个调控所有对象的容器将依赖的对象引用传递给他，就是通过一个容器来管理类之间的依赖，减少它们之间的耦合。两种方式，依赖注入，依赖查找

#### IOC框架

awilix和inversify

awilix，将service注入容器，在路由中用到时会从容器中获取并自动注入

inversify，将serveice和controller都注入容器，在路由激活时才会去容器中获取路由，路由中用到service也从容器中获取

对比MVC，将serveice和controlle耦合到一起

#### 原理

利用装饰器和反射实现

container用来存储对象，将对象注入container，通过装饰器inject对构造器参数进行拦截，在容器中查询给定对象并注册到构造器参数；装饰器controller对构造函数进行拦截，使用js解析器来分析参数并在容器中寻找，找到后注入构造函数。代码**编译时**会将参数对应的对象注入到构造函数中，最后使用这个类时，只需要传递约定好的参数名，不用引入真实的类，就可以直接使用容器中的对象，实现了这两个类之间的解耦，

```js
// esprima是一个js解释器
import { parseScript } from 'esprima';
import CreateIoc from './ioc';
import type { Pattern } from 'estree';
// 元编程
import 'reflect-metadata';

//常量区域
interface ITypes {
  [key: string]: symbol;
}
const TYPES: ITypes = {
  indexService: Symbol.for('indexService'),
};
interface IIndexService {
  log(str: string): void;
}
class IndexService implements IIndexService {
  log(str: string) {
    console.log(str);
  }
}
const container = new CreateIoc();
//把所需注入的服务注入到容器中container
container.bind(TYPES.indexService, () => new IndexService());

function getParams(fn: Function) {
  const ast = parseScript(fn.toString());
  // 忽略
  // @ts-expect-error
  const node = ast.body[0]['body']['body'][0];
  let fnParams: Pattern[] = [];
  if (node.kind === 'constructor') {
    fnParams = node['value'].params;
  }
  const validParams: string[] = [];
  fnParams.forEach((obj) => {
    if (obj.type === 'Identifier') {
      validParams.push(obj.name);
    }
  });
  //   console.log('node: ', validParams);
  return validParams;
}

// keyof any表示string，number或者symbol，使用PropertyKey也可以
function haskey<O extends Object>(obj: O, key: PropertyKey): key is keyof O {
  return obj.hasOwnProperty(key);
}

function inject(serviceIdentifier: symbol) {
  return (target: Function, targetKey: string, index: number) => {
    if (!targetKey) {
      // 把想构造的参数事先注册好
      Reflect.defineMetadata(
        serviceIdentifier,
        container.get(serviceIdentifier),
        target
      );
    }
  };
}

function controller<T extends { new (...args: any[]): {} }>(constructor: T) {
  class Controller extends constructor {
    // 拦截
    constructor(...args: any[]) {
      super(args);
      // 获取所有的参数
      const _parmas = getParams(constructor);
      let identity: string;
      // 寻找并注入
      for (identity of _parmas) {
        if (haskey(this, identity)) {
          //this[identity] = container.get(TYPES[identity]);
          this[identity] = Reflect.getMetadata(TYPES[identity], constructor); 
        }
      }
    }
  }
  return Controller;
}

@controller
class IndexController {
  public indexService: IIndexService;
  constructor(@inject(TYPES.indexService) indexService?: IndexService) {
    if (indexService) {
      this.indexService = indexService;
    }
  }
  info() {
    this.indexService.log('京程一灯 🏮' + Math.random());
  }
}
const index = new IndexController();
index.info();
//①最愚蠢的业务和所需的service 在一起
// const instance = new IndexService();
// this.indexService = instance;
//②稍微好一点 但是业务逻辑的代码还是跟所需的服务混合一起
// const instance = new IndexService();
// const index = new IndexController(instance);

class CreateIoc {
  public container: Map<symbol, { callback: Function }>;
  constructor() {
    this.container = new Map();
  }
  // 获取
  get(namespace: symbol) {
    const item = this.container.get(namespace);
    if (item) {
      return item.callback();
    } else {
      throw new Error('暂未找到实例');
    }
  }
  // 绑定
  bind(key: symbol, callback: Function) {
    this.container.set(key, {
      callback,
    });
  }
}
export default CreateIoc;
```





## node

### GC

https://zhuanlan.zhihu.com/p/55917130?yidian_docid=0LCztEHa&yidian_s=&yidian_amp;appid=pro

Orinoco是V8垃圾回收器项目，使之前的容易造成卡顿延迟（stop-the-word）的垃圾回收器，变得更加并行，并发和增量

所有垃圾回收器的共同任务：

- 标记活动和非活动对象

- 回收或者重用非活动对象内存

- 合并或整理内存

**主垃圾回收器**-全量标记整理

**从整个堆中**收集垃圾，主要有三个阶段：标记，清除，整理

标记：确定可访问对象的过程，通过可访问性确定，从根集开始，包含了执行栈和全局对象，跟踪每一个对象的指针并标记为可访问，是一个递归的过程

清除：标记完成后，将非活动对象占用的内存页添加到free-list中

整理：通过碎片启发式算法整理内存页，将活动对象复制到当前没有被整理的其他内存页中，利用内存中高度分散的内存空间。

堆在V8中分为老生带和新生代，新生代分为两个子带nursery和intermediate，对象第一次分配会在nursery，下一次回收时还在就移动到intermediate，再下一次就会移动到老生带

代际假说表明很多对象在内存的时间很短

垃圾回收的实质就是整理内存，移动内存中的对象

**副垃圾回收器**scavenger，**从新生代中**回收垃圾，新生代内存采用半空间（semi-space）设计，在疏散（移动对象）时，有一半内存是空闲的，清理时，初始的空闲区是to-space，复制对象区为from-space，最坏情况下每个对象都存活就需要都复制

对于清理，我们会维护一个额外的根集（root set），这个根集里会存放一些从旧到新的引用。这些引用是在旧空间（old-space）中指向新生代中对象的指针。使用“写屏障（[write barriers](https://link.zhihu.com/?target=https%3A//www.memorymanagement.org/glossary/w.html%23term-write-barrier)）”来维护从旧到新的引用列表，而不是跟踪整个堆中的每一个对象变更。

疏散步骤将所有的活动对象移动到连续的一块内存中；然后把两块内存空间互换，即把 ‘To-Space’ 变成 ‘From-Space’，反之亦然。一旦垃圾回收完成，新分配的内存空间将从 ‘From-Space’ 下一个空闲内存地址开始。

为了新生代的内存空间不被耗尽，在下一次垃圾回收的时候，我们会把活动对象移动（evacuate）到老生代

清理的最后一步是把移动后的对象的指针地址更新。

**Orinoco** 使用了各种技术降低主线程挂起的时间， 比如：并行（parallel）垃圾回收，增量（incremental）垃圾回收和并发（concurrent）垃圾回收。

**并行垃圾回收**

并行是主线程和协助线程同时执行同样的工作，但是这仍然是一种 ‘stop-the-world’ 的垃圾回收方式。这是这三种技术中最简单的只要确保同时只有一个协助线程在访问对象就好了。

**增量垃圾回收**

增量式垃圾回收是主线程间歇性的去做少量的垃圾回收的方式。做这样的工作是极其困难的，因为 JavaScript 也在做增量式垃圾回收的时候同时执行，这意味着堆的状态已经发生了变化，这有可能会导致之前的增量回收工作完全无效。并没有减少主线程暂停的时间（事实上，通常会略微增加）。但这仍然是解决问题的的好方法，JavaScript 的执行仍然可以在用户输入或者执行动画的时候得到及时的响应。

**并发垃圾回收**

并发是主线程一直执行 JavaScript，而辅助线程在后台完全的执行垃圾回收。这种方式是这三种技术中最难的一种，JavaScript 堆里面的内容随时都有可能发生变化，从而使之前做的工作完全无效。而且主线程和辅助线程极有可能在同一时间去更改同一个对象。这种方式的优势也非常明显，主线程不会被挂起，为了保证同一对象同一时间只有一个辅助线程在修改而带来的一些同步开销。

#### V8当前的回收机制

**Scavenging 垃圾回收器**（并行在主线程和协助线程之间分配疏散任务）

现今，V8 在**新生代垃圾回收中使用并行清理**，每个协助线程会将所有的活动对象都移动到 ‘To-Space’。在每一次尝试将活动对象移动到 ‘To-Space’ 的时候必须通确保原子化的读和写以及比较和交换操作。不同的协助线程都有可能通过不同的路径找到相同的对象，无论哪个协助线程成功移动对象到 ‘To-Space’，都必须更新这个对象的指针，并且去维护移动这个活动对象所留下的转发地址。以便于其他协助线程可以找到该活动对象更新后的指针。为了快速的给幸存下来的活动对象分配内存，清理任务会使用线程局部分配缓冲区。

**主垃圾回收器**（主垃圾回收器会并发的标记和清除对象，并行整理内存和更新活动对象指针）

V8 中的**主垃圾回收器主要使用并发标记**，一旦堆的动态分配接近极限的时候，将启动并发标记任务。每个辅助线程都会去追踪每个标记到的对象的指针以及对这个对象的引用。在 JavaScript 执行的时候，并发标记在后台进行。

当并发**标记完成或者动态分配到达极限**的时候，主线程会执行**最终的快速标记步骤**；在这个阶段**主线程会被暂停**，这段时间也就是主垃圾回收器执行的所有时间（其他是别的线程）。在这个阶段主线程会**再一次的扫描根集**以确保所有的对象都完成了标记；然后辅助线程就会去做**更新指针和整理内存**的工作。在暂停的时候主线程会启动**并发清理**的任务，这些任务都是并发执行的，并不会影响并行内存页的整理工作和 JavaScript 的执行。

**空闲时垃圾回收器**

JavaScript 是无法去直接访问垃圾回收器的。但是 V8 确实提供了一种机制让Embedders（嵌入V8的环境）去触发垃圾回收。垃圾回收器会发布一些 “空闲时任务（Idle Tasks）”，虽然这些任务都是可选的，但最终这些任务会被触发。像 Chrome 这些嵌入了 V8 的环境会有一些空闲时间的概念。比如：在 Chrome 中，以每秒60帧的速度去执行一些动画，浏览器大约有16.6毫秒的时间去渲染动画的每一帧，如果动画提前完成，那么 Chrome 在下一帧之前的空闲时间去触发垃圾回收器发布的空闲时任务。

什么时候进行GC？

空闲时间，每一帧16.7ms，如果提前完成进行GC



### 事件循环

**如何理解node高并发**

node是构建在v8引擎上的js运行环境，底层是v8引擎

**架构**

node框架由nodejs标准库，nodejs bindings，和底层库组成

nodejs标准库，js编写，能直接使用的api

node bindings，能直接调用c++的关键，将底层实现的c++库暴露给js环境，可以让js调用c++。node通过一层c++ binding，把js传入v8，v8解析后交给libuv发起async IO，并等待消息循环调度

底层库，v8，提供了在非浏览器的运行环境，libuv，提供了跨平台，线程池，事件池，异步IO等能力，还有C-ares，http-parser，openSSL，zlib等库

与操作系统的交互：在js中调用的方法，都会通过process.binding传递到c++层面

**单线程**

nodejs不为每一个用户创建一个新的线程，只使用一个线程，当有一个用户连接，就触发一个内部事件，通过非阻塞机制io，事件驱动机制，让宏观上是并行的。cpu利用率较高，还有操作系统也不会有线程创建和销毁的开销。

单线程程序，并行极大时cpu计算能力理论上是100%

多线程程序，cpu经常需要等IO结束，cpu被浪费

IO操作越多nodejs宏观上越是并行

**非阻塞IO**

IO操作不会阻塞代码的执行，将后续的代码放到回调中，当IO执行完成后，以事件的形式通知IO操作线程，执行回调。为了处理异步IO线程必须有事件循环，不断检查未处理事件

**事件循环**

每个node进程只有一个主线程，形成执行栈

主线程中维护了一个事件队列，当异步操作到来时，放到队列中，直到主线程执行完成

主线程执行完成后通过事件循环，检查队列，判断是否IO操作，非IO亲自处理，如果是IO操作就从线程池中拿一个线程来处理，指定回调函数，当IO操作完成后将回调放到事件队列尾部，等待事件循环，线程归还给线程池。再次循环到该事件时，就直接处理。

期间主线程不断检查事件队列中是否有未执行事件，直到执行完成，此后每当有新的事件，都会通知主线程按顺序取出交给eventloop处理

eventloop一共7个阶段每个阶段都有一个任务队列，当所有阶段被顺序执行一次eventloop完成一个tick

本质上node将所有的阻塞操作都交给了内部的线程池执行的，本身只负责调度，所以node可以单线程处理高并发的原因就在于libuv的事件循环机制和底层线程池的实现

7个阶段：都属于宏任务，主要阶段timers，poll，check，close

timers：执行setTimeout和setInterval回调，由poll阶段控制

pending callbacks：执行某些系统操作的回调

idle，prepare：内部使用

poll：执行IO回调，检查定时器。队列不为空时遍历执行队列直到为空或到达系统限制，然后继续等待，期间如果监测到timer定时器超时则进入timers阶段，如果存在setImmediate则进入check阶段

check：setImmediate回调

close callbacks：关闭的回调

对于微任务会在每个阶段前清空，promise，process.nextTick，MutationObserver

Node 中的 `process.nextTick`，这个函数其实是独立于 Event Loop 之外的，它有一个自己的队列，当每个阶段完成后，如果存在 nextTick 队列，就会**清空队列中的所有回调函数**，并且优先于其他 microtask 执行

**与浏览器事件循环的区别**

11之前有区别，之后和浏览器统一了

**执行完一个宏任务就会去检查微任务队列是否有需要执行的微任务**，即使微任务内嵌套微任务，也会将嵌套的微任务执行完毕后（这点上nodejs与browser是相同的，对应的就是清空微任务的队列），再去宏任务队列执行下一个宏任务，内部的任务会放在下一次事件循环时执行。



### 错误监控和日志

监控：一般分三个维度，性能监控，调用失败，业务监控

性能监控：内存，cpu的占用情况

调用失败：出错次数，QPS（每秒查询率）=PV/t，RT（响应时间）等

业务监控：监控日常业务，总结出的数据用于业务决策

开源方案：fundebug，sentry

日志包含日志源（日志来源，服务名称，主机名等），时间戳，级别和上下文

日志级别：INFO，DEBUG，WARN，ERROR

一般只开启WARN，ERROR，调试时可以使用DEBUG

## 框架

vue和react的区别

从架构层面来说，vue有一套自己的语法标准，必须按照这样写vue才会识别然后进行优化，浏览器运行的一般是编译后的代码，所以vue的优化重点就在编译时的优化，打包出来的代码也分为包括编译器的代码和只有运行时的代码，而react没有像这样的语法规范，只是将jsx中的标签替换成了react.createElement，相当于还是在写js，所以没有什么编译时优化，重点在运行时的优化也就是fiber架构

vue模版编译是使用with进行的this的绑定，因为它使用的正则表达式进行编译时，分析不出来js中的this，只能使用with来统一绑定，所以vue所有的属性都需要绑定在vue实例上，否则模版获取不到，模版省略this。在vue3的离线编译抛弃了这种方式，集成了js解析器，在线编译不能集成，还是使用的with。

### Vue2

#### vue架构

编译流程：

正则匹配模版生成ast，有回溯问题，扩展性差，然后静态节点优化，递归标记每一个节点，将ast生成可执行代码，拼接with方法

运行时流程：

从config.js中可以找到每个版本的入口，比如包含编译器和运行时的版本，扩展了默认的$mount方法，没有传入render时将template或el转换为render函数

初始化阶段：实现初始化函数以及各种api

```js
// 实现vue初始化函数_init
initMixin(Vue)
	Vue.prototype._init
    // 把组件实例里面用到的常用属性初始化，比如$parent/$root/$children
    initLifecycle(vm)
    // 父组件中定义的需要子组件处理的事件
    initEvents(vm)
    // $slots $scopedSlots初始化
    // $createElement函数声明
    // $attrs和$listeners响应化
    initRender(vm)
    callHook(vm, 'beforeCreate')
    // 注入内容的响应化
    initInjections(vm) // resolve injections before data/props
    // 初始化data包括数据响应化/props/methods/computed/watch，
    initState(vm)
    initProvide(vm) // resolve provide after data/props
    callHook(vm, 'created')
		// 执行mount方法
		vm.$mount(vm.$options.el)
// 组件状态相关api如$set,$delete,$watch实现
stateMixin(Vue)
// 事件相关api如$on,$emit,$oﬀ,$once实现
eventsMixin(Vue)
// 组件生命周期api如_update,$forceUpdate,$destroy实现 
lifecycleMixin(Vue)
// 实现组件渲染函数_render, $nextTick
renderMixin(Vue)
```

创建实例会执行初始化函数_init()，各种属性的初始化，执行**beforeCreated**生命周期，实例上各种数据的初始化，包括数据的响应化`observe(data, true )`，执行**created**生命周期，最后执行mount方法

默认的mount方法（执行mountComponent方法）：执行**beforeMount**生命周期，`new Watcher()`传入组件更新方法`updateComponent`，执行时初始化赋值时会触发依赖收集，触发updateComponent生成dom节点，执行**mounted**生命周期

updateComponent：判断是否存在上一个节点，没有就render新建vnode，创建dom节点，如果有上一个节点，render生成新的节点，与上一个节点进行dom diff，根据结果进行定向修改

#### 双向数据绑定

利用了Object.defineProperty实现数据的监听，Object.defineProperty有一定缺陷，监听数组时拦截操作会造成大量不必要的渲染，vue为了解决这个问题重写了数组7个方法，执行原有的数组方法，并且手动进行更新操作，还有就是不能监听新增数据

在vue中我们写的html会被打包成with的形式，运行时生成vnode，在执行mount期间会获取数据，触发observer中的get，进行依赖收集deps，在vue1时一个指令对应一个watcher，vue2中一个mountComponent对应一个watcher，在数据改变的时候遍历所有的依赖dep，通知每一个对应的watcher进行更新，生成新的vnode

#### 虚拟dom

为什么使用虚拟dom

本质上是因为原生的dom上面属性太多了，有很多我们用不到的属性，会浪费空间

#### dom diff

为什么需要dom diff

vue1时一个指令对应一个watcher时，watcher可以直接定向到dom节点，不需要dom diff，但是如果页面上指令较多，每一个都需要单独的空间进行维护，内存占用会特别大，vue2进行了优化一个组件对应一个watcher，但是组件又不需要每次都整体进行重新渲染，所以引入了dom diff，只渲染改变的部分

此时为了实现数据绑定和dom diff，可以定向更新到组件级别，vue会维护一套映射关系，大型应用的内存占用会很高

而react没有维护这样一个映射关系，每次更新会重新构建fiber（jsx -> element -> fiber），再进行fiber diff，diff较花费时间，可以中断

算法

简单来说diff的过程

- 同级比较，再比较子节点
- 先判断一方有子节点一方没有子节点的情况，新的没有子节点，将旧的子节点移除
- 比较都有子节点的情况
- 递归比较子节点

vue2采用了双端比较法，利用双指针同时从新旧的两端进行比较，借助key找到可以复用的节点，再进行相关操作。

具体比较时分四种情况：

对比头尾一致

对比头或尾一致，直接进行dom移动

都不一样时

​	返回老节点的key-index的映射表

​	根据key判断是否新增节点，新增vnode节点直接插入dom，

​	非新增，再对比是否同一个节点

​		是同一个节点，则进行dom移动

​		不是则新增vnnode直接插入dom，将旧的位置置为undefined，

每次操作完成后指针会进行移动，每次对比相等时都会打补丁，并且继续递归子节点

对比完成后判断越界，老节点先遍历完新增新节点剩下的节点，新节点先遍历完删除老节点剩下的节点

注意：

双指针遍历的是新旧的虚拟节点不是dom

老节点有ele属性，指向真实节点，真实节点的插入和删除都是靠这个属性

尽可能复用了原本的dom

缺点：每一个节点都进行了对比

#### 优化

##### 批量更新

在执行更新时默认执行批量更新queueWatcher，防止频繁更新，维护了一个watcher队列，首先判断是否已经存在，不存在时添加进队列，判断是否等待中，不是的情况，异步执行循环执行队列中的watcher更新

##### keep-alive算法

使用了LRU缓存算法，取最新最常使用的缓存

keep-alive保存了vnode虚拟节点，在render阶段判断缓存是否已经存在，存在时先移除再推入，没有直接添加，超出范围时，从后面删除

##### 与vue3模版处理区别

vue2的模版处理使用的时正则匹配，贪婪匹配存在回溯问题，而且分析功能有限不能做更多的优化

vue3使用的是状态机，根据自身语法和状态机模型写了一套compile，可以做更多的编译时优化

### Vue3

#### 对vue2的优化

运行时阶段，数据监听逻辑：

把Object.defineProperty替换为**Proxy**，Object.defineProperty会遍历所有的key重写每个key的值，相当于修改了原本的数据，而且不能监听到新增的数据，proxy则是对数据进行行为上的拦截，没有改变原有值，会生成一个新的包装过后的数据，可以拦截到新增的数据，数组的某些操作还是会触发多次拦截，拦截不到嵌套数据，只能拦截到外层

把flow替换为**ts**

新的架构，**拆分模块**，可以分单独的模块进行引用，使用了esmodule特性，使用monorepo进行代码管理，可以拆分子模块，使用lerna管理多个package.json，可以使用composition api，引入需要的模块方法，相互组合完成功能，而不是像以前一样写配置

模版编译优化：根据自身语法和**状态机**模型构建ast，模版分析能力增强，可以做更多的编译时优化

#### vue架构

编译时，状态机

#### 双向数据绑定



#### 虚拟dom

#### dom diff

vue3在创建vnode时就确定类型，diff算法通过最长递归子序列进行了优化，将节点移动操作最小化

对vue2的dom-diff完全重写

使用单指针循环，先遍历头部直到不同的节点，再遍历尾部直到不同的节点，然后判断是否遍历完成，完成则进行挂载和删除，否则进行核心逻辑：

先遍历新节点生成key-index映射表keyToNewIndexMap

根据比较项数量toBePatched，初始化newIndexToOldIndexMap内容都为0

遍历旧节点，通过旧节点的key查询映射表，没有就删除旧节点，最后生成一个newIndex-oldIndex+1映射表newIndexToOldIndexMap

通过newIndexToOldIndexMap获取最长升序子序列的index集合

同时从后向前遍历newch和newIndexToOldIndexMap和index集合，map在index中没有时，对应的ch节点就需要移动，存在就不需要移动，map中0对应的ch为新增节点



## 原理

## 手写算法

手写函数式

手写redux

手写vuex

手写koa

手写webpack

写一个LRU缓存算法

```js
class LRUCache {
  constructor(capacity) {
    this.cache = new Map()
    this.capacity = capacity
  }
  get(k) {
    if(!this.cache.get(k)) {
      return
    }
    const v = this.cache.get(k)
    this.cache.delete(k)
    this.cache.set(k, v)
    return v
  }
  push(k, v) {
    if(this.cache.has(k)) {
      this.cache.delete(k)
    }
    this.cache.set(k, v)
    if(this.cache.size > this.capacity) {
      // map.keys()返回迭代器
      const firstK = this.cache.keys().next().value
      this.cache.delete(firsetK)
    }
  }
}
```

> 偶发性批量处理会污染缓存，优化
>
> **LRU-K**
>
> LRU-K算法有两个队列，一个是缓存队列，一个是数据访问历史队列。当访问一个数据时，首先先在访问历史队列中累加访问次数，当历史访问记录超过K次后，才将数据缓存至缓存队列，从而避免缓存队列被污染。同时访问历史队列中的数据可以按照LRU的规则进行淘汰。
>
> 一般来讲，当K的值越大，则缓存的命中率越高，但是也会使得缓存难以被淘汰。综合来说，使用LRU-2的性能最优。

写一个promise

写一个mvvm

写一个发布订阅模式

写一下防抖节流

```js
// 节流，一段时间内最多执行一次
function trottle(fn, delay) {
  let timerId
  let execDate = getTime()
  let lastThis
  let lastArgs
  let result
  function execFn() {
		result = fn.call(lastThis, lastArgs)
    execDate = getTime()
    return result
  }
  return function(...args) {
    lastThis = this
    lastArgs = args
    //首次立即执行
    if(timerId === 'undefined') {
      execFn()
    }else {
      const current = getTime()
      // 清除计时器
      timerId && clearTimeout(timerId)
      // 判断是否超过delay
      if(current - execDate > delay) {
        // 超过直接执行
        execFn()
      }else {
        // 没超过设置定时器
        const wait = delay - (current - execDate)
        timerId = setTomeout(() => {
          execFn()
        }, wait)
      }
    }
    return result
  }
}
function getTime() {
  return + new Date()
}

// 简化版，区别：第一次没有立刻执行，超过时间也还是会创建定时器
function throttle(fn, delay) {
  let flag = true
  return function(...args) {
    if(flag) {
      flag = false
      setTimeout = (() => {
        fn.apply(this, args)
        flag = true
      }, delay)
    }
  }
}

// 防抖，触发结束一段时间后才执行
function debounce(fn, delay) {
  let timerId = ''
  return function(...args) {
    timerId && clearTimeout(timer)
    timerId = setTimeout(() => {
      fn.apply(this, args)
    }, delay)
  }
}
```

写一个Ajax

```js
// 一般写法
const xhr = new XMLHttpRequest()
xhr.open('GET', SERVER_URL, true)
// xhr.responsType = 'json'
// xhr.setRequestHeader('Accept', 'application/json')
xhr.onreadystatechange = function () {
  if(this.readyState === 4 && this.status === 200) {
    console.log(this.responseText)
  }
}
xhr.onerror = function () {
  console.error(this.statusText)
}
xhr.send(null)

// promise封装
function getJson(url) {
  return new Promise((resolve, reject) => {
    xhr.onreadystatechange = function () {
      if(this.readyState === 4 && this.status === 200) {
        resolve(this.responseText)
      }
    }
    xhr.onerror = function () {
      reject(this.statusText)
    }
    xhr.send(null)
  })
}
```

能否被3整除

```js
// fsm有限状态机
function createFSM() {
  return {
    // 初始余数为0
    initial: 0,
    states: {
      0: {
        on: {
          read(ch) {
            return {
              0: 0,
              3: 0,
              9: 0,
              1: 1,
              4: 1,
              7: 1,
              2: 2,
              5: 2,
              8: 2,
            }[ch];
          },
        },
      },
      1: {
        on: {
          read(ch) {
            return {
              0: 1,
              3: 1,
              9: 1,
              1: 2,
              4: 2,
              7: 2,
              2: 0,
              5: 0,
              8: 0,
            }[ch];
          },
        },
      },
      2: {
        on: {
          read(ch) {
            return {
              0: 2,
              3: 2,
              9: 2,
              1: 0,
              4: 0,
              7: 0,
              2: 1,
              5: 1,
              8: 1,
            }[ch];
          },
        },
      },
    },
  };
}

const fsm = createFSM();
const str = "281902812894839483047309573843389230298329038293829329";
let cur = fsm.initial;

for (let i = 0; i < str.length; i++) {
  if (!["0", "1", "2", "3", "4", "5", "6", "7", "8", "9"].includes(str[i])) {
    throw new Error("非法数字");
  }
  cur = fsm.states[cur].on.read(str[i]);
}
if (cur === 0) {
  console.log("可以被3整除");
} else {
  console.log("不可以被3整除");
}
```

### 代码题

```js
<script>
  // 使用未定义的变量
  sin;
  console.log(1);
</script>
<script>
  console.log(2);
</script>
// sin is not defined
// 2
```

## 其他

### 函数式编程

编程范式，面向过程/对象，函数式

函数是一等公民，可以作为变量，参数，返回值

### RPC

remote procedure call远程过程调用

简单来说就是从一台机器上通过参数调用另一台机器上的一个函数或者方法，并得到返回结果

- RPC会隐藏通讯细节
- 是一个请求响应模型
- 形式上像调用本地函数一样调用远程函数

本地调用：（计算机内部或浏览器V8做了许多优化）

- 解析函数名
- 通过作用域寻找函数声明
- 计算机寻址，找到该函数地址
- 入栈参数，执行函数
- 计算并返回结果

远程调用：

- 通讯问题：建立**TCP连接**，比如grpc框架，协议数据类型有unary和stream，底层还是通过二进制流拼凑的数据帧进行传输，包头中表明数据类型。unary，通过一问一答的形式在客户端和服务端通信，stream分为客户端流（客户端发多条服务端回一条），服务端流（客户端发一条服务端回多条）和双工流（都可以主动发）
- 寻址问题：在传输时调用方需要传递被调用方的**ip，端口和函数id**，这部分信息成为call id映射。一般双方都会维护一个**映射表**。包含了调用函数的入参和出参
- 序列化和反序列化：基于网络协议传输都是二进制形式，调用方传输信息前需要序列化，被调用方需要反序列化后，找到对应函数，传回结果时也需要序列化，调用方需要反序列化结果

为什么要用？

- http：restful规范为代表，可读性好，支持防火墙，跨语言，工作在第七层，有用信息占比少，效率低，调用远程方法复杂，需要封装各种参数
- RPC协议牺牲可读性提升效率，易用性
  - 双方维护一份结构和映射表，调用和传输数据更加透明，严格限制参数类型
  - 对tcp进行优化，参考HTTP2
  - 结构层可以做更多的监控，容错和性能优化

