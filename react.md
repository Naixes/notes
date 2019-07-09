# 移动App

## 什么是移动App开发

1. 苹果上的软件使用IOS平台的开发工具和开发语言进行设计开发的！苹果上的开发语言：OC、Swift
2. 安卓平台上的软件使用Java，结合一些Android控件，就可以开发安卓上的手机软件；
3. 现在，我们可以使用混合App开发的方式，来同时进行两个平台上软件的开发；
4. 也就是说，抛开OC、Swift、Java、Android；可以直接使用前端技术（HTML + CSS + JS）来进行移动端App开发；这种开发方式叫做混合App开发！

> 什么是移动App开发：通俗的理解，就是把开发Web网站的技术，通过某种方式，移植到移动App开发上进行使用，这种利用Web开发技术进行移动端开发体验的方式，叫做混合App开发！

### 关于移动App开发

- 原生开发（NativeApp）：是使用手机平台官方推荐的开发语言和框架，进行开发的方式，叫做原生开发！

- 混合开发（HybirdApp）：抛开官方提供的开发方式，使用前端技术，进行移动APP开发的方式，叫做混合开发！

- App的分类：App -> Application(应用程序)：什么是应用程序：可以安装的、提供了某些具体功能的软件，叫做应用程序；

  - 按照平台来划分：
    - PC端：LOL、VS Code、网易云音乐、视频软件
    - 移动端：手机QQ、外卖、地图【战略资源】、亡者农药
    - 电视
  - 按照功能来划分：
    - 游戏：亡者农药、英雄联盟
    - 应用：Office办公软件、翻译软件、外卖软件

- App和Web的区别：

  - APP：App是Application的缩写，含义为：“可安装的应用程序”，特点：需要安装；需要手动去升级；

  - 优点：**性能稳定、体验好**；内容丰富；安全；对网络要求比较低（受网络影响小）；
  - 缺点：需要手动安装；需要手动去升级；**不能跨平台**

  - Web：特指基于浏览器开发的网站（说白了就是运行在浏览器中的网页）

  - 优点：免安装，只要安装了浏览器就能访问Web；不需要用户手动升级（升级过程对用户来说是透明的）；**能够跨平台**；（因为Web天生就是跨平台的）
  - 缺点：严重依赖于网络的情况；**用户体验没有App优秀**；也有平台之间的兼容性！

## 混合App开发的优点

- 节省开发成本

  - 从工资上
  - 从时间上:使用前端技术开发App的话，速度很快，因为前端技术够简单（HTML+CSS+JS），但是原生的 安卓和 IOS 语言就很难学，其次，一些复杂的概念比较难懂，

1. 市面上常见的App开发方式

- WebApp：基于浏览器实现的，有特定功能的网站，称作WebApp（本质就是一个网站，只不过功能很复杂，所以把它叫做 Web 类型的 APP）
  - 例如：百度脑图、https://m.jd.com/、https://m.taobao.com/#index
  - 优点：跨平台（最大的优点）
  - 缺点：依赖网络，有白屏效果，相对来说，用户体验差；不能调用硬件底层得设备，比如摄像头；
- NativeApp：用android和Object-C等原生语言开发的应用
  - 优点：体验好；用户使用起来很流畅；非常适合做游戏【性能高】；可以直接调用硬件底层的API；
  - 缺点：不能跨平台
- HybirdApp：利用前端所学的知识去开发移动端App，兼具2者的优势
  - 优点：能够跨平台；体验会好一些；能够调用硬件底层API；
  - 缺点：相对于原生体验稍微弱一丢丢；不适合做游戏；
    - 混合App适合做应用类型得App，比如外卖，比如非游戏类型得软件；
    - 混合APP开发的特点：外层用原生的NativeContainer来包裹所有的应用程序代码；同时这个NativeContainer也提供了调用硬件底层API的能力；注意：在NatvieContainer中，运行的不是原生的机器码，而是我们的HTML + CSS + JS搭建的出来的网页；
    - React Native：打包出来之后是原生app不是搭建的出来的网页，解决了性能问题，但是目前组件不够丰富

1. 三种开发方式的原理和对比

   ![](E:/%E4%B8%B4%E6%97%B6/26%20React/%E7%AC%94%E8%AE%B0+%E6%BA%90%E4%BB%A3%E7%A0%81/%E7%AC%94%E8%AE%B0+%E6%BA%90%E4%BB%A3%E7%A0%81/React%E8%B5%84%E6%96%99/%E6%B7%B7%E5%90%88app%E8%B5%84%E6%96%99/code/day02/%E7%AC%94%E8%AE%B0/images/%E4%B8%89%E7%A7%8D%E5%BC%80%E5%8F%91%E7%B1%BB%E5%9E%8B%E7%9A%84%E5%8E%9F%E7%90%86.png)
   ![](E:/%E4%B8%B4%E6%97%B6/26%20React/%E7%AC%94%E8%AE%B0+%E6%BA%90%E4%BB%A3%E7%A0%81/%E7%AC%94%E8%AE%B0+%E6%BA%90%E4%BB%A3%E7%A0%81/React%E8%B5%84%E6%96%99/%E6%B7%B7%E5%90%88app%E8%B5%84%E6%96%99/code/day02/%E7%AC%94%E8%AE%B0/images/%E4%B8%89%E7%A7%8D%E5%BC%80%E5%8F%91%E7%B1%BB%E5%9E%8B%E7%9A%84%E5%AF%B9%E6%AF%94.png)

   java或ios编译执行，js解析执行

