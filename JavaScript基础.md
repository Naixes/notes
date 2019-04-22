# JavaScript基础

## JavaScript介绍

### JavaScript是什么

JavaScript运行在客户端(浏览器)的脚本语言

- 解释性脚本语言（其源代码在发往客户端运行之前不需编译，而是将文本格式的字符代码发送给浏览器由浏览器解释运行）
- 动态性（采用事件驱动的脚本语言,它不需要经过Web服务器就可以对用户的输入做出响应）  
- 基于对象  （可以创建对象,也能使用现有的对象 ）
- 跨平台（不依赖于操作系统,仅需要浏览器的支持）
- 动态类型（变量只有再赋值后才确定了类型 ）

Netscape在最初将其脚本语言命名为LiveScript，后来Netscape在与Sun合作之后将其改名为JavaScript。JavaScript最初受Java启发而开始设计的，因此语法上有类似之处，一些名称和命名规范也借自Java。JavaScript与Java名称上的近似，是当时Netscape为了营销考虑与Sun微系统达成协议的结果。Java和JavaScript的关系就像张雨和张雨生的关系，只是名字很像。

- Java  服务器端的编程语言

JavaScript的解释器被称为JavaScript引擎，为浏览器的一部分，广泛用于客户端的脚本语言。

### JavaScript最初的目的

最初的目的是为了处理表单的验证操作。

### JavaScript现在的意义(应用场景)

JavaScript 发展到现在几乎无所不能。

1. 网页特效
2. 服务端开发(Node.js)
3. 命令行工具(Node.js)
4. 桌面程序(Electron)
5. App(Cordova)
6. 控制硬件-物联网(Ruff)
7. 游戏开发(cocos2d-js)

## JavaScript的组成

![1496912475691](media/1496912475691.png)

### ECMAScript - JavaScript的核心 

ECMA欧洲计算机制造联合会

定义了JavaScript的语法规范  

JavaScript的核心，描述了语言的基本语法和数据类型，ECMAScript是一套标准，定义了一种语言的标准与具体实现无关

### BOM - 浏览器对象模型

一套操作浏览器功能的API

通过BOM可以操作浏览器窗口，比如：弹出框、控制浏览器跳转、获取分辨率等

### DOM - 文档对象模型

一套操作页面元素的API

DOM可以把HTML看做是文档树，通过DOM提供的API可以对树上的节点进行操作

## JavaScript初体验

### JavaScript的书写位置 

- 写在行内

```html
<input type="button" value="按钮" onclick="alert('Hello World')" />
```

- 写在script标签中

```html
<head>
  <script>
    alert('Hello World!');
  </script>
</head>
```

- 写在外部js文件中，在页面引入

```html
<script src="main.js"></script>
```

- 注意点

  **引用外部js文件的script标签中不可以写JavaScript代码**

  一对script标签中有错，错误代码之后不会执行，但不会影响其他script标签

## 计算机组成

### 软件

- 应用软件：浏览器(Chrome/IE/Firefox)、QQ、Sublime、Word
- 系统软件：Windows、Linux、mac OSX

### 硬件

- 三大件：CPU、内存、硬盘    -- 主板
- 输入设备：鼠标、键盘、手写板、摄像头等
- 输出设备：显示器、打印机、投影仪等

## 变量

### 什么是变量

- 什么是变量

  变量是计算机内存中存储数据的标识符，根据变量名称可以获取到内存中存储的数据

- 为什么要使用变量

  使用变量可以方便的获取或者修改内存中的数据

### 如何使用变量

```javascript
// var声明变量
var age;
// 变量的赋值
age = 18;
// 同时声明多个变量
var age, name, sex;
age = 10;
name = 'zs';
// 同时声明多个变量并赋值
var age = 10, name = 'zs';
```

### 变量在内存中的存储

```javascript
var age = 18;
```

![1496981558575](media/1496981558575.png)

### 变量的命名规则和规范

- 规则 - 必须遵守的，不遵守会报错

  - 由字母、数字、下划线、$符号组成，不能以数字开头

  - 不能是关键字和保留字，例如：for、while。

  - 区分大小写

- 规范 - 建议遵守的，不遵守不会报错

  - 变量名必须有意义
  - 遵守驼峰命名法。


### 案例

1. 交换两个变量的值

   ``````html
   ES5
   <script>
     var a = 10, b = 20
     var tem = a
     a = b
     b = tem
     console.log(a)
     console.log(b)
   </script>
   ES6
   <script>
     let a = 10, b = 20
     ;[a, b] = [b, a]
     console.log(a)
     console.log(b)
   </script>
   ``````

2. 不使用临时变量，交换两个数值变量的值

   ``````js
    // 交换数值
     var a = 10, b = 20
     a = b + a
     b = a - b
     a = a - b
     console.log(a)
     console.log(b)
   ``````


## 数据类型

### 简单数据类型

首先简单数据类型存储的都是值，是没有函数可以调用的，比如 `undefined.toString()` 会报错

`'1'.toString()` 是可以使用的。其实在这种情况下，`'1'` 已经不是原始类型了，而是**被强制转换成了 `String` 类型**也就是字符串的对象包装类型，所以可以调用 `toString` 函数。 

Number、String、Boolean、Undefined、Null

#### Number类型

- 数值字面量：数值的固定值的表示法    110 1024  60.5

- 进制

```js
十进制
	var num = 9;
	进行算数计算时，八进制和十六进制表示的数值最终都将被转换成十进制数值。
十六进制
	var num = 0xA;
	数字序列范围：0~9以及A~F
八进制
    var num1 = 07;   // 对应十进制的7
    var num2 = 019;  // 对应十进制的19
    var num3 = 08;   // 对应十进制的8
    数字序列范围：0~7
    如果字面值中的数值超出了范围，那么前导零将被忽略，后面的数值将被当作十进制数值解析
```

- 浮点数
  - 浮点数需要的内存空间为整数的两倍，所以没有小数或小数为零都会被转换为整数
  - 浮点数的精度问题

```js
浮点数
	var n = 5e-324;   // 科学计数法  5乘以10的-324次方  
浮点数值的最高精度是 17 位小数，但在进行算术计算时其精确度远远不如整数
   var result = 0.1 + 0.2;    // 结果不是 0.3，而是：0.30000000000000004
   console.log(0.07 * 100);
   不要判断两个浮点数是否相等
```

- 数值范围

```js
最小值：Number.MIN_VALUE，这个值为： 5e-324
最大值：Number.MAX_VALUE，这个值为： 1.7976931348623157e+308
无穷大：Infinity
无穷小：-Infinity
如果计算中超过数值范围会转换成Infinity/-Infinity，无法继续计算，isInfinity(xx)判断是否超过范围
```

- NaN
  - 表示**本来要返回数值的操作数未返回的情况**
  - NaN：not a number
    - 任何数除以0，都会返回NaN  
    - NaN 与任何值都不相等，包括他本身
    - 涉及到的 任何关于NaN的操作，都会返回NaN  
  - isNaN(): 函数用于检查其参数是否是非数字值。 
- 数值转换
  - Number()
  - parseInt()忽略空格找到第一个非空字符，如果不是数字或负号返回NaN，可以解析八进制和十六进制，ECMAScript5之后不能解析八进制，可以传入**第二个参数**表示`var num = parseInt("070", 8)`建议明确指定基数
  - parseFloat()只能解析十进制，如果是可解析为整数的值则返回整数

####  0.1 + 0.2 != 0.3

先说原因，因为 JS 采用 IEEE 754 双精度版本（64位），并且只要采用 IEEE 754 的语言都有该问题。

我们都知道计算机是通过二进制来存储东西的，那么 `0.1` 在二进制中会表示为

```js
// (0011) 表示循环
0.1 = 2^-4 * 1.10011(0011)
```

我们可以发现，`0.1` 在二进制中是无限循环的一些数字，其实不只是 `0.1`，其实**很多十进制小数用二进制表示都是无限循环的**。这样其实没什么问题，但是 JS 采用的浮点数标准**由于存储空间有限会裁剪掉我们的数字，所以在计算机中0.1只能存储成一个近似值**。在js中如果这个近似值足够近似，那么js就会认为他就是那个值。

```js
console.log(0.1000000000000001)  
// 0.1000000000000001 (中间14个0，会打印出它本身)

console.log(0.10000000000000001)  
// 0.1 (中间15个0，js会认为这两个值足够接近，所以会显示0.1)
```

另外说一句，除了那些能表示成 `x/2^n` 的数可以被精确表示以外，其余小数都是以近似值得方式存在的。

所以 `0.1` 不再是 `0.1` 了，而是变成了  `0.100000000000000002`

```js
0.100000000000000002 === 0.1 // true
```

那么同样的，`0.2` 在二进制也是无限循环的，被裁剪后也失去了精度变成了 `0.200000000000000002`

