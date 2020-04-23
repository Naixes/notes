# TS

**js的增强**

类型标注和编译时类型检查

基于类的面向对象编程

泛型

接口

声明文件

提供不断发展的js特性

...

## 安装

安装node

`npm i -g typescript`

安装完成后会有全局命令`tsc -v // 查看版本 tsc xxx // 编译ts文件 tsc xxx --strictNullChecks //严格模式检查空值`

## 语法

### 初识TS

```ts
// 类
class User {
	fullName: string
	firstName: string
	lastName: string

	constructor(firstName, lastName) {
		this.firstName = firstName
		this.lastName = lastName
		this.fullName = `${firstName} ${lastName}`
	}
}

//  接口
interface Person {
	firstName: string
	lastName: string
}

//  类型注解，参数类型及个数
 function greeter(person: Person) {
	 return `hello ${person.firstName} ${person.lastName}`
 }

//  let user: Person = {
// 	 firstName: 'S',
// 	 lastName: 'in'
//  }

let user = new User('S', 'in')
 console.log(greeter(user))
```

#### 类型标注和类型检查

直接赋值可以不用注解，有类型推论

多种类型（|）

没有赋值时可以用！表示一定会赋值

函数参数只要声明就是必选参数，？表示可选参数

重载（使用参数或返回值区分函数）：需要先声明再 实现

### 基础类型

```ts
// 基本类型
// 布尔值
let isDone: boolean = false

// 数值
let decLiteral: number = 20
let hexLiteral: number = 0x14
let binaryLiteral: number = 0b10100
let octalLiteral: number = 0o24

// 字符串
let str: string = 'aaa'

// 数组
let list: number[] = [1, 2, 3, 4]
// 数组泛型
// let list: Array<number> = [1, 2, 3, 4]

// 元祖：指定类型和数量，越界赋值会报错（老版本3.1之前不会）
let x: [string, number] = ['aaa', 1 ]

// 枚举
enum Color {
		Red,
		Green = 0,
		Blue
}

let c: Color = Color.Green
let cName: string = Color[1]
console.log(cName)

// any
let notSure: any = 4
notSure = 'aaa'
// 用于数组
let arr: any[] = [1, 'aaa', false]

// void
function handler(): void {
	console.log('hello')
}

// null
let n: null = null
// 子类型可以赋值给父类型，--strictNullChecks  严格模式下编译不通过：
// Type 'null' is not assignable to type 'undefined'.
n = undefined

// undefined
let u: undefined = undefined
u = null

// never：不能返回的，不能结束的，报错的，是任何类型的子类型
function error(message: string): never {
	throw new Error(message)
}
function fail() {
	return error('something failed')
}

function infiniteLoop(): never {
	while(true) {

	}
}

// object：非原始类型
declare function create(o: object | null): void
create({prop: 0})

// 类型断言
let some: any = 'string'
// 强制转换
// let strLength: number = (<string>some).length
let strLength: number = (some as string).length

```

### 变量声明

var

let

const

解构

```ts
let a = {a: 'a', b: 'b'}
// 在这里不能指定类型，：是变量名指定
let {a: c, b: d} = a
```

展开

### 接口

interface，仅定义结构，不需要实现  

面向接口编程

TypeScript 的核心原则之一是对值所具有的结构进行类型检查。它有时被称做“鸭式辨型法”或“结构性子类型化”。 在 TypeScript 里，接口的作用就是为这些类型命名和为你的代码或第三方代码定义契约。 

