## 概览

vuejs/rfsc：可以看到一些api在3和2的区别

https://github.com/vuejs/rfcs

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

