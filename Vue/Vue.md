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

![01.MVC和MVVM的关系图解](.\media\01.MVC和MVVM的关系图解.png)

### Vue.js 基本代码和MVVM

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

当一个 Vue 实例被创建时，它将 `data` 对象中的所有的属性加入到 Vue 的**响应式系统**中。当这些属性的值发生改变时，视图将会产生“响应”，即匹配更新为新的值。

当这些数据改变时，视图会进行重渲染。值得注意的是只有当实例被创建时 `data` 中存在的属性才是**响应式**的。

这里唯一的例外是使用 `Object.freeze()`，这会阻止修改现有的属性，也意味着响应系统无法再*追踪*变化。

除了数据属性，Vue 实例还暴露了一些有用的实例属性与方法。它们都有前缀 `$`，以便与用户定义的属性区分开来。例如：`$data, $el, $watch`


### [vue实例的生命周期](https://cn.vuejs.org/v2/guide/instance.html#实例生命周期)

- 什么是生命周期：从Vue实例创建、运行、到销毁期间，总是伴随着各种各样的事件，这些事件，统称为生命周期！![lifecycle](.\media\lifecycle.png)
- [生命周期钩子](https://cn.vuejs.org/v2/api/#选项-生命周期钩子)：就是生命周期事件的别名而已；
- **创建期间**的生命周期函数：

  - `beforeCreate`：实例刚在内存中被创建出来，只初始化了**默认事件和生命周期函数**。还没有初始化好 data 和 methods 属性
  - `created`：实例已经在内存中创建OK，此时 **data 和 methods** 已经创建，此时还没有开始 编译模板。可以在这里**请求数据**
  经验：如果请求得到的数据需要传递给其他组件并且需要操作后使用时可以在组件的路由守卫beforeRouteEnter中获取，利用next()保证在数据操作之前完成数据的获取
  - `beforeMount`：此时已经完成了模板的编译，开始创建` VDOM`，但是还没有挂载到页面中
  - `mounted`：此时，将 `VDOM` 渲染为真实 DOM 并且渲染数据。组件中如果有子组件的话，会递归挂载子组件，只有当所有子组件全部挂载完毕，才会执行根组件的挂载钩子。 **可以操作组件元素**。
- **运行期间**的生命周期函数：

  - `beforeUpdate`：状态更新之前执行此函数， 此时 data 中的状态值是最新的，但是界面上显示的 数据还是旧的，因为此时还没有开始重新渲染DOM节点
  - `updated`：实例更新完毕之后调用此函数，此时 data 中的状态值 和 界面上显示的数据，都已经完成了更新，界面已经被重新渲染好了！
- 另外还有 `keep-alive` 独有的生命周期

   `activated` 和 `deactivated` 。用 `keep-alive` 包裹的组件在切换时不会进行销毁，而是缓存到内存中并执行 `deactivated` 钩子函数，命中缓存渲染后会执行 `actived` 钩子函数。 
- **销毁期间**的生命周期函数：不能保证会执行到，比如关闭浏览器

  - `beforeDestroy`：实例销毁之前调用。在这一步，实例仍然完全可用。适合**移除事件、定时器**等等，否则可能会引起内存泄露的问题。 
  - `destroyed`：`Vue` 实例销毁后调用。调用后，`Vue` 实例指示的所有东西都会解绑定，所有的事件监听器会被移除，所有的子实例也会被销毁。

## keep-alive 组件

`<keep-alive>` 包裹动态组件时，会缓存不活动的组件实例，而不是销毁它们。和 `<transition>` 相似，`<keep-alive>` 是一个抽象组件：它自身不会渲染一个 DOM 元素，也不会出现在父组件链中。 

如果你需要**在组件切换的时候，保存一些组件的状态防止多次渲染**，就可以使用 `keep-alive` 组件包裹需要保存的组件。

对于 `keep-alive` 组件来说，它拥有两个独有的生命周期钩子函数，分别为 `activated` 和 `deactivated` 。用 `keep-alive` 包裹的组件在切换时不会进行销毁，而是缓存到内存中并执行 `deactivated` 钩子函数，命中缓存渲染后会执行 `actived` 钩子函数。

## 模板语法
数据绑定最常见的形式就是使用“Mustache”语法 (双大括号) 的文本插值：

`<span>Message: {{ msg }}</span>`

Mustache 标签将会被替代为对应数据对象上 msg 属性的值。无论何时，绑定的数据对象上 msg 属性发生了改变，插值处的内容都会更新。

通过使用 `v-once` 指令，你也能执行一次性地插值。但请留心这会影响到该节点上的其它数据绑定


## Vue指令（directive）

补充了html的属性

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

v-bind可以绑定标签的属性，可以用于任何属性class和style的写法比较特殊，class支持数组和对象，style支持对象，参考：在`Vue`中使用样式

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

- .stop          阻止冒泡

- .prevent    阻止默认事件

  注意：submit事件的传递的this和原生的不同，不是form而是window

- .native       使用原生的事件，和组件结合使用

- .once          事件只触发一次
- .keycode|name      筛选键盘按键，可以组合键
- 事件修饰符可以写多个

- .capture    添加事件侦听器时使用事件捕获模式
- .self            只当事件在该元素本身（比如不是子元素）触发时触发回调，只阻止自身冒泡行为的触发

```html
<a href="http://www.baidu.com" @click.prevent.once="alertmsg">百度</a>
...
```

### v-model

数据双向绑定，只能用于表单，经过v-model绑定的数据都是字符串

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

3. 迭代字符串
4. 迭代数字，从1开始

```html
<p v-for="i in 10">这是第 {{i}} 个P标签</p>
```

> 2.2.0+ 的版本里，**当在组件中使用** v-for 时，key 现在是必须的。

当 Vue.js 用 v-for 正在更新已渲染过的元素列表时，它默认用 “**就地复用**” 策略。如果数据项的顺序被改变，Vue将**不是移动 DOM 元素来匹配数据项的顺序**， 而是**简单复用此处每个元素**，并且确保它在特定索引（vue会提供默认的key但是与数据的特性无关）下显示已被渲染过的每个元素。

-  key 属性必须是不会重复的字符串或数字，并且必须绑定

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

### v-pre

跳过这个元素和它的子元素的编译过程。可以用来显示原始 Mustache 标签。跳过大量没有指令的节点会**加快编译**。

`<span v-pre>{{ this will not be compiled }}</span>`

### v-once

只渲染元素和组件**一次**。随后的重新渲染，元素/组件及其所有的子节点将被视为静态内容并跳过。这可以用于**优化更新性能**。

### [自定义指令](https://cn.vuejs.org/v2/guide/custom-directive.html)

Vue 2x中：

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

## 键盘修饰符及自其定义

### 键盘修饰符

内置：.enter,.tab,.delete,.esc,.space,.up,.down,.left,.right

`<input type="text" v-model="name" @keyup.enter="add">`

也可以直接使用键盘码值

### [自定义键盘修饰符](https://cn.vuejs.org/v2/guide/events.html#键值修饰符)

2.x中:

1. 通过`Vue.config.keyCodes.名称 = 按键值`来自定义案件修饰符的别名：

```js
Vue.config.keyCodes.f2 = 113;
```

2. 使用自定义的按键修饰符：

```html
<input type="text" v-model="name" @keyup.f2="add">
```

## 相关文章

1. [vue.js 2.x 文档](https://cn.vuejs.org/)
2. [String.prototype.padStart(maxLength, fillString)](http://www.css88.com/archives/7715)
3. [js 里面的键盘事件对应的键码](http://www.cnblogs.com/wuhua1/p/6686237.html)
4. [Vue.js双向绑定的实现原理](http://www.cnblogs.com/kidney/p/6052935.html)

## 数据通信

- 库：axios、vue-resource
- 原生：fetch

### `axios`

需要安装`axios`，`vue-axios`

和`vue-resource`用法相似，没有`jsonp`，没有挂载到实例中，可以直接使用

以对象形式发送post请求：

```javascript
postInfo() {
  var url = 'http://127.0.0.1:8899/api/post';
  // 默认以json的形式提交数据，transformRequest可以对data进行操作
  // 方法2：webpack支持引入node系统模块，引入querystring的stringify方法
  // import {stringify} from 'querystring'
  // 方法3：修改contentType
  axios({url: '', method: 'POST', data: {}
         transformRequest: [
             function(data) {
      			// 方法1：手动操作字符串
             	let arr = []
                for(let name in data) {
                    arr.push(`${mame}=${data[name]}`)
                }
      			return arr.join('&')
      			// 方法2：使用querystring的stringify方法
      			return stringify(data)
             }
         ]
        }).then(res => {
    console.log(res.body);
  });
}
```

#### Axios.create()

返回一个`axios`实例，后面可以直接使用

```js
axios.Axios.create({
    transformRequest: [
        function(data) {
            // 方法2：使用querystring的stringify方法
            return stringify(data)
        }
    ]
})
```

#### all()方法

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

#### 拦截器

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

#### 配置

### [vue-resource](https://github.com/pagekit/vue-resource)

#### http请求

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

`this.$http({url: '', params:{}, headers:{}, timeout:5, before: fn, method: 'POST'})`

#### 全局拦截器-interceptors

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

#### 配置

- 全局配置数据接口根域名，配置过后，用到的地方不能加/

`Vue.http.options.root = '/root'`

也可以在vm实例中的http属性中配置

`http: {root: ''}`

- 全局配置`emulateJSON`

`Vue.http.options.emulateJSON= true`

### fetch

```js
let formdata = new FormData() // 不兼容IE9
formdata.append("a", 9)
formdata.append("b", 9)
// let formdata = new FormData(this.$refs[from1])

fetch('', {method: '', body: formdata...})
    // 第一个then中获取不到数据，得到response对象，可以通过res.json()返回一个promise对象
    .then(res => {
    return res.json()
	})
 	// 第二个then返回的data就是获得的数据
    .then(data => {
    console.log(data)
})
```

## [Vue动画](https://cn.vuejs.org/v2/guide/transitions.html)

为什么要有动画：动画能够提高用户的体验，帮助用户更好的理解页面中的功能；

### 使用过渡类名

![1543925491592](E:\Jennifer\other\notes\media\1543925491592.png)

1. HTML结构：

```html
<div id="app">
    <input type="button" value="动起来" @click="isshow = !isshow">
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

### [第三方 CSS 动画库](https://cn.vuejs.org/v2/guide/transitions.html#自定义过渡类名)

animate.css

1. 导入动画类库：

```
<link rel="stylesheet" type="text/css" href="./lib/animate.css">
```

2. 定义 transition 及属性：

```html

<!-- animated也可以放在这里 -->
<!-- 时间相同可以直接等于500 -->
<transition
	enter-active-class="fadeInRight"
    leave-active-class="fadeOutRight"
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
    <transition-group tag="ul" name="list" appear>
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

### vue2-animate

`npm i vue2-animate -D`

本质是CSS，封装了animate.css库

`import 'vue2-animate/dist/vue2-animate.min.css'`

```css
...
// 指定动画类型，只能用于一个元素，一组需要用transition-group
<transition name='fade'>
	<div ...></div>
<transition>

.box {
    width: 200px; height: 200px;
    animation-duration: 5s;
}

// transition-group

<transition-group name='fade' tag='ul' class='list'>
	<li v-for=...></li>
<transition-group>
```



## 相关文章

1. [vue.js 1.x 文档](https://v1-cn.vuejs.org/)
2. [vue.js 2.x 文档](https://cn.vuejs.org/)
3. [String.prototype.padStart(maxLength, fillString)](http://www.css88.com/archives/7715)
4. [js 里面的键盘事件对应的键码](http://www.cnblogs.com/wuhua1/p/6686237.html)
5. [pagekit/vue-resource](https://github.com/pagekit/vue-resource)
6. [navicat如何导入sql文件和导出sql文件](https://jingyan.baidu.com/article/a65957f4976aad24e67f9b9b.html)
7. [贝塞尔在线生成器](http://cubic-bezier.com/#.4,-0.3,1,.33)

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

###  `this.$refs` 获取元素和组件

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

## `watch`属性-侦听器

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
        firstName (newVal, oldVal) { // 第一个参数是新数据，第二个参数是旧数据
          this.fullName = newVal + ' - ' + this.lastName;
        },
        lastName (newVal, oldVal) {
          this.fullName = this.firstName + ' - ' + newVal;
        }
      }
    });
  </script>
```

### 监听路由

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
        // 表达式包含.时要使用引号
        $route(newVal, oldVal) {
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

注意：不推荐使用watch监视路由（只能观察不能控制），可以使用路由守卫（可以控制）

## `computed`计算属性

`computer` 是计算属性，依赖其他属性计算值，本质是一个方法，使用时当作把名称属性来使用

特征（区分methods）：

- 计算属性的求值结果会被缓存起来，方便下次直接调用，没有变化时不会重复计算

- 可读可写

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

### `watch`、`computed`和`methods`之间的对比

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

## Vue-cli

`npm install -g @vue/cli`

3.x：`vue create xxx`

Vue CLI >= 3 和旧版使用了相同的 `vue` 命令，所以 Vue CLI 2 (`vue-cli`) 被覆盖了。如果你仍然需要使用旧版本的 `vue init` 功能，你可以全局安装一个桥接工具：

```sh
npm install -g @vue/cli-init
# `vue init` 的运行效果将会跟 `vue-cli@2.x` 相同
vue init webpack my-project
```

### 快速原型开发

可以快速识别vue文件，封装组件插件等功能

```js
sudo npm i @vue/cli -g
sudo npm i @vue/cli-service-global -g
vue serve App.vue // 启动
```

## render函数和jsx

### 函数式组件

```jsx
// 返回t级标题
export default {
    props: {
        t: {}
    },
    render(h) {
        // 标签名，属性，内容
        // return h('h1', {
        //     on: {
        //         click() {}
        //     },
        //     attrs: {
        //         a: 1
        //     }
        // }, 'xxx')
        let tag = 'h' + this.t
        return <tag on-click={() => {}}>{this.$slots.default}</tag>
    }
}
```

应用：自定义模板标签，向子组件传render函数，子组件将render传给函数式组件渲染自定义标签

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

export default：`export default var data = {}`

- 可以使用任意变量来接收
- 只能导出一次
- 可以同时使用这两种方式

export：`export var title = ''`

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

#### scoped

scoped属性会让组件内的根元素增加一个独有的data属性，并利用属性选择器中就可以实现组件内部作用域，阻止上层的css样式传递到下层，使其只对当前组件生效。

```html
<style scoped lang='scss'>
</style>
```

#### module

module的用法也很简单，只要在style中增加`module`属性即可。不同之处是它在布局中的引用，都需要添加前缀`$style`。因为通过module作用的style都被保存到`$style`对象中。我可以通过console查看它的具体引用名，通过module作用的style将会重新命名为：文件名_原style名_不定后缀。

相对于scoped的方式，module的方式能够一眼知道该元素时属于哪个文件组件中。在大型项目中能够帮助我们迅速定位到要查找的组件。

除了上述的快速定位，由于module会将所有的style都归入`$style`中，所以我们可以很灵活的将任意的父组件样式传递到任意深层的子组件中。例如，将父组件中的`title-wrap`通过props传递到子组件中

module还有一个特性非常不错，它可以导出定义的变量，将变量归入`$style`中

```html
<template>
  <div :class="$style.content">
    <div :class="$style['title-wrap']">我是红色的</div>
    <green-title :styleTitle="$style['title-wrap']"></green-title>
    <div>{{$style.titleColor}}</div>
  </div>
</template>
 
<style lang="scss" module>
$title-color: red;
:export {
  titleColor: $title-color
}
/* 可以使用标签选择器 */ 
.content {
  .title-wrap {
    font-size: 20px;
    color: $title-color;
  }
}
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

### 自定义插件

#### 应用

1. 添加全局方法或者属性。如: [vue-custom-element](https://github.com/karol-f/vue-custom-element)
2. 添加全局资源：指令/过滤器/过渡等。如 [vue-touch](https://github.com/vuejs/vue-touch)
3. 通过全局混入来添加一些组件选项。如 [vue-router](https://github.com/vuejs/vue-router)
4. 添加 Vue 实例方法，通过把它们添加到 `Vue.prototype` 上实现。
5. 一个库，提供自己的 API，同时提供上面提到的一个或多个功能。如 [vue-router](https://github.com/vuejs/vue-router)

#### 使用

在`new Vue()`启动之前通过`Vue.use(xxx)`使用插件，也可以传入可选的选项对象`Vue.use(xxx, {})`

### 图片懒加载

vue-lazyload



## vue-resource

1. 运行`cnpm i vue-resource -S`安装模块
2. 导入 vue-resource 组件

```
import VueResource from 'vue-resource'
```

1. 在vue中使用 vue-resource 组件

```
Vue.use(VueResource);
```

## 其他

### 工具

富文本编辑器：tinymce

### 移除严格模式

[babel-plugin-transform-remove-strict-mode](https://github.com/genify/babel-plugin-transform-remove-strict-mode)

### [vue-preview](https://github.com/LS1231/vue-preview)

一个Vue集成PhotoSwipe图片预览插件

### 在手机中调试的方式

处于同一个局域网

在package.json的dev脚本中添加一个--host值设为当前wifi的ip地址

### 开启Apache的gzip压缩

要让apache支持gzip功能，要用到deflate_Module和headers_Module。打开apache的配置文件httpd.conf，大约在105行左右，找到以下两行内容：（这两行不是连续在一起的）

```
#LoadModule deflate_module modules/mod_deflate.so
#LoadModule headers_module modules/mod_headers.so
```

然后将其前面的“#”注释删掉，表示开启gzip压缩功能。开启以后还需要进行相关配置。在httpd.conf文件的最后添加以下内容即可：

```html
<IfModule deflate_module>
    #必须的，就像一个开关一样，告诉apache对传输到浏览器的内容进行压缩
    SetOutputFilter DEFLATE
    DeflateCompressionLevel 9
</IfModule>
```

最少需要加上以上内容，才可以生gzip功能生效。由于没有做其它的额外配置，所以其它相关的配置均使用Apache的默认设置。这里说一下参数“DeflateCompressionLevel”，它表示压缩级别，值从1到9，值越大表示压缩的越厉害。

### 使用ngrok将本机映射为一个外网的Web服务器

注意：由于默认使用的美国的服务器进行中间转接，所以访问速度炒鸡慢，访问时可启用FQ软件，提高网页打开速度！