```typescript

// 定义接口
interface o {
	prop: number,
	num: number
}

declare function create(o: o | null): void
create({prop: 0, num: 2})

// 可选属性
interface Square {
	color: string
	area: number
}

interface SquareConfig {
    // 为了解决导航时变量值为null时，页面运行时出错的问题
	color?: string
	width?: number

	// 索引签名：可能拥有特殊用途或者额外属性时使用，表示其他任意数量的属性
	// 索引属性名（字符串），值（any）
	[propName: string]: any
} 

function createSquare(config: SquareConfig): Square {
	// 应用：对属性进行预定义
	let newSquare = {color: 'white', area: 100}
	// 可以防止拼写错误
	if(config.color) {
		newSquare.color = config.color
	}
	if(config.width) {
		newSquare.area = config.width * config.width
	}
	return newSquare
}

// 额外属性检查：利用字面量传递属性有额外属性时会报错（现在又不报了，可能是版本的不同），可以不使用字面量或者属性断言，不推荐，可以使用索引签名
let mySquare = createSquare({color: 'black', height: 200})
// let mySquare = createSquare({color: 'black'})

// 只读属性
interface Point {
	readonly x: number
	readonly y: number
}

let p1: Point = {x: 10, y: 10}
// p1.x = 0

// 泛型只读数组
let a: number[] = [1, 2, 3]
let ro: ReadonlyArray<number> = a
// ro[0] = 0

// 函数类型
interface SearchFunc {
	(source: string, subString: string): boolean
}
// 参数名称可以改变，但是类型不能变
// let mySearch: SearchFunc = function(src: string, sub: string): boolean {
// 也可以省略类型
let mySearch: SearchFunc = function(src, sub) {
	let result = src.search(sub)
	return result > -1
}

// 可索引类型
interface StringArray {
	// 索引签名，可以是数字和字符串，可以同时使用但是数字索引的返回值必须是字符串索引返回值的子类型 
	[index: number]: string  
}

let myArray: StringArray = ['Bob', 'Fred']
let str: string = myArray[0]

// 可以同时使用但是数字索引的返回值必须是字符串索引返回值的子类型 
// class Animal {
// 	name: string
// }
// class Dog extends Animal {
// 	breed: string
// }
// 报错
// inter
interface IsOkay {
	[x: number]: Dog
	[x: string]: Animal
}

// 只读索引类型
interface ReadonlyStringArray {
	readonly [index: number]: string
}

let myReadonlyStringArray: ReadonlyStringArray = ['Alice', 'Bob']
// myReadonlyStringArray[2] = 'Mallory  '

// 类类型
// 1. 实例接口
// interface ClockInterface {
// 	currentTime: Date 
// 	setTime(d: Date)
// }

class Clock implements ClockInterface {
	currentTime: Date
	constructor(h: number, m: number) {

	}
	setTime(d: Date) {
		this.currentTime = d
	}
}

// 2. 构造器接口
// 实例部分
interface ClockInterface {
	tick()
}
// 静态部分
interface ClockConstructor {
	new(h: number, m: number): ClockInterface
}

function createClock(ctor: ClockConstructor, h: number, m: number): ClockInterface {
	return new ctor(h, m)
}

class DigitalClock implements ClockInterface {
	constructor(h: number, m: number) {
	}
	tick() {
		console.log('tick')
	}
}

let digital = createClock(DigitalClock, 12, 13)

// 继承接口：可继承多个
interface Shape {
	color: string
}
interface Square extends Shape {
	sideLength: number
}
let square = {} as Square
square.color = 'blue'
square.sideLength = 2

// 混合类型
interface Counter {
	// 作为函数
	(start: number): string

	// 作为对象
	interval: number
	reset(): void
}
function getCounter(): Counter {
	let counter = (function (start: number) {

	}) as Counter
	counter.interval = 123
	counter.reset = function() {}
	return counter
}

let counter = getCounter()
c(10)
c.reset()

// 接口继承类
class Control {
	private state: any
}
// 接口继承类时会继承到类的成员（包括私有成员和受保护成员）但是不会继承实现，就是说这个接口只能被这个类或子类所实现
interface SelectableControl extends Control {
	select()
}
class Button extends Control implements SelectableControl {
	select() {}
}
// SelectableControl只能被Control类或子类所实现
// class ImageC implements SelectableControl {
// 	select() {}
// }

```

