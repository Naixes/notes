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

## 混合App开发的优点

- 节省开发成本
  - 从工资上
  - 从时间上:使用前端技术开发App的话，速度很快，因为前端技术够简单（HTML+CSS+JS），但是原生的 安卓和 IOS 语言就很难学，其次，一些复杂的概念比较难懂，

市面上常见的App开发方式

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

[谁在使用React Native？？？](https://facebook.github.io/react-native/showcase.html)

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

# ReactNative

1. ReactNative是基于React这门框架的语法来进行开发的；
2. 因为RN不是网页，我们在网页中使用html，css都不能用，RN中提供了移动端 专用的一些组件，只能使用RN固有的组件；
3. 最终，开发出来的项目，是要运行到手机上的，那么，把一个 RN 的项目，完整的发布到手机上需要结合 安卓的签名打包步骤，并使用 RN 提供的打包命令，进行完整 apk 文件的发布；最终发布出来的就是 Release 版本的项目，可以上传到应用商店；

## 环境搭建

Android Studio：作用：安装SDK，自带模拟器，环境变量：ANDROID_HOME（SDK路径）

yarn---npm i -g yarn

jdk 1.8：环境变量：JAVA_HOME（安装路径）和Path（bin路径）

genymotion：安卓模拟器，注意设置SDK路径

> Demo项目参考demo-collection中的learnRN

### 遇到的问题

**adb server version（39）doesn't match this client（40）；killing……**

使用genymotion时遇到

原因：**启动Genymotion Android模拟器时遇到版本不一致问题**

解决方法：**设置SDK路径**

### 创建项目

react-native-cli：npm i -g react-native-cli

react-native init xxx 

react-native run-android

## 基本概念

### 基本组件

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

### 样式

文本只能放在text组件中，样式不能继承所以view不能设置颜色、字体等属性

样式名资本遵循web的css，使用驼峰命名

项目中一般使用`StyleSheet.create({xx:xx})`

#### 单位：绝对值/百分比

绝对值无单位，表示的是与设备像素密度无关的逻辑像素点，数值一样时在所有手机上显示的宽高一样

换算：

```js
import {Dimensions} from 'react-native'

const BASE_width = 750
export function calc(size) {
    let {width} = Dimensions.get('window')
    return size*width/BASE_WIDTH
}
```

#### flex布局

```jsx
<Text>flex布局也是可以用的</Text>
{/* rr可以重新渲染 */}
<View style={{flexDirection: 'row', justifyContent: 'center'}}>
    <Text style={{flex:1, color: '#333'}}>欢迎~</Text>
    <Text style={{flex:1}}>来到</Text>
    <Text style={{flex:1}}>RN</Text>
</View>
```

### 事件绑定

RN提供了一系列ouchable组件：TouchableOpacity，TouchableNativeFeedback，TouchableHighlight等

onPress，onBlur，onFocus，onLayout，onLongPress，onPressIn（onPress之前），onPressOut

### 网络请求

支持Fetch API，ajax（XMLHttpRequest API），Websocket等

### 其他

**判断组件是否被卸载**

```
if (this._reactInternalInstance){
	// 组件没有被卸载
}
```

ctrl+m debug：打开浏览器调试工具

## 组件

### 滚动视图

FlatList和ScrollView都有滚动效果

#### ScrollView

ScrollView 必须有一个确定的高度才能正常工作，因为它实际上所做的就是将一系列不确定高度的子组件装进一个确定高度的容器（通过滚动操作）。要给 ScrollView 一个确定的高度的话，要么直接给它设置高度（不建议），要么确定所有的父容器都有确定的高度。一般来说我们会给 ScrollView 设置`flex: 1`以使其自动填充父容器的空余空间，但前提条件是所有的父容器本身也设置了 flex 或者指定了高度，否则就会导致无法正常滚动。

`ScrollView`和`FlatList`应该如何选择？

ScrollView 会简单粗暴地把所有子元素一次性全部渲染出来。然而这样简单的渲染逻辑自然带来了性能上的不足。创建和渲染那些屏幕以外的 JS 组件和原生视图，显然对于渲染性能和内存占用都是一种极大的拖累和浪费。

`FlatList`会惰性渲染子元素，只在它们将要出现在屏幕中时开始渲染。这种惰性渲染逻辑要复杂很多，因而 API 在使用上也更为繁琐。除非你要渲染的数据特别少，否则你都应该尽量使用`FlatList`。此外`FlatList`还可以方便地渲染行间分隔线，支持多列布局，无限滚动加载等等。

#### FlatList

支持水平布局，显示和隐藏回调，单独的头部/尾部组件，下拉刷新，上拉加载，分割线，跳转指定行，多列布局等

```tsx
import React from 'react';
import { SafeAreaView, View, FlatList, StyleSheet, Text, StatusBar } from 'react-native';

const DATA = [
  {
    id: 'bd7acbea-c1b1-46c2-aed5-3ad53abb28ba',
    title: 'First Item',
  },
  {
    id: '3ac68afc-c605-48d3-a4f8-fbd91aa97f63',
    title: 'Second Item',
  },
  {
    id: '58694a0f-3da1-471f-bd96-145571e29d72',
    title: 'Third Item',
  },
];

const Item = ({ title }) => {
  return (
    <View style={styles.item}>
      <Text style={styles.title}>{title}</Text>
    </View>
  );
}

const App = () => {
  const renderItem = ({ item }) => (
    <Item title={item.title} />
  );

  return (
    <SafeAreaView style={styles.container}>
      <FlatList
        data={DATA}
        renderItem={renderItem}
        keyExtractor={item => item.id}
      />
    </SafeAreaView>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    marginTop: StatusBar.currentHeight || 0,
  },
  item: {
    backgroundColor: '#f9c2ff',
    padding: 20,
    marginVertical: 8,
    marginHorizontal: 16,
  },
  title: {
    fontSize: 32,
  },
});

export default App;
```

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
