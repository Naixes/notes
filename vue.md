# Vue.js 

## 基本概念

### 什么是Vue.js

- Vue.js 是一套构建用户界面的框架，**只关注视图层**，它不仅易于上手，还便于与第三方库或既有项目整合。（Vue有配套的第三方类库，可以整合起来做大型项目的开发）

### 框架和库的区别

- 框架：是一套完整的技术解决方案；对项目的侵入性较大，项目如果需要更换框架，则需要重新架构整个项目。

  - node 中的 express；

- 库（插件）：提供某一个小功能，对项目的侵入性较小，如果某个库无法完成某些需求，可以很容易切换到其它库实现需求。

  - 从Jquery 切换到 Zepto
  - 从 EJS 切换到 art-template

### MVC 与MVVM 之间的区别

- MVC 是后端的分层开发概念：

  传统的 MVC 架构通常是使用控制器更新模型，视图从模型中获取数据去渲染。当用户有输入时，会通过控制器去更新模型，并且通知视图进行更新。

  ![img](https://user-gold-cdn.xitu.io/2018/12/20/167cad938817eb7e?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)MVC

  但是 MVC 有一个巨大的缺陷就是**控制器承担的责任太大**了，随着项目愈加复杂，控制器中的代码会越来越**臃肿**，导致出现不利于**维护**的情况。

- MVVM是前端视图层的概念，主要关注于 视图层分离，也就是说：MVVM把前端的视图层，分为了 三部分 Model, View , VM ViewModel

  ViewModel 只关心数据和业务的处理，不关心 View 如何处理数据，在这种情况下，View 和 Model 都可以独立出来，任何一方改变了也不一定需要改变另一方，并且可以将一些可复用的逻辑放在一个 ViewModel 中，让多个 View 复用这个 ViewModel。

  ![img](https://user-gold-cdn.xitu.io/2018/12/21/167ced454926a458?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)  

![01.MVC和MVVM的关系图解](G:\note\前端\html\01.MVC和MVVM的关系图解.png)

### Vue.js 基本代码 和 MVVM 之间的对应关系

以 Vue 框架来举例，ViewModel 就是组件的实例。View 就是模板，Model 的话在引入 Vuex 的情况下是完全可以和组件分离的。

除了以上三个部分，其实在 MVVM 中还引入了一个隐式的 Binder 层，实现了 View 和 ViewModel 的绑定。

![img](https://user-gold-cdn.xitu.io/2018/12/21/167cf01bd8430243?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

同样以 Vue 框架来举例，这个**隐式**的 Binder 层就是 Vue 通过解析模板中的插值和指令从而实现 View 与 ViewModel 的绑定。

对于 MVVM 来说，其实最重要的并不是通过双向绑定或者其他的方式将 View 与 ViewModel 绑定起来，**而是通过 ViewModel 将视图中的状态和用户的行为分离出一个抽象，这才是 MVVM 的精髓**。

```javascript
// html页面对应v，可以直接使用{{msg}}渲染数据
// vm调度者
var vm = new Vue({
    // 也可以使用$mount("#app")方法绑定画面区域
    // el: '#app',
    // m
    data: {msg: 'msg'}
}).$mount("#app")
```

## Vue实例
```js
var vm = new Vue({
  // 选项
})
```

### 数据与方法


### [vue实例的生命周期](https://cn.vuejs.org/v2/guide/instance.html#实例生命周期)

- 什么是生命周期：从Vue实例创建、运行、到销毁期间，总是伴随着各种各样的事件，这些事件，统称为生命周期！![lifecycle](G:\note\前端\html\lifecycle.png)
- [生命周期钩子](https://cn.vuejs.org/v2/api/#选项-生命周期钩子)：就是生命周期事件的别名而已；
- 主要的生命周期函数分类：
- 创建期间的生命周期函数：
  - beforeCreate：实例刚在内存中被创建出来，只初始化了默认事件和生命周期函数。此时，还没有初始化好 data 和 methods 属性
  - created：实例已经在内存中创建OK，此时 data 和 methods 已经创建OK，此时还没有开始 编译模板
  - beforeMount：此时已经完成了模板的编译，开始创建 VDOM，但是还没有挂载到页面中
  - mounted：此时，将 VDOM 渲染为真实 DOM 并且渲染数据。组件中如果有子组件的话，会递归挂载子组件，只有当所有子组件全部挂载完毕，才会执行根组件的挂载钩子。 
- 运行期间的生命周期函数：
  - beforeUpdate：状态更新之前执行此函数， 此时 data 中的状态值是最新的，但是界面上显示的 数据还是旧的，因为此时还没有开始重新渲染DOM节点
  - updated：实例更新完毕之后调用此函数，此时 data 中的状态值 和 界面上显示的数据，都已经完成了更新，界面已经被重新渲染好了！
- 另外还有 `keep-alive` 独有的生命周期

   `activated` 和 `deactivated` 。用 `keep-alive` 包裹的组件在切换时不会进行销毁，而是缓存到内存中并执行 `deactivated` 钩子函数，命中缓存渲染后会执行 `actived` 钩子函数。 
- 销毁期间的生命周期函数：
  - beforeDestroy：实例销毁之前调用。在这一步，实例仍然完全可用。适合移除事件、定时器等等，否则可能会引起内存泄露的问题。 
  - destroyed：Vue 实例销毁后调用。调用后，Vue 实例指示的所有东西都会解绑定，所有的事件监听器会被移除，所有的子实例也会被销毁。

## keep-alive 组件

`<keep-alive>` 包裹动态组件时，会缓存不活动的组件实例，而不是销毁它们。和 `<transition>` 相似，`<keep-alive>` 是一个抽象组件：它自身不会渲染一个 DOM 元素，也不会出现在父组件链中。 

如果你需要**在组件切换的时候，保存一些组件的状态防止多次渲染**，就可以使用 `keep-alive` 组件包裹需要保存的组件。

对于 `keep-alive` 组件来说，它拥有两个独有的生命周期钩子函数，分别为 `activated` 和 `deactivated` 。用 `keep-alive` 包裹的组件在切换时不会进行销毁，而是缓存到内存中并执行 `deactivated` 钩子函数，命中缓存渲染后会执行 `actived` 钩子函数。

## 模板语法
数据绑定最常见的形式就是使用“Mustache”语法 (双大括号) 的文本插值：

`<span>Message: {{ msg }}</span>`

Mustache 标签将会被替代为对应数据对象上 msg 属性的值。无论何时，绑定的数据对象上 msg 属性发生了改变，插值处的内容都会更新。

通过使用 `v-once` 指令，你也能执行一次性地插值。但请留心这会影响到该节点上的其它数据绑定


## Vue指令

### v-cloak

这个指令保持在元素上直到关联实例结束编译,编译后会删除该属性。和 CSS 规则如 [v-cloak] { display: none } 一起用时，这个指令可以隐藏未编译的 Mustache 标签直到实例准备完毕。

网速慢的时候，编译前差值表达式会直接显示出来，有闪烁问题，v-cloak可以解决


```html
<style>
    [v-cloak]: {
        display: none;
    }
</style>

<div id="app">
    <p v-cloak>
        {{msg}}
    </p>
</div>

<script>、
var vm = new Vue({
    el: '#app',
    data: {msg: 'msg'}
}
</script>
```

### v-text和v-html

```html
<div id="app">
    <!-- 会覆盖标签内的内容，没有闪烁问题 -->
    <p v-text="msg">内容</p>
    <!-- 会将数据以html格式渲染 -->
    <!-- v-html:容易导致 XSS 攻击。请只对可信内容使用 HTML 插值，绝不要对用户提供的内容使用插值。 -->
    <div v-html="msg"></div>
</div>

<script>、
var vm = new Vue({
    el: '#app',
    data: {msg: '<p>xxx</p>'}
}
</script>
```

### v-bind

v-bind可以绑定标签的属性

1. 简化指令`:`
2. v-bind中可以写合法的js表达式

修饰符：
-  `.sync (2.3.0+)` 语法糖，会扩展成一个更新父组件绑定值的 v-on 侦听器。

```html
<!-- 绑定一个属性 -->
<img v-bind:src="imageSrc">

<!-- 动态特性名 (2.6.0+) -->
<button v-bind:[key]="value"></button>

<!-- 缩写 -->
<img :src="imageSrc">

<!-- 动态特性名缩写 (2.6.0+) -->
<button :[key]="value"></button>

<!-- 内联字符串拼接 -->
<img :src="'/path/to/images/' + fileName">

<!-- class 绑定 -->
<div :class="{ red: isRed }"></div>
<div :class="[classA, classB]"></div>
<div :class="[classA, { classB: isB, classC: isC }]">

<!-- style 绑定 -->
<div :style="{ fontSize: size + 'px' }"></div>
<div :style="[styleObjectA, styleObjectB]"></div>

<!-- 绑定一个有属性的对象 -->
<div v-bind="{ id: someProp, 'other-attr': otherProp }"></div>

<!-- 通过 prop 修饰符绑定 DOM 属性 -->
<div v-bind:text-content.prop="text"></div>

<!-- prop 绑定。“prop”必须在 my-component 中声明。-->
<my-component :prop="someThing"></my-component>

<!-- 通过 $props 将父组件的 props 一起传给子组件 -->
<child-component v-bind="$props"></child-component>

<!-- XLink -->
<svg><a :xlink:special="foo"></a></svg>
```

### v-on

绑定事件

```html
<input type="button" value="按钮" v-on:click="alertmsg">
<input type="button" value="按钮" @click="alertmsg">
<script>
    var vm = new Vue({
        el: '#app',
        data: {
            msg: 'msg'
        },
        methods: {
            alertmsg: function () {
                alert('msg')
            }
        }
    })
```

修饰符：

- .stop       阻止冒泡
- .prevent    阻止默认事件
- .capture    添加事件侦听器时使用事件捕获模式
- .self       只当事件在该元素本身（比如不是子元素）触发时触发回调，只阻止自身冒泡行为的触发
- .once       事件只触发一次
- 事件修饰符可以写多个

```html
<a href="http://www.baidu.com" @click.prevent.once="alertmsg">百度</a>
...
```

### v-model和双向数据绑定

只能用于表单

```html
<input type="text" v-model="msg">
<script>
    var vm = new Vue({
        el: '#app',
        data: {
            msg: 'msg'
        }
    })
</script>
```
修饰符：
- .lazy - 取代 input 监听 change 事件
- .number - 输入字符串转为有效的数字
- .trim - 输入首尾空格过滤

### `v-for`和`key`属性

1. 迭代数组

```html
<ul>
  <li v-for="(item, i) in list">索引：{{i}} --- 姓名：{{item.name}} --- 年龄：{{item.age}}</li>
</ul>
```

2. 迭代对象中的属性

```html
<!-- 循环遍历对象身上的属性 -->
<div v-for="(val, key, i) in userInfo">{{val}} --- {{key}} --- {{i}}</div>
```

3. 迭代数字，从1开始

```html
<p v-for="i in 10">这是第 {{i}} 个P标签</p>
```

> 2.2.0+ 的版本里，**当在组件中使用** v-for 时，key 现在是必须的。

当 Vue.js 用 v-for 正在更新已渲染过的元素列表时，它默认用 “**就地复用**” 策略。如果数据项的顺序被改变，Vue将**不是移动 DOM 元素来匹配数据项的顺序**， 而是**简单复用此处每个元素**，并且确保它在特定索引下显示已被渲染过的每个元素。

-  key 属性必须是字符串或数字，并且必须绑定

为了给 Vue 一个提示，**以便它能跟踪每个节点的身份，从而重用和重新排序现有元素**，你需要为每项提供一个唯一 key 属性。

`<li v-for="(item, i) in list" :key="item.name">索引：{{i}}姓名：{{item.name}}</li>`

### 筛选

[filterBy - 指令](https://v1-cn.vuejs.org/api/#filterBy)2.x已经废除

在2.x版本中[手动实现筛选的方式](https://cn.vuejs.org/v2/guide/list.html#显示过滤-排序结果)：

- 筛选框绑定到 VM 实例中的 `searchName` 属性：

```html
<hr> 输入筛选名称：
<input type="text" v-model="searchName">
```

- 在使用 `v-for` 指令循环每一行数据的时候，不再直接 `item in list`，而是 `in` 一个 过滤的methods 方法，同时，把过滤条件`searchName`传递进去：

```html
<tbody>
    <tr v-for="item in search(searchName)">
        <td>{{item.id}}</td>
        <td>{{item.name}}</td>
        <td>{{item.ctime}}</td>
        <td>
            <a href="#" @click.prevent="del(item.id)">删除</a>
        </td>
    </tr>
</tbody>
```

- `search` 过滤方法中，使用 数组的 `filter` 方法进行过滤：

```javascript
search(name) {
  return this.list.filter(x => {
    // return x.name.indexOf(name) != -1;
    // ES6 String.prototype.includes()
    return x.name.includes(name)
  });
}
```

### `v-if`和`v-show`

`v-show` 只是在 `display: none` 和 `display: block` 之间切换。无论初始条件是什么都会被渲染出来，后面只需要切换 CSS。所以总的来说 `v-show` 在初始渲染时有更高的开销，但是切换开销很小，更适合于频繁切换的场景。

`v-if` 当属性初始为 `false` 时，组件就不会被渲染，直到条件为 `true`，并且切换条件时会触发销毁/挂载组件，所以总的来说在切换时开销更高，更适合不经常切换的场景。

并且基于 `v-if` 的这种惰性渲染机制，可以在必要的时候才去渲染组件，减少整个页面的初始渲染开销。

## [自定义指令](https://cn.vuejs.org/v2/guide/custom-directive.html)

### Vue 2x 自定义元素指令

1. 自定义全局和局部的自定义指令：

```javascript
    // 自定义全局指令 v-focus，js原生方法focus()为绑定的元素自动获取焦点：
    Vue.directive('focus', {
      inserted: function (el) { // inserted 表示被绑定元素插入父节点时调用
        el.focus();
      }
    });
    // 自定义局部指令 v-color 和 v-font-weight，为绑定的元素设置指定的字体颜色 和 字体粗细：
    directives: {
      color: { // 为元素设置指定的字体颜色
        bind(el, binding) {
        el.style.color = binding.value;
        }
      },
      'font-weight': function (el, binding2) { // 自定义指令的简写形式，等同于定义了 bind 和 update 两个钩子函数
        el.style.fontWeight = binding2.value;
      }
    }
```

自定义指令的使用方式：

```
<input type="text" v-model="searchName" v-focus v-color="'red'" v-font-weight="900">
```

#### 钩子函数

一个指令定义对象可以提供如下几个钩子函数 (均为可选)：

- `bind`：只调用一次，指令第一次绑定到元素时调用，此时元素在内存中还没有被加到任何节点上。在这里可以进行一次性的初始化设置。
- `inserted`：被绑定元素插入父节点时调用 (仅保证父节点存在，但不一定已被插入文档中)。
- `update`：所在组件的 VNode 更新时调用，**但是可能发生在其子 VNode 更新之前**。指令的值可能发生了改变，也可能没有。但是你可以通过比较更新前后的值来忽略不必要的模板更新 (详细的钩子函数参数见下)。
- `componentUpdated`：指令所在组件的 VNode **及其子 VNode** 全部更新后调用。
- `unbind`：只调用一次，指令与元素解绑时调用。

一般样式修改使用bind函数，行为操作使用inserted

如果指令需要多个值，可以传入一个 JavaScript 对象字面量。指令函数能够接受所有合法的 JavaScript 表达式。

```html
<div v-demo="{ color: 'white', text: 'hello!' }"></div>
```
```js
Vue.directive('demo', function (el, binding) {
  console.log(binding.value.color) // => "white"
  console.log(binding.value.text)  // => "hello!"
})
```

#### 钩子函数参数

指令钩子函数会被传入以下参数： 

- `el`：指令所绑定的元素，可以用来直接操作 DOM 。
- `binding`：一个对象，包含以下属性： 
  - `name`：指令名，不包括 `v-` 前缀。
  - `value`：指令的绑定值，例如：`v-my-directive="1 + 1"` 中，绑定值为 `2`。
  - `oldValue`：指令绑定的前一个值，仅在 `update` 和 `componentUpdated` 钩子中可用。无论值是否改变都可用。
  - `expression`：字符串形式的指令表达式。例如 `v-my-directive="1 + 1"`中，表达式为 `"1 + 1"`。
  - `arg`：传给指令的参数，可选。例如 `v-my-directive:foo` 中，参数为 `"foo"`。
  - `modifiers`：一个包含修饰符的对象。例如：`v-my-directive.foo.bar` 中，修饰符对象为 `{ foo: true, bar: true }`。
- `vnode`：Vue 编译生成的虚拟节点。移步 [VNode API](https://cn.vuejs.org/v2/api/#VNode-接口) 来了解更多详情。
- `oldVnode`：上一个虚拟节点，仅在 `update` 和 `componentUpdated` 钩子中可用。

#### 函数简写

在很多时候，你可能想在 `bind` 和 `update` 时触发相同行为，而不关心其它的钩子。比如这样写:

```js
Vue.directive('color-swatch', function (el, binding) {
  el.style.backgroundColor = binding.value
})
```

### Vue 1.x 自定义元素指令

```js
Vue.elementDirective('red-color', {
  bind: function () {
    this.el.style.color = 'red';
  }
});
```

使用方式：

```html
<red-color>1232</red-color>
```

## 在Vue中使用样式

### 使用class样式

- 数组

```html
<h1 :class="['red', 'thin']">这是一个邪恶的H1</h1>
```

注意要使用字符串形式

- 数组中使用三元表达式

```html
<h1 :class="['red', 'thin', isactive?'active':'']">这是一个邪恶的H1</h1>
```

- 数组中嵌套对象

```html
<h1 :class="['red', 'thin', {'active': isactive}]">这是一个邪恶的H1</h1>
```

- 直接使用对象

```html
<h1 :class="{red:true, italic:true, active:true, thin:true}">这是一个邪恶的H1</h1>
```

- 在data上定义class样式

### 使用内联样式

1. 直接在元素上通过 `:style` 的形式，书写样式对象

```html
<h1 :style="{color: 'red', 'font-size': '40px'}">这是一个善良的H1</h1>
```

2. 将样式对象，定义到 `data` 中，并直接引用到 `:style` 中

- 在data上定义样式：

```js
data: {
  h1StyleObj: { color: 'red', 'font-size': '40px', 'font-weight': '200' }
}
```

- 在元素中，通过属性绑定的形式，将样式对象应用到元素中：

```html
<h1 :style="h1StyleObj">这是一个善良的H1</h1>
```

3. 在 `:style` 中通过数组，引用多个 `data` 上的样式对象

- 在data上定义样式：

```js
data: {
  h1StyleObj: { color: 'red', 'font-size': '40px', 'font-weight': '200' },
  h1StyleObj2: { fontStyle: 'italic' }
}
```

- 在元素中，通过属性绑定的形式，将样式对象应用到元素中：

```html
<h1 :style="[h1StyleObj, h1StyleObj2]">这是一个善良的H1</h1>
```

## Vue调试工具`vue-devtools`

[Vue.js devtools - 翻墙安装方式 - 推荐](https://chrome.google.com/webstore/detail/vuejs-devtools/nhdogjmejiglipccpnnnanhbledajbpd?hl=zh-CN)

## 过滤器

概念：Vue.js 允许你自定义过滤器，**可被用作一些常见的文本格式化**。过滤器可以用在两个地方：**mustache 插值和 v-bind 表达式**。过滤器应该被添加在 JavaScript 表达式的尾部，由“管道”符指示；

可以同时调用多个

**注意：过滤器中没有this上下文**

### 私有过滤器

1. HTML元素：

```html
<td>{{item.ctime | dataFormat('yyyy-mm-dd')}}</td>
```

1. 私有 `filters` 定义方式：

```javascript
filters: { // 私有局部过滤器，只能在 当前 VM 对象所控制的 View 区域进行使用
    dataFormat(input, pattern = "") { // 在参数列表中 通过 pattern="" 来指定形参默认值，防止报错
      var dt = new Date(input);
      // 获取年月日
      var y = dt.getFullYear();
      var m = (dt.getMonth() + 1).toString().padStart(2, '0');
      var d = dt.getDate().toString().padStart(2, '0');
      // 如果 传递进来的字符串类型，转为小写之后，等于 yyyy-mm-dd，那么就返回 年-月-日
      // 否则，就返回  年-月-日 时：分：秒
      if (pattern.toLowerCase() === 'yyyy-mm-dd') {
        return `${y}-${m}-${d}`;
      } else {
        // 获取时分秒
        var hh = dt.getHours().toString().padStart(2, '0');
        var mm = dt.getMinutes().toString().padStart(2, '0');
        var ss = dt.getSeconds().toString().padStart(2, '0');
        return `${y}-${m}-${d} ${hh}:${mm}:${ss}`;
      }
    }
  }
```

> 使用ES6中的字符串新方法 `String.prototype.padStart(maxLength, fillString='')` 或 `String.prototype.padEnd(maxLength, fillString='')`来填充字符串；

### 全局过滤器

```javascript
// 定义一个全局过滤器，回调的第一个参数是管道符前面的值，其余的为调用时传递的参数
Vue.filter('dataFormat', function (input, pattern = '') {
  var dt = new Date(input);
  // 获取年月日
  var y = dt.getFullYear();
  var m = (dt.getMonth() + 1).toString().padStart(2, '0');
  var d = dt.getDate().toString().padStart(2, '0');
  // 如果 传递进来的字符串类型，转为小写之后，等于 yyyy-mm-dd，那么就返回 年-月-日
  // 否则，就返回  年-月-日 时：分：秒
  if (pattern.toLowerCase() === 'yyyy-mm-dd') {
    return `${y}-${m}-${d}`;
  } else {
    // 获取时分秒
    var hh = dt.getHours().toString().padStart(2, '0');
    var mm = dt.getMinutes().toString().padStart(2, '0');
    var ss = dt.getSeconds().toString().padStart(2, '0');
    return `${y}-${m}-${d} ${hh}:${mm}:${ss}`;
  }
});
```

> 注意：当有局部和全局两个名称相同的过滤器时候，会以就近原则进行调用，即：局部过滤器优先于全局过滤器被调用！

## 键盘修饰符以及自定义键盘修饰符

### 键盘修饰符

内置：.enter,.tab,.delete,.esc,.space,.up,.down,.left,.right

`<input type="text" v-model="name" @keyup.enter="add">`

也可以直接使用键盘码值

### [2.x中自定义键盘修饰符](https://cn.vuejs.org/v2/guide/events.html#键值修饰符)

1. 通过`Vue.config.keyCodes.名称 = 按键值`来自定义案件修饰符的别名：

```js
Vue.config.keyCodes.f2 = 113;
```

1. 使用自定义的按键修饰符：

```html
<input type="text" v-model="name" @keyup.f2="add">
```

## 相关文章

1. [vue.js 1.x 文档](https://v1-cn.vuejs.org/)
2. [vue.js 2.x 文档](https://cn.vuejs.org/)
3. [String.prototype.padStart(maxLength, fillString)](http://www.css88.com/archives/7715)
4. [js 里面的键盘事件对应的键码](http://www.cnblogs.com/wuhua1/p/6686237.html)
5. [Vue.js双向绑定的实现原理](http://www.cnblogs.com/kidney/p/6052935.html)


##axios

和vue-resource用法相似，没有jsonp，没有挂载到实例中，可以直接使用

## axios

### all()方法

```js
function getUserName() {
    return axios.get('')
}
function getUserAge() {
    return axios.get('')
}
axios.all(getUserName(), getUserAge())
    .then(axios.spread(function(name, age) {
    // 两个请求都完成之后
}))
```

### 拦截器

```js
axios.interceptor.request.use(function(config) {
    // todo
    return config
})
axios.interceptor.response.use(function(response) {
    // todo
    return response
})
```

### 配置



## [vue-resource](https://github.com/pagekit/vue-resource)

### http请求

除了 vue-resource 之外，还可以使用 `axios` 的第三方包实现实现数据的请求

JSONP的实现原理

- 由于浏览器的安全性限制，不允许AJAX访问 协议不同、域名不同、端口号不同的 数据接口，浏览器认为这种访问不安全；
- 可以通过动态创建script标签的形式，把script标签的src属性，指向数据接口的地址，因为script标签不存在跨域限制，这种数据获取方式，称作JSONP（注意：根据JSONP的实现原理，JSONP只支持Get请求）；
- 具体实现过程：
  - 先在客户端定义一个回调方法，预定义对数据的操作；
    - 再把这个回调方法的名称，通过URL传参的形式，提交到服务器的数据接口；
    - 服务器数据接口组织好要发送给客户端的数据，再拿着客户端传递过来的回调方法名称，拼接出一个调用这个方法的字符串，发送给客户端去解析执行；
    - 客户端拿到服务器返回的字符串之后，当作Script脚本去解析执行，这样就能够拿到JSONP的数据了；
- Node.js 手动实现一个JSONP的请求例子；

```javascript
    const http = require('http');
    // 导入解析 URL 地址的核心模块
    const urlModule = require('url');

    const server = http.createServer();
    // 监听 服务器的 request 请求事件，处理每个请求
    server.on('request', (req, res) => {
      const url = req.url;

      // 解析客户端请求的URL地址
      var info = urlModule.parse(url, true);

      // 如果请求的 URL 地址是 /getjsonp ，则表示要获取JSONP类型的数据
      if (info.pathname === '/getjsonp') {
        // 获取客户端指定的回调函数的名称
        var cbName = info.query.callback;
        // 手动拼接要返回给客户端的数据对象
        var data = {
          name: 'zs',
          age: 22,
          gender: '男',
          hobby: ['吃饭', '睡觉', '运动']
        }
        // 拼接出一个方法的调用，在调用这个方法的时候，把要发送给客户端的数据，序列化为字符串，作为参数传递给这个调用的方法：
        var result = `${cbName}(${JSON.stringify(data)})`;
        // 将拼接好的方法的调用，返回给客户端去解析执行
        res.end(result);
      } else {
        res.end('404');
      }
    });

    server.listen(3000, () => {
      console.log('server running at http://127.0.0.1:3000');
    });
```

vue-resource 的配置步骤：

- 直接在页面中，通过`script`标签，引入 `vue-resource` 的脚本文件；
- 注意：引用的先后顺序是：先引用 `Vue` 的脚本文件，再引用 `vue-resource` 的脚本文件；

| Parameter        | Type                           | Description                                                  |
| ---------------- | ------------------------------ | ------------------------------------------------------------ |
| url              | `string`                       | URL to which the request is sent                             |
| body             | `Object`, `FormData`, `string` | Data to be sent as the request body                          |
| headers          | `Object`                       | Headers object to be sent as HTTP request headers            |
| params           | `Object`                       | Parameters object to be sent as URL parameters               |
| method           | `string`                       | HTTP method (e.g. GET, POST, ...)                            |
| responseType     | `string`                       | Type of the response body (e.g. text, blob, json, ...)       |
| timeout          | `number`                       | Request timeout in milliseconds (`0` means no timeout)       |
| credentials      | `boolean`                      | Indicates whether or not cross-site Access-Control requests should be made using credentials |
| emulateHTTP      | `boolean`                      | Send PUT, PATCH and DELETE requests with a HTTP POST and set the `X-HTTP-Method-Override` header |
| emulateJSON      | `boolean`                      | Send request body as `application/x-www-form-urlencoded` content type |
| before           | `function(request)`            | Callback function to modify the request object before it is sent |
| uploadProgress   | `function(event)`              | Callback function to handle the [ProgressEvent](https://developer.mozilla.org/en-US/docs/Web/API/ProgressEvent) of uploads |
| downloadProgress | `function(event)`              | Callback function to handle the [ProgressEvent](https://developer.mozilla.org/en-US/docs/Web/API/ProgressEvent) of downloads |

发送get请求：

```javascript
getInfo() { // get 方式获取数据
  this.$http.get('http://127.0.0.1:8899/api/getlunbo').then(res => {
    console.log(res.body);
  })
}
```

发送post请求：

```javascript
postInfo() {
  var url = 'http://127.0.0.1:8899/api/post';
  // post 方法接收三个参数：
  // 参数1： 要请求的URL地址
  // 参数2： 要发送的数据对象
  // 参数3： 指定post提交的编码类型为 application/x-www-form-urlencoded
  this.$http.post(url, { name: 'zs' }, { emulateJSON: true }).then(res => {
    console.log(res.body);
  });
}
```

发送JSONP请求获取数据：

```js
jsonpInfo() { // JSONP形式从服务器获取数据
  var url = 'http://127.0.0.1:8899/api/jsonp';
  this.$http.jsonp(url).then(res => {
    console.log(res.body);
  });
}
```

对象参数的形式发送请求

`this.$http({url: '', params:{}, headers:{}, timeout:5, before: fn})`

### 全局拦截器interceptors

应用loading处理

```js
// 请求也可以使用Vue.http发送，由于被挂载到实例中所以也可以通过this.$http
// 可以在mounted函数中创建全局拦截器
Vue.http.interceptors.push((req, next)=>{
    // 请求发送前
    next(res=>{
        // 请求发送后
        return res
    })
})
```

### 配置

- 全局配置数据接口根域名，配置过后，用到的地方不能加/

`Vue.http.options.root = '/root'`

也可以在vm实例中的http属性中配置

`http: {root: ''}`

- 全局配置emulateJSON

`Vue.http.options.emulateJSON= true`

## [Vue动画](https://cn.vuejs.org/v2/guide/transitions.html)

为什么要有动画：动画能够提高用户的体验，帮助用户更好的理解页面中的功能；

### 使用过渡类名

![1543925491592](C:\Users\ADMINI~1\AppData\Local\Temp\1543925491592.png)	

1. HTML结构：

```html
<div id="app">
    <input type="button" value="动起来" @click="myAnimate">
    <!-- 使用 transition 将需要过渡的元素包裹起来，name是类名的前缀，没有时是v- -->
    <transition name="fade">
      <div v-show="isshow">动画哦</div>
    </transition>
  </div>
```

2. VM 实例：

```javascript
// 创建 Vue 实例，得到 ViewModel
var vm = new Vue({
  el: '#app',
  data: {
    isshow: false
  },
  methods: {
    myAnimate() {
      this.isshow = !this.isshow;
    }
  }
});
```

3. 定义两组类样式：

```css
/* 定义进入和离开时候的过渡状态 */
.fade-enter-active,
.fade-leave-active {
    transition: all 0.2s ease;
    position: absolute;
}

/* 定义进入过渡的开始状态 和 离开过渡的结束状态 */
.fade-enter,
.fade-leave-to {
    opacity: 0;
    transform: translateX(100px);
}
```

### [使用第三方 CSS 动画库](https://cn.vuejs.org/v2/guide/transitions.html#自定义过渡类名)

animate.css

1. 导入动画类库：

```
<link rel="stylesheet" type="text/css" href="./lib/animate.css">
```

2. 定义 transition 及属性：

```html
<transition>
    <!-- animated也可以放在这里 -->
	enter-active-class="fadeInRight"
    leave-active-class="fadeOutRight"
    <!-- 时间相同可以直接等于500 -->
    :duration="{ enter: 500, leave: 800 }">
  	<div class="animated" v-show="isshow">动画哦</div>
</transition>
```

### 使用动画钩子函数实现半场动画

1. 定义 transition 组件以及三个钩子函数：

```html
<div id="app">
    <input type="button" value="切换动画" @click="isshow = !isshow">
    <transition
                @before-enter="beforeEnter"
                @enter="enter"
                @after-enter="afterEnter">
        <div v-if="isshow" class="show">OK</div>
    </transition>
</div>
```

2. 定义三个 methods 钩子方法：

```javascript
methods: {
    beforeEnter(el) { // 动画进入之前的回调
    	el.style.transform = 'translateX(500px)'; // 初始化位置，保证每次的起点位置
    },
    enter(el, done) { // 动画进入完成时候的回调
        el.offsetWidth; // 没有实际作用，不设置没有动画效果，相当于强制刷新
        el.style.transform = 'translateX(0px)';
        done(); // afterEnter的函数引用，使动画完成后，立即执行
    },
    afterEnter(el) { // 动画进入完成之后的回调
    	this.isshow = !this.isshow;
    }
}
```

3. 定义动画过渡时长和样式：

```css
.show{
      transition: all 0.4s ease;
    }
```

### [v-for 的列表过渡](https://cn.vuejs.org/v2/guide/transitions.html#列表的进入和离开过渡)

1. 定义过渡样式：

```html
<style>
    .list-enter,
    .list-leave-to {
      opacity: 0;
      transform: translateY(10px);
    }

    .list-enter-active,
    .list-leave-active {
      transition: all 0.3s ease;
    }
</style>
```

2. 定义DOM结构，其中，需要使用 transition-group 组件把v-for循环的列表包裹起来：

```html
  <div id="app">
    <input type="text" v-model="txt" @keyup.enter="add">
	<!-- 需要使用 transition-group 组件把v-for循环的列表包裹起来，并且必须设置key属性 -->
    <!-- appear可以实现第一次显示时渐进的入场效果 -->
    <!-- 默认将transition-group渲染成span元素，可使用tag修改 -->
    <transition-group tag="ul" name="list" appear tag="ul">
      <li v-for="(item, i) in list" :key="i">{{item}}</li>
    </transition-group>
  </div>
```

3. 定义 VM中的结构：

```javascript
    // 创建 Vue 实例，得到 ViewModel
    var vm = new Vue({
      el: '#app',
      data: {
        txt: '',
        list: [1, 2, 3, 4]
      },
      methods: {
        add() {
          this.list.push(this.txt);
          this.txt = '';
        }
      }
    });
```

### 列表的排序过渡

`<transition-group>` 组件还有一个特殊之处。不仅可以进入和离开动画，**还可以改变定位**。要使用这个新功能只需了解新增的 `v-move` 特性，**它会在元素的改变定位的过程中应用**。

- `v-move` 和 `v-leave-active` 结合使用，能够让列表的过渡更加平缓柔和：

```
.v-move{
  transition: all 0.8s ease;
}
.v-leave-active{
  position: absolute;
}
```

## 相关文章

1. [vue.js 1.x 文档](https://v1-cn.vuejs.org/)
2. [vue.js 2.x 文档](https://cn.vuejs.org/)
3. [String.prototype.padStart(maxLength, fillString)](http://www.css88.com/archives/7715)
4. [js 里面的键盘事件对应的键码](http://www.cnblogs.com/wuhua1/p/6686237.html)
5. [pagekit/vue-resource](https://github.com/pagekit/vue-resource)
6. [navicat如何导入sql文件和导出sql文件](https://jingyan.baidu.com/article/a65957f4976aad24e67f9b9b.html)
7. [贝塞尔在线生成器](http://cubic-bezier.com/#.4,-0.3,1,.33)

## Vue组件

什么是组件： 组件的出现，就是为了拆分Vue实例的代码量的，能够让我们以不同的组件，来划分不同的功能模块，将来我们需要什么样的功能，就可以去调用对应的组件即可；
组件化和模块化的不同：

- 模块化： 是从代码逻辑的角度进行划分的；方便代码分层开发，保证每个功能模块的职能单一；
- 组件化： 是从UI界面的角度进行划分的；前端的组件化，方便UI组件的重用；

### 全局组件定义的三种方式

extend这个 API 很少用到，作用是扩展组件生成一个构造器，通常会与 `$mount` 一起使用。

```js
// 创建组件构造器
let Component = Vue.extend({
  template: '<div>test</div>'
})
// 挂载到 #app 上
new Component().$mount('#app')
// 除了上面的方式，还可以用来扩展已有的组件
let SuperComponent = Vue.extend(Component)
new SuperComponent({
    created() {
        console.log(1)
    }
})
new SuperComponent().$mount('#app')
```

1. 使用 Vue.extend 配合 Vue.component 方法：

```javascript
var login = Vue.extend({
	template: '<h1>登录</h1>'
});
// Vue.component('组件名称', 模板对象)
// 注册时可以用驼峰，使用时必须改为-连接
Vue.component('login', login);
```

2. 直接使用 Vue.component 方法：

```
Vue.component('register', {
	template: '<h1>注册</h1>'
});
```

3. 将模板字符串，定义到template标签中：

```
<template id="tmpl">
	 <div><a href="#">登录</a> | <a href="#">注册</a></div>
</template>
```

同时，需要使用 Vue.component 来定义组件：

```
Vue.component('account', {
	template: '#tmpl'
});
```

> 注意： 组件中的DOM结构，有且只能有唯一的根元素（Root Element）来进行包裹！

### 使用render函数渲染组件

```javascript
var login = {
    template: '#login'
}

var vm = new Vue({
    el: '#app',
    data: {},
    methods: {},
    // 返回渲染好的html结构替换el指定的容器
    render: function(createElement) {
        return createElement(login)
    }
})
```

### 组件中展示数据和响应事件

1. 在组件中，`data`需要被定义为一个方法并返回一个对象，例如：

如果不通过方法返回，所有的组件会公用同一个data，如果 `data` 是对象的话，就会造成一个组件修改 `data` 以后会影响到其他所有组件，所以需要将 `data` 写成函数，每次用到就调用一次函数获得新的数据。 

当我们使用 `new Vue()` 的方式的时候，无论我们将 `data` 设置为对象还是函数都是可以的，因为 `new Vue()` 的方式是生成一个根组件，该组件不会复用，也就不存在共享 `data` 的情况了。 

```javascript
Vue.component('account', {
    template: '#tmpl',
    data() {
        return {
        msg: '大家好！'
	}
},
    methods:{
        login(){
            alert('点击了登录按钮');
        }
    }
});
```

2. 在子组件中，如果将模板字符串，定义到了script标签中，那么，要访问子组件身上的`data`属性中的值，需要使用`this`来访问；

### 使用`components`属性定义局部子组件

1. 组件实例定义方式：

```html
<script>
    // 创建 Vue 实例，得到 ViewModel
    var vm = new Vue({
      el: '#app',
      data: {},
      methods: {},
      components: { // 定义子组件
        account: { // account 组件
          template: '<div><h1>这是Account组件{{name}}</h1><login></login></div>', // 在这里使用定义的子组件
          components: { // 定义子组件的子组件
            login: { // login 组件
              template: "<h3>这是登录组件</h3>"
            }
          }
        }
      }
    });
</script>
```

2. 引用组件，引用时组件名不能大写：

```
<div id="app">
    <account></account>
</div>
```

### 切换组件：`flag`标识符结合`v-if`和`v-else`

1. 页面结构：

```html
<div id="app">
    <input type="button" value="toggle" @click="flag=!flag">
    <my-com1 v-if="flag"></my-com1>
    <my-com2 v-else="flag"></my-com2>
</div>
```

2. Vue实例定义：

```html
<script>
    Vue.component('myCom1', {
      template: '<h3>奔波霸</h3>'
    })

    Vue.component('myCom2', {
      template: '<h3>霸波奔</h3>'
    })

    // 创建 Vue 实例，得到 ViewModel
    var vm = new Vue({
      el: '#app',
      data: {
        flag: true
      },
      methods: {}
    });
</script>
```

### 切换组件：`:is`属性,并添加切换动画

1. 组件实例定义方式：

```javascript
  // 登录组件
    const login = Vue.extend({
      template: `<div>
        <h3>登录组件</h3>
      </div>`
    });
    Vue.component('login', login);

    // 注册组件
    const register = Vue.extend({
      template: `<div>
        <h3>注册组件</h3>
      </div>`
    });
    Vue.component('register', register);

    // 创建 Vue 实例，得到 ViewModel
    var vm = new Vue({
      el: '#app',
      data: { comName: 'login' },
      methods: {}
  });
```

1. 使用`component`标签，来引用组件，并通过`:is`属性来指定要加载的组件：

```html
  <div id="app">
    <a href="#" @click.prevent="comName='login'">登录</a>
    <a href="#" @click.prevent="comName='register'">注册</a>
    <hr>
    <!-- mode：设置动画模式，out-in避免动画同时发生 -->
    <transition mode="out-in">
      <component :is="comName"></component>
    </transition>
  </div>
```

1. 添加切换样式：

```html
  <style>
    .v-enter,
    .v-leave-to {
      opacity: 0;
      transform: translateX(30px);
    }

    .v-enter-active,
    .v-leave-active {
    
      position: absolute;
      transition: all 0.3s ease;
    }

    h3{
      margin: 0;
    }
  </style>
```

### 组件通信

#### 父子通信

#####通过 `props` 

父组件通过 `props` 传递数据给子组件，子组件通过 `emit` 发送事件传递数据给父组件，这两种方式是最常用的父子通信实现办法。

这种父子通信方式也就是典型的**单向数据流**，父组件通过 `props` 传递数据，子组件不能直接修改 `props`， 而是必须通过发送事件的方式告知父组件修改数据。

- 父组件向子组件传值

组件实例定义方式，注意：一定要使用`props`属性来定义父组件传递过来的数据

```html
<script>
    // 创建 Vue 实例，得到 ViewModel
    var vm = new Vue({
      el: '#app',
      data: {
        msg: '这是父组件中的消息'
      },
      components: {
        son: {
          template: '<h1>这是子组件 --- {{finfo}}</h1>',
          // 从父组件传递过来的值，只读
          props: ['finfo']
        }
      }
    });
</script>
```

使用`v-bind`或简化指令，将数据传递到子组件中：

```html
<div id="app">
    <son :finfo="msg"></son>
</div>
```

使用v-on:传递方法

- 子组件向父组件传值

原理：父组件将方法的引用，传递到子组件内部，子组件在内部调用父组件传递过来的方法，同时把要发送给父组件的数据，在调用方法的时候当作参数传递进去；

父组件将方法的引用传递给子组件，其中，`getMsg`是父组件中`methods`中定义的方法名称，`func`是子组件调用传递过来方法时候的方法名称

```
<son @func="getMsg"></son>
```

子组件内部通过`this.$emit('方法名', 要传递的数据)`方式，来调用父组件中的方法，同时把数据传递给父组件使用

```html
<div id="app">
    <!-- 引用父组件 -->
    <son @func="getMsg"></son>

    <!-- 组件模板定义 -->
    <script type="x-template" id="son">
      <div>
        <input type="button" value="向父组件传值" @click="sendMsg" />
        </div>
    </script>
</div>

  <script>
    // 子组件的定义方式
    Vue.component('son', {
      template: '#son', // 组件模板Id
      methods: {
        sendMsg() { // 按钮的点击事件
          this.$emit('func', 'OK'); // 参数1调用父组件传递过来的方法，参数2把数据传递出去
        }
      }
    });

    // 创建 Vue 实例，得到 ViewModel
    var vm = new Vue({
      el: '#app',
      data: {},
      methods: {
        getMsg(val){ // 子组件中，通过 this.$emit() 实际调用的方法，在此进行定义
          alert(val);
        }
      }
    });
  </script>
```

#####使用语法糖 `v-model` 

使用语法糖 `v-model` 来直接实现，因为 `v-model` 默认会解析成名为 `value` 的 `prop` 和名为 `input` 的事件。这种语法糖的方式是典型的双向绑定，常用于 UI 控件上，但是究其根本，还是通过事件的方法让父组件修改数据。

**children组件**

```html
<template lang="pug">
  .demo
    .demo-example(@click="changePropsValue") {{value}}
</template>

<script>
export default {
  props: ['value'],
  methods: {
    changePropsValue () {
      this.$emit('input', '通过$emit触发input事件了')
    }
  }
}
</script>复制代码
```

这里的value前面说过了就是v-model传过来的value (  v-bind:value="something")，但是只能用value去接收
这里主要巧用了一点，平时我们改变input输入框的时候，input事件是自己主动触发的，但是，我们也同时可以给他手动触发，我们用$emit进行了手动触发(input)事件

**parent组件**

```html
<template lang="pug">
  div
    demo(v-model ='msg')
</template>

<script>
import Demo from './demo.vue'
export default {
  data () {
    return {
      msg: '首次数据传递'
    }
  },
  components: {
    Demo
  }
}
</script>复制代码
```

这个我们直接用v-model像表单那样绑定就直接可以进行父子组件双向绑定了。在v-model的语法糖里封装了v-on:input 去进行监听事件

#####通过访问 `$parent` 或者 `$children` 对象

当然我们还可以通过访问 `$parent` 或者 `$children` 对象来访问组件实例中的方法和数据。

这在一些显示操作的时候，向外部暴露props和event的时候是不推荐用的，那有人要问了**$$parent**什么时候用呢，在一些自己内部逻辑操用的时候可以用一下，不用很繁琐的来进行双向来回导，节省代码和逻辑，有时候也可以让人一目了然

**children组件**

```html
<template lang="pug">
  .demo
    .demo-example(@click="changePropsValue") 点击按钮
</template>


<script>
export default {
  methods: {
    changePropsValue () {
      this.$parent.msg = '通过$parent改变了更新事件'
    }
  }
}
</script>复制代码
```

子组件，通过点击按钮，显示的改变了父组件的parent.msg里面的数据

**parent**

```html
<template lang="pug">
  div
    demo
    p {{msg}}
</template>

<script>
import Demo from './demo.vue'
export default {
  data () {
    return {
      msg: '第一次写入数据'
    }
  },
  components: {
    Demo
  }
}
</script>复制代码
```

#####使用 `$listeners` 和 `.sync`

另外如果你使用 Vue 2.3 及以上版本的话还可以使用 `$listeners` 和 `.sync` 这两个属性。

`$listeners` 属性会将父组件中的 (不含 `.native` 修饰器的) `v-on` 事件监听器传递给子组件，子组件可以通过访问 `$listeners` 来自定义监听器。

`.sync` 属性是个语法糖，可以很简单的实现子组件与父组件通信

**children组件**

```html
<template lang="pug">
  .demo
    .demo-example(@click="changePropsValue") {{msg}}
</template>


<script>
export default {
  props: ['msg'],
  methods: {
    changePropsValue () {
      this.$emit('update:msg', '通过$emit显示触发了更新事件')
    }
  }
}
</script>复制代码
```

1.通过props来进行msg的数据接收
2.通过$emit来进行触发，第一个参数则是显示触发，update:msg  (msg)则是你需要改变的props里从父组件里接收的值，第二个参数，还是你要更新的值，从语意上设计的也很有感觉，有木有

**parent**

```html
<template lang="pug">
  div
    demo(:msg.sync="msg")
</template>

<script>
import Demo from './demo.vue'
export default {
  data () {
    return {
      msg: '首次数据传递'
    }
  },
  components: {
    Demo
  }
}
</script>复制代码
```

主要看demo(:msg.sync="msg") 这里直接在向子组件传递的时候还是像1.0的时候加一个.sync,本质上还是它会被扩展为一个自动更新父组件属性的 v-on 侦听器
(推荐用法，一般对一个模态框进行封装的时候很有用，有了.sync不建议用v-model)

```html
<!--父组件中-->
<input :value.sync="value" />
<!--以上写法等同于-->
<input :value="value" @update:value="v => value = v"></comp>
<!--子组件中-->
<script>
  this.$emit('update:value', 1)
</script>
```

#### 兄弟组件通信

对于这种情况可以通过查找父组件中的子组件实现，也就是 `this.$parent.$children`，在 `$children`中可以通过组件 `name` 查询到需要的组件实例，然后进行通信。

####跨多层次组件通信

对于这种情况可以使用 Vue 2.2 新增的 API `provide / inject`，虽然文档中不推荐直接使用在业务中，但是如果用得好的话还是很有用的。

假设有父组件 A，然后有一个跨多层级的子组件 B

```js
// 父组件 A
export default {
  provide: {
    data: 1
  }
}
// 子组件 B
export default {
  inject: ['data'],
  mounted() {
    // 无论跨几层都能获得父组件的 data 属性
    console.log(this.data) // => 1
  }
}
```

#### 终极办法解决一切通信问题

只要你不怕麻烦，可以使用 Vuex 或者 Event Bus 解决上述所有的通信情况。

组件的嵌到超过3层的话，我还是建议用vuex来进行数据的共享，不然一层一层传，再一层一层的向上导，到最后你页面会把控不住，业务代码也就不直观了

## mixin 和 mixins 区别

`mixin` 用于全局混入，会影响到每个组件实例，通常插件都是这样做初始化的。

```js
Vue.mixin({
    beforeCreate() {
        // ...逻辑
        // 这种方式会影响到每个组件的 beforeCreate 钩子函数
    }
})
```

虽然文档不建议我们在应用中直接使用 `mixin`，但是如果不滥用的话也是很有帮助的，比如可以全局混入封装好的 `ajax` 或者一些工具函数等等。

`mixins` 应该是我们最常使用的扩展组件的方式了。如果多个组件中有相同的业务逻辑，就可以将这些逻辑剥离出来，通过 `mixins` 混入代码，比如上拉下拉加载数据这种逻辑等等。

另外需要注意的是 `mixins` 混入的钩子函数会先于组件内的钩子函数执行，并且在遇到同名选项的时候也会有选择性的进行合并，具体可以阅读 [文档](https://link.juejin.im/?target=https%3A%2F%2Fcn.vuejs.org%2Fv2%2Fguide%2Fmixins.html)。

## 特性

### 使用 `this.$refs` 来获取元素和组件

```html
  <div id="app">
    <div>
      <input type="button" value="获取元素内容" @click="getElement" />
      <!-- 使用 ref 获取元素 -->
      <h1 ref="myh1">这是一个大大的H1</h1>

      <hr>
      <!-- 使用 ref 获取子组件 -->
      <my-com ref="mycom"></my-com>
    </div>
  </div>

  <script>
    Vue.component('my-com', {
      template: '<h5>这是一个子组件</h5>',
      data() {
        return {
          name: '子组件'
        }
      }
    });

    // 创建 Vue 实例，得到 ViewModel
    var vm = new Vue({
      el: '#app',
      data: {},
      methods: {
        getElement() {
          // 通过 this.$refs 来获取元素
          console.log(this.$refs.myh1.innerText);
          // 通过 this.$refs 来获取组件，可以获取到data和方法
          console.log(this.$refs.mycom.name);
        }
      }
    });
  </script>
```

### slot插槽

在定义组件时声明为插槽的部分可以在使用时进行定义，即可以动态加载组件中的一部分，在组件使用的位置定义插槽的内容，如果没有定义插槽，内容会被抛弃

声明插槽：`<slot name="sname"></slot>`

使用插槽：在使用组件时所有内容会被渲染到组件的slot区域

使用具名插槽：`<span slot="sname"><a>...</a>...</span>`会替换组件对应的slot区域

## 路由

> 涉及面试题：前端路由原理？两种实现方式有什么区别？

1. **后端路由：**对于普通的网站，所有的超链接都是URL地址，所有的URL地址都对应服务器上对应的资源；

2. **前端路由**实现起来其实很简单，本质就是**监听 URL 的变化**，然后匹配路由规则，显示相应的页面，并且无须刷新页面。目前前端使用的路由就只有两种实现方式

- Hash 模式
- History 模式

### Hash 模式

[路由模式](https://www.cnblogs.com/goloving/p/9147551.html)

`www.test.com/#/` 就是 Hash URL，当 `#` 后面的哈希值发生变化时，可以**通过 `hashchange` 事件来监听到 URL 的变化**，从而进行跳转页面，并且无论哈希值如何变化，服务端接收到的 URL 请求永远是 `www.test.com`。

```js
window.addEventListener('hashchange', () => {
  // ... 具体逻辑
})

```

可以在`window`对象上监听这个事件 

```js
window.onhashchange = function(event){
    console.log(event.oldURL, event.newURL);
    let hash = location.hash.slice(1);
    document.body.style.color = hash;
}
```

上面的代码可以通过改变hash来改变页面字体颜色，一定程度上说明了原理。

更关键的一点是，因为**hash发生变化的url都会被浏览器记录下来**，从而你会发现浏览器的前进后退都可以用了，同时点击后退时，页面字体颜色也会发生变化。这样一来，尽管浏览器没有请求服务器，但是页面状态和url一一关联起来。

`vue-router` 默认 hash 模式 —— 使用 URL 的 hash 来模拟一个完整的 URL，于是当 URL 改变时，页面不会重新加载。 

Hash 模式相对来说**更简单，并且兼容性也更好**。 

### History 模式

随着history api的到来，前端路由开始进化了，前面的**hashchange，你只能改变#后面的url片段，而history api则给了前端完全的自由**

History 模式是 HTML5 新推出的功能，主要使用 `history.pushState` 和 `history.replaceState` 改变 URL。

通过 History 模式改变 URL **同样不会引起页面的刷新，只会更新浏览器的历史记录**。

```js
// 新增历史记录
history.pushState(stateObject, title, URL)
// 替换当前历史记录
history.replaceState(stateObject, title, URL)

```

当用户做出浏览器动作时，比如点击后退按钮时会触发 `popState` 事件

```js
window.addEventListener('popstate', e => {
  // e.state 就是 pushState(stateObject) 中的 stateObject
  console.log(e.state)
})
```

`vue-router`的history模式充分利用 `history.pushState` API 来完成 URL 跳转而无须重新加载页面。

不过这种模式要玩好，还**需要后台配置支持**。因为我们的应用是个单页客户端应用，如果后台没有正确的配置，当用户在浏览器直接访问 `http://oursite.com/user/id` 就会返回 404 。要在服务端增加一个覆盖所有情况的候选资源：如果 URL 匹配不到任何静态资源，则应该返回同一个 `index.html` 页面，这个页面就是你 app 依赖的页面。  

### 两种模式对比

- Hash 模式只可以更改 `#` 后面的内容，History 模式可以通过 API 设置任意的同源 URL
- History 模式可以通过 API 添加任意类型的数据到历史记录中，Hash 模式只能更改哈希值，也就是字符串
- Hash 模式无需后端配置，并且兼容性好。History 模式在用户手动输入地址或者刷新页面的时候会发起 URL 请求，后端需要配置 `index.html` 页面用于匹配不到静态资源的时候

### 在 vue 中使用 vue-router

1. 导入 vue-router 组件类库：

```
<!-- 1. 导入 vue-router 组件类库 -->
  <script src="./lib/vue-router-2.7.0.js"></script>
```

1. 使用 router-link 组件来导航

```html
<!-- 2. 使用 router-link 组件来导航，也可以在地址前加# -->
<router-link to="/login">登录</router-link>
<router-link to="/register">注册</router-link>
```

1. 使用 router-link 组件来传参

`<router-link :to={path: '', query: {'': ''}}>登录</router-link>`

1. 使用 router-view 组件来显示匹配到的组件

```
<!-- 3. 使用 router-view 组件来显示匹配到的组件 -->
<router-view></router-view>
```

1. 创建使用`Vue.extend`创建组件

```javascript
    // 4.1 使用 Vue.extend 来创建登录组件
    var login = Vue.extend({
      template: '<h1>登录组件</h1>'
    });

    // 4.2 使用 Vue.extend 来创建注册组件
    var register = Vue.extend({
      template: '<h1>注册组件</h1>'
    });
```

1. 创建一个路由 router 实例，通过 routers 属性来定义路由匹配规则

```javascript
// 5. 创建一个路由 router 实例，通过 routers 属性来定义路由匹配规则
    var router = new VueRouter({
      routes: [
        { path: '/login', component: login },
        { path: '/register', component: register }
      ]
    });
```

1. 使用 router 属性来监听url地址变化使用路由规则展示响应的组件

```javascript
// 6. 创建 Vue 实例，得到 ViewModel
    var vm = new Vue({
      el: '#app',
      router: router // 使用 router 属性来使用路由规则
    });
```

过程：修改url==》监听到路由改变==》进行路由匹配==》在画面指定位置显示指定组件

### 路由重定向

和后台的重定向完全不同

`{path: '/', redirect: '/login'}`

### 设置路由高亮

在切换路由时选中的路由class会改变，可以利用这一点给当前路由添加样式

```css
.router-link-active {
    color: red;
}
```

修改全局激活类名，在路由的构造选项`linkActiveClass`修改

### 设置路由切换动效

router-view外添加transition，设置动画类和过渡模式

### 动态路由：在路由规则中定义参数

1. 在规则中使用占位符定义参数：

```
{ path: '/register/:id', component: register }
```

1. 通过 `this.$route.params`来获取路由中的参数：

```
var register = Vue.extend({
      template: '<h1>注册组件 --- {{this.$route.params.id}}</h1>'
});
```

通过 `this.$route.query`来获取路由查询字符串中的参数，path不用修改

###  `children` 属性实现路由嵌套

```html
  <div id="app">
    <router-link to="/account">Account</router-link>
    <router-view></router-view>
  </div>

  <script>
    // 父路由中的组件
    const account = Vue.extend({
      template: `<div>
        这是account组件
        <router-link to="/account/login">login</router-link> | 
        <router-link to="/account/register">register</router-link>
        <router-view></router-view>
      </div>`
    });

    // 子路由中的 login 组件
    const login = Vue.extend({
      template: '<div>登录组件</div>'
    });

    // 子路由中的 register 组件
    const register = Vue.extend({
      template: '<div>注册组件</div>'
    });

    // 路由实例
    var router = new VueRouter({
      routes: [
        { path: '/', redirect: '/account/login' }, // 使用 redirect 实现路由重定向
        {
          path: '/account',
          component: account,
          children: [ // 通过 children 数组属性，来实现路由的嵌套
            { path: 'login', component: login }, // 注意，子路由的开头位置，不要加 / 路径符
            { path: 'register', component: register }
          ]
        }
      ]
    });

    // 创建 Vue 实例，得到 ViewModel
    var vm = new Vue({
      el: '#app',
      data: {},
      methods: {},
      components: {
        account
      },
      router: router
    });
  </script>
```

#### 命名视图实现经典布局

1. 标签代码结构：

```html
<div id="app">
    <router-view></router-view>
    <div class="content">
      <router-view name="a"></router-view>
      <router-view name="b"></router-view>
    </div>
  </div>
```

1. JS代码：

```javascript
<script>
    var header = Vue.component('header', {
      template: '<div class="header">header</div>'
    });

    var sidebar = Vue.component('sidebar', {
      template: '<div class="sidebar">sidebar</div>'
    });

    var mainbox = Vue.component('mainbox', {
      template: '<div class="mainbox">mainbox</div>'
    });

    // 创建路由对象
    var router = new VueRouter({
      routes: [
        {
          path: '/', components: {
            default: header,
            a: sidebar,
            b: mainbox
          }
        }
      ]
    });

    // 创建 Vue 实例，得到 ViewModel
    var vm = new Vue({
      el: '#app',
      data: {},
      methods: {},
      router
    });
  </script>
```

1. CSS 样式：

```
  <style>
    .header {
      border: 1px solid red;
    }

    .content{
      display: flex;
    }
    .sidebar {
      flex: 2;
      border: 1px solid green;
      height: 500px;
    }
    .mainbox{
      flex: 8;
      border: 1px solid blue;
      height: 500px;
    }
  </style>
```

### 编程式导航

网页中的两种跳转方式：a标签，编程式导航（window.location.href）

vue中的编程式导航：绑定事件，在事件中跳转

```javascript
// 区分：this.$route是路由参数对象，this.$router是路由导航对象
this.$router.push('' + id)
this.$router.push({path:'' + id})
// name是路由规则的名字
// {path: '', component: comp, name: 'info'}
this.$router.push({name: 'info', params: {id: id}})
// 提供path，params会被忽略，不能同时使用
this.$router.push({path: '', query: {id: id}})

// $router的原型对象上有go(),forword(),back()
```

## `watch`属性的使用-侦听器

考虑一个问题：想要实现 `名` 和 `姓` 两个文本框的内容改变，则全名的文本框中的值也跟着改变；（用以前的知识使用keyup事件，只需要定义一个函数）

`watch` 监听到值的变化就会执行回调，在回调中可以进行一些逻辑操作。 

监听`data`中属性的改变：

```html
<div id="app">
    <input type="text" v-model="firstName"> +
    <input type="text" v-model="lastName"> =
    <span>{{fullName}}</span>
  </div>

  <script>
    // 创建 Vue 实例，得到 ViewModel
    var vm = new Vue({
      el: '#app',
      data: {
        firstName: 'jack',
        lastName: 'chen',
        fullName: 'jack - chen'
      },
      methods: {},
      watch: {
        'firstName': function (newVal, oldVal) { // 第一个参数是新数据，第二个参数是旧数据
          this.fullName = newVal + ' - ' + this.lastName;
        },
        'lastName': function (newVal, oldVal) {
          this.fullName = this.firstName + ' - ' + newVal;
        }
      }
    });
  </script>
```

监听路由对象的改变：

```html
<div id="app">
    <router-link to="/login">登录</router-link>
    <router-link to="/register">注册</router-link>

    <router-view></router-view>
  </div>

  <script>
    var login = Vue.extend({
      template: '<h1>登录组件</h1>'
    });

    var register = Vue.extend({
      template: '<h1>注册组件</h1>'
    });

    var router = new VueRouter({
      routes: [
        { path: "/login", component: login },
        { path: "/register", component: register }
      ]
    });

    // 创建 Vue 实例，得到 ViewModel
    var vm = new Vue({
      el: '#app',
      data: {},
      methods: {},
      router: router,
      watch: {
        '$route': function (newVal, oldVal) {
          if (newVal.path === '/login') {
            console.log('这是登录组件');
          }
        }
      }
    });
  </script>

```

`watch` 还支持对象的写法

```js
vm.$watch('obj', {
    // 深度遍历
    deep: true,
    // 立即触发
    immediate: true,
    // 执行的函数
    handler: function(val, oldVal) {}
})
```

## `computed`计算属性的使用

`computer` 是计算属性，依赖其他属性计算值，本质是一个方法，使用时当作把名称属性来使用

计算属性的求值结果会被缓存起来，方便下次直接调用，没有变化时不会重复计算

默认只有`getter`的计算属性：

```html
<div id="app">
    <input type="text" v-model="firstName"> +
    <input type="text" v-model="lastName"> =
    <span>{{fullName}}</span>
  </div>

  <script>
    // 创建 Vue 实例，得到 ViewModel
    var vm = new Vue({
      el: '#app',
      data: {
        firstName: 'jack',
        lastName: 'chen'
      },
      methods: {},
      computed: { // 计算属性； 特点：当计算属性中所以来的任何一个 data 属性改变之后，都会重新触发 本计算属性 的重新计算，从而更新 fullName 的值
        fullName() {
          return this.firstName + ' - ' + this.lastName;
        }
      }
    });
  </script>

```

定义有`getter`和`setter`的计算属性：

```html
<div id="app">
    <input type="text" v-model="firstName">
    <input type="text" v-model="lastName">
    <!-- 点击按钮重新为 计算属性 fullName 赋值 -->
    <input type="button" value="修改fullName" @click="changeName">

    <span>{{fullName}}</span>
  </div>

  <script>
    // 创建 Vue 实例，得到 ViewModel
    var vm = new Vue({
      el: '#app',
      data: {
        firstName: 'jack',
        lastName: 'chen'
      },
      methods: {
        changeName() {
          this.fullName = 'TOM - chen2';
        }
      },
      computed: {
        fullName: {
          get: function () {
            return this.firstName + ' - ' + this.lastName;
          },
          set: function (newVal) {
            var parts = newVal.split(' - ');
            this.firstName = parts[0];
            this.lastName = parts[1];
          }
        }
      }
    });
  </script>
```

## `watch`、`computed`和`methods`之间的对比

1. `computed`属性的结果会被缓存，除非依赖的响应式属性变化才会重新计算。主要当作属性来使用，必须有return；
2. `methods`方法表示一个具体的操作，主要书写业务逻辑；
3. `watch`一个对象，键是需要观察的表达式，值是对应回调函数。主要用来监听某些特定数据的变化，从而进行某些具体的业务逻辑操作；可以看作是`computed`和`methods`的结合体；
4. 一般来说需要依赖别的属性来动态获得值的时候可以使用 `computer`，对于监听到值的变化需要做一些复杂业务逻辑的情况可以使用 `watch`。 

## `nrm`的安装使用

作用：提供了一些最常用的NPM包镜像地址，能够让我们快速的切换安装包时候的服务器地址；
什么是镜像：原来包刚一开始是只存在于国外的NPM服务器，但是由于网络原因，经常访问不到，这时候，我们可以在国内，创建一个和官网完全一样的NPM服务器，只不过，数据都是从人家那里拿过来的，除此之外，使用方式完全一样；

1. 运行`npm i nrm -g`全局安装`nrm`包；
2. 使用`nrm ls`查看当前所有可用的镜像源地址以及当前所使用的镜像源地址；
3. 使用`nrm use npm`或`nrm use taobao`切换不同的镜像源地址；

## 相关文件

1. [URL中的hash（井号）](http://www.cnblogs.com/joyho/articles/4430148.html)

## ES6中语法使用总结

1. 使用 `export default` 和 `export` 导出模块中的成员; 对应ES5中的 `module.exports` 和 `export`

2. 使用 `import ** from **` 和 `import '路径'` 还有 `import {a, b} from '模块标识'` 导入其他模块

   也可以`import * as util from ''`

3. 使用箭头函数：`(a, b)=> { return a-b; }`

## Vuex

vue应用程序的状态管理模式，集中管理所有组件的状态

```javascript
import Vue from 'vue'
import Vuex from 'vuex'

const store = new vuex.Store({
    // 存储状态
    // 通过this.$store.state.xx来访问
    state: {
        count: 0
    },
    // 更改状态
    // 通过this.$store.commit('increment', 用来传递的参数2)来调用
    mutations: {
        increment(state, data) {
            state.count++
        }
    },
    // 通过getters向外提供数据，类似于过滤器和computed属性的集合
    // this.$getters.optCount获取
    getters: {
        optCount: function(state) {
            
    }
})

Vue.use(vuex)

const vm = new Vue({
    el: '#app',
    render: c=>c(App),
    // 挂载到vm上
    store
})
```

# Vue进阶

## 响应式原理

https://juejin.im/post/5a734b6cf265da4e70719386#heading-0

**vue实例初始化中data初始化时(initData(vm))通过`Observer`类将vue的`data`变成响应式，即为每一个data都利用`Object.defineProperty()`实现了getter/setter方法，用于进行依赖收集和通知更新。**

Observer类的walk()做的是遍历data对象中的每一设置的数据，defineReactive ()将其转为`setter/getter`。（new Observer(value) ）

为每个data声明一个`dep`实例对象

get

1. `dep`被对应的data给闭包引用了。举例来说就是每次对`counter`取值或修改时，它的dep实例都可以访问到，不会消失。
2. 在取值之前，根据`Dep.target`来判断是否收集依赖。dep.depend()

set

1. 对数据的值进行修改 

2. 即通过dep实例通知观察者我的数据更新了，dep.notify()

**随后进行`watch`的初始化(initWatch(vm: Component, watch: Object ))，创建Watcher实例**

Watcher：（new Watcher(vm, expOrFn, cb, options) ）

1. 构造函数：`this.deps = [] // 保存观察数据当前的dep实例对象 `

2. 获取对象的getter方法

3. get

   Dep.target = this，把Dep.target设置为该Watcher实例 ，Dep.target是个全局变量，一旦设置了在观察数据中的getter方法就可使用了

   调用getter方法，用来获取观察对象的值，并触发它的依赖收集。

   依赖收集完成后，重置Dep.target=null ，清除旧的deps

![Observer-Watcher-rel](https://user-gold-cdn.xitu.io/2018/2/2/1615530034cf9353?imageView2/0/w/1280/h/960/format/webp/ignore-error/1) 

- 红色箭头：Watcher类实例化，调用watcher实例的`get()`方法，并设置`Dep.target`为当前watcher实例，触发观察对象的`getter`方法。
- 蓝色箭头：`counter`对象的`getter`方法被触发，调用`dep.depend()`进行依赖收集并返回`counter`的值。依赖收集的结果：**1.counter闭包的dep实例的subs添加观察它的watcher实例w1**；**2. w1的deps中添加观察对象counter的闭包dep**。
- 橙色箭头：当`counter`的值变化后，触发`subs`中观察它的w1执行`update()`方法，最后实际上是调用w1的回调函数cb。

**Dep类**

```js
export default class Dep {
  static target: ?Watcher;
  id: number;
  subs: Array<Watcher>;
  constructor () {
    this.id = uid++
    // 保存观察者watcher实例的数组
    this.subs = []
  }
  // 添加观察者
  addSub (sub: Watcher) {
    this.subs.push(sub)
  }
  // 移除观察者
  removeSub (sub: Watcher) {
    remove(this.subs, sub)
  }
  // 进行依赖收集
  depend () {
    if (Dep.target) {
      Dep.target.addDep(this)
    }
  }
  // 通知观察者数据有变化
  notify () {
    // stabilize the subscriber list first
    const subs = this.subs.slice()
    for (let i = 0, l = subs.length; i < l; i++) {
      subs[i].update()
    }
  }
}
```

Dep类比较简单，对应方法也非常直观，这里最主要的就是维护了保存有观察者实例watcher的一个数组`subs`。

`Watcher`，`Dep`，`Observer`这几个类之间的关系？

A1：`Watcher`是观察者观察经过`Observer`封装过的数据，`Dep`是`Watcher`和观察数据间的纽带，主要起到依赖收集和通知更新的作用。

`Dep`中的`subs`存储的是什么？

A2: `subs`存储的是观察者Watcher实例。

`Watcher`中的`deps`存储的是什么？

A3：`deps`存储的是观察数据闭包中的`dep`实例。

`Dep.target`是什么， 该值是何处赋值的？

A4：`Dep.target`是全局变量，保存当前的watcher实例，在`new Watcher()`的时候进行赋值，赋值为当前Watcher实例。 

- 简单实现

Vue 内部使用了 `Object.defineProperty()` 来实现数据响应式，通过这个函数可以监听到 `set` 和 `get` 的事件。

```js
var data = { name: 'yck' }
observe(data)
let name = data.name // -> get value
data.name = 'yyy' // -> change value

// 添加监视
function observe(obj) {
  // 判断类型
  if (!obj || typeof obj !== 'object') {
    return
  }
  Object.keys(obj).forEach(key => {
    defineReactive(obj, key, obj[key])
  })
}

function defineReactive(obj, key, val) {
  // 递归子属性
  observe(val)
  // Object.defineProperty() 方法会直接在一个对象上定义一个新属性，或者修改一个对象的现有属性， 并返回这个对象。
  Object.defineProperty(obj, key, {
    // 可枚举
    enumerable: true,
    // 可配置
    configurable: true,
    // 自定义函数
    get: function reactiveGetter() {
      console.log('get value')
      return val
    },
    set: function reactiveSetter(newVal) {
      console.log('change value')
      val = newVal
    }
  })
}
```

以上代码简单的实现了如何监听数据的 `set` 和 `get` 的事件，但是仅仅如此是不够的，因为自定义的函数一开始是不会执行的。只有先执行了依赖收集，才能在属性更新的时候派发更新，所以接下来我们需要先触发依赖收集。

```html
<div>
    {{name}}
</div>
```

在解析如上模板代码时，遇到 `{{name}}` 就会进行依赖收集。

接下来我们先来实现一个 `Dep` 类，用于解耦属性的依赖收集和派发更新操作。

```js
// 通过 Dep 解耦属性的依赖和更新操作
class Dep {
  constructor() {
    this.subs = []
  }
  // 添加依赖
  addSub(sub) {
    this.subs.push(sub)
  }
  // 更新
  notify() {
    this.subs.forEach(sub => {
      sub.update()
    })
  }
}
// 全局属性，通过该属性配置 Watcher
Dep.target = null
```

以上的代码实现很简单，当需要依赖收集的时候调用 `addSub`，当需要派发更新的时候调用 `notify`。

接下来我们先来简单的了解下 Vue 组件挂载时添加响应式的过程。**在组件挂载时，会先对所有需要的属性调用 `Object.defineProperty()`，然后实例化 `Watcher`，传入组件更新的回调。在实例化过程中，会对模板中的属性进行求值，触发依赖收集。**

接下来的代码简略的表达触发依赖收集时的操作

```js
class Watcher {
  constructor(obj, key, cb) {
    // 将 Dep.target 指向自己
    // 然后触发属性的 getter 添加监听
    // 最后将 Dep.target 置空
    Dep.target = this
    this.cb = cb
    this.obj = obj
    this.key = key
    // 触发属性的 getter 添加监听
    this.value = obj[key]
    Dep.target = null
  }
  update() {
    // 获得新值
    this.value = this.obj[this.key]
    // 调用 update 方法更新 Dom
    this.cb(this.value)
  }
}
```

以上就是 `Watcher` 的简单实现，在执行构造函数的时候将 `Dep.target` 指向自身，从而使得收集到了对应的 `Watcher`，在派发更新的时候取出对应的 `Watcher` 然后执行 `update` 函数。

接下来，需要对 `defineReactive` 函数进行改造，在自定义函数中添加依赖收集和派发更新相关的代码。

```js
function defineReactive(obj, key, val) {
  // 递归子属性
  observe(val)
  let dp = new Dep()
  Object.defineProperty(obj, key, {
    enumerable: true,
    configurable: true,
    get: function reactiveGetter() {
      console.log('get value')
      // 将 Watcher 添加到订阅
      if (Dep.target) {
        dp.addSub(Dep.target)
      }
      return val
    },
    set: function reactiveSetter(newVal) {
      console.log('change value')
      val = newVal
      // 执行 watcher 的 update 方法
      dp.notify()
    }
  })
}
```

以上所有代码实现了一个简易的数据响应式，核心思路就是手动触发一次属性的 getter 来实现依赖收集。

现在我们就来测试下代码的效果，只需要把所有的代码复制到浏览器中执行，就会发现页面的内容全部被替换了。

```js
var data = { name: 'yck' }
// 添加监视
// 首先对所有需要的属性调用 Object.defineProperty()
observe(data)
function update(value) {
  document.querySelector('div').innerText = value
}
// 模拟解析到 `{{name}}` 触发的操作
// 然后实例化 Watcher，传入组件更新的回调。在实例化过程中，会对模板中的属性进行求值，触发依赖收集。
new Watcher(data, 'name', update)
// update Dom innerText
data.name = 'yyy' 
```

### Object.defineProperty 的缺陷

以上已经分析完了 Vue 的响应式原理，接下来说一点 `Object.defineProperty` 中的缺陷。

如果通过下标方式修改数组数据或者给对象新增属性并不会触发组件的重新渲染，因为 `Object.defineProperty` 不能拦截到这些操作，更精确的来说，对于数组而言，大部分操作都是拦截不到的，只是 Vue 内部通过重写函数的方式解决了这个问题。

对于第一个问题，Vue 提供了一个 API 解决

```js
export function set (target: Array<any> | Object, key: any, val: any): any {
  // 判断是否为数组且下标是否有效
  if (Array.isArray(target) && isValidArrayIndex(key)) {
    // 调用 splice 函数触发派发更新
    // 该函数已被重写
    target.length = Math.max(target.length, key)
    target.splice(key, 1, val)
    return val
  }
  // 判断 key 是否已经存在
  if (key in target && !(key in Object.prototype)) {
    target[key] = val
    return val
  }
  const ob = (target: any).__ob__
  // 如果对象不是响应式对象，就赋值返回
  if (!ob) {
    target[key] = val
    return val
  }
  // 进行双向绑定
  defineReactive(ob.value, key, val)
  // 手动派发更新
  ob.dep.notify()
  return val
}
```

对于数组而言，Vue 内部重写了以下函数实现派发更新

```js
// 获得数组原型
const arrayProto = Array.prototype
export const arrayMethods = Object.create(arrayProto)
// 重写以下函数
const methodsToPatch = [
  'push',
  'pop',
  'shift',
  'unshift',
  'splice',
  'sort',
  'reverse'
]
methodsToPatch.forEach(function (method) {
  // 缓存原生函数
  const original = arrayProto[method]
  // 重写函数
  def(arrayMethods, method, function mutator (...args) {
  // 先调用原生函数获得结果
    const result = original.apply(this, args)
    const ob = this.__ob__
    let inserted
    // 调用以下几个函数时，监听新数据
    switch (method) {
      case 'push':
      case 'unshift':
        inserted = args
        break
      case 'splice':
        inserted = args.slice(2)
        break
    }
    if (inserted) ob.observeArray(inserted)
    // 手动派发更新
    ob.dep.notify()
    return result
  })
})
```

## 编译过程

想必大家在使用 Vue 开发的过程中，基本都是使用模板的方式。那么你有过「模板是怎么在浏览器中运行的」这种疑虑嘛？

首先直接把模板丢到浏览器中肯定是不能运行的，模板只是为了方便开发者进行开发。Vue 会通过编译器将模板通过几个阶段最终编译为 `render` 函数，然后通过执行 `render` 函数生成 Virtual DOM 最终映射为真实 DOM。

接下来我们就来学习这个编译的过程，了解这个过程中大概发生了什么事情。这个过程其中又分为三个阶段，分别为：

1. 将模板解析为 AST
2. 优化 AST
3. 将 AST 转换为 `render` 函数

在第一个阶段中，最主要的事情还是通过各种各样的正则表达式去匹配模板中的内容，然后将内容提取出来做各种逻辑操作，接下来会生成一个最基本的 AST 对象

```js
{
    // 类型
    type: 1,
    // 标签
    tag,
    // 属性列表
    attrsList: attrs,
    // 属性映射
    attrsMap: makeAttrsMap(attrs),
    // 父节点
    parent,
    // 子节点
    children: []
}
```

然后会根据这个最基本的 AST 对象中的属性，进一步扩展 AST。

当然在这一阶段中，还会进行其他的一些判断逻辑。比如说对比前后开闭标签是否一致，判断根组件是否只存在一个，判断是否符合 HTML5 [Content Model](https://link.juejin.im/?target=https%3A%2F%2Fdeveloper.mozilla.org%2Fzh-CN%2Fdocs%2FWeb%2FGuide%2FHTML%2FContent_categories) 规范等等问题。

接下来就是优化 AST 的阶段。在当前版本下，Vue 进行的优化内容其实还是不多的。只是对节点进行了静态内容提取，也就是将永远不会变动的节点提取了出来，实现复用 Virtual DOM，跳过对比算法的功能。在下一个大版本中，Vue 会在优化 AST 的阶段继续发力，实现更多的优化功能，尽可能的在编译阶段压榨更多的性能，比如说提取静态的属性等等优化行为。

最后一个阶段就是通过 AST 生成 `render` 函数了。其实这一阶段虽然分支有很多，但是最主要的目的就是遍历整个 AST，根据不同的条件生成不同的代码罢了。

## NextTick 原理分析

`nextTick` 可以让我们在下次 DOM 更新循环结束之后执行延迟回调，用于获得更新后的 DOM。

在 Vue 2.4 之前都是使用的 microtasks，但是 microtasks 的优先级过高，在某些情况下可能会出现比事件冒泡更快的情况，但如果都使用 macrotasks 又可能会出现渲染的性能问题。所以在新版本中，会默认使用 microtasks，但在特殊情况下会使用 macrotasks，比如 v-on。

对于实现 macrotasks ，会先判断是否能使用 `setImmediate` ，不能的话降级为 `MessageChannel` ，以上都不行的话就使用 `setTimeout`

```
if (typeof setImmediate !== 'undefined' && isNative(setImmediate)) {
  macroTimerFunc = () => {
    setImmediate(flushCallbacks)
  }
} else if (
  typeof MessageChannel !== 'undefined' &&
  (isNative(MessageChannel) ||
    // PhantomJS
    MessageChannel.toString() === '[object MessageChannelConstructor]')
) {
  const channel = new MessageChannel()
  const port = channel.port2
  channel.port1.onmessage = flushCallbacks
  macroTimerFunc = () => {
    port.postMessage(1)
  }
} else {
  macroTimerFunc = () => {
    setTimeout(flushCallbacks, 0)
  }
}
```

以上代码很简单，就是判断能不能使用相应的 API。

https://segmentfault.com/a/1190000009065987)

## 在webpack中使用vue

1. 运行`cnpm i vue -S`将vue安装为运行依赖；引入

`import Vue from 'Vue'`这样直接导入的包是运行时的包，不是完整版

1. 运行`cnpm i vue-loader vue-template-compiler -D`将解析转换vue的包安装为开发依赖；
2. 运行`cnpm i style-loader css-loader -D`将解析转换CSS的包安装为开发依赖，因为.vue文件中会写CSS样式；
   1. 在`webpack.config.js`中，添加如下`module`规则：

```
module: {
    rules: [
      { test: /\.css$/, use: ['style-loader', 'css-loader'] },
      { test: /\.vue$/, use: 'vue-loader' } // 会将.vue文件进行解析
    ]
  }
```

1. 创建`App.vue`组件页面：
2. vsc中安装Vetur和Vue 2 Snippets插件可以得到vue文件的智能提示

```html
    <template>
      <!-- 注意：在 .vue 的组件中，template 中必须有且只有唯一的根元素进行包裹，一般都用 div 当作唯一的根元素 -->
      <div>
        <h1>这是APP组件 - {{msg}}</h1>
        <h3>我是h3</h3>
      </div>
    </template>
    <script>
    // 注意：在 .vue 的组件中，通过 script 标签来定义组件的行为，需要使用 ES6 中提供的 export default 方式，导出一个vue实例对象
    export default {
      data() {
        return {
          msg: 'OK'
        }
      }
    }
    </script>
    <style scoped>
    h1 {
      color: red;
    }
    </style>
```

1. 创建`main.js`入口文件：

```javascript
    // 导入 Vue 组件
    import Vue from 'vue'
    // 导入 App组件
    import App from './components/App.vue'
    // 创建一个 Vue 实例，使用 render 函数，渲染指定的组件
    var vm = new Vue({
      el: '#app',
      render: c => c(App)
    });
```

- 在使用webpack构建的Vue项目中使用模板对象

由于直接导入的包是运行时的包，不是完整版，不能使用Vue项目中使用模板对象

方法1可以直接修改vue包中package.json里main的配置，但是不推荐

方法2使用路径导入

方法3添加配置webpack.config.js

1. 在`webpack.config.js`中添加`resolve`属性：

```javascript
// 每次引入时会来到这里查找
resolve: {
    alias: {
      'vue$': 'vue/dist/vue.esm.js'
    }
  }
```

### export default和export

都是ES6中向外暴露成员的方式

export default`export default var data = {}`

- 可以使用任意变量来接收
- 只能导出一次
- 可以同时使用这两种方式

export`export var title = ''`

- 必须通过`{}`的形式接收，叫按需导出
- 不能改变导出时的变量名
- 可以导出多次
- 接收时可以使用as起别名

### 在vue组件页面中，集成vue-router路由模块

[vue-router官网](https://router.vuejs.org/)

1. 导入路由模块：

```
import VueRouter from 'vue-router'
```

1. 安装路由模块：

```
Vue.use(VueRouter);
```

1. 导入需要展示的组件:

```javascript
import login from './components/account/login.vue'
import register from './components/account/register.vue'
```

1. 创建路由对象:

```javascript
var router = new VueRouter({
  routes: [
    { path: '/', redirect: '/login' },
    { path: '/login', component: login },
    { path: '/register', component: register }
  ]
});
```

1. 将路由对象，挂载到 Vue 实例上:

```javascript
var vm = new Vue({
  el: '#app',
  // render: c => { return c(App) } // 将组件App渲染到index中的app区域，和通过路由渲染出来的组件不冲突
  render(c) {
    return c(App);
  },
  router // 将路由对象，挂载到 Vue 实例上
});
```

1. 改造App.vue组件，在 template 中，添加`router-link`和`router-view`：

```html
    <router-link to="/login">登录</router-link>
    <router-link to="/register">注册</router-link>
    <router-view></router-view>
```

### 使用children子路由

```javascript
// 路由实例
var router = new VueRouter({
  routes: [
   { path: '/', redirect: '/account/login' }, // 使用 redirect 实现路由重定向
   {
      path: '/account',
      component: account,
      children: [ // 通过 children 数组属性，来实现路由的嵌套
         { path: 'login', component: login }, // 注意，子路由的开头位置，不要加 / 路径符
         { path: 'register', component: register }
      ]
    }
  ]
});

// 在account组件中添加router-view和router-link
```

### 组件中的css作用域问题

scoped属性会让组件内的根元素增加一个独有的data属性，并利用属性选择器中就可以实现组件内部作用域

```html
<style scoped lang='scss'>
</style>
```

### 抽离路由为单独的模块

将路由抽离到router.js文件导出，在main.js文件中导入

### 使用vue-resource

```js
import VueResource from 'vue-resource'
// 安装vueResource安装完成后Vue实例中就多了$http
Vue.use(VueResource)
```

## 插件

### 图片懒加载

vue-lazyload

# UI组件

## ant-design-vue



## 饿了么 MintUI 组件

基于vue.js封装的移动端组件库，只适用于Vue

和bootstrap不同，bootstrap类似于代码段

[Github 仓储地址](https://github.com/ElemeFE/mint-ui)

[Mint-UI官方文档](http://mint-ui.github.io/#!/zh-cn)

`cnpm i mint-ui -S`

1. 导入所有MintUI组件：

```
// 引入全部的组件
import MintUI from 'mint-ui'
// 按需导入
import {Cell}
```

1. 导入样式表：

```
import 'mint-ui/lib/style.css'
```

1. 在 vue 中使用 MintUI：

```
// 引入全部的组件
Vue.use(MintUI) 
// 按需导入
Vue.component(Cell.name, Cell)
```

1. 使用的例子：

```
<mt-button type="primary" size="large">primary</mt-button>
```

### 组件的使用：button

### 组件的使用：toast

### babel-plugin-component实现按需导入

`npm install babel-plugin-component -D`

修改.babelrc

```json
{
  "presets": [
    ["es2015", { "modules": false }]
  ],
  "plugins": [["component", [
    {
      "libraryName": "mint-ui",
      "style": true
    }
  ]]]
}
```

main.js

```javascript
import Vue from 'vue'
import { Button, Cell } from 'mint-ui'
import App from './App.vue'

Vue.component(Button.name, Button)
Vue.component(Cell.name, Cell)
/* 或写为
 * Vue.use(Button)
 * Vue.use(Cell)
 */

new Vue({
  el: '#app',
  components: { App }
})
```

## 使用 MUI 组件

类似于bootstrap，代码段

不能使用npm下载，从github上下载解压，examples

[官网首页](http://dev.dcloud.net.cn/mui/)

[文档地址](http://dev.dcloud.net.cn/mui/ui/)

1. 导入 MUI 的样式表：

```
import '../lib/mui/css/mui.min.css'
```

1. 在`webpack.config.js`中添加新的loader规则：

```
{ test: /\.(png|jpg|gif|ttf)$/, use: 'url-loader' }
```

1. 根据官方提供的文档和example，尝试使用相关的组件

### App.vue 组件的基本设置

1. 头部的固定导航栏使用 `Mint-UI` 的 `Header` 组件；
2. 底部的页签使用 `mui` 的 `tabbar`;
3. 购物车的图标，使用 `icons-extra` 中的 `mui-icon-extra mui-icon-extra-cart`，同时，应该把其依赖的字体图标文件 `mui-icons-extra.ttf`，复制到 `fonts` 目录下！
4. 将底部的页签，改造成 `router-link` 来实现单页面的切换；
5. Tab Bar 路由激活时候设置高亮的两种方式：

- 全局设置样式如下：

```
 	.router-link-active{
      	color:#007aff !important;
    }
```

- 或者在 `new VueRouter` 的时候，通过 `linkActiveClass` 来指定高亮的类：

```
 	// 创建路由对象

    var router = new VueRouter({

      routes: [

        { path: '/', redirect: '/home' }

      ],

      linkActiveClass: 'mui-active'

    });

```

### 实现 tabbar 页签不同组件页面的切换

1. 将 tabbar 改造成 `router-link` 形式，并指定每个连接的 `to` 属性；
2. 在入口文件中导入需要展示的组件，并创建路由对象：

```
    // 导入需要展示的组件
    import Home from './components/home/home.vue'
    import Member from './components/member/member.vue'
    import Shopcar from './components/shopcar/shopcar.vue'
    import Search from './components/search/search.vue'

    // 创建路由对象
    var router = new VueRouter({
      routes: [
        { path: '/', redirect: '/home' },
        { path: '/home', component: Home },
        { path: '/member', component: Member },
        { path: '/shopcar', component: Shopcar },
        { path: '/search', component: Search }
      ],
      linkActiveClass: 'mui-active'
    });
```

### 使用 mt-swipe 轮播图组件

1. 假数据：

```
lunbo: [
        'http://www.itcast.cn/images/slidead/BEIJING/2017440109442800.jpg',
        'http://www.itcast.cn/images/slidead/BEIJING/2017511009514700.jpg',
        'http://www.itcast.cn/images/slidead/BEIJING/2017421414422600.jpg'
      ]
```

1. 引入轮播图组件：

```
<!-- Mint-UI 轮播图组件 -->
    <div class="home-swipe">
      <mt-swipe :auto="4000">
        <mt-swipe-item v-for="(item, i) in lunbo" :key="i">
          <img :src="item" alt="">
        </mt-swipe-item>
      </mt-swipe>
    </div>
  </div>
```

### 使用mui的`tab-top-webview-main`完成分类滑动栏

#### 兼容问题

1. 和 App.vue 中的 `router-link` 身上的类名 `mui-tab-item` 存在兼容性问题，导致tab栏失效，可以把`mui-tab-item`改名为`mui-tab-item1`，并复制相关的类样式，来解决这个问题；

```
    .mui-bar-tab .mui-tab-item1.mui-active {
      color: #007aff;
    }

    .mui-bar-tab .mui-tab-item1 {
      display: table-cell;
      overflow: hidden;
      width: 1%;
      height: 50px;
      text-align: center;
      vertical-align: middle;
      white-space: nowrap;
      text-overflow: ellipsis;
      color: #929292;
    }

    .mui-bar-tab .mui-tab-item1 .mui-icon {
      top: 3px;
      width: 24px;
      height: 24px;
      padding-top: 0;
      padding-bottom: 0;
    }

    .mui-bar-tab .mui-tab-item1 .mui-icon~.mui-tab-label {
      font-size: 11px;
      display: block;
      overflow: hidden;
      text-overflow: ellipsis;
    }
```

1. `tab-top-webview-main`组件第一次显示到页面中的时候，无法被滑动的解决方案：

- 先导入 mui 的JS文件:

```
 import mui from '../../../lib/mui/js/mui.min.js'
```

- 在 组件的 `mounted` 事件钩子中，注册 mui 的滚动事件：

```
 	mounted() {
    	// 需要在组件的 mounted 事件钩子中，注册 mui 的 scroll 滚动事件
        mui('.mui-scroll-wrapper').scroll({
          deceleration: 0.0005 //flick 减速系数，系数越大，滚动速度越慢，滚动距离越小，默认值0.0006
        });
  	}
```

1. 滑动的时候报警告：`Unable to preventDefault inside passive event listener due to target being treated as passive. See https://www.chromestatus.com/features/5093566007214080`

```
解决方法，可以加上* { touch-action: none; } 这句样式去掉。
```

原因：（是chrome为了提高页面的滑动流畅度而新折腾出来的一个东西） http://www.cnblogs.com/pearl07/p/6589114.html
https://developer.mozilla.org/zh-CN/docs/Web/CSS/touch-action

## 在`.vue`组件中使用`vue-resource`获取数据

1. 运行`cnpm i vue-resource -S`安装模块
2. 导入 vue-resource 组件

```
import VueResource from 'vue-resource'
```

1. 在vue中使用 vue-resource 组件

```
Vue.use(VueResource);
```

##移除严格模式

[babel-plugin-transform-remove-strict-mode](https://github.com/genify/babel-plugin-transform-remove-strict-mode)

## [vue-preview](https://github.com/LS1231/vue-preview)

一个Vue集成PhotoSwipe图片预览插件

## 在手机中调试的方式

处于同一个局域网

在package.json的dev脚本中添加一个--host值设为当前wifi的ip地址

## 开启Apache的gzip压缩

要让apache支持gzip功能，要用到deflate_Module和headers_Module。打开apache的配置文件httpd.conf，大约在105行左右，找到以下两行内容：（这两行不是连续在一起的）

```
#LoadModule deflate_module modules/mod_deflate.so
#LoadModule headers_module modules/mod_headers.so
```

然后将其前面的“#”注释删掉，表示开启gzip压缩功能。开启以后还需要进行相关配置。在httpd.conf文件的最后添加以下内容即可：

```
<IfModule deflate_module>
    #必须的，就像一个开关一样，告诉apache对传输到浏览器的内容进行压缩
    SetOutputFilter DEFLATE
    DeflateCompressionLevel 9
</IfModule>
```

最少需要加上以上内容，才可以生gzip功能生效。由于没有做其它的额外配置，所以其它相关的配置均使用Apache的默认设置。这里说一下参数“DeflateCompressionLevel”，它表示压缩级别，值从1到9，值越大表示压缩的越厉害。

## 使用ngrok将本机映射为一个外网的Web服务器

注意：由于默认使用的美国的服务器进行中间转接，所以访问速度炒鸡慢，访问时可启用FQ软件，提高网页打开速度！