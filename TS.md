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

 