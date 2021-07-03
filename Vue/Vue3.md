## 概览

### 历史

过渡阶段的底层还是vue2

<img src="Vue3.assets/截屏2021-06-08 下午11.03.19.png" alt="截屏2021-06-08 下午11.03.19" style="zoom:30%;" />

vuejs/rfsc：可以看到一些api在3和2的区别

https://github.com/vuejs/rfcs

### vite

官方，esbuild构建，esmodule，速度快，核心原理把module临时替换

不考虑兼容可以直接使用，否则使用webpack

#### 原理

1. 内置服务器拦截HTTP请求

   ```js
   import {createApp} from 'vue'
   // node_modules路径转移
   import {createApp} from '/@modules/vue'
   ```

2. import ts, *.vue替换，使用es-module-lexer分析import，返回js
3. 核心编译Esbuild+Esmodule+按需加载
4. 热更新websocket



### slot

#### 使用-0001

Using `v-slot` to declare the props passed to the scoped slots of `<foo>`:

```
<!-- default slot -->
<foo v-slot="{ msg }">
  {{ msg }}
</foo>

<!-- named slot -->
<foo>
  <template v-slot:one="{ msg }">
    {{ msg }}
  </template>
</foo>
```

#### 简写-0002

```
<foo>
  <template #header="{ msg }">
    Message from header: {{ msg }}
  </template>

   <template #footer>
    A static footer
  </template>
</foo>
```

- `this.$slots` now exposes slots as functions;
- `this.$scopedSlots` removed.

#### 在render函数中使用-0006

```
h(Comp, [
  h('div', this.msg)
])

// equivalent:
h(Comp, () => [
  h('div', this.msg)
])
```

实现区别

```
// 2.x
h(Comp, [
  h('div', { slot: 'foo' }, this.foo),
  h('div', { slot: 'bar' }, this.bar)
])

// 3.0
// Note the `null` is required to avoid the slots object being mistaken
// for props.
h(Comp, null, {
  foo: () => h('div', this.foo),
  bar: () => h('div', this.bar)
})
```

### 全局API规范

#### API treeshaking-0004

```
import { nextTick, observable } from 'vue'

nextTick(() => {})

const obj = observable({})
```

#### API 变化-0009

##### Before

一个页面有多个vue应用时，用的同一个实例会相互影响

```js
import Vue from 'vue'
import App from './App.vue'

Vue.config.ignoredElements = [/^app-/]
Vue.use(/* ... */)
Vue.mixin(/* ... */)
Vue.component(/* ... */)
Vue.directive(/* ... */)

Vue.prototype.customProperty = () => {}

new Vue({
  render: h => h(App)
}).$mount('#app')
```

##### After

为每一个vue应用创建单独的实例

```js
import { createApp } from 'vue'
import App from './App.vue'

const app = createApp(App)

app.config.isCustomElement = tag => tag.startsWith('app-')
app.use(/* ... */)
app.mixin(/* ... */)
app.component(/* ... */)
app.directive(/* ... */)

app.config.globalProperties.customProperty = () => {}

app.mount(App, '#app')
```

### Teleport-0025

远程传送

比如旧的模态框会被强行渲染在树结构中，布局和样式会收到外部影响

```html
<body>
  <div id="app">
    <h1>Move the #content with the portal component</h1>
    <!-- 可以用to指定实际的挂在节点 -->
    <teleport to="#endofbody">
      <div id="content">
        <p>
          this will be moved to #endofbody.<br />
          Pretend that it's a modal
        </p>
        <Child />
      </div>
    </teleport>
  </div>
  <div id="endofbody"></div>
  <script>
    new Vue({
      el: "#app",
      components: {
        Child: { template: "<div>Placeholder</div>" }
      }
    });
  </script>
</body>
```

### Composition API-0013

### v-model-0011

Adjust `v-model` API when used on custom components.

This builds on top of #8 (Replace `v-bind`'s `.sync` with a `v-model` argument).

### 指令API的变化-0003

## Vue2 and Vue3核心API对比

### 性能上的提升

- 核心体积更小 gzipped ~10kb

- 支持 three-shaking，很多api通过解构的方式引入

- 静态节点优化

  input

  ```vue
  <div>
    <span class="foo">
      Static
    </span>
    <span>
      {{ dynamic }}
    </span>
  </div>
  ```

  output

  ```js
  const __static1 = h(
    "span", 
    { class: "foo" },
    "static"
  );
  
  render() {
    return h('div', [
      __static1,
      h('span', dynamic)
    ])
  }
  ```

### 自定义渲染器

### 创建App

##### Vue2

```js
import Vue from 'vue'
import App from './App.vue'

new Vue({
  render: h => h(App),
}).$mount('#app')
```

##### Vue3

更加函数式

```js
import { createApp } from 'vue'
import App from './App.vue'

createApp(App).mount('#app')
```

### 多个根节点

##### Vue2

```vue
<template>
  <div>
    <h1>{{ msg }}</h1>
    <button @click="count++">count is: {{ count }}</button>
    <p>Edit <code>components/HelloWorld.vue</code> to test hot module replacement.</p>
  </div>
</template>
```

