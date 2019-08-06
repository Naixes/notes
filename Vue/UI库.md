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

## UI轮子

### UI设计

用户体验

可用性，易用性，美观性

#### 网站开发流程

立项----人员，预算等

**需求**----收集和分析，收集更难；可以使用用例图

可行性分析----资源等

系统设计（功能，框架）----UML图，时序图

**原型设计**（草稿，线框图）----线框图可以用Baisamiq----可用性，易用性

**交互设计**----Axure RP，墨刀，Sketch.app----易用性

**视觉设计**----PS，Fireworks，Sketch.app

**程序开发**

**测试**

功能预演

内测

灰度发布----对部分用户先发布，逐步提高比例，防止崩溃

**正式发布** 

#### Sketch

可以用墨刀代替

- 功能少
- 操作方便
- 贴近前端

#### 交互设计

**设计约定**

1. 有反馈----比如键盘的tab，输入不合法时有提示
2. 一致性（可学习）----提交时按钮不可用
3. 可预测

### 需求分析

#### 按钮

##### 状态分析

1. 点击：loading状态
2. 不可点击
3. hover（手机没有）
4. 按下

##### 画用例图

### 项目搭建

见仓库sin-vue