```js
0.200000000000000002 === 0.2 // true
```

在0.1 + 0.2这个式子中，0.1和0.2都是近似表示的，在他们相加的时候，两个近似值进行了计算，所以这两者相加不等于 `0.3` 而是 `0.300000000000000004`

```js
0.1 + 0.2 === 0.30000000000000004 // true
```

此时对于JS来说，其不够近似于0.3，于是就出现了`0.1 + 0.2 != 0.3` 这个现象。 

那么可能你又会有一个疑问，既然 `0.1` 不是 `0.1`，那为什么 `console.log(0.1)` 却是正确的呢？

因为**在输入内容的时候，二进制被转换为了十进制，十进制又被转换为了字符串，在这个转换的过程中发生了取近似值的过程**，所以打印出来的其实是一个近似值，你也可以通过以下代码来验证

```js
console.log(0.100000000000000002) // 0.1
```

其实解决的办法有很多，原生提供的方式来解决问题

```js
// toFixed() 方法可把 Number 四舍五入为指定小数位数的数字。
// 规定小数的位数，是 0 ~ 20 之间的值，包括 0 和 20，有些实现可以支持更大的数值范围。如果省略了该参数，将用 0 代替。
parseFloat((0.1 + 0.2).toFixed(10)) === 0.3 // true
```

想办法规避掉这类小数计算时的精度问题，那么最常用的方法就是将**浮点数转化成整数计算**。因为整数都是可以精确表示的。

```js
对于0.1 + 0.02 我们需要转化成 ( 10 + 2 ) / 1e2
对于0.1 * 0.02 我们则转化成 1 * 2 / 1e3
```

#### String类型

- 字符串字面量:'abc'   "abc"

- 转义符

  ![1498289626813](media/1498289626813.png)

- **字符串不可变**，改变变量保存的字符串时会创建新字符串，销毁旧字符串，然后再用新字符串填充变量，也是旧版本浏览器**字符拼接速度慢**的原因

- 字符串长度

  **length属性**用来获取字符串的长度

- 字符串拼接

  字符串拼接使用 + 连接

  1. 两边只要有一个是字符串，那么+就是字符串拼接功能
  2. 两边如果都是数字，那么就是算术功能。

- 类型转换：

  1. String()：适用于任何数据类型（null,undefined 转换后为null和undefined）；
  2. xx.toString()：null,defined没有toString()方法，参数是基数默认为10。 

#### Boolean类型

- Boolean字面量：  true和false，区分大小写
- Boolean()可以将一个值转换为相应的Boolean值，会被转换为false的有：null，undefined，0，“”，false，NaN
- 流程控制语句（如if）会自动执行转换

#### Undefined和Null（空类型）

Undefined类型只有一个值即undefined，为了区分空对象指针和未初始化的变量，没有必要将一个变量显示得设置为undefined

1. undefined表示一个**声明了没有赋值的变量**，变量只声明的时候值默认是undefined，对没有声明的变量使用`typeof`也返回undefined
2. 函数**没有明确返回值**，如果接收了，结果为undefined
3. 和数值计算结果是NaN

Null类型只有一个值即null，如果变量将用于保存对象，最好初始化为null

1. null表示一个**空对象指针**，变量的值如果想为null，必须手动设置

   ``````
   var null = null
   typeof null // object
   ``````

2. undefined的值派生自null因此相等性测试返回true（==会转换操作数）

   `undefined == null // true`

#### Symbol

目的：保证属性的名字都是独一无二的，从根本上防止属性名的冲突。 

Symbol 值**通过`Symbol`函数生成**。这就是说，对象的属性名现在可以有两种类型，一种是原来就有的字符串，另一种就是新增的 Symbol 类型。凡是属性名属于 Symbol 类型，就都是**独一无二**的，可以保证不会与其他属性名产生冲突。

```js
let s = Symbol();

typeof s
// "symbol"
```

注意，`Symbol`函数前**不能使用`new`命令**，否则会报错。这是因为生成的 Symbol 是一个原始类型的值，不是对象，不能添加属性。基本上，它是一种类似于字符串的数据类型。

`Symbol`函数可以**接受一个字符串作为参数，表示对 Symbol 实例的描述**，主要是为了在控制台显示，或者转为字符串时，比较容易区分。

```js
let s1 = Symbol('foo');
let s2 = Symbol('bar');

s1 // Symbol(foo)
s2 // Symbol(bar)

s1.toString() // "Symbol(foo)"
s2.toString() // "Symbol(bar)"
```

如果 Symbol 的参数是一个对象，就会调用该对象的`toString`方法，将其转为字符串，然后才生成一个 Symbol 值。

```js
const obj = {
  toString() {
    return 'abc';
  }
};
const sym = Symbol(obj);
sym // Symbol(abc)
```

注意，`Symbol`函数的参数只是表示对当前 Symbol 值的描述，因此相同参数的`Symbol`函数的返回值是不相等的。

```js
// 没有参数的情况
let s1 = Symbol();
let s2 = Symbol();

s1 === s2 // false

// 有参数的情况
let s1 = Symbol('foo');
let s2 = Symbol('foo');

s1 === s2 // false
```

Symbol 值**不能与其他类型的值进行运算**，会报错。

```js
let sym = Symbol('My symbol');

"your symbol is " + sym
// TypeError: can't convert symbol to string
`your symbol is ${sym}`
// TypeError: can't convert symbol to string
```

但是，Symbol 值**可以显式转为字符串**。

```
let sym = Symbol('My symbol');

String(sym) // 'Symbol(My symbol)'
sym.toString() // 'Symbol(My symbol)'
```

另外，Symbol 值也可以转为布尔值，但是不能转为数值。

```js
let sym = Symbol();
Boolean(sym) // true
!sym  // false

if (sym) {
  // ...
}

Number(sym) // TypeError
sym + 2 // TypeError
```

 ##### 作为属性名

Symbol 值作为标识符，用于对象的属性名，就能保证不会出现同名的属性。这对于一个对象由多个模块构成的情况非常有用，能防止某一个键被不小心改写或覆盖。

```js
let mySymbol = Symbol();

// 第一种写法
let a = {};
a[mySymbol] = 'Hello!';

// 第二种写法
let a = {
  [mySymbol]: 'Hello!' // Symbol 值必须放在方括号之中
};

// 第三种写法
let a = {};
Object.defineProperty(a, mySymbol, { value: 'Hello!' });

// 以上写法都得到同样结果
a[mySymbol] // "Hello!"
```

注意，Symbol 值作**为对象属性名时，不能用点运算符**。

```js
const mySymbol = Symbol();
const a = {};

a.mySymbol = 'Hello!'; // 点运算符后面总是字符串，所以不会读取mySymbol作为标识名所指代的那个值，导致a的属性名实际上是一个字符串，而不是一个 Symbol 值。
a[mySymbol] // undefined
a['mySymbol'] // "Hello!"
```

同理，在对象的内部，使用 Symbol 值定义属性时，Symbol 值必须放在方括号之中

Symbol 类型还可以用于**定义一组常量**，保证这组常量的值都是不相等的。

```js
const log = {};

log.levels = {
  DEBUG: Symbol('debug'),
  INFO: Symbol('info'),
  WARN: Symbol('warn')
};
console.log(log.levels.DEBUG, 'debug message');
console.log(log.levels.INFO, 'info message');
```

下面是另外一个例子。

```js
const COLOR_RED    = Symbol();
const COLOR_GREEN  = Symbol();

function getComplement(color) {
  switch (color) {
    case COLOR_RED:
      return COLOR_GREEN;
    case COLOR_GREEN:
      return COLOR_RED;
    default:
      throw new Error('Undefined color');
    }
}
```

**常量使用 Symbol 值最大的好处，就是其他任何值都不可能有相同的值了，因此可以保证上面的`switch`语句会按设计的方式工作。**

还有一点需要注意，Symbol 值作为属性名时，该属性还是公开属性，不是私有属性。

应用：消除魔术字符串，魔术字符串指的是，在代码之中多次出现、与代码形成强耦合的某一个具体的字符串或者数值。风格良好的代码，应该尽量消除魔术字符串，改由含义清晰的变量代替。 

##### 属性名遍历

Symbol 作为属性名，该属性**不会出现在`for...in`、`for...of`循环中，也不会被`Object.keys()`、`Object.getOwnPropertyNames()`、`JSON.stringify()`返回**。

`Object.getOwnPropertySymbols`方法返回一个数组，成员是当前对象的所有用作属性名的 Symbol 值。

```js
const obj = {};
let a = Symbol('a');
let b = Symbol('b');

obj[a] = 'Hello';
obj[b] = 'World';

const objectSymbols = Object.getOwnPropertySymbols(obj);

objectSymbols
// [Symbol(a), Symbol(b)]
```