##### Vue3

```vue
<template>
  <h1>{{ msg }}</h1>
  <button @click="count++">count is: {{ count }}</button>
  <p>Edit <code>components/HelloWorld.vue</code> to test hot module replacement.</p>
</template>
```

### Composition API

创建Composition API 的原因是：

- 大型组件变得难以阅读和维护。
- 逻辑复用。

Composition API带来的特性：

- 更好的typescript支持
- 更容易复用逻辑
- 需要开发者组织代码结构

#### Vue3 setup

- Props
- Data
- Methods
- Computed Properties
- Lifecycle methods

```vue
<template>
  <!-- your template code -->
</template>
<script lang="ts">
import { ref, onMounted } from 'vue';

interface SetupContext {
  attrs: Data
  slots: Slots
  emit: (event: string, ...args: unknown[]) => void
}
 
export default {
  setup(props, context: SetupContext) {
  	onMounted(() => {})
  }
};
</script>
```

#### Vue2

```vue
<template>
  <!-- template code -->
</template>
<script>
export default {
  name: "App",
  props: {
    /*...*/
  }
  components: {
    /*...*/
  },
  data(){
    return {
      /*...*/
    }
  },
  computed:{
    /*...*/
  },
  watch:{
    /*...*/
  },
  methods: {
    /*...*/
  },
  created(){
    /*...*/
  },
  mounted(){
    /*...*/
  }
};
</script>
```

### Data

#### vue2

```vue
<template>
  <div id="app">
    <div>Name: {{ name }}</div>
  </div>
</template>

<script>
export default {
  name: "App",
  data(){
    return {
      name: "Name"
    }
  }
};
</script>
```

#### vue3

##### ref

```vue
<template>
  <div>Name: {{ name }}</div>
</template>
<script>
import { ref } from "vue";
export default {
  setup() {
    const name = ref('Name');
    console.log(name.value);
    return { name };
  }
};
</script>
```

##### `reactive`

```js
const obj = reactive({ count: 0 })
obj.count ++
console.log(obj.count) // 1
```

##### `reactive` and `ref`

```js
const count = ref(0);
const state = reactive({
  count,
});
// 不用state.count.value
console.log(state.count); // 0
```

**区别：其实ref相当于reactive的简化版，ref背后也是通过reactive实现的，唯一的区别是ref返回的是包装对象**

> 原始值没有引用只有值，没办法监听变化，所以需要用对象再包装一层

```js
const count = ref(0)  等价 const count = reactive({value:0})
```

##### `isRef`

用来判断某个值是否为 ref() 创建出来的对象，应用场景：当需要展开某个可能为 ref() 创建出来的值的时候

```js
 const unwrapped = isRef(foo) ? foo.value : foo;
```

##### `toRefs`

```vue
<template>
  <p>{{ obj.count }}</p>
  <p>{{ count }}</p>
  <p>{{ value }}</p>
</template>

<script setup lang="ts">
export default {
  setup() {
    const obj = reactive({
      count: 0,
      value: 100,
    });
    return {
      obj,
      ...toRefs(obj),
    };
  },
}
</script>

```

##### `readonly`

接收一个ref或者reactive包装对象，返回一个只读的响应式对象

```js
const original = reactive({ count: 0 })

const copy = readonly(original)

watchEffect(() => {
  // 用于响应性追踪
  console.log(copy.count)
})

// 变更 original 会触发依赖于副本的侦听器
original.count++

// 变更副本将失败并导致警告
copy.count++ // 警告!
```

### Methods

#### vue2

```vue
<template>
  <div>
    <div>Amount: {{ amount }}</div>
    <button @click="increaseAmount()">Increase Capacity</button>
  </div>
</template>

<script>
export default {
  data(){
    return {
      amount: 3,
    }
  },
  methods: {
    increaseAmount() {
      this.amount+=1
    }
  }
};
</script>
```

#### vue3

```vue
<template>
  <div>
    <div>Amount: {{ amount }}</div>
    <button @click="increaseAmount()">Increase Capacity</button>
  </div>
</template>

<script>
import { ref, reactive } from "vue";

export default {
  setup() {
    const amount = ref(3);
    const increaseAmount = () => {
      amount.value+=1
    }
    return { amount, increaseAmount };
  }
};
</script>
```

### Computed

#### vue2

```vue
<template>
  <div id="app">
    <p>Upper: {{ upperName }} out of {{ name }}</p>
  </div>
</template>
<script>
export default {
  data(){
    return {
      name: "author",
    }
  },
  computed: {
    upperName(){
      return this.name.toUpperCase() + "VUE_3";
    }
  }
};
</script>
```

#### Vue3

```vue
<template>
  <div id="app">
    <p>Upper: {{ upperName }} out of {{ name }}</p>
  </div>
</template>
<script>
import { ref, computed } from "vue";
export default {
  setup() {
    const name = ref("author");
    const upperName = computed(() => {
      return name.value.toUpperCase() + "VUE_3";
    });
    return { name, upperName };
  }
};
</script>
```

