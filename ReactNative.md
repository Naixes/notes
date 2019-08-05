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

# ReactNative

1. ReactNative是基于React这门框架的语法来进行开发的；
2. 因为RN不是网页，我们在网页中使用html，css都不能用，RN中提供了移动端 专用的一些组件，只能使用RN固有的组件；
3. 最终，开发出来的项目，是要运行到手机上的，那么，把一个 RN 的项目，完整的发布到手机上需要结合 安卓的签名打包步骤，并使用 RN 提供的打包命令，进行完整 apk 文件的发布；最终发布出来的就是 Release 版本的项目，可以上传到应用商店；

## 安装

Android Studio：作用：安装SDK，自带模拟器，环境变量：ANDROID_HOME（SDK路径）

yarn---npm i -g yarn

jdk 1.8：环境变量：JAVA_HOME（安装路径）和Path（bin路径）

genymotion：安卓模拟器，注意设置SDK路径



react-native-cli：npm i -g react-native-cli

react-native init xxx 

react-native run-android

### 遇到的问题

**adb server version（39）doesn't match this client（40）；killing……**

使用genymotion时遇到

原因：**启动Genymotion Android模拟器时遇到版本不一致问题**

解决方法：**设置SDK路径**

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

## 组件

### 对话框组件

Modal，Lightbox（路由的一部分）：通过Actions.push('xx', {})显示

```jsx
import {Lightbox} from 'react-native-router-flux'

export default class App extends Component {
  render() {
    return (
      <Router>
            // 会将第一个子元素作为页面，其他为弹框
            <Lightbox>
                <Scene key="root">
                  <Scene key="pageOne" component={PageOne} title="PageOne" initial={true} />
                  <Scene key="pageTwo" component={PageTwo} title="PageTwo" />
                </Scene>
                <Scene key="modal" component={Modal} title="Modal" />
            </Lightbox>
      </Router>
    )
  }
}
```

### 选择器

```jsx
import {Picker} from 'react-native'

export default class App extends Component {
    constructor(...args) {
        super(...args)
        this.state = {
            income: 0
        }
    }
    render() {
        return (
            <View>
                <Picker selectedValue={this.state.income} onValueChange={(value, index) => {this.setState({income: value})}}>
                    <Picker.Item label="支出" value={0}></Picker.Item>
                    <Picker.Item label="收入" value={1}></Picker.Item>
                </Picker>
            </View>
        )
    }
}

```

### 文字输入

```jsx
import {TextInput} from 'react-native'

export default class App extends Component {
    constructor(...args) {
        super(...args)
        this.state = {
            title: '',
            amount: 0
        }
    }
    render() {
        return (
            <View>
                <TextInput onChangeText={(text) => {this.setState({title: text})}} placehoder='请输入'>
                </TextInput>
                <TextInput onChangeText={(text) => {this.setState({amount: text})}} placehoder='请输入金额' keyboardType='number-pad'>
                </TextInput>
            </View>
        )
    }
}
```

### 按钮

```jsx
import {Button} from 'react-native'

export default class App extends Component {
    constructor(...args) {
        super(...args)
        this.state = {
            title: '',
            amount: 0
        }
    }
    render() {
        return (
            <View>
                <Button title='提交' color='#ccc' onPress={() => { }}></Button>
            </View>
        )
    }
}
```

### 提示

```jsx
import {Alert} from 'react-native'

export default class App extends Component {
    constructor(...args) {
        super(...args)
        this.state = {
            title: '',
            amount: 0
        }
    }
    render() {
        return (
            <View>
                <Button title='提交' color='#ccc' onPress={() => {Alert.alert('xxx', [{text: '确定'}])}}></Button>
            </View>
        )
    }
}
```

## 案例：豆瓣电影列表

- 电影列表数据：`https://api.douban.com/v2/movie/in_theaters`
- 电影详细数据：`https://api.douban.com/v2/movie/subject/26309788`

## 安装路由

1. 运行`npm i react-native-router-flux --save`
2. 路由官网：`https://github.com/aksonov/react-native-router-flux`
3. 路由相关配置：`https://github.com/aksonov/react-native-router-flux/blob/master/docs/API.md`
4. 路由简单的DEMO：`https://github.com/aksonov/react-native-router-flux/blob/v3/docs/MINI_TUTORIAL.md`

```jsx
import React, { Component } from 'react';
import { Router, Scene } from 'react-native-router-flux';

import PageOne from './PageOne';
import PageTwo from './PageTwo';

export default class App extends Component {
  render() {
    return (
      // router中只能有一个子元素
      <Router>
        <Scene key="root">
          <Scene key="pageOne" component={PageOne} title="PageOne" initial={true} />
          <Scene key="pageTwo" component={PageTwo} title="PageTwo" />
        </Scene>
      </Router>
    )
  }
}
```

each route (or page) is called a `<Scene>`. Conventionally, your Scenes should be wrapped inside a **root Scene** before being finally wrapped inside a `<Router>` component that is returned in the `render()` function.

At the very minimum, each `<Scene>` component should have the following props:

- **key**: A unique string that can be used to refer to the particular scene.
- **component**: The component to be rendered for that `Scene` or page.
- **title**: The string to be displayed in the nav bar at the top of the screen.

Note that the first scene we wish to load has the prop `initial={true}` to indicate that it's the scene that should be initially rendered.

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

   ```js
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

   ```js
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
- [React Native for Android 发布独立的安装包](