2. [谁在使用React Native？？？](https://facebook.github.io/react-native/showcase.html)

## 企业如何选择合适自己的App开发方式

如果企业中之前有用原生开发出来的App，那么需要继续使用原生的方式去维护；
如果企业是做手游的，也只能使用原生，或者，对app性能要求特别高，也要用原生；
一般，如果有了一个好的方案，就需要立即把方案实现为具体的应用；快速的推向市场，占领市场；基于这种需求，混合APP开发方式，更适合；尤其适用于小企业；【裤衩开发】

## 企业中项目开发流程

- 需求调研：产品定位、受众群体、市场需求、开发价值；【产出物：需求文档】
- 产品设计：功能模块、流程逻辑；【产出物：设计文档，交互稿】，确定项目的基本功能；
- 项目开发：项目架构、美工、前端、后台、测试【产品的把控】**要理解前后端分离的概念**
- 运营维护：上线试运行、调Bug、微调功能模块、产品迭代

> 根据需求搞设计，根据设计做开发

## 企业技术选型 - 几大主流技术之间的关系

1. Angular.js 和 Ionic

- [Angular1官网](https://angularjs.org/)
- [Angular2官网](https://angular.io/)
- [Ionic 中文网](http://www.ionic.wang/)
- [Ionic 英文官网](http://ionicframework.com/getting-started/)

1. Vue.js 和 Weex

- [Vue.js官网](https://cn.vuejs.org/)
- [Weex文档](http://weex.apache.org/cn/references/index.html)
- [Weex - github地址 - 新](https://github.com/apache/incubator-weex)
- [Weex - github地址 - 旧](https://github.com/alibaba/weex)

1. React.js 和 React-Native

- [React.js英文官网](https://facebook.github.io/react/)
- [ReactNative中文网](http://reactnative.cn/)
- [ReactNative英文网](http://facebook.github.io/react-native/)

Angular，Vue，React混合App开发时只是用到了这三个框架的基础语法

Ionic，Weex，React-Native都提供了打包的命令行工具，提供了相关的组件，只能用他们提供的组件才能进行打包

> Angular, Vue, React 这三个都是前端框架，我们在进行混合App开发的时候，只是用到了这三个框架的基础语法而已；
> Ionic， Weex， ReactNatvie 这三个都是打包工具，能够把我们开发出来的应用，最终打包成一个可安装的手机端程序安装包；同时，这三个东西，也提供了好用的一些小组件；

## 前端混合App开发框架

1. Html5+、ReactNative、Weex、Ionic
2. [认识HTML5+](http://www.html5plus.org/#home)

- h5+是一个产业联盟，它有一些互联网成员，专门在中国推广H5

1. [HBuilder官网](http://www.dcloud.io/)

## 开发框架之间的区别

1. Html5+ 和 Ionic
   - 先完使用提供的UI成一个完整的网站，再使用打包技术，将网站打包成应用
     - 目的1：安装到手机
     - 目的2：调用底层API
   - 应用的内部运行的是一个网站
   - 开发效率高，本质上是网站运行效率和性能不太好
2. ReactNative 和 Weex
   - 开发出一个模块项目，不能运行到浏览器和手机中，半成品
   - 打包工具将源代码编译成原生的java或oc代码，得到一个原生App
   - 性能好，但是组件不够丰富

## 使用HBuilder生成安卓应用（在线）

[API地址](http://www.html5plus.org/doc/zh_cn/webview.html)
Hbuilder这个工具，是一个在线打包工具，使用很方便，不需要在本地配置开发环境；直接将做好的网站，通过一些简单的操作，就能在线打包为一个App出来；

- 在项目上右键 -> 发行 -> 发行为原生安装包

好处：本地不用配置开发环境；操作方便，对于程序员来说不关心打包的过程，打包过程对于我们来说是透明的；
缺点：程序员很少能干预打包的过程；源代码被提交到了云端的服务器，存在项目核心代码被泄露的风险；

## 环境变量的使用

作用：将需要全局使用的工具或者应用程序，配置到Path环境变量中，可以很方便的通过命令行的形式，在任何想要运行这些应用程序的地方，运行它们；

## 移动App开发环境配置

### 安装最新版本的java jdk

1. 修改环境变量，新增`JAVA_HOME`的系统环境变量，值为`C:\Program Files (x86)\Java\jdk1.8.0_112`，也就是安装JDK的根目录
2. 修改系统环境变量`Path`，在`Path`之后新增`%JAVA_HOME%\bin;%JAVA_HOME%\jre\bin;`
3. 新建**系统环境变量**`CLASSPATH`，值为`.;%JAVA_HOME%\lib\dt.jar;%JAVA_HOME%\lib\tools.jar;`
4. 保存所有的系统环境变量，同时退出系统环境变量配置窗口，然后运行cmd命令行工具，输入`javac`，如果能出现javac的命令选项，就表示配置成功！

### 安装Node.js环境

注意：需要安装最新的长期稳定版本，不要实验版本；安装完毕之后的node.js会自动配置到全局系统环境变量中
安装完毕后，可以输入`node -v`查看node版本号；

### 安装C++环境

大多数情况下操作系统自带C\++环境，不需要手动安装C\++环境；
如果运行报错，则需要手动安装visual studio中的C\++环境；

### 安装Git环境

Git安装完毕后，会自动配置到系统环境变量中；
可以通过运行`git --version`来检查是否正确安装和配置了Git的环境变量；

### 安装Python环境

1. 注意：安装Python时候，只能**安装2.×的版本**，注意勾选安装界面上的`Add Python to path`，这样才能自动将Python安装到系统环境变量中；
2. 安装完毕之后，可以在命令行中运行`python`，检查是否成功安装了python。

### 配置安卓环境

1. 安装`installer_r24.3.4-windows.exe`，最好手动选择安装到C盘下的android目录
2. 打开安装的目录，将`android-25`、`android-23`(react-native必须依赖这个)解压后，放到`platforms`文件夹下
3. 解压并得到`platform-tools`文件夹，放到安装目录的根目录中；
4. 【这一步直接忽略即可！】**tools文件夹不解压覆盖也行；**~~解压`tools`，放到安装根目录中~~
5. 解压`build-tools_r23.0.1-windows.zip(react-native必须依赖这个)`、`build-tools_r23.0.2-windows.zip(weex必须依赖这个)`和`build-tools_r23.0.3-windows.zip`，并将解压出来的文件夹，分别改名为版本号`23.0.1`、`23.0.2`和`23.0.3`；在安装目录中新建文件夹`build-tools`，并将改名为版本号之后的文件夹，放到新创建出来的`build-tools`文件夹下
6. 在安装目录中，新建`extras`文件夹，在`extras`文件夹下新建`android`文件夹；解压`m2responsitory`文件夹和`support`文件夹，放到新建的`extras -> android`文件夹下
7. 配置安装环境变量：在系统环境变量中新建`ANDROID_HOME`，值为android SDK Manager的安装路径`C:\Users\liulongbin\AppData\Local\Android\android-sdk`，紧接着，在Path中新增`;%ANDROID_HOME%\tools;%ANDROID_HOME%\platform-tools;`

## [ReactNative快速打包](http://reactnative.cn/docs/0.42/getting-started.html)

1. 安装完node后建议**设置npm镜像**以加速后面的过程（或使用科学上网工具）。注意：**不要使用cnpm！**cnpm安装的模块路径比较奇怪，packager不能正常识别！

> npm config set registry https://registry.npm.taobao.org --global<br/>
>
> npm config set disturl https://npm.taobao.org/dist --global

1. Yarn、React Native的命令行工具（react-native-cli）

- Yarn是Facebook提供的替代npm的工具，可以加速node模块的下载。React Native的命令行工具用于执行创建、初始化、更新项目、运行打包服务（packager）等任务。

  > npm install -g yarn react-native-cli

- 安装完yarn后同理也要设置镜像源：

  > yarn config set registry https://registry.npm.taobao.org --global<br/>
  > yarn config set disturl https://npm.taobao.org/dist --global

1. 运行`react-native init AwesomeProject`创建React-Native项目

2. 运行`cd AwesomeProject`切换到项目根目录中，运行`adb devices`来确保有设备连接到了电脑上

3. 运行`react-native run-android`打包编译安卓项目，并部署到模拟器或开发机中

4. 运行上一条命令之前，要确保有设备连接到了电脑上，可以运行`adb devices`查看当前接入的设备列表，打包好的文件，放到了`android\app\build\outputs\apk`目录下

5. [入坑指南](http://www.open-open.com/lib/view/open1477469117948.html)

   > **问题1：开启悬浮框权限；**<br/>
   > **问题2：Could not get BatchedBridge, make sure your bundle is packaged correctly**<br/>
   > 解决方案：在终端中，进入到项目的根目录，执行下面这段命令行：<br/>
   > `react-native bundle --platform android --dev false --entry-file index.android.js --bundle-output android/app/src/main/assets/index.android.bundle --assets-dest android/app/src/main/res/`<br/>
   > 运行之前，需要确保`android/app/src/main/`目录下有`assets`文件夹，如果没有，手动创建之~，再运行上面的命令；<br/>
   > **问题3：could not connect to development server**<br/>
   > 解决方案：晃动手机，唤起设置属性窗口，点击“Dev settings”，再点击Debuug server host 出现设置ip地址窗口，填写Ip地址和端口号8081，例如`192.168.1.111:8081`

## [Weex快速打包](http://weex.apache.org/cn/guide/tools/toolkit.html)

1. 安装依赖:Weex 官方提供了 weex-toolkit 的脚手架工具来辅助开发和调试。首先，你需要最新稳定版的 Node.js 和 Weex CLi。
2. 运行`npm install -g weex-toolkit`安装Weex 官方提供的 `weex-toolkit` 脚手架工具到全局环境中
3. 运行`weex create project-name`初始化Weex项目
4. 进入到项目的根目录中，打开cmd窗口，运行`weex platform add android`安装android模板，首次安装模板时，等待时间较长，建议fq安装模板
5. 打开`android studio`中的`安卓模拟器`，或者将`启用USB调试的真机`连接到电脑上，运行`weex run android`，打包部署weex项目
6. 部署完成，查看项目效果

## 总结重点

1. 什么是前端移动App开发
2. 市面上常见的App开发方式及优缺点
3. 使用Hbuilder在线生成安卓应用
4. 学会配置ReactNative开发环境
5. 掌握ReactNative打包流程

# React.js

## React简介

- React 起源于 Facebook 的内部项目，因为该公司对市场上所有 JavaScript MVC 框架，都不满意，就决定自己写一套，用来架设 Instagram（照片交友） 的网站。做出来以后，发现这套东西很好用，**就在2013年5月开源了**。
- 由于 React 的**设计思想极其独特**，属于革命性创新，性能出众，代码逻辑却非常简单。所以，越来越多的人开始关注和使用，认为它可能是将来 Web 开发的主流工具。
- 清楚两个概念：
  - library（库）：小而巧的库，只提供了特定的API；优点就是 船小好掉头，可以很方便的从一个库切换到另外的库；但是代码几乎不会改变；
  - Framework（框架）：大而全的是框架；框架提供了一整套的解决方案；所以，如果在项目中间，想切换到另外的框架，是比较困难的；

### 前端三大主流框架

### React与vue的对比

Vue 的表单可以使用 `v-model` 支持**双向绑定**，相比于 React 来说开发上更加方便，当然了 `v-model`其实就是个语法糖，本质上和 React 写表单的方式没什么区别。

改变数据方式不同，Vue **修改状态**相比来说要简单许多，React 需要使用 `setState` 来改变状态，并且使用这个 API 也有一些坑点。并且 Vue 的底层使用了依赖追踪，页面更新渲染已经是最优的了，但是 React 还是需要用户手动去优化这方面的问题。

React 16以后，有些钩子函数会执行多次，这是因为引入 Fiber 的原因，这在后续的章节中会讲到。

React 需要**使用 JSX**，有一定的上手成本，并且需要一整套的**工具链支持**，但是**完全可以通过 JS 来控制页面，更加的灵活**。Vue 使用了**模板语法**，相比于 JSX 来说**没有那么灵活，但是完全可以脱离工具链**，通过直接编写 `render` 函数就能在浏览器中运行。

在生态上来说，两者其实没多大的差距，当然 React 的用户是远远高于 Vue 的。

在上手成本上来说，Vue 一开始的定位就是尽可能的降低前端开发的门槛，然而 React 更多的是去改变用户去接受它的概念和思想，相较于 Vue 来说上手成本略高。

#### 组件化方面

1. **什么是模块化：**是从**代码**的角度来进行分析的；把一些可复用的代码，抽离为单个的模块；便于项目的维护和开发；
2. **什么是组件化：** 是从 **UI 界面**的角度来进行分析的；把一些可服用的UI元素，抽离为单独的组件；便于项目的维护和开发；
3. **组件化的好处：**随着项目规模的增大，手里的组件越来越多；很方便就能把现有的组件，拼接为一个完整的页面；
4. **Vue是如何实现组件化的：** 通过 `.vue` 文件，来创建对应的组件；
   - template  结构
   - script        行为
   - style           样式

5. **React如何实现组件化**：React中有组件化的概念，但是，并没有像vue这样的组件模板文件；React中，一切都是以JS来表现的；因此要学习React，JS要合格；ES6 和 ES7 （async  和 await） 要会用；

#### 开发团队方面

- React是由FaceBook前端官方团队进行维护和更新的；因此，React的维护开发团队，技术实力比较雄厚；
- Vue：第一版，主要是有作者 尤雨溪 专门进行维护的，当 Vue更新到 2.x 版本后，也有了一个以 尤雨溪 为主导的开源小团队，进行相关的开发和维护；

#### 移动APP开发体验方面

- Vue，结合 Weex 这门技术，提供了 迁移到 移动端App开发的体验（Weex，目前只是一个 小的玩具， 并没有很成功的 大案例；）
- React，结合 ReactNative，也提供了无缝迁移到 移动App的开发体验（RN用的最多，也是最火最流行的）；

### React的优点

1. 和Angular1相比，React设计很优秀，一切基于JS并且实现了组件化开发的思想；
2. 开发团队实力强悍，不必担心断更的情况；
3. 社区强大，很多问题都能找到对应的解决方案；
4. 提供了无缝转到 ReactNative 上的开发体验，让我们技术能力得到了拓展；增强了我们的核心竞争力；
5. 很多企业中，前端项目的技术选型采用的是React.js；

## 几个核心的概念

### 虚拟DOM（Virtual Document Object Model）

- **DOM的本质是什么**：浏览器中的概念，浏览器中用JS对象来表示页面上的元素，并提供了操作DOM 对象的API；

- **什么是React中的虚拟DOM**：是框架中的概念，框架中用JS对象来模拟页面上的 DOM 和 DOM嵌套；

- **为什么要实现虚拟DOM：**为了实现页面中， DOM 元素的高效更新

- **DOM和虚拟DOM的区别**：

  - **DOM：**浏览器中，提供的概念；用JS对象，表示页面上的元素，并提供了操作元素的API；

  - 网页的呈现

    - 浏览器请求获取HTML代码
    - 在内存中解析DOM结构，渲染出DOM树
    - 将DOM树呈现到页面

  - **虚拟DOM：**是框架中的概念；而是开发框架的程序员，手动用JS对象来模拟DOM元素和嵌套关系；

    - 本质： 用JS对象，来模拟DOM元素和嵌套关系；
    - 目的：就是为了实现页面元素的高效更新；

    ![虚拟DOM - 表格排序案例](F:/01_video/%E5%89%8D%E7%AB%AF/16.react4.js%EF%BC%88%E5%85%B155%E9%9B%86%EF%BC%89/reactjs%E7%B2%BE%E5%93%81%E6%95%99%E7%A8%8B%E8%B5%84%E6%96%99/day1%E8%B5%84%E6%96%99/%E7%AC%94%E8%AE%B0/images/%E8%99%9A%E6%8B%9FDOM%E5%BC%95%E5%85%A5%E5%9B%BE%E7%89%87.png)

相较于 DOM 来说，操作 JS 对象会快很多，可以通过 JS 来模拟 DOM

```js
const ul = {
  tag: 'ul',
  props: {
    class: 'list'
  },
  children: {
    tag: 'li',
    children: '1'
  }
}
```

上述代码对应的 DOM 就是

```html
<ul class='list'>
  <li>1</li>
</ul>
```

### Diff算法

那么既然 DOM 可以通过 JS 对象来模拟，反之也可以通过 JS 对象来渲染出对应的 DOM。当然了，通过 JS 来模拟 DOM 并且渲染对应的 DOM 只是第一步，难点在于如何判断新旧两个 JS 对象的**最小差异**并且实现**局部更新** DOM。

首先 DOM 是一个多叉树的结构，如果需要完整的对比两颗树的差异，那么需要的时间复杂度会是 O(n ^ 3)，这个复杂度肯定是不能接受的。于是 React 团队优化了算法，实现了 O(n) 的复杂度来对比差异。 实现 O(n) 复杂度的关键就是**只对比同层的节点**，而不是跨层对比，这也是考虑到在实际业务中很少会去跨层的移动 DOM 元素。 所以判断差异的算法就分为了两步

- 首先从上至下，从左往右遍历对象，也就是树的深度遍历，这一步中会给每个节点添加索引，便于最后渲染差异
- 一旦节点有子元素，就去判断子元素是否有不同

在第一步算法中我们需要判断新旧节点的 `tagName` 是否相同，如果不相同的话就代表节点被替换了。如果没有更改 `tagName` 的话，就需要判断是否有子元素，有的话就进行第二步算法。

在第二步算法中，我们需要判断原本的列表中是否有节点被移除，在新的列表中需要判断是否有新的节点加入，还需要判断节点是否有移动。

举个例子来说，假设页面中只有一个列表，我们对列表中的元素进行了变更

```js
// 假设这里模拟一个 ul，其中包含了 5 个 li
[1, 2, 3, 4, 5]
// 这里替换上面的 li
[1, 2, 5, 4]
```

从上述例子中，我们一眼就可以看出先前的 `ul` 中的第三个 `li` 被移除了，四五替换了位置。

那么在实际的算法中，我们如何去识别改动的是哪个节点呢？这就引入了 `key` 这个属性，想必大家在 Vue 或者 React 的列表中都用过这个属性。这个属性是用来给每一个节点打标志的，用于判断是否是同一个节点。

当然在判断以上差异的过程中，我们还需要判断节点的属性是否有变化等等。

当我们判断出以上的差异后，就可以把这些差异记录下来。当对比完两棵树以后，就可以通过差异去局部更新 DOM，实现性能的最优化。

当然了 Virtual DOM 提高性能是其中一个优势，其实**最大的优势**还是在于：

1. 将 Virtual DOM 作为一个兼容层，让我们还能对接非 Web 端的系统，实现跨端开发。
2. 同样的，通过 Virtual DOM 我们可以渲染到其他的平台，比如实现 SSR、同构渲染等等。
3. 实现组件的高度抽象化

- **tree diff:**新旧两棵DOM树，逐层对比的过程，就是 Tree Diff； 当整颗DOM逐层对比完毕，则所有需要被按需更新的元素，必然能够找到；

- **component diff：**在进行Tree Diff的时候，每一层中，组件级别的对比，叫做 Component Diff；

  - 如果对比前后，组件的类型相同，则**暂时**认为此组件不需要被更新；
  - 如果对比前后，组件类型不同，则需要移除旧组件，创建新组件，并追加到页面上；

- **element diff:**在进行组件对比的时候，如果两个组件类型相同，则需要进行 元素级别的对比，这叫做 Element Diff；

  ![Diff算法图](./media/Diff.png)

## 初识React

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <!-- 解析jsx,babel中的 -->
    <script src="browser.js" charset="utf-8"></script>
    <script src="react.development.js" charset="utf-8"></script>
    <!-- 渲染 -->
    <script src="react-dom.development.js" charset="utf-8"></script>
</head>
<body>
    <div id="div"></div>
</body>
<!-- 必须使用text/babel -->
<script type="text/babel">
let root = document.getElementById("div")

// 渲染页面
ReactDOM.render(
    // className替换class,htmlFor替换label的for
    // 只能有一个根元素
    <div className="box">
        <div>aaa</div>
        <div>bbb</div>
        <div>
            <label htmlFor="user">用户名：</label>
            <input id="user" type="text" />
        </div>
    </div>,
    root
)
</script>
</html>
```

## 创建基本的webpack4.x项目

1. 运行`npm init -y` 快速初始化项目
2. 在项目根目录创建`src`源代码目录和`dist`产品目录
3. 在 src 目录下创建 `index.html`
4. 使用 cnpm 安装 webpack ，运行`cnpm i webpack webpack-cli -D`
   - 如何安装 `cnpm`: 全局运行 `npm i cnpm -g`
5. 注意：webpack 4.x 提供了 约定大于配置的概念；目的是为了尽量减少 配置文件的体积；
   - 默认约定了：
   - 打包的入口是`src` -> `index.js`
   - 打包的输出文件是`dist` -> `main.js`
   - 4.x 中 新增了 `mode` 选项(为必选项)，可选的值为：`development` 开发模式和 `production`;

### 配置webpack-dev-server

### 配置html-webpack-plugin配置

## 使用react

需要用到

```html
<script src="browser.js" charset="utf-8"></script>
<script src="react.development.js" charset="utf-8"></script>
<script src="react-dom.development.js" charset="utf-8"></script>
```

react：核心

react-dom：渲染

jsx：创建元素方便，语法糖，会编译成js

## 在项目中使用 react

1. 运行 `cnpm i react react-dom -S` 安装包

   - react： 专门用于创建组件和虚拟DOM的，同时组件的生命周期都在这个包中
   - react-dom： 专门进行DOM操作的，最主要的应用场景，就是`ReactDOM.render()`

2. 在`index.html`页面中，创建容器：

   ```html
   <!-- 容器，将来，使用 React 创建的虚拟DOM元素，都会被渲染到这个指定的容器中 -->
   <div id="app"></div>
   ```

3. 导入包：

   ```js
   import React from 'react' // 名字必须是React
   import ReactDOM from 'react-dom' // 名字必须是ReactDOM
   ```

4. 创建虚拟DOM元素：

   ```jsx
   // 这是 创建虚拟DOM元素的 API    <h1 title="啊，五环" id="myh1">你比四环多一环</h1>
   //  第一个参数： 字符串类型的参数，表示要创建的标签的名称
   //  第二个参数： 对象类型的参数， 表示 创建的元素的属性节点
   //  第三个参数及以后： 子节点
   const myh1 = React.createElement('h1', { title: '啊，五环', id: 'myh1' }, '你比四环多一环')
   ```

5. 渲染：

   ```js
   // 3. 渲染虚拟DOM元素
   // 参数1： 表示要渲染的虚拟DOM对象
   // 参数2： 指定容器,注意：这里不能直接放 容器元素的Id字符串，需要放一个容器的DOM对象
   ReactDOM.render(myh1, document.getElementById('app'))
   ```

### 脚手架-create-react-app

需要yarn或者用npm重新下

`npm i -g create-react-app`

`create-react-add xxx`

## JSX语法

> 什么是JSX语法：就是符合 xml 规范的 JS 语法；（语法格式相对来说，要比HTML严谨很多）

1. **如何启用 jsx 语法？**

   - 安装 `babel` 插件

     - 运行`cnpm i babel-core babel-loader babel-plugin-transform-runtime -D`
     - 运行`cnpm i babel-preset-env babel-preset-stage-0 -D`

   - 安装能够识别转换jsx语法的包 `babel-preset-react` 

     - 运行`cnpm i babel-preset-react -D`

   - 添加 `.babelrc` 配置文件

     ```json
     {
       "presets": ["env", "stage-0", "react"],
       "plugins": ["transform-runtime"]
     }
     ```

   - 添加babel-loader配置项：

     ```js
     module: { //要打包的第三方模块
         rules: [
           { test: /\.js|jsx$/, use: 'babel-loader', exclude: /node_modules/ }
         ]
     }
     ```

2. **jsx 语法的本质：**并不是直接把 jsx 渲染到页面上，而是 内部先转换成了 createElement 形式，再渲染的；

3. **在 jsx 中混合写入 js 表达式**：在 jsx 语法中，要把 JS代码写到 `{ }` 中

   - 渲染数字
   - 渲染字符串
   - 渲染布尔值
   - 为属性绑定值
   - 渲染jsx元素
   - 渲染jsx元素数组
   - 将普通字符串数组，转为jsx数组并渲染到页面上【两种方案】

```jsx
const arr = ['aa', 'bb', 'cc']
// map，数据是对象时注意加上key属性
ReactDOM.render({arr.map(item => <h3>{item}</h3>)}, document.getElementById('app'))
```

1. **在 jsx 中 写注释**：推荐使用`{ /* 这是注释 */ }`

2. **为 jsx 中的元素添加class类名**：需要使用`className` 来替代 `class`；`htmlFor`替换label的`for`属性

3. 在JSX创建DOM的时候，所有的节点，必须有唯一的根元素进行包裹；

4. 在 jsx 语法中，标签必须 成对出现，如果是单标签，则必须自闭和！

> 当 编译引擎，在编译JSX代码的时候，如果遇到了`<`那么就把它当作 HTML代码去编译，如果遇到了 `{}` 就把 花括号内部的代码当作 普通JS代码去编译；

## 相关文章

- [2018 年，React 将独占前端框架鳌头？](https://mp.weixin.qq.com/s/gV-w_rRfdBVAqsOpBGZaVw)
- [前端框架三巨头年度走势对比：Vue 增长率最高](https://mp.weixin.qq.com/s/0wXWqKIigaKzMSfy4vJMVw)

- [React数据流和组件间的沟通总结](http://www.cnblogs.com/tim100/p/6050514.html)
- [单向数据流和双向绑定各有什么优缺点？](https://segmentfault.com/q/1010000005876655/a-1020000005876751)
- [怎么更好的理解虚拟DOM?](https://www.zhihu.com/question/29504639?sort=created)
- [React中文文档 - 版本较低](http://www.css88.com/react/index.html)
- [React 源码剖析系列 － 不可思议的 react diff](http://blog.csdn.net/yczz/article/details/49886061)
- [深入浅出React（四）：虚拟DOM Diff算法解析](http://www.infoq.com/cn/articles/react-dom-diff?from=timeline&isappinstalled=0)
- [一看就懂的ReactJs入门教程（精华版）](http://www.cocoachina.com/webapp/20150721/12692.html)
- [CSS Modules 用法教程](http://www.ruanyifeng.com/blog/2016/06/css_modules.html)
- [将MarkDown转换为HTML页面](http://blog.csdn.net/itzhongzi/article/details/66045880)
- [win7命令行 端口占用 查询进程号 杀进程](https://jingyan.baidu.com/article/0320e2c1c9cf0e1b87507b26.html)

##  安装 React Developer Tools 调试工具

[React Developer Tools - Chrome 扩展下载安装地址](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi?hl=zh-CN)

## React中创建组件

### 构造函数创建组件

> **使用构造函数来创建组件**，如果要接收外界传递的数据，需要在构造函数的参数列表中使用`props`来接收；
>
> 必须要向外return一个合法的JSX创建的虚拟DOM；

- 创建组件：

  ```jsx
  function Hello (props) { 
  	// return null 
  	return <div>Hello 组件</div>
  }
  ```

- 为组件传递数据：

  ```jsx
  // 使用组件并为组件传递 props 数据
  <Hello name={dog.name} age={dog.age} gender={dog.gender}></Hello>
  <Hello {...dog}></Hello>
  
  // 在构造函数中，使用 props 形参，接收外界传递过来的数据
  function Hello(props) {
    // props.name = 'zs'
    console.log(props)
    // 结论：不论是 Vue 还是 React，组件中的 props 永远都是只读的；不能被重新赋值；
    return <div>这是 Hello 组件 --- {props.name} --- {props.age} --- {props.gender}</div>
  }
  ```


1. 父组件向子组件传递数据

2. 使用{...obj}属性扩散传递数据

3. 将组件封装到单独的文件中

4. 注意：组件的名称首字母必须是大写

5. 在导入组件的时候，如何省略组件的`.jsx`后缀名：

   ```js
   // 打开 webpack.config.js ，并在导出的配置对象中，新增 如下节点：
   resolve: {
       extensions: ['.js', '.jsx', '.json'], // 表示，这几个文件的后缀名，可以省略不写
       alias: {
           '@': path.join(__dirname, './src')
       }
     }
   ```

6. 在导入组件的时候，配置和使用`@`路径符号

### class创建组件

#### ES6中 class 关键字的使用

1. class 中 `constructor` 的基本使用
2. 实例属性和实例方法
3. 静态属性和静态方法

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

#### 基于class关键字创建组件

1. 最基本的组件结构：

   ```jsx
   // 如果要使用 class 定义组件，必须 让自己的组件，继承自 React.Component
   class 组件名称 extends React.Component {
       constructor(...args){
           super(...args)
           // 状态：constructor中初始化，要用setState({})修改更新后会重新渲染
           this.state = {
           }
       }
       // 在组件内部，必须有 render 函数,作用：渲染当前组件对应的 虚拟DOM结构
       render(){
           // render 函数中，必须 返回合法的 JSX 虚拟DOM结构
           return <div>这是 class 创建的组件</div>
       }
   }
   // 使用<名称></名称>相当与'组件名称'类的实例对象
   ```

传递的参数不用接收，直接使用this.props访问，只读

### 两种创建组件方式的对比

> 注意：使用 class 关键字创建的组件，有自己的私有数据（this.state） 和生命周期函数；
>
> 注意：使用 function 创建的组件，只有props，没有自己的私有数据和生命周期函数；

1. 用**构造函数**创建出来的组件：叫做“无状态组件”【不需要有自己的私有数据时使用】
2. 用**class关键字**创建出来的组件：叫做“有状态组件”【需要有自己的私有数据时使用】
3. React官方说：无状态组件，由于没有自己的state和生命周期函数，所以运行效率会比有状态组件稍微高一些；

### 渲染评论列表

![效果](./media/cmtlist.png)

有两个组件，一个父组件一个子组件

#### 通过for循环生成多个组件

```jsx
import React from 'react'
import ReactDOM from 'react-dom'

function CommentsItem(props) {
    return {<div>
        <h1>{props.user}</h1>
    	<p>{props.content}</p>
    </div>)}
}

class Comments extends React.Component {
    constructor() {
        super()
        this.state = CommentList: [
            { id: 1, user: '张三', content: '哈哈，沙发' },
            { id: 2, user: '李四', content: '哈哈，板凳' },
            { id: 3, user: '王五', content: '哈哈，凉席' },
            { id: 4, user: '赵六', content: '哈哈，砖头' },
            { id: 5, user: '田七', content: '哈哈，楼下山炮' }
        ]
    }
    render() {
        return (
            <div>
            	<h1>评论列表</h1>
            	{this.state.CommentList.map(item => <CommentsItem {...item} key={item.id}>				 </CommentsItem>}
        	</div>
		)
    }
}
```

抽离组件

### 组件通信

props

```jsx
let root = document.getElementById("div")
// 父组件向子组件传值，子组件可修改
class Comp extends React.Component{
    constructor(...args){
        super(...args)
        this.state = {
            a: 0
        }
    }
    add(n){
        this.setState({
            a: this.state.a + n
        })
    }
    render() {
        return (
            <div>
                {this.state.a}
                <Sub par={this}/>
            </div>
        )
    }
}
class Sub extends React.Component {
    constructor(...args){
        super(...args)
        this.state = {
        }
    }
    fn(){
        this.props.par.add(1)
    }
    render() {
        return (
            <div>
                <input type="button" value="+1" onClick={this.fn.bind(this)} />
            </div>
        )
    }
}
ReactDOM.render(
    <div className="box">
        <div>
            <Comp a={2}/>
        </div>
    </div>,
    root
)
```

ref

```jsx
let root = document.getElementById("div")
// 子组件向父组件传值，父组件可修改

class Comp extends React.Component{
    constructor(...args){
        super(...args)
        this.state = {
        }
    }
    fn(){
        this.refs['sub'].add(1);
    }
    render() {
        return (
            <div>
                <input type="button" value="+1" onClick={this.fn.bind(this)} />
                <Sub ref='sub'/>
            </div>
        )
    }
}
class Sub extends React.Component{
    constructor(...args){
        super(...args)
        this.state = {
            a: 2
        }
    }
    add(n){
        this.setState({
            a: this.state.a + n
        })
    }
    render() {
        return (
            <div>
                {this.state.a}
            </div>
        )
    }
}
ReactDOM.render(
    <div className="box">
        <div>
            <Comp a={2}/>
        </div>
    </div>,
    root
)
```

## 设置样式

1. 使用普通的 `style` 样式，第一层括号表示js代码，第二层括号表示样式对象

   ```jsx
   <h1 style={ {color: 'red', fontWeight: 200} }></h1>
   ```

2. 将样式封装成单独的文件

   封装成多个对象

   封装成一个对象

   封装到一个文件

   ```js
   export default {
     item: {
       border: '1px dashed #ccc',
       margin: '10px',
       padding: '5px',
       boxShadow: '0 0 3px #ccc'
     },
     user: {
       fontSize: '14px'
     },
     content: {
       fontSize: '12px'
     }
   }
   ```

   ```jsx
   import style from './style.js'
   var dom = <h1 style={style.title}></h1>
   
   {/* style.js */}
   export default {
       title: {color: 'red'}
   }
   ```

3. 使用样式表

   ```jsx
   import style from './style.css'
   {/* 由于样式表没有作用域，这样使用的样式表是全局生效的 */}
   var dom = <h1 className="title"></h1>
   ```

### 启用 css-modules

1. 修改 `webpack.config.js`这个配置文件，为 `css-loader` 添加参数：

   ```js
   { test: /\.css$/, use: ['style-loader', 'css-loader?modules'] } // 为 .css 后缀名的样式表  启用 CSS 模块化
   ```

2. 在需要的组件中，`import`导入样式表，并接收模块化的 CSS 样式对象：

   cssObj返回类名或id名和模块化类名或id名的对应关系

   ```js
   // cssObj返回类名或id名和模块化类名或id名的对应关系
   import cssObj from '../css/CmtList.css' 
   ```

3. 在需要的HTML标签上，使用`className`指定模块化的样式：

   ```jsx
   <h1 className={cssObj.title}>评论列表组件</h1>
   ```

4. 使用`localIdentName`自定义生成的类名格式，可选的参数有：

   - [path]  表示样式表 `相对于项目根目录` 所在路径
   - [name]  表示 样式表文件名称
   - [local]  表示样式的类名定义名称
   - [hash:length]  表示32位的hash值
   - 例子：`{ test: /\.css$/, use: ['style-loader', 'css-loader?modules&localIdentName=[path][name]-[local]-[hash:5]'] }`

### 使用 `:local()` 和 `:global()`

- `:local()`包裹的类名，是被模块化的类名，只能通过`className={cssObj.类名}`来使用

  同时，`:local`默认可以不写，这样，默认在样式表中定义的类名，都是被模块化的类名；

- `:global()`包裹的类名，是全局生效的，不会被 `css-modules` 控制，定义的类名是什么，就是使用定义的类名`className="类名"`

1. 注意：只有`.title`这样的类样式选择器，才会被模块化控制，类似于`body`这样的标签选择器，不会被模块化控制；

2. 同时指定多个类名

   `<h1 className={styleObj.title + ' test'}></h1>`

   `<h1 className={[styleObj.tetle, 'test'].join(' ')}></h1>`

### 第三方样式表

在项目中启用模块化并同时使用bootstrap，也可以像自定义样式表那样使用但是麻烦，可以使用下面的方式

1. 把自己的样式表，定义为 `.scss`  文件

2. 第三方的 样式表，还是 以 `.css` 结尾

3. 我们只需要为自己的 `.scss` 文件，启用模块化即可；

4. 运行`cnpm i sass-loader node-sass -D` 安装能够解析`scss`文件的loader

5. 添加loader规则：

   ```json
   { test: /\.scss$/, use: ['style-loader', 'css-loader?modules&localIdentName=[path][name]-[local]-[hash:5]', 'sass-loader'] } // 打包处理 scss 文件的 loader​
   ```

## 绑定事件

### 原生方式获取元素并绑定事件

在componentDidMount()中获取DOM绑定事件：

使用箭头函数保证this指向

要改变props时，定义state保存要修改的属性并从props中获取值进行初始化

### React 中的绑定事件

1. 事件的名称都是React的提供的，因此名称的首字母必须大写`onClick`、`onMouseOver`

2. 为事件提供的处理函数，必须是如下格式

   ```
   onClick= { function }
   ```

3. 用的最多的事件绑定形式为：

   ```jsx
   // 这里的this是组件实例
   <button onClick={ () => this.show('传参') }>按钮</button>
   
   // 事件的处理函数，需要定义为 一个箭头函数，然后赋值给 函数名称，如果定义为普通方法，this为undefined
   show = (arg1) => {
       console.log('show方法' + arg1)
   }
   ```

4. 在React中，如果想要修改 state 中的数据，推荐使用 `this.setState({ })`这个方法是异步的，要立即拿到更改完数据可以用回调函数`this.setState({ }, cb)`

## 绑定文本框与state中的值

1. 在 Vue 中，默认提供了`v-model`指令，可以很方便的实现 `数据的双向绑定`；
2. 但是，在 React 中，默认只是`单向数据流`，也就是 只能把 state 上的数据绑定到 页面，无法把 页面中数据的变化，自动同步回 state ； 如果需要把 页面上数据的变化，保存到 state，则需要程序员手动监听`onChange`事件，拿到最新的数据，手动调用`this.setState({  })` 更改回去；
3. 如果文本框只是单项绑定了state状态，没有提供onChange事件，文本框是只读的并且会有警告，如果只想要一个只读的文本框，要添加readOnly属性

```jsx
    {/*只要将value属性，和state上的状态进行绑定，那么，这个表单元素就变成了受控表单元素，这时候，如果没有调用相关的事件，是无法手动修改表单元素中的值的*/}
    <input style={{ width: '100%' }} ref="txt" type="text" value={this.state.msg} onChange={this.handleTextChange} />

    // 这是文本框内容改变时候的处理函数
    handleTextChange = () => {
        this.setState({
            msg: this.refs.txt.value
        });
    }
```

1. 注意`setState的一个问题`：

```jsx
// 保存最新的state状态值，在保存的时候，是异步地进行保存的，所以，如果想要获取最新的，刚刚保存的那个状态，需要通过回掉函数的形式去获取最新state
this.setState({
    msg: this.refs.txt.value
    // msg: e.target.value
    // 或通过DOM获取
}, function () {
    // 获取最新的state状态值
    console.log(this.state.msg);
});
```

### e.target获取文本框的值

```jsx
<input type="text" style={{ width: '100%' }} value={this.state.msg} onChange={() => this.textChanged()} ref="mytxt" />

  // 响应 文本框 内容改变的处理函数
  // 获取文本框的值
  // 1.通过事件对象e.target.value
  // 2.通过ref属性
  textChanged = () => {
    // console.log(this);
    // console.log(this.refs.mytxt.value);
    this.setState({
      msg: this.refs.mytxt.value
    })
  }
```

### 使用ref获取DOM元素引用

和 Vue 中差不多，vue 为页面上的元素提供了 `ref` 的属性，如果想要获取 元素引用，则需要使用`this.$refs.引用名称`

在 React 中，也有 `ref`, 如果要获取元素的引用`this.refs.引用名称`

## 组件的生命周期

- 概念：在组件创建、到加载到页面上运行、以及组件被销毁的过程中，总是伴随着各种各样的事件，这些在组件特定时期，触发的事件，统称为组件的生命周期；

- 组件生命周期分为三部分：

  - 初始化props属性默认值`static defaultProps = {}`，防止组件中必须属性没传递时报错

  - **组件创建阶段**：组件创建阶段的生命周期函数，只执行一次；

    先执行构造函数`this.state = {}`，new之后就调用

  > componentWillMount: 组件将要被挂载，此时还没有开始渲染虚拟DOM
  > render：第一次开始渲染真正的虚拟DOM，当render执行完，内存中就有了完整的虚拟DOM了
  > componentDidMount: 组件完成了挂载，此时，组件已经显示到了页面上，当这个方法执行完，组件就进入都了运行中的状态

  - **组件运行阶段**：根据组件的state和props的改变，有选择性的触发0次或多次；

  > componentWillReceiveProps: 组件将要接收新属性，此时，只要这个方法被触发，就证明父组件为当前子组件传递了新的属性值；
  > shouldComponentUpdate: 组件是否需要被更新，此时，组件尚未被更新，但是，state 和 props 肯定是最新的，返回false重新回到运行中，但是页面不是最新的
  > componentWillUpdate: 组件将要被更新，此时，尚未开始更新，内存中的虚拟DOM树还是旧的
  > render: 此时，又要重新根据最新的 state 和 props 重新渲染一棵内存中的 虚拟DOM树，当 render 调用完毕，内存中的旧DOM树，已经被新DOM树替换了！此时页面还是旧的
  > componentDidUpdate: 此时，页面又被重新渲染了，state 和 虚拟DOM 和 页面已经完全保持同步

  - **组件销毁阶段**：只执行一次；

  > componentWillUnmount: 组件将要被卸载，此时组件还可以正常使用；
  >

[React Native 中组件的生命周期](http://www.race604.com/react-native-component-lifecycle/)


![React中组件的生命周期](./images/LifeCycle.png)

### defaultProps

> 在组件创建之前，会先初始化默认的props属性，这是全局调用一次，严格地来说，这不是组件的生命周期的一部分。在组件被创建并加载候，首先调用 constructor 构造器中的 this.state = {}，来初始化组件的状态。

React生命周期的回调函数总结成表格如下：
![React生命周期表格](E:/%E4%B8%B4%E6%97%B6/26%20React/%E7%AC%94%E8%AE%B0+%E6%BA%90%E4%BB%A3%E7%A0%81/%E7%AC%94%E8%AE%B0+%E6%BA%90%E4%BB%A3%E7%A0%81/React%E8%B5%84%E6%96%99/%E6%B7%B7%E5%90%88app%E8%B5%84%E6%96%99/code/day04/%E7%AC%94%E8%AE%B0/images/React%E7%94%9F%E5%91%BD%E5%91%A8%E6%9C%9F%E8%A1%A8%E6%A0%BC.png)
组件生命周期的执行顺序：

- Mounting：

  - constructor()
  - componentWillMount()
  - render()
  - componentDidMount()

- Updating：

  - componentWillReceiveProps(nextProps)
  - shouldComponentUpdate(nextProps, nextState)
  - componentWillUpdate(nextProps, nextState)
  - render()
  - componentDidUpdate(prevProps, prevState)

- Unmounting：

  - componentWillUnmount()

### Counter计数器的小案例

封装组件

1. 给组件设置默认启动属性：`static defaultProps = {}`

2. 给属性进行类型校验，需要先运行`cnpm i prop-types --save`，v.15之后单独抽离了这个包

   ```jsx
   import React from 'react'
   import PropTypes from 'prop-types'
   class Counter{
       constructor(props) extends React.Componet{
           super(props)
           this.state = {}
       }
   	static defaultProps = {initCount: 0}
   	// 创建一个propTypes对象，可以给外界传递的属性进行类型校验
   	static propTypes = {initCount: PropTypes.number}
   	render() {
       	return <div>
           </div>
   	}
   }
   ```

### 组件初始化时生命周期事件总结

1. componentWillMount：可以获取props，state和已经定义的函数，相当于Vue的created函数

2. render：创建虚拟DOM

3. componentDidMount：可以获取页面的DOM元素，想要操作DOM最早在这个函数

4. shouldComponentUpdate：必须返回布尔，返回false时虚拟DOM和页面都不会更新，可能会造成画面和组件状态的不一致

   直接通过`this.state`获取的state值是上一次的值，要获取最新的值，要通过参数列表的`nextProps或nextState`获取

5. componentWillUpdate：虚拟DOM和页面上的DOM都是旧的

6. render：创建阶段和运行阶段都有，DOM还没渲染之前可以利用短路运算防止报错

7. 注意：在render函数中，不能调用`setState()`方法

8. componentDidUpdate：DOM都是最新的

9. componentWillReceiveProp：第一次渲染不会触发，`this.props`获取到的是上一次的值，要获取最新的值，要通过参数列表的`nextProps或nextState`获取

## 绑定this并传参的三种方式

1. 在事件中绑定this并传参：

```jsx
// bind可以改变前面函数的this指向，和call/apply不同，call/apply改变this后会执行前面的函数
// bind的第一个参数改变了this指向，后面就是要传递的参数
<input type="button" value="在事件中绑定this并传参" onClick={this.handleMsg1.bind(this, '🍕', '🍟')} />

// 在事件中绑定this并传参
handleMsg1(arg1, arg2) {
    console.log(this);
    // 此时this是个null
    this.setState({
        msg: '在事件中绑定this并传参：' + arg1 + arg2
    });
}
```

1. 在构造函数中绑定this并传参:

```jsx
// 修改构造函数中的代码：
// bind的返回值是改变this之后的函数的引用
// bind不会改变原函数的this指向，要使用改变之后的函数要重新接收
this.handleMsg2 = this.handleMsg2.bind(this, '🚗', '🚚');

<input type="button" value="在构造函数中绑定this并传参" onClick={this.handleMsg2} />

// 在构造函数中绑定this并传参
handleMsg2(arg1, arg2) {
    this.setState({
        msg: '在构造函数中绑定this并传参：' + arg1 + arg2
    });
}
```

1. 用箭头函数绑定this并传参：

```jsx
// 用箭头函数绑定this并传参
<input type="button" value="用箭头函数绑定this并传参" onClick={() => { this.handleMsg3('👩', '👰') }} />

handleMsg3(arg1, arg2) {
    this.setState({
        msg: '用箭头函数绑定this并传参：' + arg1 + arg2
    });
}
```

## 父组件使用Context属性

如果结构过多，参数逐层传递不方便，可以在父组件中直接共享一个Context对象

在父组件定义`getChildContext`方法返回共享数据

规定共享数据的类型：`static childContextTypes = {color: propTypes.string}`

在子组件中校验类型：`static contextType = {color: propTypes.string}`

使用：`this.context.color`

### 相关文章

[类型校验](https://facebook.github.io/react/docs/typechecking-with-proptypes.html)
[Animation Add-Ons](https://reactjs.org/docs/animation.html#high-level-api-reactcsstransitiongroup)

## Redux

provider：包在最外面

connect：状态映射，合并冲突

reducer：状态对象

状态更新：action

npm i redux react-redux -D

```js
import {createStore} from 'redux'
import {Provider} from 'react-redux'

// 初始化和每次更新状态对象都会执行
function reducer1(state, action) {
    if(!state) {
        // 初始化
    }
    return state
}
// 简写
// 传入旧状态返回新状态
function reducer1(state={xxx}, action) {
    return state
}
// 创建存储对象
const store = createStore(reducer1)
// 用<Provider>包装根组件传入store对象store = {store}
// 使用
import {connect} from 'react-redux'
// export default App
// state来自reducer，props来自组件
// 只能接收不能修改，单向数据流，组件内也不能赋值
export default connect(function(state, props){
    // 混合，解决冲突
    // 使用state，组件props中会包含state的内容
    return state
    return {
        ...state,
        // 会重复的属性使用props
		name: props.name
        // 都进行保留
        name: [state.name, props.name]
    }
}, {
	// 当做组件的一部分，用props访问使用
    // 参数自定义
    setName(name) {
    	// 必须return，返回值为action，在reducer中
        return {
			type: 'set_name',
             name
        }
	}
})(App)
// reducer
function reducer1(state={xxx}, action) {
    if(action.type === 'set_name') {
        return {
            ...state,
            name: action.name
        }
    }
    // 要返回一个新的state
    return state
}

```

优化

```js
// 优化
// 单独的actions.js，找不到时会报错
export const SET_NAME = 'set_name'
// 单独的store.js
// 多个reducer
import {combineReducers} from 'redux'
let reducers = combineReducers({
    user: reducer1,
    comp: reducer2
})
export default createStorer(reducers)
// 修改相应的映射，修改时会触发所有的reducer
// 分模块，分成单独的文件
```

## 路由

react-router-dom

```js
import {BrowserRouter as Router, Route, Link} from 'react-router-dom'
...
```



```jsx
import React from 'react'
// BrowserRouter，以path为键，会刷新页面
// HashRouter，以哈希值为键，路由根容器，所有与路由相关的东西都包裹在它里面，一个网站只需要一个
// MemoryRouter，路由信息保存在内存中，刷新后状态不会保留
// Route，表示路由规则，重要的属性path， component
// Link，路由链接，有to属性
import {HashRouter, Route, Link} from 'react-router-dom'

export default class app extends React.Component{
    constructor(props) {
        super(props)
        this.state = {}
    }
    render() {
        // 使用HashRouter包裹表示使用路由，路径中多了＃，只需要使用一次
        // HashRouter中只能有一个根元素
        return
        <HashRouter>
            <div>
            	<Link to="/home"></h1>
            	<Link to="/movie"></h1>
            	<Link to="/about"></h1>
            </div>
            <hr/>
        	{/* 路由规则以及组件位置占位符 */}
            {/* 默认的路由匹配是模糊匹配，部分匹配也可以成功，加上exact属性表示精确匹配,精确匹配也会从上到下依次匹配 */}
            <Route path="/home" component={Home}></Route>
            {/* 使用:匹配参数 */}
            <Route path="/movie/:type/:id" component={Movie} exact></Route>
            <Route path="/about" component={About}></Route>
        </HashRouter>
    }
}
```

route：表示路由规则，自带三个 render method 和三个 props 。 

`<Route component> `

`<Route render> `

`<Route children> `

```
match
location
history
```

### 路由传参

使用:匹配参数 

`<Route path="/movie/:type/:id" component={Movie} exact></Route>`

获取参数，可以把路由参数保存到state中去，但是参数改变不会让组件销毁重新渲染，需要在componentDidUpdate中更新，由于state，props更新都会update，会导致重复更新，直接使用props更新不会有这个问题

`{this.props.match.params.type}`

```js
componentDidUpdate(old_props, old_state){
    // 判断是否更新
    if (old_state.id === this.props.match.params.id) {
        // 一般是获取数据，更新数据
        this.setState({
            // 设置状态也会导致update
            // props.location.params也行
            id: this.props.match.params.id
        })
    }
}
```

不提供query的传参可以自己解析，一般不会用，会导致页面刷新

### 嵌套路由

在组件中继续添加路由path需要包含父级路由，直接写不好维护，可以使用this.props.match.path

在父级设置默认路由：直接修改path

```jsx
render() {
    const path = this.props.match.path

    return (
        <div>
            {/* 嵌套路由 */}
            <Link to={`${path}/inter`}>国际</Link>
            <Link to={`${path}/society`}>社会</Link>

            <Route path={`${path}/inter`} componet={inter}></Route>
            <Route path={`${path}/society`} componet={society}></Route>
        </div>
	)
}
```

### 编程式导航

`this.props.hisory.push('')`

### switch组件

```js
import {HashRouter, Route, Link, Switch} from 'react=router-dom'

// 表示已经匹配到一个路由的情况下不再继续匹配
<Switch>
    <Route exact path="" component={}></Route>
    <Route exact path="" component={}></Route>
    <Route exact path="" component={}></Route>
</Switch>
```

## AntDesign框架UI

electron使用js，html，css的跨平台桌面应用

1. 运行`npm install antd --save`安装ant design
2. 导入相关组件：

```
import { DatePicker } from 'antd';
```

1. 导入样式：

```
import 'antd/dist/antd.css';
```

### 实现ANT组件的按需加载

1. 运行`cnpm i babel-plugin-import --save-dev`
2. 修改`.babelrc`文件：

```
{
    "presets":["es2015", "stage-0", "react"],
    "plugins":[
        "transform-runtime",
        ["import", { "libraryName": "antd", "style": "css" }]
        ]
}
```

1. 然后只需从 antd 引入模块即可，**无需单独引入样式**。等同于下面手动引入的方式。

### 组件

分页

## Redux

provider：包在最外面

connect：状态映射，合并冲突

reducer：状态对象

状态更新：action

npm i redux react-redux -D

```js
import {createStore} from 'redux'
import {Provider} from 'react-redux'

// 初始化和每次更新状态对象都会执行
function reducer1(state, action) {
    if(!state) {
        // 初始化
    }
    return state
}
// 简写
// 传入旧状态返回新状态
function reducer1(state={xxx}, action) {
    return state
}
// 创建存储对象
const store = createStore(reducer1)
// 用<Provider>包装根组件传入store对象store = {store}
// 使用
import {connect} from 'react-redux'
// export default App
// state来自reducer，props来自组件
// 只能接收不能修改，单向数据流，组件内也不能赋值
export default connect(function(state, props){
    // 混合，解决冲突
    // 使用state，组件props中会包含state的内容
    return state
    return {
        ...state,
        // 会重复的属性使用props
		name: props.name
        // 都进行保留
        name: [state.name, props.name]
    }
}, {
	// 当做组件的一部分，用props访问使用
    // 参数自定义
    setName(name) {
    	// 必须return，返回值为action，在reducer中
        return {
			type: 'set_name',
            name
        }
	}
})(App)
// reducer
function reducer1(state={xxx}, action) {
    if(action.type === 'set_name') {
        return {
            ...state,
            name: action.name
        }
    }
    // 要返回一个新的state
    return state
}
// 优化
// 单独的actions.js，找不到时会报错
export const SET_NAME = 'set_name'
// 单独的store.js
// 多个reducer
import {combineReducers} from 'redux'
let reducers = combineReducers({
    user: reducer1,
    comp: reducer2
})
export default createStorer(reducers)
// 修改相应的映射，修改时会触发所有的reducer
// 分模块，分成单独的文件

```

基本思想：单向数据流

state-》（component）props-》action-》state

## React-Server

# 豆瓣电影案例

## Node.js设置跨域

```js
app.use('*', function (req, res, next) {
	// 设置请求头为允许跨域
    res.header("Access-Control-Allow-Origin", "*");
    // 设置服务器支持的所有头信息字段
    res.header("Access-Control-Allow-Headers", "Content-Type,Content-Length, Authorization, Accept,X-Requested-With");
    // 设置服务器支持的所有跨域请求的方法
    res.header("Access-Control-Allow-Methods", "POST,GET");
    // next()方法表示进入下一个路由
    next();
});
```

## ES6基于Promise的fetch使用

受跨域限制

```js
fetch('')
    // 第一个then中获取不到数据，得到response对象，可以通过res.json()返回一个promise对象
    .then(res => {
    return res.json()
	})
 	// 第二个then返回的data就是获得的数据
    .then(data => {
    console.log(data)
})
```

## 第三方fetch-jsonp

和fetch使用是一样的

```js
import fetchJSONP from 'fetch-jsonp'
fetchJSONP('')
    // 第一个then中获取不到数据，得到response对象，可以通过res.json()返回一个promise对象
    .then(res => {
    return res.json()
	})
 	// 第二个then返回的data就是获得的数据
    .then(data => {
    console.log(data)
})
```

## react-router-dom路由跳转

- HashRouter：是一个路由的跟容器，一个应用程序中，一般只需要唯一的一个HashRouter容器即可！将来，所有的Route和Link都要在HashRouter中进行使用

- 注意：HashRouter中，只能有唯一的一个子元素

- Link：是相当于超链接一般的存在；点击Link，跳转到相应的路由页面！负责进行路由地址的切换！
- Route：是路由匹配规则，当路由地址发生切换的时候，就会来匹配这些定义好的Route规则，如果有能匹配到的路由规则，那么，就会展示当前路由规则所对应的页面！
- Route：除了是一个匹配规则之外，还是一个占位符，将来，此Route所匹配到的组件页面，将会展示到Route所在的这个位置！

```
// 其中path指定了路由匹配规则，component指定了当前规则所对应的组件
<Route path="" component={}></Route>
```

- 注意：react-router中的路由匹配，是进行模糊匹配的！可以通过`Route`身上的`exact`属性，来表示当前的`Route`是进行精确匹配的
- 可以使用`Redirect`实现路由重定向

```
    // 导入路由组件
    import {Route, Link, Redirect} from 'react-router-dom'
    <Redirect to="/movie/in_theaters"></Redirect>
```

## 相关文章

- [ANT DESIGN 一个 UI 设计语言](https://ant.design/index-cn)
- [react-router-dom](https://reacttraining.com/react-router/web/guides/quick-start)
- [豆瓣电影API地址](https://developers.douban.com/wiki/?title=api_v2)

- [正在热映 - in_theaters](https://api.douban.com/v2/movie/in_theaters)
- [即将上映 - coming_soon](https://api.douban.com/v2/movie/coming_soon)
- [top250](https://api.douban.com/v2/movie/top250)
- [电影详细信息 - subject](https://api.douban.com/v2/movie/subject/26309788)

- [跨域资源共享 CORS 详解 - 阮一峰](http://www.ruanyifeng.com/blog/2016/04/cors.html)
- [Request - Simplified HTTP client](https://github.com/request/request)
- [CSS3 transform 属性](http://www.w3school.com.cn/cssref/pr_transform.asp)
- [ES6 - Promise规范 - 阮一峰](http://es6.ruanyifeng.com/#docs/promise)
- [刘龙彬 - 博客园 - Javascript中Promise的简单使用](http://www.cnblogs.com/liulongbinblogs/p/6731288.html)
- [Javascript 中的神器——Promise](http://www.jianshu.com/p/063f7e490e9a)
- [MDN - Fetch API](https://developer.mozilla.org/zh-CN/docs/Web/API/Fetch_API)
- [MDN - Response](https://developer.mozilla.org/zh-CN/docs/Web/API/Response)
- [fetch-jsonp - 支持JSONP的Fetch实现](https://www.npmjs.com/package/fetch-jsonp)

# ReactNative

1. ReactNative是基于React这门框架的语法来进行开发的；
2. 因为RN不是网页，我们在网页中使用html，css都不能用，RN中提供了移动端 专用的一些组件，只能使用RN固有的组件；
3. 最终，开发出来的项目，是要运行到手机上的，那么，把一个 RN 的项目，完整的发布到手机上需要结合 安卓的签名打包步骤，并使用 RN 提供的打包命令，进行完整 apk 文件的发布；最终发布出来的就是 Release 版本的项目，可以上传到应用商店；

## 安装

Android Studio

yarn---npm i -g yarn

jdk 1.8



react-native-cli：npm i -g react-native-cli

react-native init xxx 

react-native run-android

## 配置ReactNative基本开发环境

[搭建基本的开发环境 - 英文官网](http://facebook.github.io/react-native/docs/getting-started.html)<br/>
[搭建基本的开发环境 - 中文](http://reactnative.cn/docs/0.42/getting-started.html#content)
这两篇文档对比着进行参考，进行相关的安装；

## 手机的相关配置

1. 使用数据线，把手机链接到电脑上；
2. 运行 `adb devices` 的命令，这个命令，是安卓开发环境提供的；
3. 需要先开启手机的`开发者模式`
4. 如果开启开发者模式之后，还是看不到设备，则尝试安装 `豌豆荚` 这样的工具，让这些工具帮助你在电脑上安装手机的驱动；

## 搭建RN的项目

1. 运行`react-native init 项目名称`来初始化一个react native项目；
   ![01.项目初始化完毕之后截图并说明](E:/%E4%B8%B4%E6%97%B6/26%20React/%E7%AC%94%E8%AE%B0+%E6%BA%90%E4%BB%A3%E7%A0%81/%E7%AC%94%E8%AE%B0+%E6%BA%90%E4%BB%A3%E7%A0%81/React%E8%B5%84%E6%96%99/%E6%B7%B7%E5%90%88app%E8%B5%84%E6%96%99/code/day07/%E7%AC%94%E8%AE%B0/images/01.%E9%A1%B9%E7%9B%AE%E5%88%9D%E5%A7%8B%E5%8C%96%E5%AE%8C%E6%AF%95%E4%B9%8B%E5%90%8E%E6%88%AA%E5%9B%BE%E5%B9%B6%E8%AF%B4%E6%98%8E.png)
2. 打包运行项目，把打包好的项目部署到手机中！

- 确保手机已经正确的链接到了当前电脑上，同时手机开启了`开发者调试模式`；可以使用`adb devices`来查看当前链接到电脑上的手机设备列表！
- 当确认手机正确链接到电脑上之后，可以运行`react-native run-android`来打包当前项目，并把打包好的项目以调试的模式安装到手机中！
- 打包完成之后的截图
  ![02.打包完成之后的截图](E:/%E4%B8%B4%E6%97%B6/26%20React/%E7%AC%94%E8%AE%B0+%E6%BA%90%E4%BB%A3%E7%A0%81/%E7%AC%94%E8%AE%B0+%E6%BA%90%E4%BB%A3%E7%A0%81/React%E8%B5%84%E6%96%99/%E6%B7%B7%E5%90%88app%E8%B5%84%E6%96%99/code/day07/%E7%AC%94%E8%AE%B0/images/02.%E6%89%93%E5%8C%85%E5%AE%8C%E6%88%90%E4%B9%8B%E5%90%8E%E7%9A%84%E6%88%AA%E5%9B%BE.png)
- React Package窗口的作用
  ![03.React Package窗口的作用](E:/%E4%B8%B4%E6%97%B6/26%20React/%E7%AC%94%E8%AE%B0+%E6%BA%90%E4%BB%A3%E7%A0%81/%E7%AC%94%E8%AE%B0+%E6%BA%90%E4%BB%A3%E7%A0%81/React%E8%B5%84%E6%96%99/%E6%B7%B7%E5%90%88app%E8%B5%84%E6%96%99/code/day07/%E7%AC%94%E8%AE%B0/images/03.React%20Package%E7%AA%97%E5%8F%A3%E7%9A%84%E4%BD%9C%E7%94%A8.png)
- 04.React  Packager打包编译代码截图
  ![04.React  Packager打包编译代码截图](E:/%E4%B8%B4%E6%97%B6/26%20React/%E7%AC%94%E8%AE%B0+%E6%BA%90%E4%BB%A3%E7%A0%81/%E7%AC%94%E8%AE%B0+%E6%BA%90%E4%BB%A3%E7%A0%81/React%E8%B5%84%E6%96%99/%E6%B7%B7%E5%90%88app%E8%B5%84%E6%96%99/code/day07/%E7%AC%94%E8%AE%B0/images/04.React%20%20Packager%E6%89%93%E5%8C%85%E7%BC%96%E8%AF%91%E4%BB%A3%E7%A0%81%E6%88%AA%E5%9B%BE.png)
- 当第一打包编译项目部署到手机上之后 - 如何设置开发服务器的地址
  ![05.当第一打包编译项目部署到手机上之后 - 如何设置开发服务器的地址.png](E:/%E4%B8%B4%E6%97%B6/26%20React/%E7%AC%94%E8%AE%B0+%E6%BA%90%E4%BB%A3%E7%A0%81/%E7%AC%94%E8%AE%B0+%E6%BA%90%E4%BB%A3%E7%A0%81/React%E8%B5%84%E6%96%99/%E6%B7%B7%E5%90%88app%E8%B5%84%E6%96%99/code/day07/%E7%AC%94%E8%AE%B0/images/05.%E5%BD%93%E7%AC%AC%E4%B8%80%E6%89%93%E5%8C%85%E7%BC%96%E8%AF%91%E9%A1%B9%E7%9B%AE%E9%83%A8%E7%BD%B2%E5%88%B0%E6%89%8B%E6%9C%BA%E4%B8%8A%E4%B9%8B%E5%90%8E%20-%20%E5%A6%82%E4%BD%95%E8%AE%BE%E7%BD%AE%E5%BC%80%E5%8F%91%E6%9C%8D%E5%8A%A1%E5%99%A8%E7%9A%84%E5%9C%B0%E5%9D%80.png)

## 项目结构介绍以及一些注意事项

## 样式

## 基本组件的使用介绍

- View：
- Text：文字必须放在这里，rr更新
- TextInput：
- Image：
- Button：
- ActivityIndicator：
- ScrollView：这是一个列表滚动的组件
- ListView：也是一个列表滚动的组件，但是，这个组件已经过时了，官方推荐使用 FlatList 来代替它

都是block

可以写一些基本样式：`color bacgrondColor textAlign lineHeight等`，没有继承

### 单位：绝对值/百分比

换算：

```js
import {Dimensions} from 'react-native'

const BASE_width = 750
export function calc(size) {
    let {width} = Dimensions.get('window')
    return size*width/BASE_WIDTH
}
```

### flex布局

```jsx
<Text>flex布局也是可以用的</Text>
{/* rr可以重新渲染 */}
<View style={{flexDirection: 'row', justifyContent: 'center'}}>
    <Text style={{flex:1, color: '#333'}}>欢迎~</Text>
    <Text style={{flex:1}}>来到</Text>
    <Text style={{flex:1}}>RN</Text>
</View>
```

## 判断组件是否被卸载

```
if (this._reactInternalInstance){
	// 组件没有被卸载
}
```

## [配置Tab栏](https://github.com/happypancake/react-native-tab-navigator)

## [配置Tab栏的图标](https://github.com/oblador/react-native-vector-icons)

> 注意：使用图标，需要使用 `Android SDK Manager` 安装 `Android SDK Build-tools 26.0.1` 并接收其 license;

## 案例：豆瓣电影列表

- 电影列表数据：`https://api.douban.com/v2/movie/in_theaters`
- 电影详细数据：`https://api.douban.com/v2/movie/subject/26309788`

## 安装路由

1. 运行`npm i react-native-router-flux --save`
2. 路由官网：`https://github.com/aksonov/react-native-router-flux`
3. 路由相关配置：`https://github.com/aksonov/react-native-router-flux/blob/master/docs/API.md`
4. 路由简单的DEMO：`https://github.com/aksonov/react-native-router-flux/blob/v3/docs/MINI_TUTORIAL.md`

## 路由的一些基本使用方法

## 配置首页的轮播图

1. 轮播图官网：`https://github.com/leecade/react-native-swiper?utm_source=tuicool&utm_medium=referral`
2. 运行`npm i react-native-swiper --save`安装轮播图组件
3. 导入轮播图组件`import Swiper from 'react-native-swiper';`
4. 其中，在Swiper身上，`showsPagination={false}`是用来控制页码的；`showsButtons={false}`是用来控制左右箭头显示与隐藏；`height={160}`是用来控制轮播图区域的高度的！
5. 设置轮播图的样式：

```css
var styles = StyleSheet.create({
    wrapper: {},
    slide1: {
        flex: 1,
        justifyContent: 'center',
        alignItems: 'center',
        backgroundColor: '#9DD6EB',
    },
    slide2: {
        flex: 1,
        justifyContent: 'center',
        alignItems: 'center',
        backgroundColor: '#97CAE5',
    },
    slide3: {
        flex: 1,
        justifyContent: 'center',
        alignItems: 'center',
        backgroundColor: '#92BBD9',
    },
    image:{
        width:'100%',
        height:'100%'
    }
})
```

1. 将组件的代码结构引入到页面上：

```jsx
<Swiper style={styles.wrapper} showsButtons={true} height={160} autoplay={true}>
                <View style={styles.slide1}>
                    <Image source={{uri:'http://www.itcast.cn/images/slidead/BEIJING/2017410109413000.jpg'}} style={styles.image}></Image>
                </View>
                <View style={styles.slide2}>
                    <Image source={{uri:'http://www.itcast.cn/images/slidead/BEIJING/2017440109442800.jpg'}} style={styles.image}></Image>
                </View>
                <View style={styles.slide3}>
                    <Image source={{uri:'http://www.itcast.cn/images/slidead/BEIJING/2017441409442800.jpg'}} style={styles.image}></Image>
                </View>
            </Swiper>
```

### 首页轮播图片URL地址：

- 图片地址1：http://www.itcast.cn/images/slidead/BEIJING/2017410109413000.jpg
- 图片地址2：http://www.itcast.cn/images/slidead/BEIJING/2017440109442800.jpg
- 图片地址3：http://www.itcast.cn/images/slidead/BEIJING/2017441409442800.jpg

## 渲染电影列表数据

## 渲染电影详情页面

## 调用摄像头拍照

[react-native-image-picker的github官网](https://github.com/marcshilling/react-native-image-picker)
[react native 之 react-native-image-picke的详细使用图解](http://www.cnblogs.com/shaoting/p/6148085.html)

1. 运行`npm install react-native-image-picker@latest --save`安装到项目运行依赖，此时调试**可能会报错**，如果报错，需要使用下面的步骤解决：
   - 先删除`node_modules`文件夹
   - 运行`npm i`
   - 运行`npm start --reset-cache`
2. 运行`react-native link`自动注册相关的组件到原生配置中
3. 打开项目中的`android`->`app`->`src`->`main`->`AndroidManifest.xml`文件，在第8行添加如下配置：

```
<uses-permission android:name="android.permission.CAMERA" />
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
```

1. 打开项目中的`android`->`app`->`src`->`main`->`java`->`com`->`当前项目名称文件夹`->`MainActivity.java`文件，修改配置如下：

   ```
   package com.native_camera;
   import com.facebook.react.ReactActivity;
   
   // 1. 添加以下两行：
   import com.imagepicker.permissions.OnImagePickerPermissionsCallback; // <- add this import
   import com.facebook.react.modules.core.PermissionListener; // <- add this import
   
   public class MainActivity extends ReactActivity {
       // 2. 添加如下一行：
       private PermissionListener listener; // <- add this attribute
   
       /**
        * Returns the name of the main component registered from JavaScript.
        * This is used to schedule rendering of the component.
        */
       @Override
       protected String getMainComponentName() {
           return "native_camera";
       }
   }
   ```

2. 在项目中添加如下代码：

   ```
   // 第1步：
   import {View, Button, Image} from 'react-native'
   import ImagePicker from 'react-native-image-picker'
   var photoOptions = {
     //底部弹出框选项
     title: '请选择',
     cancelButtonTitle: '取消',
     takePhotoButtonTitle: '拍照',
     chooseFromLibraryButtonTitle: '选择相册',
     quality: 0.75,
     allowsEditing: true,
     noData: false,
     storageOptions: {
       skipBackup: true,
       path: 'images'
     }
   }
   
   // 第2步：
   constructor(props) {
   super(props);
       this.state = {
         imgURL: ''
       }
     }
   
   // 第3步：
   <Image source={{ uri: this.state.imgURL }} style={{ width: 200, height: 200 }}></Image>
   <Button title="拍照" onPress={this.cameraAction}></Button>
   
   // 第4步：
   cameraAction = () => {
   ImagePicker.showImagePicker(photoOptions, (response) => {
     console.log('response' + response);
     if (response.didCancel) {
       return
     }
     this.setState({
       imgURL: response.uri
     });
   })
     }
   ```

3. **一定要退出之前调试的App**，并重新运行`react-native run-android`进行打包部署；这次打包期间会下载一些jar的包，需要耐心等待！

## 签名打包发布Release版本的apk安装包

- 请参考以下两篇文章：

- [ReactNative之Android打包APK方法（趟坑过程）](http://www.jianshu.com/p/1380d4c8b596)
- [React Native发布APP之签名打包APK](http://blog.csdn.net/fengyuzhengfan/article/details/51958848)

### 如何发布一个apk

1. 先保证自己正确配置了所有的 RN 环境
2. 在 cmd 命令行中，运行这一句话`keytool -genkey -v -keystore my-release-key2.keystore -alias my-key-alias2 -keyalg RSA -keysize 2048 -validity 10000`

- 其中： `my-release-key.keystore` 表示你一会儿要生成的那个 签名文件的 名称【很重要，包找个小本本记下来】
- `-alias` 后面的东西，也很重要，需要找个小本本记下来，这个名称可以根据自己的需求改动`my-key-alias`
- 当运行找个命令的时候，需要输入一系列的参数，找个口令的密码，【一定要找个小本本记下来】

1. 当生成了签名之后，这个签名，默认保存到了自己的用户目录下`C:\Users\liulongbin\my-release-key2.keystore`
2. 将你的签名证书copy到 android/app目录下。
3. 编辑 `android` -> `gradle.properties`文件，在最后，添加如下代码：

```
MYAPP_RELEASE_STORE_FILE=your keystore filename
MYAPP_RELEASE_KEY_ALIAS=your keystore alias
MYAPP_RELEASE_STORE_PASSWORD=*****
MYAPP_RELEASE_KEY_PASSWORD=*****
```

1. 编辑 android/app/build.gradle文件添加如下代码：

```
...
android {
    ...
    defaultConfig { ... }
    + signingConfigs {
    +    release {
    +        storeFile file(MYAPP_RELEASE_STORE_FILE)
    +        storePassword MYAPP_RELEASE_STORE_PASSWORD
    +        keyAlias MYAPP_RELEASE_KEY_ALIAS
    +        keyPassword MYAPP_RELEASE_KEY_PASSWORD
    +    }
    +}
    buildTypes {
        release {
            ...
    +        signingConfig signingConfigs.release
        }
    }
}
...
```

1. 进入项目根目录下的`android`文件夹，在当前目录打开终端，然后输入`./gradlew assembleRelease`开始发布APK的Release版；
2. 当发行完毕后，进入自己项目的`android\app\build\outputs\apk`目录中，找到`app-release.apk`，这就是我们发布完毕之后的完整安装包；就可以上传到各大应用商店供用户使用啦；

> 注意：请记得妥善地保管好你的密钥库文件，不要上传到版本库或者其它的地方。

## 相关文章

- [React Native 小米（红米）手机安装失败、白屏 Failed to establish session 解决方案](http://blog.csdn.net/u011240877/article/details/51983262)
- [React Native Android 初次试用遇到的各种坑](http://lib.csdn.net/article/reactnative/48721)
- [Redux 中文文档](http://www.redux.org.cn/)
- [react-native 在使用require加载本地图片时报Unexcepted character](http://blog.csdn.net/u014038534/article/details/53943862)
- [React Native for Android 发布独立的安装包](http://blog.csdn.net/u013531824/article/details/51003775)