### Watch

#### Vue2

```vue
<template>
  <div>
    <input type="text" v-model="name" />
  </div>
</template>

<script>
export default {
  data(){
    return {
      name: null,
    }
  },
  watch: {
    name(newVal, oldVal){
      console.log(`${newVal} ${oldVal}`);
    }
  }
};
</script>
```

#### Vue3

```vue
<template>
  <div>
    <input type="text" v-model="name" />
  </div>
</template>

<script>
import { ref, watchEffect } from "vue";
export default {
  setup() {
    const name = ref('');
    watchEffect(() => {
      console.log(name.value);
    })
    return { name };
  }
};
</script>
```

### 删除了 filter

删除原因：`{{ new Date() | formatUnix}}` 中的 `|` 非常奇怪，这让开发者感到困惑。删除filter的最终原因是，将鼓励开发者创建公用的函数来重用或在每个组件中建立明确的方法。

#### Vue2

```vue
<template>
  <div id="app">
    {{ new Date() | formatUnix}}
  </div>
</template>

<script>
import moment from "moment";
export default {
  name: "App",
  filters: {
    formatUnix(value) {
      if (value) {
        return moment(value).format("DD/MM/YYYY");
      }
    },
  },
};
</script>
```

#### Vue3

```vue
<template>
  <div id="app">
    // js新语法，管道运算符
    <div>{{new Date |> formatUnix>  }}</div>
  </div>
</template>

<script>
import formatUnix from "./Utils/DateFormat.js";
export default {
  name: "App",
  components: {
  },
  setup() {
    return {
      formatUnix 
    };
  },
};
</script>
```

### 多个v-models

#### Vue2

```vue
<input v-model="property" />

<input                          
  :value="property"                         
  @input="property = $event.target.value"                       
/>
```

#### Vue3

```vue
<template>
  <form>
    <div>
      <label for="name">Name</label>
      <input type="text" :value="name" @input="updateName($event.target.value)" />
    </div>
    <div>
      <label for="email">Email</label>
      <input type="email" :value="email" @input="updateEmail($event.target.value)" />
    </div>
  </form>
</template>
<script>
export default {
  props: {
    name: String,
    email: String,
  },
  setup(props, { emit }) {
    const updateName = (value) => {
      emit("update:name", value);
    };
    const updateEmail = (value) => {
      emit("update:email", value);
    };
    return { updateName, updateEmail };
  },
};
</script>
```

```vue
<template>
  <div id="app">
    <InviteForm v-model:name="inviteName" v-model:email="inviteEmail" />
    <div>
      <div>{{ inviteName }}</div>
      <div>{{ inviteEmail }}</div>
    </div>
  </div>
</template>

<script>
import InviteForm from "./components/InviteForm.vue";
import { ref } from "vue";
export default {
  name: "App",
  components: {
    InviteForm,
  },
  setup() {
    const inviteName = ref("name");
    const inviteEmail = ref("invite");
    return {
      inviteName,
      inviteEmail,
    };
  },
};
</script>
```

### Teleport

相当于react的Portals

```vue
<template>
  <teleport to="#out-side-app"> // .className body
  	This is teleport
  </teleport>
  <div>APP</div>
</template>Z
```

支持多个

```vue
<teleport to="#modals">
  <div>A</div>
</teleport>
<teleport to="#modals">
  <div>B</div>
</teleport>

<!-- result-->
<div id="modals">
  <div>A</div>
  <div>B</div>
</div>
```

### 生命周期

- `beforeCreate` ->  `setup()`
- `created` ->  `setup()`
- `beforeMount` -> `onBeforeMount`
- `mounted` -> `onMounted`
- `beforeUpdate` -> `onBeforeUpdate`
- `updated` -> `onUpdated`
- `beforeUnmount` -> `onBeforeUnmount`
- `unmounted` -> `onUnmounted`
- `errorCaptured` -> `onErrorCaptured`

### script-setup

？？？

```vue
<template>
  <button @click="inc">{{ count }}</button>
</template>

<script setup lang="ts">
import { ref } from "vue";
const count = ref(0);
const inc = () => count.value++;
</script>
```

### ref-sugar

？？？

https://github.com/vuejs/rfcs/pull/228

```vue
<template>
  <button @click="inc">{{ count }}</button>
</template>

<script setup lang="ts"> // =>  lang="vs"
ref: count = 0;
const inc = () => count++;
</script>
```

社区中其他的方案？？？

```js
$variable

// @ref
let count = 1;

let @ref count = 1;

ref count = 1;
```

### Vite

基于 ESM的 构建工具，

```bash
npm init @vitejs/app
```

Bundleless，不打包

> 为什么需要打包？HTTP1.1时浏览器的并行连接数时6，打包进行限制
>
> 不打包：
>
> 2.0连接数增多（20个左右），并且支持多路复用
>
> 第三方包支持esm

snowpack

import cdn

Skypacks