### 类

```typescript
class Greeter {
	greeting: string
	constructor(msg: string) {
		this.greeting = msg
	}
	greet() {
		return `hello ${this.greeting}`
	}
}
let greeter = new Greeter('word')
greeter.greet()

// 继承
class Animal {
	name: string
	// 私有成员：不能在外部（实例）使用，包括子类
	// private age: number
	// 保护成员：不能在外部（实例）使用，不包括子类 
	// protected age: number
	// readonly：只读修饰符
	// readonly age: number

	// 构造函数也可以加protected
	// protected constructor(name: string, age: number) {
	// 参数属性（给构造函数参数前加访问限定符来声明），readonly也可以直接写到这里，创建和初始化
    // 参数前加修饰符，能定义并初始化一个成员变量
	constructor(name: string, readonly age: number) {
		this.name = name 
		// this.age = age 
	}
	move(dis: number = 0) {
		console.log(`${this.name} moved ${dis}m`)
	}
}
class Dog extends Animal{
	bark() {
		console.log('www')
	}
}
let dog = new Dog('hh', 2)
dog.bark()
dog.move(10)

class Snake extends Animal {
	constructor(name: string, age: number) {
		// 写在最前面
		super(name, age)
	}
	move(dis: number = 5) { 
		console.log('sss')
		super.move(dis)
	}
}

let snake = new Snake('ss', 3)
snake.move(20)

class Rhino extends Animal {
	constructor() {
		super('Rhino', 3)
	}
}

class Employee {
	name: string
	private age: number
	constructor(name: string, age: number) {
		this.name = name
		this.age = age
	}
}

let animal = new Animal('aa', 4)
let rhino = new Rhino()
let employee = new Employee('ee', 6)

animal = rhino
// animal = employee

// 存取器，vue中实现计算属性
class Person {
	private _fullNme: string
	get fullName(): string {
		return this._fullNme
	}
	set fullNmae(newName: string) {
		this._fullNme = newName
	}
}
// 编译不通过时 --target es5

// 静态属性
class Grid {
	static origin = {x: 0, y: 0}
	scale: number
	constructor(scale: number) {
		this.scale = scale
	}
	calculateDistanceFromOrigin(point: {x: number, y: number}) {
		let xDist = point.x - Grid.origin.x
		let yDist = point.y - Grid.origin.y
		return Math.sqrt(xDist * xDist + yDist * yDist) * this.scale
	}
}

let grid = new Grid(1)
console.log(grid.calculateDistanceFromOrigin({x: 3, y: 4}))
```

语法糖

```js
class Person{ // 类指向构造函数
    constructor(name, age){ // constructor是默认方法，new实例时自动调用
    this.name = name; // 属性会声明在实例上，因为this指向实例
    this.age = age;
	} 
    say(){ // 方法会声明在原型上
		return "我的名字叫" + this.name + "今年" + this.age + "岁了";
	}
} 
console.log(typeof Person); // function
console.log(Person === Person.prototype.constructor); // true
// 等效于
function Person(name,age) {
    this.name = name;
    this.age = age;
} 
Person.prototype.say = function(){
	return "我的名字叫" + this.name+"今年"+this.age+"岁了";
}
```



### 访问修饰符

private，public，protected

### 函数

```js
// 参数只要声明就是必选，?表示可选参数
// 函数重载，先声明，后统一实现
```

### 泛型

Generics是指在定义函数、接口或类的时候，不预先指定具体的类型，而在使用的时候再指定类型的一种特性。 增加代码的通用性

可以理解为类型变量，使返回值的类型与传入参数的类型是相同的，不同于使用 `any`，它不会丢失信息

