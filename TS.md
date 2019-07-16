# TS

**js的增强**

添加可选择类型标注

提供不断发展的js特性

**前端开发趋势和技术转型趋势**

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

// 存取器
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



 