另一个新的 API，`Reflect.ownKeys`方法可以返回所有类型的键名，包括常规键名和 Symbol 键名。

```js
let obj = {
  [Symbol('my_key')]: 1,
  enum: 2,
  nonEnum: 3
};

Reflect.ownKeys(obj)
//  ["enum", "nonEnum", Symbol(my_key)]
```

由于以 Symbol 值作为名称的属性，不会被常规方法遍历得到。我们**可以利用这个特性，为对象定义一些非私有的、但又希望只用于内部的方法**。

##### Symbol.for()，Symbol.keyFor()

有时，我们希望重新使用同一个 Symbol 值，`Symbol.for`方法可以做到这一点。它接受一个字符串作为参数，然后搜索有没有以该参数作为名称的 Symbol 值。如果有，就返回这个 Symbol 值，否则就新建并返回一个以该字符串为名称的 Symbol 值。

```js
let s1 = Symbol.for('foo');
let s2 = Symbol.for('foo');

s1 === s2 // true
```

`Symbol.for()`与`Symbol()`这两种写法，都会生成新的 Symbol。它们的区别是，前者**会被登记在全局环境中供搜索**，后者不会。`Symbol.for()`不会每次调用就返回一个新的 Symbol 类型的值，而是会先检查给定的`key`是否已经存在，如果不存在才会新建一个值。

`Symbol.keyFor`方法返回一个已登记的 Symbol 类型值的`key`。

```js
let s1 = Symbol.for("foo");
Symbol.keyFor(s1) // "foo"

let s2 = Symbol("foo");
Symbol.keyFor(s2) // undefined
```

需要注意的是，`Symbol.for`为 Symbol 值登记的名字，是**全局环境**的，可以在不同的 iframe 或 service worker 中取到同一个值。

```js
iframe = document.createElement('iframe');
iframe.src = String(window.location);
document.body.appendChild(iframe);

iframe.contentWindow.Symbol.for('foo') === Symbol.for('foo')
// true
// iframe 窗口生成的 Symbol 值，可以在主页面得到。
```

##### 实例：模块的 Singleton 模式（单例模式）

Singleton 模式指的是调用一个类，任何时候返回的都是同一个实例。

对于 Node 来说，模块文件可以看成是一个类。怎么保证每次执行这个模块文件，返回的都是同一个实例呢？

很容易想到，可以把实例放到顶层对象`global`。

```js
// mod.js
function A() {
  this.foo = 'hello';
}

if (!global._foo) {
  global._foo = new A();
}

module.exports = global._foo;
```

然后，加载上面的`mod.js`。

```js
const a = require('./mod.js');
console.log(a.foo);
```

但是，全局变量`global._foo`是可写的，任何文件都可以修改。

为了防止这种情况出现，我们就可以使用 Symbol。

```js
// mod.js
const FOO_KEY = Symbol.for('foo');

function A() {
  this.foo = 'hello';
}

if (!global[FOO_KEY]) {
  global[FOO_KEY] = new A();
}

module.exports = global[FOO_KEY];
```

上面代码中，可以保证`global[FOO_KEY]`不会被无意间覆盖，但还是可以被改写。

```js
global[Symbol.for('foo')] = { foo: 'world' };

const a = require('./mod.js');
```

如果键名使用`Symbol`方法生成，那么外部将无法引用这个值，当然也就无法改写。

```js
// mod.js
const FOO_KEY = Symbol('foo');

// 后面代码相同 ……
```

上面代码将导致其他脚本都无法引用`FOO_KEY`。但这样也有一个问题，就是如果多次执行这个脚本，每次得到的`FOO_KEY`都是不一样的。虽然 Node 会将脚本的执行结果缓存，一般情况下，不会多次执行同一个脚本，但是用户可以手动清除缓存，所以也不是绝对可靠。

### 复杂数据类型

复杂数据类型类型和原始类型不同的是，简单数据类型存储的是值，复杂数据类型存储的是地址。

复杂类型进行赋值或作为参数时传递的也是地址 

#### Object

Object每个实例都有以下方法和属性

```
constructor：保存用于创建当前对象的构造函数
hasOwnProperty(propertyName)：属性是否在实例中而非实例原型
isPrototypeOf(object)：是否传入对象原型
propertyIsEnumrable(propertyName)：是否可用for-in枚举
toLocalString()：返回对象的字符串表示，该字符串与执行环境对应
toString()：返回对象的字符串表示
valueOf()：返回对象的字符串，数值或布尔值表示
```

### 引用类型

### 简单类型和复杂类型的区别

> 基本类型又叫做值类型，复杂类型又叫做引用类型
>
> 值类型：简单数据类型，基本数据类型，在存储时，变量中存储的是值本身，因此叫做值类型。
>
> 引用类型：复杂数据类型，在存储是，变量中存储的仅仅是地址（引用），因此叫做引用数据类型。

- 堆和栈	

  ```
  堆栈空间分配区别：
  　　1、栈（操作系统）：先进后出，由操作系统自动分配释放 ，存放函数的参数值，局部变量的值等。 
  　　2、堆（操作系统）： 存储复杂类型的值(对象)，一般由程序员分配释放， 若程序员不释放，由垃圾回收机制回收。
  ```

- 注意：JavaScript中没有堆和栈的概念，此处我们用堆和栈来讲解，目的方便理解和方便以后的学习。

#### 基本类型在内存中的存储

![1498288494687](d:/note/%E5%89%8D%E7%AB%AF/html/media/1498288494687.png)

#### 复杂类型在内存中的存储

![1498700592589](D:/note/%E5%89%8D%E7%AB%AF/html/media/1498700592589.png)

#### 基本类型作为函数的参数

![1497497605587](D:/note/%E5%89%8D%E7%AB%AF/html/media/1497497605587-8288640195.png)

#### 复杂类型作为函数的参数

![1497497865969](D:/note/%E5%89%8D%E7%AB%AF/html/media/1497497865969.png)

```javascript
// 下面代码输出的结果?
function Person(name,age,salary) {
  this.name = name;
  this.age = age;
  this.salary = salary;
}
function f1(person) {
  person.name = "ls";
  person = new Person("aa",18,10);
}

var p = new Person("zs",18,1000);
console.log(p.name);// zs
f1(p);
console.log(p.name);// aa
```

思考：

```javascript
var num = 50;
function f1(num) {
    num = 60;
    console.log(num);// 60
}
f1(num);
console.log(num);// 60
```

### 获取变量的类型

#### typeof操作符

操作数可以是变量或数值字面量

``````
typeof（xx）/typeof  xx
``````

返回的结果用该类型的字符串(全小写字母)形式表示，包括以下 7 种：number、boolean、symbol、string、object、undefined、function 等

```javascript
typeof null//Object 无效 null类型进行typeof操作符后，结果是object，原因在于，null类型被当做一个空对象引用。在 JS 的最初版本中使用的是 32 位系统，为了性能考虑使用低位存储变量的类型信息，000 开头代表是对象，然而 null 表示为全零，所以将它错误的判断为 object 。虽然现在的内部类型判断代码已经改变了，但是对于这个 Bug 却是一直流传下来。 
typeof { }//Object 无效
typeof [ ]//Object 无效
typeof new Function(); // function 有效
typeof new Date(); //object 无效
typeof new RegExp(); //function/object 无效
```

有些时候，typeof 操作符会返回一些令人迷惑但技术上却正确的值：

- 对于基本类型，除 null 以外，均可以返回正确的结果。
- 对于引用类型，除 function 以外，一律返回 object 类型。
- 对于 null ，返回 object 类型。
- 对于 function 返回  function 类型。

#### instanceof操作符

内部机制是通过原型链来判断的