```js
// 定义函数
function identity<T>(arg: T): T {
    return arg;
}
// 使用
// 方法1
let output = identity<string>("myString"); 
// 方法2：利用了类型推论 -- 即编译器会根据传入的参数自动地帮助我们确定T的类型
let output = identity("myString");

// 使用泛型变量
// 报错
function loggingIdentity<T>(arg: T): T {
    console.log(arg.length);  // Error: T doesn't have .length
    return arg;
}
// 这可以让我们把泛型变量T当做类型的一部分使用，而不是整个类型，增加了灵活性。
function loggingIdentity<T>(arg: T[]): T[] {
    console.log(arg.length);  // Array has a .length, so no more error
    return arg;
}

// 泛型类型
function identity<T>(arg: T): T {
    return arg;
}
// =>后面表示函数的返回值类型
let myIdentity: <T>(arg: T) => T = identity;
```



```js
// 定义泛型接口
interface Result<T> {
    ok: 0 | 1;
    data: T[];
} 
// 定义泛型函数
function getData<T>(): Result<T> {
    const data: any[] = [
        { id: 1, name: "类型注解", version: "2.0" },
        { id: 2, name: "编译型语言", version: "1.0" }
    ];
    return { ok: 1, data };
} 
// 使用泛型
this.features = getData<Feature>().data;

function getData<T>(): Promise<Result<T>> {
    const data: any[] = [
        { id: 1, name: "类型注解", version: "2.0" },
        { id: 2, name: "编译型语言", version: "1.0" }
    ];
    return Promise.resolve<Result<T>>({ ok: 1, data });
}
async created() {
    const result = await getData<Feature>();
    this.features = result.data;
}
```



## 在Vue中使用

新建一个基于ts的vue项目`vue create vue-ts`

选项选择：

- 自定义选项 - Manually select features
- 添加ts支持 - TypeScript
- 基于类的组件 - y
- tslint 

> 已有项目引入ts（cli3环境）：
>
> 查看cli文档：`vue add @vue/typescript`

配置文件：tsconfig.json，tslint.json

范例

```html
<template>
    <div>
        {{msg}}
    	<ul>
    	<li v-for="feature in features" :key="feature">{{feature}}</li>
    	</ul>
    </div>
</template>
<script lang='ts'>
import { Component, Prop, Vue } from "vue-property-decorator";
@Component
export default class Hello extends Vue {
    @Prop() msg!: string;
    features: string[];
    constructor() {
        super();
        this.features = ["类型注解", "编译型语言"];
    }
} 
</script>
```

### 装饰器

装饰器实际上是工厂函数，传入一个对象，输出处理后的新对象。 

#### 组件声明

```js
import {Componet, Prop, Vue, Emit} from "vue-property-decorator"
// 类装饰器
// 也可以声明在@Component({props: {msg: {xxx}}, components: [xxx]})
@Component
export default class Hello extends Vue {
    // 属性装饰器：也可以写在外面
    // !非空断言
    @Prop({ required: true, type: String }) private msg!: string;
    // 函数装饰器
    @Watch("features", {deep: true})
    onFeaturesChange(val: string, oldVal: any) {
    	console.log(val, oldVal);
	} 
	// 函数装饰器
    @Emit('add')
    private addFeature(event: any) {
        const feature = {
            name: event.target.value,
            id: this.features.length + 1,
            version: "1.0"
        };
        this.features.push(feature);
        event.target.value = feature;
        return event.target.value;
    }
}
```

#### 事件处理

```js
// 父组件中@foo="fn"
// 名称也可以指定@Emit('foo')??
 @Emit()
foo(e: any) {
    // 返回值就是参数
    return xxx
}
```

#### 变更监测

```js
// 函数装饰器
@Watch("features", {deep: true})
onFeaturesChange(val: string, oldVal: any) {
    console.log(val, oldVal);
} 
```

#### vuex

安装vue-class

映射

```js
@State('xx') cc!:number[]
@Action('xx') foo:any // 映射到computed
@Mutation('xx') doo:any // 映射到methods
```

#### 原理

实际是一个工厂 函数







