[判断数据类型的四种方法](http://www.cnblogs.com/onepixel/p/5126046.html)

[web前端知识体系精简](https://www.cnblogs.com/onepixel/p/7021506.html)

### 字面量

在源代码中一个固定值的表示法。

## 注释

- 单行注释

```javascript
// 这是一行注释
```

- 多行注释

用来注释多条代码

```javascript
/*
var age = 18;
var name = 'zs';
console.log(name, age);
*/
```

## 数据类型转换

![img](https://user-gold-cdn.xitu.io/2018/11/15/16716dec14421e47?imageView2/0/w/1280/h/960/format/webp/ignore-error/1) 

### 对象转原始类型

对象在转换类型的时候，会**调用内置的 `[[ToPrimitive]]` 函数**，对于该函数来说，算法逻辑一般来说如下：

- 如果已经是原始类型了，那就不需要转换了
- 调用 **`x.valueOf()**`，如果转换为基础类型，就返回转换的值
- 调用 **`x.toString()**`，如果转换为基础类型，就返回转换的值
- 如果都没有返回原始类型，就会报错

当然你也可以重写 `Symbol.toPrimitive` ，该方法在转原始类型时调用优先级最高。

```
let a = {
  valueOf() {
    return 0
  },
  toString() {
    return '1'
  },
  [Symbol.toPrimitive]() {
    return 2
  }
}
1 + a // => 3
```

### 转换成字符串类型

- toString()

  ```
  var num = 5;
  console.log(num.toString());
  ```

- String()

  ```
  String()函数存在的意义：有些值没有toString()，这个时候可以使用String()。比如：undefined和null
  ```

- 拼接字符串方式

  num  +  ""，当 + 两边一个操作符是字符串类型，一个操作符是其它类型的时候，会先把其它类型转换成字符串再进行字符串拼接，返回字符串

  - 运算中其中一方为字符串，那么就会把另一方也转换为字符串

  - 如果一方不是字符串或者数字，那么会将它转换为数字或者字符串

    ```js
    1 + '1' // '11' 
    true + true // 2 
    4 + [1,2,3] // "41,2,3" 
    ```

  另外对于加法还需要注意这个表达式 `'a' + + 'b'`

  ```
  'a' + + 'b' // -> "aNaN"
  ```

  因为 `+ 'b'` 等于 `NaN`，所以结果为 `"aNaN"`，你可能也会在一些代码中看到过 **`+ '1'` 的形式来快速获取 `number` 类型**。

  那么对于除了加法的运算符来说，只要其中一方是数字，那么另一方就会被转为数字

  ```
  4 * '3' // 12
  4 * [] // 0
  4 * [1, 2] // NaN
  ```

### 转换成数值类型

- Number()

  ```
  Number()可以把任意值转换成数值，如果要转换的字符串中有一个不是数值的字符，返回NaN
  ```

- parseInt()

  ```javascript
  var num1 = parseInt("12.3abc");  // 返回12，如果第一个字符是数字会解析知道遇到非数字结束
  var num2 = parseInt("abc123");   // 返回NaN，如果第一个字符不是数字或者符号就返回NaN
  ```

- parseFloat()

  ```
  parseFloat()把字符串转换成浮点数
  parseFloat()和parseInt非常相似，不同之处在与
  	parseFloat会解析第一个. 遇到第二个.或者非数字结束
  	如果解析的内容里只有整数，解析成整数
  ```

- +，-0等运算

  ```javascript
  var str = '500';
  console.log(+str);		// 取正
  console.log(-str);		// 取负
  console.log(str - 0);
  ```

思考：

```js
{}+[] // 0 如果{}被放在运算的最前面一位，他就会被当作代码块来处理，不论里面有什么，都不会影响计算结果 
[]+{} // "[object Object]"  []数组转换成字符串''+对象转换成字符串`[object Object]`
console.log({}+[]) // [object Object]
```

### 转换成布尔类型

- Boolean()    0 (空字符串) null undefined NaN 会转换成false  其它都会转换成true

## 操作符

运算符  operator

表达式  组成 操作数和操作符，会有一个结果

### 一元运算符

一元运算符：只有一个操作数的运算符

++  自身加1

--  自身减1

### 算术运算符

```
+ - * / %  
```

加法运算符不同于其他几个运算符，它有以下几个特点：

- 运算中其中一方为字符串，那么就会把另一方也转换为字符串
- 如果一方不是字符串或者数字，那么会将它转换为数字(两个都是简单类型)或者字符串

```
1 + '1' // '11'
true + true // 2
4 + [1,2,3] // "41,2,3"
```

如果你对于答案有疑问的话，请看解析：

- 对于第一行代码来说，触发特点一，所以将数字 `1` 转换为字符串，得到结果 `'11'`
- 对于第二行代码来说，触发特点二，所以将 `true` 转为数字 `1`
- 对于第三行代码来说，触发特点二，所以将数组通过 `toString` 转为字符串 `1,2,3`，得到结果 `41,2,3`

另外对于加法还需要注意这个表达式 `'a' + + 'b'`

```
'a' + + 'b' // -> "aNaN"
```

因为 `+ 'b'` 等于 `NaN`，所以结果为 `"aNaN"`，你可能也会在一些代码中看到过 `+ '1'` 的形式来快速获取 `number` 类型。

那么对于除了加法的运算符来说，只要其中一方是数字，那么另一方就会被转为数字

```
4 * '3' // 12
4 * [] // 0
4 * [1, 2] // NaN
```

### 逻辑运算符(布尔运算符)
	&& 与 两个操作数同时为true，结果为true，否则都是false
	|| 或 两个操作数有一个为true，结果为true，否则为false
	!  非  取反


短路运算：&&左边为true返回右边，否则返回左边

||左边为false返回右边，否则返回左边

### 关系运算符(比较运算符)

1. 如果是对象，就通过 `toPrimitive` 转换对象
2. 如果是字符串，就通过 `unicode` 字符索引来比较

```js
let a = {
  valueOf() {
    return 0
  },
  toString() {
    return '1'
  }
}
a > -1 // true
```

在以上代码中，因为 `a` 是对象，所以会通过 `valueOf` 转换为原始类型再比较值。

	<  >  >=  <=  == != === !==
#### ==与===的区别

==只进行值得比较，===类型和值同时相等，则相等

对于 `==` 来说，如果对比双方的类型**不一样**的话，就会进行**类型转换**。 

假如我们需要对比 `x` 和 `y` 是否相同，就会进行如下判断流程：

1. 首先会判断两者类型是否**相同**。相同的话就是比大小了
2. 类型不相同的话，那么就会进行类型转换
3. 会先判断是否在对比 `null` 和 `undefined`，是的话就会返回 `true`
4. 判断两者类型是否为 `string` 和 `number`，是的话就会**将字符串转换为 `number`** 
5. 判断其中一方是否为 `boolean`，是的话就会把 **`boolean` 转为 `number` 再进行判断** 
6. 判断其中一方是否为 `object` 且另一方为 `string`、`number` 或者 `symbol`，是的话就会把 `object` 转为原始类型再进行判断 

![img](https://user-gold-cdn.xitu.io/2018/12/19/167c4a2627fe55f1?imageView2/0/w/1280/h/960/format/webp/ignore-error/1) 

当然了，这个流程图并没有将所有的情况都列举出来，只将常用到的情况列举了，如果想了解更多的内容可以参考 [标准文档](https://link.juejin.im/?target=https%3A%2F%2Fwww.ecma-international.org%2Fecma-262%2F5.1%2F%23sec-11.9.1)。

对于 `===` 来说就简单多了，就是判断两者类型和值是否相同。

思考：

``` js
[] == ![]  
// ![]=>false=>0   
// [].valueof()=>[]=>[].toString()=>'' 
// ''==0 Nmber('')=>0 
// 0==0
// true
```

### 赋值运算符

=   +=   -=   *=   /=   %=
```javascript
例如：
var num = 0;
num += 5;	//相当于  num = num + 5;
```


### 运算符的优先级
	优先级从高到底
		1. ()  优先级最高
		2. 一元运算符  ++   --   !
		3. 算数运算符  先*  /  %   后 +   -
		4. 关系运算符  >   >=   <   <=
		5. 相等运算符   ==   !=    ===    !==
		6. 逻辑运算符 先&&   后||
		7. 赋值运算符

## 表达式和语句 

### 表达式

>一个表达式可以产生一个值，有可能是运算、函数调用、有可能是字面量。表达式可以放在任何需要值的地方。

### 语句

>语句可以理解为一个行为，循环语句和判断语句就是典型的语句。一个程序有很多个语句组成，一般情况下;分割一个一个的语句
## 流程控制

>程序的三种基本结构：顺序（默认）、分支、循环

## 分支结构

判断数字比判断字符的效率高

### if语句

语法结构

```javascript
if (/* 条件1 */){
  // 成立执行语句
} else if (/* 条件2 */){
  // 成立执行语句
} else if (/* 条件3 */){
  // 成立执行语句
} else {
  // 最后默认执行语句
}
```
### 三元运算符
	表达式1 ? 表达式2 : 表达式3
	是对if……else语句的一种简化写法

### switch语句

语法格式:
```javascript
switch (expression) {
  case 常量1:
    语句;
    break;
  …
  case 常量n:
    语句;
    break;
  default:
    语句;
    break;
}
```
	break可以省略，如果省略，代码会继续执行下一个case
	switch 语句在比较值时使用的是全等操作符, 因此不会发生类型转换（例如，字符串'10' 不等于数值 10）

## 循环结构

> 在javascript中，循环语句有三种，while、do..while、for循环。

### while语句

基本语法：

```javascript
// 当循环条件为true时，执行循环体，
// 当循环条件为false时，结束循环。
while (循环条件) {
  //循环体
}
```

### do...while语句

> do..while循环和while循环非常像，二者经常可以相互替代，但是do..while的特点是不管条件成不成立，都会执行一次。

基础语法：

```javascript
do {
  // 循环体;
} while (循环条件);
```

### for语句

>  while和do...while一般用来解决无法确认次数的循环。for循环一般在循环次数确定的时候比较方便

for循环语法：

```javascript
// for循环的表达式之间用的是;号分隔的，千万不要写成,
for (初始化表达式1; 判断表达式2; 自增表达式3) {
  // 循环体4
}
```

执行顺序：1243  ----  243   -----243(直到循环条件变成false)

1. 初始化表达式
2. 判断表达式
3. 自增表达式
4. 循环体


### continue和break

> break:立即跳出整个循环，即循环结束，开始执行循环后面的内容（直接跳到大括号）
>
> continue:立即跳出当前循环，继续下一次循环（跳到i++的地方）


### 调试

- 过去调试JavaScript的方式
  - alert()
  - console.log()
- 断点调试

>断点调试是指自己在程序的某一行设置一个断点，调试时，程序运行到这一行就会停住，然后你可以一步一步往下调试，调试过程中可以看各个变量当前的值，出错的话，调试到出错的代码行即显示错误，停下。

- 调试步骤

```javascript
浏览器中按F12-->sources-->找到需要调试的文件-->在程序的某一行设置断点
```

- 调试中的相关操作

```javascript
Watch: 监视，通过watch可以监视变量的值的变化，非常的常用。
F10: 程序单步执行，让程序一行一行的执行，这个时候，观察watch中变量的值的变化。
F8：跳到下一个断点处，如果后面没有断点了，则程序执行结束。
```

tips: ***监视变量，不要监视表达式，因为监视了表达式，那么这个表达式也会执行。***


## 数组

### 数组的定义
> 数组是一个有序的列表，可以在数组中存放任意的数据，并且数组的长度可以动态的调整。

通过数组字面量创建数组

```javascript
// 创建一个空数组
var arr1 = []; 
// 创建一个包含3个数值的数组，多个数组项以逗号隔开
var arr2 = [1, 3, 4]; 

// 可以通过数组的length属性获取数组的长度
console.log(arr3.length);
// 可以设置length属性改变数组中元素的个数
arr3.length = 0;
```

### 获取数组元素

数组的取值

```javascript
// 格式：数组名[下标]	下标又称索引
// 功能：获取数组对应下标的那个值，如果下标不存在，则返回undefined。
var arr = ['red',, 'green', 'blue'];
arr[0];	// red
arr[2]; // blue
arr[3]; // 这个数组的最大下标为2,因此返回undefined
```

### 数组中新增元素
数组的赋值

```javascript
// 格式：数组名[下标/索引] = 值;
// 如果下标有对应的值，会把原来的值覆盖，如果下标不存在，会给数组新增一个元素。
var arr = ["red", "green", "blue"];
// 把red替换成了yellow
arr[0] = "yellow";
// 给数组新增加了一个pink的值
arr[3] = "pink";
```
## 函数
### 什么是函数

>把一段相对独立的具有特定功能的代码块封装起来，形成一个独立实体，就是函数，起个名字（函数名），在后续开发中可以反复调用
>
>函数的作用就是封装一段代码，将来可以重复使用

### 函数的定义

- 函数声明

```javascript
function 函数名() {
  // 函数体
}
```

- 函数表达式

```javascript
var fn = function () {
  // 函数体
}
```

### 函数的调用
- 调用函数的语法：

函数名();

### 函数的参数

- 形参和实参

  > 1. 形式参数：在声明一个函数的时候，有些值是固定不了的，对于这些固定不了的值。我们可以给函数设置参数。这个参数没有具体的值，仅仅起到一个占位置的作用，我们通常称之为形式参数，也叫形参。
  > 2. 实际参数：如果函数在声明时，设置了形参，那么在函数调用的时候就需要传入对应的参数，我们把传入的参数叫做实际参数，也叫实参。

```javascript
var x = 5, y = 6;
fn(x,y); 
function fn(a, b) {
  console.log(a + b);
}
// x,y实参，有具体的值。函数执行的时候会把x,y复制一份给函数内部的a和b，函数内部的值是复制的新值，无法修改外部的x,y
```

### 函数的返回值

>当函数执行完的时候，并不是所有时候都要把结果打印。我们期望函数给我一些反馈（比如计算的结果返回进行后续的运算），这个时候可以让函数返回一些东西。也就是返回值。函数通过return返回一个返回值

函数的调用结果就是返回值，因此我们可以直接对函数调用结果进行操作。

返回值详解：

    如果函数没有显示的使用 return语句 ，那么函数有默认的返回值：undefined
    如果函数使用 return语句，那么跟再return后面的值，就成了函数的返回值
    如果函数使用 return语句，但是return后面没有任何值，那么函数的返回值也是：undefined
    函数使用return语句后，这个函数会在执行完 return 语句之后停止并立即退出，也就是说return后面的所有其他代码都不会再执行。

### arguments的使用

> JavaScript中，arguments对象是比较特别的一个对象，实际上是当前函数的一个内置属性。也就是说所有函数都内置了一个arguments对象，arguments对象中存储了传递的所有的实参。arguments是一个伪数组，因此及可以进行遍历

### 案例

```javascript
求斐波那契数列Fibonacci中的第n个数是多少？      1 1 2 3 5 8 13 21...
翻转数组，返回一个新数组
冒泡排序
判断素数
```

## 函数其它

### 匿名函数

> 匿名函数：没有名字的函数

匿名函数如何使用：

	将匿名函数赋值给一个变量，这样就可以通过变量进行调用
	匿名函数自调用

### 自调用函数
>匿名函数不能通过直接调用来执行，因此可以通过匿名函数的自调用的方式来执行
```javascript
(function () {
  alert(123);
})();
```
### 函数是一种数据类型

```javascript
function fn() {}
console.log(typeof fn);
```

- 函数作为参数

因为函数也是一种类型，可以把函数作为两一个函数的参数，在另一个函数中调用

- 函数做为返回值

因为函数是一种类型，所以可以把函数可以作为返回值从函数内部返回。

```javascript
function fn(b) {
  var a = 10;
  return function () {
    alert(a+b);
  }
}
fn(15)();
```


## 作用域
### 执行环境

### 全局变量和局部变量

- 全局变量

  在任何地方都可以访问到的变量就是全局变量，对应全局作用域

- 局部变量

  只在固定的代码片段内可访问到的变量，最常见的例如函数内部。对应局部作用域(函数作用域)

```
不使用var声明的变量是隐式全局变量，不推荐使用，可以删除。全局变量不能被删除
变量退出作用域之后会销毁，全局变量关闭网页或浏览器才会销毁
```

### 块级作用域

任何一对花括号（｛和｝）中的语句集都属于一个块，在这之中定义的所有变量在代码块外都是不可见的，我们称之为块级作用域。
**在es5之前没有块级作用域的的概念,只有函数作用域**

### 作用域链
	只有函数可以制造作用域结构， 那么只要是代码，就至少有一个作用域, 即全局作用域。凡是代码中有函数，那么这个函数就构成另一个作用域。如果函数中还有函数，那么在这个作用域中就又可以诞生一个作用域。
	
	将这样的所有的作用域列出来，可以有一个结构: 函数内指向函数外的链式结构。就称作作用域链。变量使用时，从里到外检索，检索到了就可以使用
```javascript
function f1() {
    var num = 123;
    function f2() {
        console.log(num); 
    }
    f2();
}
var num = 456;
f1();
```

![06-2](media/06-2.png)

## 预解析和变量提升

> JavaScript代码的执行是由浏览器中的JavaScript解析器来执行的。JavaScript解析器执行JavaScript代码的时候，分为两个过程：预解析过程和代码执行过程

预解析过程：

1. 把变量的声明提升到当前作用域的最前面，只会提升声明，不会提升赋值。
2. 把函数的声明提升到当前作用域的最前面，只会提升声明，不会提升调用。
3. **函数提升优先于变量提升**，函数提升会把整个函数挪到作用域顶部，变量提升只会把声明挪到作用域顶部

```javascript
// 案例1
var a = 25;
function abc() {
  alert(a); //undefinded
  var a = 10;
}
abc();
// 案例2
console.log(a);//function a()
function a() {
  console.log('aaaaa');
}
var a = 1;
console.log(a);//1
```

- 变量提升

根本原因就是为了解决函数间互相调用的情况 

```js
function test1() {
    test2()
}
function test2() {
    test1()
}
test1()
```

```javascript
// 1、-----------------------------------
var num = 10;
fun();
function fun() {
  console.log(num);// undefinded
  var num = 20;
}
//2、-----------------------------------
var a = 18;
f1();
function f1() {
  var b = 9;
  console.log(a);// undefinded
  console.log(b);// 9
  var a = '123';
}
// 3、-----------------------------------
f1();
console.log(c);// 9
console.log(b);// 9
console.log(a);// 报错
function f1() {
  var a = b = c = 9;// 只提升a，bc为隐式全局变量
  console.log(a);// 9
  console.log(b);// 9
  console.log(c);// 9
}
// 4、------------------------------------
f1()// 报错，f1提升后是一个变量
var f1 = function() {
    console.log(a)
    var a = 10
}
```

## 对象

### JavaScript中的对象
```
JavaScript的对象是无序属性的集合。
其属性可以包含基本值、对象或函数。对象就是一组没有顺序的值。我们可以把JavaScript中的对象想象成键值对，其中值可以是数据和函数。
对象的行为和特征
    特征---属性
    行为---方法
```

JavaScript有3大对象，分别是`本地对象`、`内置对象`和`宿主对象`。

在此引用ECMA-262（ECMAScript的制定标准）对于他们的定义：

- 本地对象
  - 与宿主无关，独立于宿主环境的ECMAScript实现提供的对象。
  - 简单来说，本地对象就是 ECMA-262 定义的类（引用类型）。
  - 这些引用类型在运行过程中需要通过new来创建所需的实例对象。
  - 包含：`Object`、`Array`、`Date`、`RegExp`、`Function`、`Boolean`、`Number`、`String`等。
- 内置对象
  - 与宿主无关，独立于宿主环境的ECMAScript实现提供的对象。
  - 在 ECMAScript 程序开始执行前就存在，本身就是实例化内置对象，开发者无需再去实例化。
  - 内置对象是本地对象的子集。
  - 包含：`Global`和`Math`。
  - ECMAScript5中增添了`JSON`这个存在于全局的内置对象。
- 宿主对象
  - 由 ECMAScript 实现的宿主环境提供的对象，包含两大类，一个是宿主提供，一个是自定义类对象。
  - 所有非本地对象都属于宿主对象。
  - 对于嵌入到网页中的JS来说，其宿主对象就是浏览器提供的对象，浏览器对象有很多，如`Window`和`Document`等。
  - 所有的`DOM`和`BOM`对象都属于宿主对象。

> 关于专业名词：本地对象也经常被叫做原生对象或内部对象，包含Global和Math在内的内置对象在《JavaScript高级程序设计》里也被叫做单体内置对象，很多时候，干脆也会直接把本地对象和内置对象统称为“内置对象”，也就是说除了宿主对象，剩下的都是ECMAScript的内部的“内置”对象。

### 对象字面量

> 字面量：11 'abc'  true  [] {}等

```javascript
var o = {
  name: 'zs,
  age: 18,
  sex: true,
  sayHi: function () {
    console.log(this.name);
  }
};
```

### 对象创建方式

- 对象字面量

```javascript
var o = {
  name: 'zs',
  age: 18,
  sex: true,
  sayHi: function () {
    console.log(this.name);
  }
};   
```

- new Object()创建对象

```javascript
var person = new Object();
person.name = 'lisi';
person.age = 35;
person.job = 'actor';
person.sayHi = function() {
  console.log('Hello,everyBody');
}
```
- 工厂函数创建对象
```javascript
function createPerson(name, age, job) {
  var person = new Object();
  person.name = name;
  person.age = age;
  person.job = job;
  person.sayHi = function(){
    console.log('Hello,everyBody');
  }
  return person;
}
var p1 = createPerson('张三', 22, 'actor');
```
- 自定义构造函数
```javascript
function Person(name, age, job){
  this.name = name;
  this.age = age;
  this.job = job;
  this.sayHi = function(){
  	console.log('Hello,everyBody');
  }
}
var p1 = new Person('张三', 22, 'actor');
```
### 属性和方法

	如果一个变量属于一个对象所有，那么该变量就可以称之为该对象的一个属性，属性一般是名词，用来描述事物的特征
	如果一个函数属于一个对象所有，那么该函数就可以称之为该对象的一个方法，方法是动词，描述事物的行为和功能
### new关键字
> 构造函数 ，是一种特殊的函数。主要用来在创建对象时初始化对象， 即为对象成员变量赋初始值，总与new运算符一起使用在创建对象的语句中。

1. 构造函数用于创建一类对象，首字母要大写。
2. 构造函数要和new一起使用才有意义。
3. 注意：构造函数有返回值，且返回一个对象，this指向这个对象，返回非对象，this指向实例

> 涉及面试题：new 的原理是什么？通过 new 的方式创建对象和通过字面量创建有什么区别？

在调用 `new` 的过程中会发生以上四件事情：

1. 新生成了一个对象
2. 链接到原型
3. 绑定 this 并执行构造函数
4. 返回新对象

#### 自己实现一个 `new`

```js
function create() {
  // 创建一个空对象
  let obj = {}
  // 获取构造函数
  let Con = [].shift.call(arguments)
  // 设置空对象的原型
  obj.__proto__ = Con.prototype
  // 绑定 this 并执行构造函数
  let result = Con.apply(obj, arguments)
  // 如果返回值是对象，返回构造函数返回的对象否则返回实例（确保返回值为对象）
  return result instanceof Object ? result : obj
}
// var person = create(构造函数, 'Kevin', '18')
```

对于对象来说，其实都是通过 `new` 产生的，无论是 `function Foo()` 还是 `let a = { b : 1 }` 。

对于创建一个对象来说，更推荐使用字面量的方式创建对象（无论性能上还是可读性）。因为你使用 `new Object()` 的方式创建对象需要通过作用域链一层层找到 `Object`，但是你使用字面量的方式就没这个问题。

```js
function Foo() {}
// function 就是个语法糖
// 内部等同于 new Function()
let a = { b: 1 }
// 这个字面量内部也是使用了 new Object()
```

### this详解

	1. 函数在定义的时候this是不确定的，只有在调用的时候才可以确定
	2. 一般函数直接执行，内部this指向全局window，严格模式下为undefined
	3. 函数作为一个对象的方法，被该对象所调用，那么this指向的是该对象
	4. 构造函数中的this其实是一个隐式对象，类似一个初始化的模型，所有方法和属性都挂载到了这个隐式对象身上，后续通过new关键字来调用，从而实现实例化，new之后this不会改变
	5. 箭头函数没有this，箭头函数中的this取决包裹箭头函数的第一个普通函数，不会改变
	6. bind，call，aplay等改变上下文的函数，this为第一个参数，不管我们给函数 bind 几次，fn 中的 this 永远由第一次 bind 决定
	7. new 的方式优先级最高，接下来是 bind 这些函数，然后是 obj.foo() 这种调用方式
如果你还是觉得有点绕，那么就看以下的这张流程图吧，图中的流程只针对于单个规则。

![img](https://user-gold-cdn.xitu.io/2018/11/15/16717eaf3383aae8?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)



## 对象的使用

### 遍历对象的属性
> 通过for..in语法可以遍历一个对象

```javascript
var obj = {};
for (var i = 0; i < 10; i++) {
  obj[i] = i * 2;
}
for(var key in obj) {
  console.log(key + "==" + obj[key]);
}
```
### 获取和修改对象属性值

通过点或者[]获取修改

[]可以写变量，用来遍历，点不行

### 删除对象的属性

```javascript
function fun() { 
  this.name = 'mm';
}
var obj = new fun(); 
console.log(obj.name); // mm 
delete obj.name;
console.log(obj.name); // undefined
```

## 内置对象

对象只是带有**属性**和**方法**的特殊数据类型。

### Object对象

- 属性

  constructor

  prototype

- 实例方法

  **toString()**：返回当前对象的字符串形式

  示例：

  ```js
  [1,'2',true].toString(); //"1,2,true"
  (new Date()).toString(); //"Sun Sep 24 2017 14:52:20 GMT+0800 (CST)"
  ({name:'ryan'}).toString(); //"[object Object]"
  ```

  > 由于所有的对象都"继承"了Object的对象实例，因此几乎所有的实例对象都可以使用该方法。
  >
  > JavaScript的许多内置对象都重写了该函数，以实现更适合自身的功能需要。

  **toLocalString()**

  **valueOf()**：返回指定对象的原始值

- 静态方法

  Object.assign(target, source)：把一个或多个源对象的可枚举、自有属性值复制到目标对象中，返回值为目标对象。 

### Math对象

Math对象不是构造函数，它具有数学常数和函数的属性和方法，都是以静态成员的方式提供

跟数学相关的运算来找Math中的成员（求绝对值，取整）

[Math](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Math)

演示：Math.PI、Math.random()、Math.floor()/Math.ceil()、Math.round()、Math.abs()	、Math.max()

```javascript
Math.PI						// 圆周率
Math.random()				// 返回0到1之间的伪随机数.
Math.floor()/Math.ceil()	 // 向下取整/向上取整
Math.round()				// 取整，四舍五入
Math.abs()					// 绝对值
Math.max()/Math.min()		 // 求最大和最小值

Math.sin()/Math.cos()		 // 正弦/余弦
Math.pow()/Math.sqrt()	 // 求指数次幂/求平方根
```

### Date对象

创建 `Date` 实例用来处理日期和时间。Date 对象基于1970年1月1日（世界标准时间）起的毫秒数。

~~~javascript
// 获取当前时间，UTC世界时间
var now = new Date();
console.log(now.valueOf());	// 获取距1970年1月1日（世界标准时间）起的毫秒数

Date构造函数的参数
1. 毫秒数 1498099000356		new Date(1498099000356)
2. 日期格式字符串  '2015-5-1'	 new Date('2015-5-1')
3. 年、月、日……				  new Date(2015, 4, 1)   // 月份从0开始
~~~

- 获取日期的毫秒形式，用于时间的计算

```javascript
var now = new Date();
// valueOf用于获取对象的原始值
console.log(date.valueOf())	

// HTML5中提供的方法，有兼容性问题
var now = Date.now();	

// 不支持HTML5的浏览器，可以用下面这种方式
var now = + new Date();			// 调用 Date对象的valueOf() 
```

- 日期格式化方法

```javascript
toString()		// 转换成字符串
valueOf()		// 获取毫秒值
// 下面格式化日期的方法，在不同浏览器可能表现不一致，一般不用
toDateString()
toTimeString()
toLocaleDateString()
toLocaleTimeString()
```

- 获取日期指定部分

```javascript
getTime()  	  // 返回毫秒数和valueOf()结果一样
getMilliseconds() // 返回毫秒 0-999
getSeconds()  // 返回0-59
getMinutes()  // 返回0-59
getHours()    // 返回0-23
getDay()      // 返回星期几 0周日   6周6
getDate()     // 返回当前月的第几天
getMonth()    // 返回月份，***从0开始***，要+！
getFullYear() //返回4位的年份  如 2016
```

#### 案例

- 写一个函数，格式化日期对象，返回yyyy-MM-dd HH:mm:ss的形式

```javascript
function formatDate(d) {
  //如果date不是日期对象，返回
  if (!date instanceof Date) {
    return;
  }
  var year = d.getFullYear(),
      month = d.getMonth() + 1, 
      date = d.getDate(), 
      hour = d.getHours(), 
      minute = d.getMinutes(), 
      second = d.getSeconds();
  month = month < 10 ? '0' + month : month;
  date = date < 10 ? '0' + date : date;
  hour = hour < 10 ? '0' + hour : hour;
  minute = minute < 10 ? '0' + minute:minute;
  second = second < 10 ? '0' + second:second;
  return year + '-' + month + '-' + date + ' ' + hour + ':' + minute + ':' + second;
}
```

- 计算时间差，返回相差的天/时/分/秒

```javascript
// 传入毫秒数
function getInterval(start, end) {
  var day, hour, minute, second, interval;
  interval = end - start;
  interval /= 1000;
  day = Math.round(interval / 60 / 60 / 24);
  hour = Math.round(interval / 60 / 60 % 24);
  minute = Math.round(interval / 60 % 60);
  second = Math.round(interval % 60);
  return {
    day: day,
    hour: hour,
    minute: minute,
    second: second
  }
}
```

### Array对象

- 创建数组对象的两种方式
  - 字面量方式
  - new Array()

```javascript
// 1. 使用构造函数创建数组对象
// 创建了一个空数组
var arr = new Array();
// 创建了一个数组，里面存放了3个字符串
var arr = new Array('zs', 'ls', 'ww');
// 创建了一个长度为3的数组
var arr = new Array(3);


// 2. 使用字面量创建数组对象
var arr = [1, 2, 3];

// 获取数组中元素的个数
console.log(arr.length);

// ES6
// 将一个类似数组的对象（有length属性）或可遍历的对象（部署了 Iterator 接口的数据结构比如：字符串和Set）转为数组
// 常用于转换document.qureySelectorAll()得到的对象和arguments对象
// 可接收第二个参数，类似于map对每个项目进行处理
// 扩展运算符也可以转换成数组，如[...arguments],[...document.querySelectorAll('')]
let arr = Array.from({'0':'a','1':'b',length:2})
// Array.of()可以将一组值转换为数组
let arr = Array.of(1,2,3)
```

- 检测一个对象是否是数组

  - instanceof
  - Array.isArray()     HTML5中提供的方法，有兼容性问题
  - Object.prototype.toString.call(arr) = '[object array]'

  函数的参数，如果要求是一个数组的话，可以用这种方式来进行判断

- toString()/valueOf()

  - toString()	把数组转换成字符串，逗号分隔每一项
  - valueOf()        方法返回指定对象的原始值  

- 数组常用方法


```javascript
// 1 栈操作(先进后出)
push() 		//添加元素到最后 返回添加后数组长度
pop() 		//删除数组中的最后一项，修改length属性 返回这一项的值
// 2 队列操作(先进先出)
shift()		//删除数组中的第一个元素，修改length属性 返回这一项的值
unshift() 	//在数组最前面插入项，返回数组的长度 返回添加后数组长度
// 3 排序方法
reverse()	//翻转数组
sort(); 	//即使是数组sort也是根据字符，从小到大排序，不稳定有时候不起作用
// 传入回调函数（固定写法）
return a-b //a-b为真交换顺序，升序
// 4 操作方法
concat()  	//把参数拼接到当前数组
slice() 	//从当前数组中截取一个新的数组，不影响原来的数组，参数start从0开始,end从1开始，slice(0)可以实现数组的浅拷贝，JSON.parse( JSON.stringify(arr) )可以实现数组的深拷贝
splice(开始索引,删除个数,要添加的元素)	//插入删除或替换当前数组的某些项目，参数start, deleteCount, options(要替换的项目)
//方法将数组的所有元素连接到一个字符串中。
join()// 参数是连接的符号
// 5 位置方法
indexOf(要匹配的元素，起始位置)、lastIndexOf()   //如果没找到返回-1，适用于简单类型
// 6 迭代方法 不会修改原数组(可选)  html5
forEach(cb)、//cb(item, i, arr)  ie8不支持
every(cb)、//cb(item, i, arr)	检测所有元素是否符合条件 返回布尔
some(cb)、//检测是否有符合条件的元素，任意一项符合就停止遍历返回true 返回布尔
filter(cb)、//cb(item, i, arr)	检测元素是否符合条件 返回符合条件的新元素数组
map()、//对每个元素进行操作后返回新数组
// ES6
find(cd) //cb(item, i, arr) {return 条件}      返回符合条件的第一个遍历项 非数组 没有返回undefined
findIndex(cd) //cb(item, i, arr) {return 条件}      返回符合条件的第一个索引 没有返回-1
includes(要匹配的元素，起始位置)
```

- 清空数组

```javascript
// 方式1 推荐 
arr = [];
// 方式2 
arr.length = 0;
// 方式3
arr.splice(0, arr.length);
```

#### 数组去重

```js
// ES5
function unique(arr) {
    var narr = []
    for(var i = 0; i<arr.length; i++) {
        if(n.indexOf(arr[i])===-1) {
            n.push(arr[i])
        }
    }
    return narr
}
// ES6
new Set([...arr])
```

#### 案例

- 将一个字符串数组输出为|分割的形式，比如“刘备|张飞|关羽”。使用两种方式实现

```javascript
function myJoin(array, seperator) {
  seperator = seperator || ',';
  array = array || [];
  if (array.length == 0){
    return '';
  }
  var str = array[0];
  for (var i = 1; i < array.length; i++) {
    str += seperator + array[i];
  }
  return str;
}
var array = [6, 3, 5, 6, 7, 8, 0];
console.log(myJoin(array, '-'));

console.log(array.join('-'))
```

- 将一个字符串数组的元素的顺序进行反转。["a", "b", "c", "d"] -> [ "d","c","b","a"]。使用两种方式实现。提示：第i个和第length-i-1个进行交换

```javascript
function myReverse(arr) {
  if (!arr || arr.length == 0) {
    return [];
  }
  for (var i = 0; i < arr.length / 2; i++) {
    var tmp = arr[i];
    arr[i] = arr[arr.length - i - 1];
    arr[arr.length - i - 1] = tmp;
  }
  return arr;
}

var array = ['a', 'b', 'c'];
console.log(myReverse(array));

console.log(array.reverse());
```

- 工资的数组[1500, 1200, 2000, 2100, 1800],把工资超过2000的删除

```javascript
// 方式1
var array =  [1500,1200,2000,2100,1800];
var tmpArray = [];
for (var i = 0; i < array.length; i++) {
  if(array[i] < 2000) {
    tmpArray.push(array[i]);
  }
}
console.log(tmpArray);
// 方式2
var array =  [1500, 1200, 2000, 2100, 1800];
array = array.filter(function (item, index) {
  if (item < 2000) {
    return true;
  }
  return false;
});
console.log(array);
```

- ["c", "a", "z", "a", "x", "a"]找到数组中每一个a出现的位置

```javascript
var array =  ['c', 'a', 'z', 'a', 'x', 'a'];
do {
  var index = array.indexOf('a',index + 1);
  if (index != -1){
    console.log(index);
  }
} while (index > 0);
```

- 编写一个方法去掉一个数组的重复元素

```javascript
var array =  ['c', 'a', 'z', 'a', 'x', 'a'];
function clear() {
  var o = {};
  for (var i = 0; i < array.length; i++) {
    var item = array[i];
    if (o[item]) {
      o[item]++;
    }else{
      o[item] = 1;
    }
  }
  var tmpArray = [];
  for(var key in o) {
    if (o[key] == 1) {
      tmpArray.push(key);
    }else{
      if(tmpArray.indexOf(key) == -1){
        tmpArray.push(key);
      }
    }
  }
  return tmpArray;
}

console.log(clear(array));
```



### 基本包装类型

普通变量不能直接调用属性或方法，调用属性或方法后变为基本包装类型，变量成为基本包装类型对象

为了方便操作简单数据类型，JavaScript还提供了三个特殊的简单类型类型：**String/Number/Boolean**

```javascript
// s1是基本类型，基本类型是没有方法的
var s1 = 'zhangsan';
var s2 = s1.substring(5);

// 当调用s1.substring(5)的时候，先把s1包装成String类型的临时对象，再调用substring方法，最后销毁临时对象, 相当于：
var s1 = new String('zhangsan');
var s2 = s1.substring(5);
s1 = null;
```

```javascript
// 创建基本包装类型的对象
var num = 18;  				//数值，基本类型
var num = Number('18'); 	//类型转换，基本类型
var num = new Number(18); 	//基本包装类型，对象
// Number和Boolean基本包装类型基本不用，使用的话可能会引起歧义。例如：
var b1 = new Boolean(false);
var b2 = b1 && true;		// true 第一个是对象结果是后面的
```

### String对象

- 字符串的不可变

```javascript
var str = 'abc';
str = 'hello';
// 当重新给str赋值的时候，常量'abc'不会被修改，依然在内存中
// 重新给字符串赋值，会重新在内存中开辟空间，这个特点就是字符串的不可变
// 由于字符串的不可变，在大量拼接字符串的时候会有效率问题，新的浏览器没有，可以使用数组
```

- 创建字符串对象

```javascript
var str = new String('Hello World');

// 获取字符串中字符的个数
console.log(str.length);
```

- 字符串对象的常用方法

  字符串所有的方法，都不会修改字符串本身(字符串是不可变的)，操作完成会返回一个新的字符串

```javascript
// 1 字符方法
charAt()    	//获取指定位置处字符
charCodeAt()  	//获取指定位置处字符的ASCII码
str[0]   		//HTML5，IE8+支持 和charAt()等效
// 2 字符串操作方法
concat()   		//拼接字符串，等效于+，+更常用
slice()    		//从start位置开始，截取到end位置，end取不到，返回新的字符串，可接收负数
substring() 	//从start位置开始，截取到end位置，end取不到，负数无效，第二个参数大时会交换位置
substr()   		//从start位置开始，截取length个字符
// 3 位置方法
indexOf()   	//返回指定内容在元字符串中的位置 lastIndexOf() 第二个参数指开始的索引位置 取不到返回-1
lastIndexOf() 	//从后往前找，只找第一个匹配的
// 4 去除空白   
trim()  		//只能去除字符串前后的空白
// 5 大小写转换方法
to(Locale)UpperCase() 	//转换大写
to(Locale)LowerCase() 	//转换小写
// 6 其它
search() 
replace()
split() // 以某字符进行分割，返回数组
"Webkit Moz O ms Khtml".split( " " )   // ["Webkit", "Moz", "O", "ms", "Khtml"]
//ES6
startsWith('前缀', '开始查找的位置以0开始')
endsWith()
includes()
// 补全字符串
padStart(补全后长度,补全字符)
padEnd(补全后长度,补全字符)
```

- 通过new创建的字符串是引用类型

#### 案例

- 截取字符串"我爱中华人民共和国"，中的"中华"

```javascript
var s = "我爱中华人民共和国";
s = s.substr(2,2);
console.log(s);
```

- "abcoefoxyozzopp"查找字符串中所有o出现的位置

```javascript
var s = 'abcoefoxyozzopp';
var array = [];
do {
  var index = s.indexOf('o', index + 1);
  if (index != -1) {
    array.push(index);
  }
} while (index > -1);
console.log(array);
```

- 把字符串中所有的o替换成!

```javascript
var s = 'abcoefoxyozzopp';
var index = -1;
do {
  index = s.indexOf('o', index + 1);
  if (index !== -1) {
    // 替换
    s = s.replace('o', '!');
  }
} while(index !== -1);
console.log(s);
```

- 把字符串中的所有空白去掉'   abc       xyz  a    123   '

```js
var s = '   abc       xyz  a    123   ';   
var arr = s.split(' ');
console.log(arr.join(''));
```


- 判断一个字符串中出现次数最多的字符，统计这个次数

```javascript
var s = 'abcoefoxyozzopp';
var o = {};

for (var i = 0; i < s.length; i++) {
  var item = s.charAt(i);
  if (o[item]) {
    o[item] ++;
  }else{
    o[item] = 1;
  }
}

var max = 0;
var char ;
for(var key in o) {
  if (max < o[key]) {
    max = o[key];
    char = key;
  }
}

console.log(max);
console.log(char);
```

- 获取url中?后面的内容，并转化成对象的形式。例如：http://www.itheima.com/login?name=zs&age=18&a=1&b=2

```js
var url = 'http://www.itheima.com/login?name=zs&age=18&a=1&b=2';
// 获取url后面的参数
function getParams(url) {
  // 获取? 后面第一个字符的索引
  var index = url.indexOf('?') + 1;
  // url中?后面的字符串 name=zs&age=18&a=1&b=2
  var params = url.substr(index);
  // 使用& 切割字符串 ，返回一个数组
  var arr = params.split('&');
  var o = {};
  // 数组中每一项的样子 key = value
  for (var i = 0; i < arr.length; i++) {
    var tmpArr = arr[i].split('=');
    var key = tmpArr[0];
    var value = tmpArr[1];

    o[key] = value;
  }
  return o;
}

var obj = getParams(url);
console.log(obj);

console.log(obj.name);
console.log(obj.age);
```

## ES6

### class 关键字

可以看做构造函数的另一种写法

1. class 中 `constructor` 就是构造函数
2. 内部定义的方法都不可枚举，与ES5不一致
3. 实例属性和实例方法
4. 静态属性和静态方法

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

1. 使用 `extends` 关键字实现继承

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

1. 为子类挂载独有的实例方法和属性

   放到super()后面



### 解构赋值

数组的解构赋值

```js
// 右边必须是可遍历的结构,可指定默认值	
let [a,b,c,d=4] = [1,2,3]
// 默认值可以是表达式，只有在用到时才会执行
```

对象的解构赋值

```js
// 与数组不同的是，数组变量的值与位置有关系，对象则是根据变量名
// 冒号前是解构的变量名，后面是赋值的变量名，相同时可以简写
```

字符串的解构赋值

注意：不要使用圆括号

应用：交换，获取返回值（import按需导入），传递参数

### let,const

首先在全局作用域下使用 `let` 和 `const` 声明变量，变量并不会被挂载到 `window` 上，这一点就和 `var` 声明有了区别。 

#### let 

- 块级作用域
- 没有变量提升
- 暂时性死区：只要块级作用域内存在`let`命令，它所声明的变量就“绑定”（binding）这个区域，不再受外部的影响。 因为暂时性死区的原因，不能在声明前使用。

```
var a = 1
let b = 1
const c = 1
console.log(window.b) // undefined
console.log(window. c) // undefined

function test(){
  console.log(a)
  let a
}
test()
```

 ![img](https://user-gold-cdn.xitu.io/2018/11/18/1672730318cfa540?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

报错的原因是存在暂时性死区 

#### const

- 块级作用域
- 没有变量提升
- 暂时性死区，声明时必须赋值
   对于复合类型只保证指针不能改变，引用的值还是可以改变	

## MDN

Mozilla 开发者网络（MDN）提供有关开放网络技术（Open Web）的信息，包括 HTML、CSS 和万维网及 HTML5 应用的 API。

- [MDN](https://developer.mozilla.org/zh-CN/)
- 通过查询MDN学习Math对象的random()方法的使用