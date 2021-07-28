## Linux

vps：虚拟服务器

### 环境

内核通过系统调用（api）向外提供功能，windows的图形界面在内核较稳定，linux在应用程序层不稳定

Centos7，8不稳定

虚拟机：vmware，mac下载fusion，win下载workstation pro

Centos：

下载：7 x86_64 ali或华为镜像7.9，minimal ios服务器版没有图形界面，dvd有图形界面（选workstation）

安装配置，录播课

牢记密码！！修改麻烦single模式

虚拟机窗口下不能卷屏，可以使用终端操作

虚拟机网络问题：桥接（vmware提供的虚拟网和宿主机网段不同，ip不会变）/映射（映射到硬件，同一网段，网络环境改变时ip会变）

终端访问虚拟机：

win终端软件：putty，xshell，cmder终端模拟器，terminal微软官方

mac：iterm2

```cmd
# linux中获取ip
# eth0
ifconfig
# 或者
ip addr

# 远程连接
ssh root@ip # 会车，首次确认指纹，输入密码
```

### 认识目录

目录树形式存在，root根用户，根目录，根权限（root超级管理员权限）

```cmd
bin # 命令，包含了大部分命令
boot # 系统内核
dev # 设备，硬件
lib # 公用函数库

etc # 配置文件，比如固定ip配置sysconfig/...没记下，注意5个点，注意备份.bak
home # 用户：两类用户，root（专用目录root）/普通用户（每个目录对应一个普通用户），cd+会车返回当前用户的home目录，su+用户名切换用户
root # root专用目录即root的home，路径中显示~
media # u盘等
mnt # 
opt # 程序
proc # 虚拟目录，内存中，存储的数据和状态，一个数字代表一个进程（pid）其他的是一些状态比如cpuinfo，memoinfo
sbin # 命令，->代表快捷方式，也叫链接，软链接，ls -l
usr # yum命令安装的软件，普通用户用的程序，include，头文件，src，源代码
var # 系统/服务等日志，www，Apache目录，log，日志
srv
sys
```

### 命令

文档资料

```cmd
ll # ls -l的简写详细信息列表，mac不支持 ls简单列表，l代表链接，d代表目录，-代表普通文件
pwd # 当前目录
man 命令 # 手册，q退出
```

### 概念

端口：端口绑定进程，网络端口

```cmd
netstat -an # 只能查看当前使用的端口
netstat -anp # 多了pid和程序名
ps aux # pid列表，不能区分主进程，越小越有可能是主进程
kill pid # 发出停止信号 -9强制终止
```

服务：守护进程

终端：

### 开发环境

nodejs，官网

xampp

开发环境，不能装到vps上，有漏洞

mac安装注意：不能点首页的，对应的vm版本打包到虚拟机里的，在download页面下载不是vm版的安装包！！

### vi

键盘图

**资料：常用命令**

## 操作系统

### 历史

早期批处理系统

操作系统基础功能：管理硬件，调用cpu，管理内存

### linux架构

<img src="Naixes阶段性学习笔记.assets/截屏2021-03-18 下午9.29.36.png" alt="截屏2021-03-18 下午9.29.36" style="zoom:50%;" />

<img src="Naixes阶段性学习笔记.assets/截屏2021-03-18 下午9.24.36.png" alt="截屏2021-03-18 下午9.24.36" style="zoom:50%;" />



分三层：用户，内核，硬件

内核主要子系统：进程管理，内存管理，文件系统，设备驱动，网络支持，到网络传输层

可以裁剪linux内核，嵌入式用到，自己做发行版等

两种模式：用户模式，内核模式

<img src="Naixes阶段性学习笔记.assets/截屏2021-03-18 下午9.34.00.png" alt="截屏2021-03-18 下午9.34.00" style="zoom:50%;" />

### windows架构

复杂，早期不稳定

95，98 -> NT5（xp，2000...）

兼容子系统，虚拟化技术支持，现在加上了ubuntu子系统

<img src="Naixes阶段性学习笔记.assets/截屏2021-03-18 下午9.32.57.png" alt="截屏2021-03-18 下午9.32.57" style="zoom:50%;" />

### 体系

mac内核，BSD系统unix分支（unix商业化之后出现的分支）后来又分出三个BSD，mac属于freeBSD（其他netBSD，openBSD）

minix：类unix，应用

Linux：类unix

cpu权限：r0-r3层，操作系统在第0层，程序在第3层，隐藏权限-1层，minix在-1层

unixware：商用unix

HP-UX：惠普

...

发行版：ubuntu（来源于debian，apt或apt -get包管理，服务管理：后来才使用system control），centos（来源于redhat，源通用，yum包管理，dnf包管理，服务管理：system control），redhat，fedora（来源于redhat，较为激进，界面好），debian（欧美多）

虚拟机：推荐服务器版，2G内存以上，桌面版，4G以上

### 远程登录linux

Windows：推荐xshell，cmder（可以使用linux命令，下载full版本）

linux和macOS：ssh命令`ssh 用户名@主机名`，主机名指ip或域名，不加协议

上传文件：cp复制文件，scp可以在不同机器之间进行复制，-r目录`scp ./xxx.zip root@192.168.1.7:/opt/backup # 注意冒号`

### 终端快捷键

ctrl+c 结束正在运行的程序【ping、telnet等】 ctrl+d 结束输入或退出shell

ctrl+s 暂停屏幕输出

ctrl+q 恢复屏幕输出

ctrl+l 清屏，等同于Clear

ctrl+a/ctrl+e 快速移动光标到行首/行尾

### linux命令

行编辑器vi/vim

服务管理命令systemctl（q退出）

- `systemctl status # 列出树结构 systemctl status nginx # 查看服务状态`
- `systemctl stop xxx # 没有反应需要重新查看状态，start restart类似`
- 特殊命令，取决于脚本，需要自己定义`systemctl reload nginx`

网络管理命令

- `ifconfig # 旧版centos < 6`
- `ip`
- `router # 路由`
- 排查网络故障`traceout`
- 重启网卡，`systemctl restart network`
- 端口，查看当前网络连接
  - ss
  - `netstate -anp | grep 80`过滤

命令行下载工具

- `curl uri -o outputname # 像wget使用时，不会下载，会打印在屏幕上，-o：output`
- `wget uri # 可能不存在，yum install wget，可以当爬虫用wget -r 网站地址：-r递归下载，广度优先，谨慎使用`

linux帮助

终端不小心`ctrl+s`：键盘无反应，`ctrl+q`：恢复屏幕输出

`ctrl+l`：清屏，相当于clear

`ctrl+a/e`：移动到行首行尾

进程管理命令

- `top：相当于任务管理器`
- `ps`
- `kill/pkill：`
- `w：当前登录`

## 后端

编程思路：需求，知识，技术，框架，工具 -> 思考/分析/想象/设计/整合/创造 -> 策略，产品，服务 -> 编码 -> 策略，产品，服务

面向对象：结构清晰，设计模式，三大特性

node是运行时不是语言

php，java，c#，python，go

### php

多线程支持不好

编码规范不统一

语法不太严谨

## QA

14:00

单元测试：TDD，BDD，断言库2个，karma自动化测试集成框架

25:00

xxx.spec.js/xxx.test.js

## 函数式编程

## 后端实践

单体应用：前后端业务逻辑都在一起都在服务器上

前后端分离分为半分离和全分离

node大并发，数据库操作不如php，java

发展：

CS/BS

CS，C，UI层 业务层 S，持久化层

BS，B，UI层，S，业务层 持久化层，B静态网站用Apache，动态网站用c写cgi用Apache调用---asp，jsp，php

### MVC模式

架构层面上的设计模式

<img src="Naixes阶段性学习笔记.assets/截屏2021-04-04 下午2.10.52.png" alt="截屏2021-04-04 下午2.10.52" style="zoom:30%;" />

controller：主要业务逻辑流程，控制数据流向

model：数据模型，与DB层交互，带有一定逻辑

view：处理器，将数据和模版结合生成页面

程序是数据结构+算法

用户进行操作触发事件，通过http传递给服务器，服务器通过路由分给相应的controller，将数据传递给相应操作的model，model操作数据库结果返回给controller，controller再调用下一个流程的model，model操作数据库获取到数据，controller将数据传递给相应的view进行页面处理，通过http的响应将最终的页面传递到浏览器进行渲染

看图：模块，操作顺序，数据流向

dao --?dbc（数据库驱动）-- db

#### ⼀个典型的**Web MVC**流程

- Controller截获⽤用户发出的请求

- Controller调⽤用Model完成状态的读写操作

- Controller把数据传递给View

- View渲染最终结果并呈献给⽤用户

MVC是一个简化的模型，controller可以再分出一个业务层，model包含pojo（不包含逻辑的纯数据）和少量逻辑

<img src="Naixes阶段性学习笔记.assets/截屏2021-04-04 下午2.15.12.png" alt="截屏2021-04-04 下午2.15.12" style="zoom:50%;" />

req，res

一个http请求是一个事务，连接，请求，响应，关闭连接

### 实战

> 百度：帮助中心，高级搜索
>
> 谷歌：表达式搜索，高级搜索，指定网址搜索：yii site:*.csdn.net

1、配置好xampp环境

2、下载yii2 basic https://www.yiiframework.com/download

3、解压缩，放到web发布路路径下

4、修改config/web.php⽂文件，给 cookieValidationKey 配置项添加⼀一个密钥，内容随意，为了配置cookie

5、保证Yii安装⽬目录的访问权限`chmod -R xxx filename`，自己的代码不需要上传文件，就不需要写权限，使用gii需要写权限

6、通过浏览器器访问web路路径 /web/index.php打开yii应⽤用，可以看到主⻚页⾯面

1、配置数据库连接。修改 config/db.php 修改配置参数

```php
<?php

return [
    // yii自己封装的驱动，是一个类
    'class' => 'yii\db\Connection',
    // 连接串，数据库:host=主机名;dbname=数据库名称
    'dsn' => 'mysql:host=localhost;dbname=yii2basic',
    'username' => 'root',
    'password' => '',
    'charset' => 'utf8',

    // Schema cache options (for production environment)
    //'enableSchemaCache' => true,
    //'schemaCacheDuration' => 60,
    //'schemaCache' => 'cache',
];

```

创建数据库，字符集utf8mb4（支持扩展字符集）\_general（一般是语言通用语言）\_ci（大小写不敏感）

2、激活Gii模块。修改config/web.php，找到以下代码，并检查（basic默认激活）

```php
if (YII_ENV_DEV) {
    $config['bootstrap'][] = 'gii';
    $config['modules']['gii'] = [
        'class' => 'yii\gii\Module',
    ];
}
```

进入localhost/basic/web/index.php?r=gii

生成model，CRUD

## 测试题

24:00

```js
console.log({}+[]); // {}代码块，原始类型转换toPrimitive：[].valueOf().toString()，+"" // 0 ()变成表达式 // [object, Object] // [别名]
{}+[]; // 0
[]+{}; // 
{} + {}; // NaN，浏览器版本不一样，[object, Object][object, Object]
console.log([] == false) // true
console.log({} == false) // false
if([]){
	console.log([] == false) // 会执行
}
("b" + "a" + + "a" + “a").toLocaleLowerCase(); 0 == ”0” // banana + "a" // NaN
Boolean(”0”) == Boolean(0) // false // true == false
console.log(NaN == 0); // false
console.log(NaN <= 0); // false
console.log(null <= 0); // true，判断null不大于0所以为true，只有null这么比较 // < 0 false // ==0 false
console.log(1 + null);
var a ={value:1};
var b ={value:2};
console.log(a<=b); // true

var obj={};
var x = +obj.yideng?.name ?? '京程一灯';
console.log(x);

// 装箱：把值转换为对应的引用类型，new String()
// 拆箱：把引用类型转换为对应的值类型，toString
var yideng=“京程一灯”;
console.log(typeof yideng);
console.log(yideng instanceof String);

// 交替进行，js引擎对promise的优化，最多等待3个then，v8
Promise.resolve().then(() => {
	console.log(11);
})
.then(() => {
  console.log(12);
})
.then(() => {
  console.log(0);
  return Promise.resolve(5);
})
.then((r) => {
  console.log('🐻 ', r);
});
Promise.resolve()
.then(() => {
  console.log(1);
})
.then(() => {
	console.log(2);
})
.then(() => {
  console.log(3);
})
.then(() => {
	console.log(4);
})
.then(() => {
  console.log(6);
})
.then(() => {
	console.log(7);
})
.then(() => {
  console.log(8);
});

// 3

// 闭包进堆区不会被回收
// eval会放弃GC，但是编译快，webpack大量使用，可以在debugger中查看
// 优化：window.eval()
// new Function()也会放弃GC，koa-swig node mpa渲染的时候的模版引擎原理使用到
// with(){}也会放弃GC，vue模版使用
// try catch，e会延长作用域链，es10可以不写e，优化：new Error('xxx')

// 4

// 6
// es6-symbol

// 7
// 元编程，对js进行编程
```

## HTTP

### HTTP请求模型

两个动作：请求，响应，针对HTTP，HTTP无连接协议

两个端：客户端（依赖另外的机器或软件才能完成功能），服务端（等待请求的程序或者硬件），node都能写，可以同时存在即是客户端又是服务端

### 浏览器行为

<img src="Naixes阶段性学习笔记.assets/截屏2021-05-07 上午10.47.39.png" alt="截屏2021-05-07 上午10.47.39" style="zoom:50%;" />

处理流程: 

1、输入网址并回车，不会直接和服务器通信，要先保证道路畅通，做准备工作，检查是否能够联网，需要跨过一个设备（防火墙，路由器，网关等边界设备隔开了互联网和局域网）

2、解析域名，将字符串转化为ip地址（对于计算机来说字符串比ip地址复杂，ip本质是一个数字，不是简单的去掉点，对应int四个字节，运算性能高，因为位运算最快），通过DNS服务器（简单来说是一个键值对数据库）解析

3、浏览器发送HTTP请求，先建立TCP连接（传输层）再发请求（应用层），通过**路由技术**连接客户端和服务器，路由转发时会生成最优路径，经过路由最少或者延迟小

4、服务器处理请求，到达机房后由反向代理进行分发到对应服务器

5、服务器返回HTML响应，按照原路返回浏览器

6、浏览器处理HTML页面，浏览器解析

7、继续请求其他资源

8、浏览器渲染，看到页面

### HTTP协议

HTTP是超文本传输协议，从www浏览器传输到本地浏览器的一种传输协议，网站是基于HTTP协议的，例如网站的图片、CSS、JS等都是基于HTTP协议进行传输的。

HTTP协议是由从客户机到服务器的请求(Request)和从服务器到客户机的响应(response)进行约束和规范。

<img src="Naixes阶段性学习笔记.assets/截屏2021-04-09 上午11.02.29.png" alt="截屏2021-04-09 上午11.02.29" style="zoom:50%;" />

0.9：基本的语义和规则

1.0：基本成熟

1.1：非常成熟，比1.0多了长连接

2.0：改变了一些底层机制（TCP的实现上的修改），默认加密，分辨1和2：F12查看协议头带冒号的是伪头（协议的封装重新设计为了兼容添加的伪头）

#### TCP/IP协议栈

七层和四层（常见的五层区分数据链路层和物理层），栈：通信时协议栈逐层调用，类似于栈结构，程序只能调应用层

七层：ISO/OSI协议，国际标准化组织制定的协议建议性，五层协议是一个事实协议，老协议绝大多数是根据五层协议设计的，后来的协议大多按照七层来设计（HTTP3），五层实现起来简单一些但是不太严密，七层更加清晰灵活

<img src="Naixes阶段性学习笔记.assets/截屏2021-04-09 上午11.17.44.png" alt="截屏2021-04-09 上午11.17.44" style="zoom:50%;" />

**应用层**

为用户提供所需要的各种服务，软件可以直接使用，例如:HTTP、FTP、DNS、SMTP（发邮件），POP（收邮件），SSH等。

**传输层**

为应用层实体提供端到端的通信功能，保证数据包的顺序传送及数据的完整性。

该层定义了两个主要的协议: 

传输控制协议，TCP：有状态，面向连接，比较严密，表现在三次握手和四次挥手

用户数据报协议，UDP：对网络层的数据报协议（PING命令发的数据包就是ICMP数据包，使用了ICMP数据报协议。）的简单封装，不面向连接，不严密，只管发

QUIC是基于UDP封装，是HTTP3的底层协议，不需要建立连接也较严密可靠，适用于网络频繁切换的场景，比如高铁上频繁切换基站，面向未来的协议。

**网络层**

主要解决主机到主机的通信问题。**IP协议**是网际互联层最重要的协议。PING发的数据包就是ICMP数据包，使用了ICMP数据报协议。

计算机连接到局域网时先通过DHCP协议拿到IP地址，然后通过IP协议维持IP地址

**网络接口层**

负责监视数据在主机和网络之间的交换。5G

- 数据链路层，简单的封装，串口通信，比如连接打印机、USB，不是驱动

- 物理层，网卡，网线，光缆，无线电等硬件

##### 在TCP/IP的位置



<img src="Naixes阶段性学习笔记.assets/截屏2021-04-09 上午11.46.26.png" alt="截屏2021-04-09 上午11.46.26" style="zoom:50%;" />

目前普遍应用版本HTTPS，在HTTP加上了加密功能，基于HTTP1.1的HTTPS，TLS不是单独的一层是嵌入进去的

正在逐步向HTTP 2迁移，基于HTTP2及以后的HTTPS，TLS单独为一层

HTTP默认端口号为80，开发时用的

HTTPS默认端口号为443

#### 工作过程

一次HTTP操作称为一个**事务**，其工作过程可分为四步：（短链接1-2-3-4，长连接1-2-3-2-3-2-3-4，TCP连接是一个IO操作，耗时间资源）

1. 首先客户机与服务器需要建立TCP连接。只要单击某个超级链接，HTTP的工作开始。

2. 建立连接后，客户机发送一个请求给服务器，**请求方式的格式分为三部分**

**请求行：请求方法名、统一资源标识符(URI)、协议版本号**

**请求头：MIME信息包括请求修饰符、客户机信息**

空行

**请求体：可能的内容**

3. 服务器接到请求后，给予相应的响应信息，**其格式为三个部分**

**响应行（状态行）：包括信息的协议版本号、服务器发回的响应状态代码和状态代码的文本描述**

**响应头：MIME信息包括服务器信息**

**响应体：实体信息、可能的内容**。

4. 客户端接收服务器所返回的信息通过浏览器显示在用户的显示屏上，然后客户机与服务器**断开连接**。

如果在以上过程中的某一步出现错误，那么产生错误的信息将返回到客户端，有显示屏输出。对于用户来说，这些过程是由HTTP自己完成的，用户只要用鼠标点击，等待信息显示就可以了。

#### 请求与响应

HTTP请求组成:请求行、消息报头、请求正文。

回车换行：属于不可见字符的控制符，换行不同系统不一样，win：\n，linux：\r\n（历史遗留，老式的键盘打印机return归位 next向上滚动）

<img src="Naixes阶段性学习笔记.assets/截屏2021-04-09 下午12.10.51.png" alt="截屏2021-04-09 下午12.10.51" style="zoom:50%;" />

<img src="Naixes阶段性学习笔记.assets/截屏2021-04-09 下午12.11.42.png" alt="截屏2021-04-09 下午12.11.42" style="zoom:50%;" />

HTTP响应组成:状态行、消息报头、响应正文。

<img src="Naixes阶段性学习笔记.assets/截屏2021-04-09 下午12.12.06.png" alt="截屏2021-04-09 下午12.12.06" style="zoom:50%;" />

请求行组成:以一个方法符号开头，后面跟着请求的URI和协议的版本。

状态行组成:服务器HTTP协议的版本，服务器发回的响应状态代码和状态代码的文本描述。

##### 请求方法

GET: 请求获取Request-URI所标识的资源，参数长度有限制是由于浏览器和web服务对uri长度的限制，HTTP对GET/POST请求长度没有任何限制

POST: 在Request-URI所标识的资源后附加新的数据

HEAD: 请求获取由Request-URI所标识的资源的响应消息报头，一般用来探测

PUT: 请求服务器存储一个资源，不是数据记录（数据库），并用Request-URI作为其标识

DELETE: 请求服务器删除Request-URI所标识的资源

TRACE: 请求服务器回送收到的请求信息，主要用于测试或诊断，检测服务器是否能正常请求和响应。类似PING，ECHO（网络协议）

CONNECT: HTTP/1.1协议中预留给能够将连接改为管道方式的代理服务器。一般用在代理，代理服务器转发，HTTP代理

OPTIONS: 请求查询服务器的性能，或者查询与资源相关的选项和需求。预请求，mongodb，一般实现一些管理功能

在跨域情况下，浏览器在发起复杂请求前会主动发起options请求，预检请求获知服务器是否允许该跨域请求，允许之后才可以发起http请求

复杂请求：请求方法是GET，POST，HEAD以外，存在自定义请求头，Content-Type不属于text/plain，multipart/form-data，application/x-www-form-urlencoded

##### 状态码

状态代码有三位数字组成，第一个数字定义了响应的类别，且有五种可能取值: 

1xx:指示信息--表示请求已接收，继续处理，协议层面的异步

**2XX 成功**--表示请求已被成功接收、理解、接受 

- 200 OK，表示从客户端发来的请求在服务器端被正确处理
- 204 No content，表示请求成功，但响应报文不含实体的主体部分
- 205 Reset Content，表示请求成功，但响应报文不含实体的主体部分，但是与 204 响应不同在于要求请求方重置内容
- 206 Partial Content，进行范围请求

**3XX 重定向**--要完成请求必须进行更进一步的操作，301永久重定向，302临时重定向

- 301 moved permanently，永久性重定向，表示资源已被分配了新的 URL
- 302 found，临时性重定向，表示资源临时被分配了新的 URL
- 303 see other，表示资源存在着另一个 URL，应使用 GET 方法获取资源
- 304 not modified，表示服务器允许访问资源，但因发生请求未满足条件的情况
- 307 temporary redirect，临时重定向，和302含义类似，但是期望客户端保持请求方法不变向新的地址发出请求

**4XX 客户端错误**--请求有语法错误或请求无法实现，400实体发送错误，402协议层面的验证机制，404

- 400 bad request，请求报文存在语法错误
- 401 unauthorized，表示发送的请求需要有通过 HTTP 认证的认证信息
- 403 forbidden，表示对请求资源的访问被服务器拒绝
- 404 not found，表示在服务器上没有找到请求的资源

**5XX 服务器错误**--服务器未能实现合法的请求，502内部网关错误，500内部异常

- 500 internal sever error，表示服务器端在执行请求时发生了错误
- 501 Not Implemented，表示服务器不支持当前请求所需要的某个功能
- 503 service unavailable，表明服务器暂时处于超负载或正在停机维护，无法处理请求

##### 请求头

Accept，请求报头域用于指定客户端接受哪些类型的信息。eg:Accept:image/gif，Accept:text/ htmlAccept-Charset请求报头域用于指定客户端接受的字符集。

Accept-Encoding，请求报头域类似于Accept，但是它是用于指定可接受的内容编码。gzip，压缩返回内容，1.1头不压缩，压缩响应体

Accept-Language，请求报头域类似于Accept，但是它是用于指定一种自然语言。

Connection:keep-alive长连接

Cookie

Referer:来源。跨域，防盗链，反爬虫（效果不大，可伪造）等用到

Authorization请求报头域主要用于证明客户端有权查看某个资源。当浏览器访问一个页面时，如果收到服务器的响应代码为401(未授权)，可以发送一个包含Authorization请求报头域的请求，要求服务器对其进行验证。

Host请求报头域主要用于指定被请求资源的Internet主机和端口号，它通常从HTTP URL中提取出来的，发送请求时，该报头域是必需的。

User-Agent:请求报头域允许客户端将它的操作系统、浏览器和其它属性告诉服务器。浏览器和操作系统基本信息

##### 响应头

Connection:keep-alive长连接

Content-Encoding:gzip，对应Accept-Encoding

Cache-Control

Expires

Location响应报头域用于重定向接受者到一个新的位置。Location响应报头域常用在更换域名的时候。

Server响应报头域包含了服务器用来处理请求的软件信息。与User- Agent请求报头域是相对应的。

WWW-Authenticate响应报头域必须被包含在401(未授权的)响应消息中，客户端收到401响应消息时候，并发送Authorization报头域请求服 务器对其进行验证时，服务端响应报头就包含该报头域。

Content-Encoding实体报头域被用作媒体类型的修饰符，它的值指示了已经被应用到实体正文的 附加内容的编码，因而要获得Content-Type报头域中所引用的媒体类型，必须采用相应的解码 机制。

Content-Language实体报头域描述了资源所用的自然语言。

Content-Length实体报头域用于指明实体正文的长度，以字节方式存储的十进制数字来表示。

Content-Type实体报头域用语指明发送给接收者的实体正文的媒体类型。

Last-Modified实体报头域用于指示资源的最后修改日期和时间。

Expires实体报头域给出响应过期的日期和时间。

#### cookie和session

HTTP无状态，但他底层的TCP有状态，原因是HTTP工作过程中一次操作结束后会断开连接

切换网络时TCP会断开，但我们不会被踢下线因为他不是依靠TCP的状态维持身份

Cookies是**保存在客户端的小段文本**，随客户端点每发送一个请求该url下的所有cookies到服务器端。

Session则保存在服务器端，通过唯一的值sessionID来区别每一个用 户。SessionID随每个连接请求发送到服务器，服务器根据sessionID来识别客户端，再通过session的key获取session值。

存在安全漏洞：cookie设定权限，浏览器实现

cookie一般是服务器生成的通过Set-Cookie设置到浏览器，浏览器也可以生成，js提供api

与Cookie相关的HTTP扩展头 

1)Cookie:客户端将服务器设置的Cookie返回到服务器; 

2)Set-Cookie:服务器向客户端设置Cookie;

服务器第一次响应时产生一个session记录，在响应消息中用Set-Cookie头将session记录的id通过cookie回送给客户端，客户端在新的请求中将相同的内容携带在Cookie 头中发送给服务器，从而实现会话的保持。

安全性不高，使用token

#### HTTP缓存

缓存无处不在

IO操作消耗大，缓存提高效率，IO操作针对cpu，计算机的运算主要有两种一种cpu密集型，一种IO密集型

就近原则

缓存会根据请求保存输出内容的副本，例如html页面，图片，文件，当下一个请求来到的时候:如果是相同的URL，缓存直接使用副本响应访问请求，而不是向源服务器再次发送请求。

缓存的优点:

- 减少相应延迟

- 减少网络带宽消耗，带宽很贵

> 浏览器缓存是性能优化中简单高效的一种方式，按照缓存位置划分为以下几种类型：
>
> - service Worker
>
> - Memory Cache
>
> - Disk Cache
>
> - Push Cache
>
> 浏览器请求时，会按照如上的优先级顺序，进行查找缓存，都没有命中时，才会去请求网络。
>
> 面试过程中问到的浏览器缓存相关问题，一般是针对Disk Cache而言的，也就是硬盘缓存。
>
> 
>
> 如何复现出 `disk cache` 呢？
>
> 重新打开一个浏览器的tab栏，输入页面地址打开，这个时候就会看到 `disk cache` 了。原因是每个tab栏都会启动新的进程，所以就不会共享内存，也就不会命中`memory cache`了。
>
> 
>
> 浏览器缓存行为还有用户的行为有关
>
> | 用户操作     | Expires/Cache-Control | Expires/Cache-Control |
> | :----------- | :-------------------- | :-------------------- |
> | 地址栏回车   | 有效                  | 有效                  |
> | 页面链接跳转 | 有效                  | 有效                  |
> | 新开窗口     | 有效                  | 有效                  |
> | 前进、后退   | 有效                  | 有效                  |
> | F5刷新       | 无效                  | 有效                  |
> | Ctrl+F5刷新  | 无效                  | 无效                  |

HTTP缓存两大类：

**强制缓存与对比缓存**

- 强制缓存，服务器通知浏览器一个缓存时间，在缓存时间内，下次请求，直接用缓存，不在时间内，执行比较缓存策略。

- 比较缓存，将缓存信息中的Etag和Last-Modified通过请求发送给服务器，由 服务器校验，返回304状态码时，浏览器直接使用缓存。

  - Etag/If-None-Match策略，更加严密，优先，计算一次保存起来

  - Last-Modified/If-Modified-Since策略，时间戳不严密，可以改，并且根据文件移动

有时候浏览器会绕过Expires，不一定完全按照这个流程，看浏览器的具体实现，根据统计学推算强制缓存有效的概率

强制刷新会清空缓存

<img src="Naixes阶段性学习笔记.assets/截屏2021-04-09 下午4.15.00.png" alt="截屏2021-04-09 下午4.15.00" style="zoom:50%;" />

<img src="Naixes阶段性学习笔记.assets/截屏2021-04-09 下午4.15.24.png" alt="截屏2021-04-09 下午4.15.24" style="zoom:50%;" />



第一次请求没有缓存，服务器设置cache-control和expires或者etag和last-modified并返回资源

再次请求时，先检查强制缓存是否过期未过期不会发起请求直接从缓存中获取，状态为200

强缓存过期后进行协商缓存，依次发送文件上的etag/last-modified，头字段if-none-match/if-modified-since，服务器判断与自己维护的内容md5/时间戳是否相同，相同时使用浏览器缓存时返回304，否则说明资源变化返回最新数据状态200，然后重新进行缓存协商

#### 密码学

密码学的对象都是字符串和数字

散列是一种数据一旦转换为其他形式将永远无法恢复的技术。

> 本质上计算机中所有的数据都是数字表示的，二进制数据，为了方便处理又分成了二进制和数字形式（图片视频）
>
> md5不是加密是散列运算，不可逆无法恢复。加密是可逆，加密和解密
>
> 彩虹表破md5用的是碰撞，保存所有文件的md5进行查询对比，解决方法：加盐，防止拖库
>
> 拖库，下载整个数据库
>
> 数据库使用beta树（本质是二叉树）算法进行查询不会很慢

**加密**

- 对称加密(AES、DES、3DES)，密钥相同

- 非对称加密(RSA：商用/军用算法)，密钥不相同，频繁通信时运算量也还是挺大的

  加密：原文+密钥+算法 --> 密文

  解密：密文+密钥+算法 --> 原文

  公私钥，公钥加密，私钥解密，密钥长度决定加密强度，普遍1024位，16进制

概念区别编码，h265属于编码

<img src="Naixes阶段性学习笔记.assets/截屏2021-04-09 下午5.06.03.png" alt="截屏2021-04-09 下午5.06.03" style="zoom:50%;" />



密码学中加密算法只是其中一部分，还有一部分是保证密钥的安全性

**密钥交换算法**

Diffie-Hellman算法是一种著名的密钥协商算法，这种算法可以使得信息交换的双方通过公开的非安全的网络协商生成安全的共享密钥。

(1)Alice与Bob确定两个大素数n和g，这两个数不用保密（素数生成，依据椭圆算法；素数越大破解越难）

(2)Alice选择另一个大随机数x，并计算A如下:A=gx mod n 

(3)Alice将A发给Bob 

(4)Bob选择另一个大随机数y，并计算B如下:B=gy mod n（可能会被中间人C冒充，同时与AB建立连接，所以AB也不是保密的，只有随机数是保密的）

(5)Bob将B发给Alice

(6)计算秘密密钥K1如下:K1=Bx mod n 

(7)计算秘密密钥K2如下:K2=Ay mod n 

K1=K2，因此Alice和Bob可以用其进行加解密

#### 证书

进入HTTPS网站时会下载网站的证书和本地的根证书（操作系统或者浏览器安装时就存在了）进行比对。证书可以验证服务器的身份也可以用来验证客户端的身份（网银，U盾）

不直接使用根证书的私钥，而是使用二级证书

浏览器验证根证书，根据根证书验证二级证书，依次类推

##### 证书签发机构CA

通过CA发放的证书完成密钥的交换，实际上是利用非对称的加密算法完成数据加密密钥的安全交换，然后再利用数据加密密钥完成数据的安全交换。

数字证书:数字证书是互联网通信中标识双方身份信息的数字文件，由CA签发。

CA:CA(certification authority)是数字证书的签发机构。作为权威机构，其审核申请者身份后签发数字证书，这样我们只需要校验数字证书即可确定对方的真实身份。

**CA的工作流程**

1. 服务器 example.com将从CA**请求TLS证书**，例如 Digicert。

2. Digicert将为example.com**创建证书**，证书将包含必要的数据，例如服务器名称， 服务器的公钥等。给一个压缩包，.pem证书和cer私钥，配到nginx

3. Digicert将**创建数据（证书）的哈希值（散列），并使用自己（签发机构）的私钥对其进行加密（签名）**。 
4. 浏览器和操作系统自带Digicert等权威机构的公钥。mac钥匙串，系统根证书

5. 当浏览器收到签名证书时，它将使用**公钥从签名生成哈希值**，它还将使用证书中指定的**散列算法生成数据（证书）的散列**，如果两个哈希值匹配，则签名验证成功并且证书是可信的。

6. 现在浏览器可以使用证书中指定的example.com的公钥继续进行身份验证过程。 

在这里，我们可以将Digicert称为 Root CA.

**浏览器验证服务器证书**

证书颁发机构是为服务器创建并签署证书，即Digicert，Geotrust，Comodo等。如果他们正在为所有服务器签署证书，则必须为所有签名使用相同的私钥，如果它被盗，那么所有的信任都会丢失。为了解决这个问题并增加更多的平均信息量，引入了**中间CA**(intermediate CA)的概念。

服务器使用中级证书颁发机构的签名，因此，在与浏览器通信时，服务器将共享两个证书:

1、包含服务器的公钥，即实际的服务器证书;

2、由 Root CA 颁发的 intermediate CA 证书。

在签名验证期间，浏览器首先使用已经存储在浏览器中的**Root CA的公钥来验证中间证书的数字签名**，如果成功，浏览器现在可以信任中间证书及其公钥。现在**使用此公钥，浏览器将验证原始服务器证书的签名**，该组织可以注册为intermediate CA，以便为其域签署证书。

#### SSL/TLS协议

两套协议，TLS兼容SSL

<img src="Naixes阶段性学习笔记.assets/截屏2021-04-10 上午10.33.52.png" alt="截屏2021-04-10 上午10.33.52" style="zoom:50%;" />

**传输层安全性协议(Transport Layer Security - TLS)，及其前身安全套接层(Secure Sockets Layer - SSL)是一种安全协议**，目的是为互联网通信提供安全及数据完整性保障。

HTTPS协议的安全性由SSL协议实现，当前使用的TLS协议（包含了SSL协议） 1.2 版本**包含了四个核心子协议**:握手协议（TCP不能加密，TCP连接时握手之后进行加密连接握手进行加密协商，包含了密钥交换，保证链路安全）、密钥配置切换协议（加密协商，决定加密算法，由对称加密切换到不对称加密，握手时是对称加密）、应用数据协议（数据传输）及报警协议（安全性出现问题时，窃听或证书过期等）。

- TLS适用于对称密钥 
- 对称密钥可以通过安全密钥交换算法共享
- 如果请求被截获，密钥交换可能会被欺骗（躲不过中间人，a<->c<->b，不能保证绝对安全）
- 使用数字签名进行身份验证 
- 证书颁发机构和信任链。

HTTPS协议、SSL协议、TLS协议、握手协议的关系

- HTTPS是Hypertext Transfer Protocol over Secure Socket Layer的缩写，即HTTP over SSL，可理解为基于SSL的HTTP协议。HTTPS协议安全是由SSL协议实现的。

- SSL协议是一种记录协议，扩展性良好，可以很方便的添加子协议 握手协议是SSL协议的一个子协议。 TLS协议是SSL协议的后续版本，本文中涉及的SSL协议默认是TLS协议1.2版本。

#### 握手

TLS 握手的步骤:（TCP握手之后）

1、2协商加密算法，3-6需要证书情况下交换证书，7-9密钥交换，10-13切换到加密

1. ClientHello:客户端发送所支持的 SSL/TLS 最高**协议版本号**和所支持的**加密算法集合及压缩方法集合等信息**给服务器端。--客户端发起

2. ServerHello:服务器端收到客户端信息后，**选定双方都能够支持的 SSL/TLS 协议版本和加密方法及压缩方法**， 返回给客户端。--协商加密算法

3. SendCertificate**(可选)**:服务器端发送服务端证书给客户端。--**服务端发送证书**

4. RequestCertificate**(可选)**:如果选择双向验证，服务器端向客户端请求客户端证书。--服务端请求客户端发送证书（**HTTPS是单向验证，验证服务端**没有第4、6、8步，网银是双向）

5. ServerHelloDone:服务器端通知客户端初始协商结束。--**服务端通知协商结束**

6. ResponseCertificate**(可选)**:如果选择双向验证，客户端向服务器端发送客户端证书。--客户端发送证书

7. ClientKeyExchange:客户端使用服务器端的公钥，对客户端公钥和密钥种子（大随机数）进行加密，再发送给服务器端。--**客户端发送加密后的公钥和密钥种子**

8. CertificateVerify**(可选)**:如果选择双向验证，客户端用本地私钥生成数字签名，并发送给服务器端，让其通过收到的客户端公钥进行身份验证。--客户端计算并发送数字签名，用来验证第六步的证书

9. CreateSecretKey:通讯双方基于密钥种子等信息生成通讯密钥。--**双方计算密钥**
10. ChangeCipherSpec:客户端通知服务器端已将通讯方式切换到加密模式。--客户端通知切换加密
11. Finished:客户端做好加密通讯的准备。--客户端准备完成
12. ChangeCipherSpec:服务器端通知客户端已将通讯方式切换到加密模式。--服务端通知切换加密
13. Finished:服务器做好加密通讯的准备。--服务端准备完成
14. Encrypted/DecryptedData:双方使用客户端密钥，通过对称加密算法对通讯内容进行加密。 --**使用客户端密钥通信**
15. ClosedConnection:通讯结束后，任何一方发出断开 SSL 连接的消息。--**通信完成断开SSL，15后断开TCP**

<img src="Naixes阶段性学习笔记.assets/截屏2021-04-10 上午11.05.34.png" alt="截屏2021-04-10 上午11.05.34" style="zoom:50%;" />

### HTTP2

HTTP/2 没有改动 HTTP 的应用语义。 HTTP 方法、状态代码、URI 和标 头字段等核心概念一如往常。

HTTP/2 修改了数据格式化（分帧，改变了数据封装格式由文本到二进制）以及在客户端与服务器间传输的方式。这两点统帅全局，通过新的分帧层向我们的应用隐藏了所有复杂性。

由于HTTP/2 引入了一个新的二进制分帧层，该层无法与之前的 HTTP/ 1.x 服务器和客户端向后兼容，因此协议的主版本提升到 HTTP/2。

<img src="Naixes阶段性学习笔记.assets/截屏2021-04-10 下午2.07.42.png" alt="截屏2021-04-10 下午2.07.42" style="zoom:50%;" />

使用上差不多，区别在实现上，改变了数据的封装格式（二进制），更高效紧凑；引入分帧层；报头压缩；多路复用；服务器主动推送；默认加密

二进制分帧层：封装规则，层次分明，更加严密

**HTTP2的特点:** 

使用二进制格式传输，更高效、更紧凑。

 对报头压缩，降低开销。 

多路复用，一个网络连接实现并行请求。 

服务器主动推送，减少请求的延迟 默认使用加密。

默认加密

#### 二进制分帧层

HTTP/2 所有性能增强的核心在于新的二进制分帧层，它**定义了如何封装 HTTP 消息并在客户端与服务器之间传输**，是一个封装规则

这里所谓的“层”指的是位于套接字接口与应用可见的高级 HTTP API 之间一个经过优化的新编码机制。

HTTP/1.x 协议以换行符作为纯文本的分隔符，而 **HTTP/2 将所有传输的信息分割为更小的消息和帧，并采用二进制格式对它们编码**。

客户端和服务器会替我们完成必要的分帧工作。

<img src="Naixes阶段性学习笔记.assets/截屏2021-04-10 下午2.24.30.png" alt="截屏2021-04-10 下午2.24.30" style="zoom:50%;" />

#### 多路复用

在 HTTP/1.x 中，如果客户端要想发起多个并行请求以提升性能，则必须使用多个 TCP 连接。这种模型也会导致队首阻塞（文件阻塞，一个文件影响整体），从而造成底层 TCP 连接的效率低下。

**将 HTTP 消息分解为独立的帧，交错发送，然后在另一端重新组装是 HTTP 2 最重要的一项增强**。这个机制会在整个网络技术栈中引发一系列连锁反 应，从而带来巨大的性能提升。

- 并行交错地发送多个请求，请求之间互不影响。

- 并行交错地发送多个响应，响应之间互不干扰。 

- 使用一个连接并行发送多个请求和响应。 

- 不必再为绕过 HTTP/1.x 限制而做很多工作

- 消除不必要的延迟和提高现有网络容量的利用率，从而减少页面加载时间。

HTTP1阻塞是阻塞在了文件上，HTTP2没有完全解决，也可能会队首阻塞（阻塞到当前文件不会影响其他）。阻塞问题在TCP层面是不可避免的

HTTP3解决了阻塞问题

#### 服务器推送

HTTP/2 新增的另一个强大的新功能是，服务器可以对一个客户端请求发送多个响应。 换句话说，除了对最初请求的响应外，服务器还可以向客户端推送额外资源， 而无需客户端明确地请求。

HTTP/2 打破了严格的请求-响应语义，支持一对多和服务器发起的推送工作流服务器已经知道客户端下一步要请求什么资源，这时候服务器推送即可派上用场。

推送资源可以进行以下处理:

- 由客户端缓存
- 在不同页面之间重用
- 与其他资源一起复用
- 由服务器设定优先级
- 被客户端拒绝

#### 伪头

HTTP2由于封装格式改变，把请求行和请求头状态行和状态头全都封装到二进制帧了，使用伪头进行替代

伪头部字段是http2内置的几个特殊的以”:”开始的 key，用于替代HTTP/1.x中请求行/响应行中的信息，比如请求方法，响应状态码等

<img src="Naixes阶段性学习笔记.assets/截屏2021-04-10 下午2.56.30.png" alt="截屏2021-04-10 下午2.56.30" style="zoom:50%;" />

- :method 目标URL模式部分(请求) :scheme 目标URL模式部分(请求)
- :authority 目标RUL认证部分(请求)
- :path 目标URL的路径和查询部分(绝对路径 产生式和一个跟着"?"字符的查询产生式)。 (请求)
- :status 响应头中的HTTP状态码部分(响应)

### HTTP3

<img src="Naixes阶段性学习笔记.assets/截屏2021-04-10 下午2.57.36.png" alt="截屏2021-04-10 下午2.57.36" style="zoom:50%;" />

运行在 QUIC 之上的 HTTP 协议被称为 HTTP/3(HTTP-over-QUIC)

平邮UDP，打电话TCP，挂号信QUIC，对数据包加密不是链路加密，没有链路问题，属于会话层和安全层

QUIC 协议(Quick UDP Internet Connection)基于 UDP，正是看中了 UDP 的速度与效率。同时 QUIC 也整合了 TCP、TLS 和 HTTP/2 的优 点，并加以优化。

特点:

- 减少了握手的延迟(1-RTT 或 0-RTT 握手)

- 更加灵活的多路复用，并且没有 TCP 的阻塞问题

- 连接迁移(主要是在客户端)当由 Wifi 转移到 4G 时，连接不会被断开。

HTTP 3与HTTP 1.1和HTTP 2没有直接的关系，也不是http2的扩展

HTTP 3将会是一个全新的WEB协议

HTTP 3目前处于制订和测试阶段

#### 队首阻塞

<img src="Naixes阶段性学习笔记.assets/截屏2021-04-10 下午3.09.04.png" alt="截屏2021-04-10 下午3.09.04" style="zoom:50%;" />

HTTP/1.1 和 HTTP/2 都存在队头阻塞问题(Head of line blocking)

HTTP/1.1 的队头阻塞。一个 TCP 连接同时传输 10 个请求，其中第 1、2、3 个请求已被客户端接收，但第 4 个请求丢失，那么后面第 5 - 10 个请求都被阻塞，需要等第 4 个请求处理完毕才能被处理，这样 就浪费了带宽资源。

HTTP/2 的多路复用虽然可以解决“请求”这个粒度的阻塞，但 HTTP/2 的基础 TCP 协议本身却也存在着队头阻塞的问题。

由于 HTTP/2 必须使用 HTTPS，而 HTTPS 使用的 TLS 协议也存在队头阻塞问题，以文件为单位加密，传输时文件会被拆分，等整个文件传过来才解密，QUIC的加密和传输都是以包为单位

队头阻塞会导致 HTTP/2 在更容易丢包的弱网络环境下比 HTTP/1.1 更慢

那 QUIC 解决队头阻塞问题的的方法:

- QUIC 的传输单元是 Packet，加密单元也是 Packet，整个加密、 传输、解密都基于 Packet，这样就能避免 TLS 的队头阻塞问题;

- QUIC 基于 UDP，UDP 的数据包在接收端没有处理顺序，即使中间 丢失一个包，也不会阻塞整条连接，其他的资源会被正常处理。

### 反向代理

正向代理-代购，反向代理-门房

<img src="Naixes阶段性学习笔记.assets/截屏2021-04-10 下午3.19.14.png" alt="截屏2021-04-10 下午3.19.14" style="zoom:50%;" />

**用途**

加密和SSL加速：HTTPS一般配在nginx上，将加解密和业务分开，提高性能

负载均衡：将压力均衡的分摊到每个服务器。一个反向代理就是一个镜像

<img src="Naixes阶段性学习笔记.assets/截屏2021-04-10 下午3.19.48.png" alt="截屏2021-04-10 下午3.19.48" style="zoom:50%;" />

缓存静态内容

压缩

减速上传：限制上传速率，丢包或者拉长响应时间

安全：堡垒，进入内网先通过关口，争取时间

外网发布：整合不同端口的服务到80端口上

#### nginx

可以做web服务器，常用作反向代理，502bad gateway就是反向代理返回的，C语言写的

资料：nginx配置

安装到Linux上，mac容易端口冲突

yum安装

```cmd
rpm -Uvh http://nginx.org/packages/centos/7/noarch/RPMS/nginx-release-centos-7-0.el7.ngx.noarch.rpm
yum install -y nginx
```

配置文件：/etc/nginx/nginx.conf，注意备份

worker_processes：工作进程，nginx启动后会有管理进程（监视）和工作进程，生产环境按照核配，默认1

server虚拟服务配置，HTTPS配置：修改端口443 ssl或者80，证书和私钥放在当前目录或修改路径

http：

gzip on压缩

keepalive_timeout长连接超时时间

##### 反向代理配置

两种：不同端口代理，不同服务器转发

```cmd
# 组，一个组对应一个应用，多个应用配置多个组
# 客户端下游，代理到的地方上游，只配上游
upstream web_crm {
  # 反向代理，一行配置，要代理到的服务器ip和port
	server 127.0.0.1:8090;
}
server {
	...
	location 路径 {
		proxy_pass http://web_crm; # 请求转向 web_crm 定义的服务器列表
	}
	location 路径 {
	
	}
}
```

##### 负载均衡

把同样的程序部署到不同的服务器，nginx转发，可以设置权重

```cmd
# 组，一个组对应一个应用，多个应用配置多个组
upstream web_crm {
  # 负载均衡，所有的服务器ip和port
	server 127.0.0.1:8090 weight=1;
}
```

多种模式：

热备，两台，主用备用

轮询，均摊

加权轮询

ip_hash:nginx会让相同的客户端ip请求相同的服务器

##### 设置缓存



## node

开发模式

spa：单页，vue+vue-cli，假路由

mpa：多页，server render，真路由

spa+mpa：混合，node，BFF（Backend For Frontend）

同构：node+vue

场景（中间层）

BFF：分离前后端开发；FCP，FP，FID，LCP；node削减api无用字段；同构

高并发：低配置高IO，游戏中间层

### 异步IO

作用

- 前端通过异步IO可以消除UI堵塞。

- 假设请求资源A的时间为M,请求资源B的时间为N.那么同步的请求耗时为M+N.如果采用异步方式占用时间为Max(M,N)。

- 随着业务的复杂，会引入分布式系统，时间会线性的增加， M+N+...和Max(M,N...)，这会放大同步和异步之间的差异。

- I/O是昂贵的，分布式I/O是更昂贵的。 

- NodeJS 适用于IO密集型不适用CPU密集型

<img src="Naixes阶段性学习笔记.assets/截屏2021-04-10 下午6.33.31.png" alt="截屏2021-04-10 下午6.33.31" style="zoom:50%;" />

> CPU时钟周期:1/cpu主频 -> 1s/3.1 GHz
>
> 异步和同步没有绝对的好坏
>
> QPS：每秒请求数,就是说服务器在一秒的时间内处理了多少个请求。
>
> 操作系统对计算机进行了抽象，将所有输入输出设备抽象为文件。内核在进行文件**I/O**操作时，通过文件描述符进行管理。应用程序如果需要进行**IO**需要打开文件描述符， 再进行文件和数据的读写。异步**IO**不带数据直接返回，要获取数据还需要通过文件描述符再次读取。
>
> 不要耗尽文件描述符，采取一些手段线程池等重用文件连接

<img src="Naixes阶段性学习笔记.assets/截屏2021-04-10 下午8.47.10.png" alt="截屏2021-04-10 下午8.47.10" style="zoom:50%;" />

#### **node对异步IO的实现**

完美的异步IO应该是应该是应用程序发起非阻塞调用，无需通过遍历或者事件轮询。

<img src="Naixes阶段性学习笔记.assets/截屏2021-04-10 下午8.57.03.png" alt="截屏2021-04-10 下午8.57.03" style="zoom:50%;" />

根据上图，Node.js的运行机制如下：

1. 写的JavaScript脚本会交给V8引擎解析
2. 解析后的代码，调用Node API，Node会交给 [Libuv库](https://link.juejin.im/?target=https%3A%2F%2Fgithub.com%2Fjoyent%2Flibuv) 处理
3. [Libuv库](https://link.juejin.im/?target=https%3A%2F%2Fgithub.com%2Fjoyent%2Flibuv) 将不同的任务分配给不同的线程（操作系统，网络，处理器等），形成一个Event Loop（事件循环），其他线程执行完任务后，会进行通知将任务的执行结果返回给V8引擎
4. V8引擎再将结果返回给用户

LIBUV：负责管理通知

<img src="Naixes阶段性学习笔记.assets/截屏2021-04-10 下午9.12.19.png" alt="截屏2021-04-10 下午9.12.19" style="zoom:50%;" />

linux：custom threadpool，轮询

windows：IOCP，通知

#### 特殊API

1.SetTimeout和SetInterval 线程池不参与

2.process.nextTick() 实现类似 SetTimeout(function(){},0);每次调用放入队列中， 在下一轮循环中取出。

3.setImmediate();比process.nextTick()优先级低 

执行顺序取决于观察者

<img src="Naixes阶段性学习笔记.assets/截屏2021-04-10 下午9.31.57.png" alt="截屏2021-04-10 下午9.31.57" style="zoom:50%;" />

```js
setTimeout(function () {
	console.log(1)
}, 0)
setImmediate(function () {
	console.log(2)
})
process.nextTick(() => {
	console.log(3)
})
new Promise((resovle,reject)=>
	console.log(4)
  resovle(4)
}).then(function()
  console.log(5)
})
console.log(6) // 463512
// ===============================
function foo() { 
  console.log(Math.random())
	foo()
}
foo()
// 爆栈
// ===============================
function foo() { 
 	console.log(Math.random()
	return Promise.resolve().then(foo
}
foo()
// 卡死
// ===============================
function foo() { 
  console.log(Math.random())
	setTimeout(foo, 0)
}
foo()
// 可以执行
```

4.Node如何实现一个Sleep?

```js
async function test() { 
  console.log('Hello') 
  await sleep(1000) 
  console.log('world!')
}
function sleep(ms) {
	return new Promise(resolve => setTimeout(resolve, ms)) }
test()
 
```

#### Await V8原理

#### 函数式编程在node的应用

1.高阶函数:可以将函数作为输入或者返回值，形成一种后续传递风格的结果接受方式，而非单一的返回值形式。 后续传递风格的程序将函数业务重点从返回值传递到回调函数中。

```js
app.use(function(){
  //todo
})
var emitter = new events.EventEmitter; 
emitter.on(function(){
  //..........todo
})
```

2.偏函数:指定部分参数产生一个新的定制函数的形式就 是偏函数。Node中异步编程非常常见，我们通过哨兵变量会很容易造成业务的混乱。underscore，after变量

> 哨兵变量 

**常用的node控制异步手段**

1.早期，Step、wind(提供等待的异步库)、Bigpipe、Q.js 

2.Async、Await

3.Promise/Defferred是一种先执行异步调用，延迟传递的处理方式。Promise是高级接口，事件是低级接口。低级接口可以构建更多复杂的场景，高级接口一旦定义，不太容易变化，不再有低级接口的灵活性，但对于解决问题非常有效

4.由于Node基于V8的原因，目前还不支持协程。协程不是进程或线程，其执行过程更类似于子例程，或者说不带返回值的函数调用。

一个程序可以包含多个协程，可以对比与一个进程包含多个线程，因而下面我们来比较协程和线程。我们知道多个线程相对独立，有自己的上下文，切换受系统控制;而协程也相对独立，有自己的上下文，但是其切换由自己控制，由当前协程切换到其他协程由当前协程来控制。generator

### 内存管理与优化

#### V8垃圾回收机制

Node使用JavaScript在服务端操作大内存对象受到了一定的限制 (堆区)，64位系统下约为1.4GB，栈区32位操作系统下是0.7G. 新生代64位是32M 32位是16M

node —max-new-space-size app.js: 

-max-old-space-size app.js 

Process.memoryUsage->rss、heaptTotal、heapUsed

##### 新生代老生代

V8的垃圾回收策略主要基于分代式垃圾回收机制。在自动垃圾回收的演变过程中，人们发现没有一种垃圾回收算法能够胜任所有场景。V8中内存分为**新生代和老生代**两代。新生代为存活时间较短对象，老生代中为存活时间较长的对象。

目前 V8 采用了两个垃圾回收器，主垃圾回收器 -Major GC (主要负责老生代的垃圾回收。)和副垃圾回收器 -Minor GC (Scavenger主要负责新生代的垃圾回收)V8 之所以使用了两个垃圾回收器，主要是受到了代际假说的影响。

> 代际假说：
>
> 第一个是大部分对象都是“朝生夕死”的。形容 有些变量存活时间很短。
>
> 第二个是不死的对象，会活得更久，比如全局 的 window、DOM、Web API 等对象。

##### 新生代Scavenge算法

在分代基础上，新生代的对象主要通过Scavenge算法进行垃圾回收，再具体实现时主要采用Cheney算法。

**Cheney算法**是一种采用复制的方式实现的垃圾回收算法。它将内存 一分为二，每一个空间称为semispace。这两个semispace中 一个处于使用，一个处于闲置。处于使用的称之为From, 闲置的称之为To.分配对象时先分配到From,当开始进行垃圾回收时，检查From存活对象赋值到To非存活被释放。 然后互换位置。再次进行回收，发现被回收过直接晋升， 或者发现To空间已经使用了超过25%。他的缺点是只能使用堆内存的一半，这是一个典型的空间换时间的办法，但是新生代声明周期较短，恰恰就适合这个算法。

##### 老生代Mark-Sweep & Mark-compact

V8老生代主要采用Mark-Sweep和Mark-compact，再使用Scavenge不合适，对象较多需要赋值量太大而且还是没能解决空间问题。Mark-Sweep是标记清除，标记那些死亡的对象，然后清除。但是清除过后出现内存不连续的情况，所以我们要使用Mark-compact，他是基于Mark-Sweep演变而来的，他先将活着的对象移到一边，移动完成后，直接清理边界外的内存。当CPU空间不足的时候会非常的高效。 

V8后续还引入了延迟处理，增量处理，并计划引入并行标记处理。

<img src="Naixes阶段性学习笔记.assets/截屏2021-04-11 上午9.18.43.png" alt="截屏2021-04-11 上午9.18.43" style="zoom:50%;" />

> 时间分片
>
> 人眼30-60fps 16.7ms 有剩余时间时v8开始GC 增量并行
>
> 两种情况下回收：当前帧有空闲，爆了强行触发GC

V8垃圾回收：Orinoco递归标记（V8）+Oilpan（Chrome）

垃圾回收是通过 GC Root(全局的 window 对象(位于 每个 iframe 中)、文档 DOM 树、存放栈上变量) 标记空间中活动对象和非活动对象。从 GC Roots 对 象出发，遍历 GC Root 中的所有对象，能遍历到的对象，该对象是可访问的(reachable)，那么必须保证这些对象应该在内存中保留，也称可访问的对象为活动对象;通过 GC Roots 没有遍历到的对象， 则是不可访问的(unreachable)，那么这些不可访问的对象就可能被回收，称不可访问的对象为非活动对象。

<img src="Naixes阶段性学习笔记.assets/截屏2021-04-11 上午9.24.10.png" alt="截屏2021-04-11 上午9.24.10" style="zoom:50%;" />

1 主线程停下来进行GC 叫全停顿(Stop-The-World)为了解决全停顿带来的卡顿。V8内部还有并行、并发、增量等垃圾回收技术。

2 并行回收，在执行一个完整的垃圾回收过程中，垃圾回收器会使用多个辅助线程来并行执行垃圾回收。增量式垃圾回收，垃圾回收器将标记工作分解为更小的块，并且穿插在主线程不同的任务之间执行。并发回收，回收线程在执行 JavaScript 的过程，辅助线程能够在后台完成的执行垃圾回收的操作。

<img src="Naixes阶段性学习笔记.assets/截屏2021-04-11 上午9.35.14.png" alt="截屏2021-04-11 上午9.35.14" style="zoom:50%;" />

<img src="Naixes阶段性学习笔记.assets/截屏2021-04-11 上午9.35.43.png" alt="截屏2021-04-11 上午9.35.43" style="zoom:50%;" />

Chrome在16.6ms的内无法完成所有工作那就没有空闲时间，但内存垃圾还是会积 累。当垃圾达到阈值就会开始进行GC，占用主线程。

V8创建了一个不透明的数据类型，称为**句柄**，它使Chrome浏览器可以在不了解数据结构的情况下操纵V8堆对象。 只要Chrome保持句柄的引用，V8的垃圾收集器就不会对该对象进行回收。

##### 标记执行

<img src="Naixes阶段性学习笔记.assets/截屏2021-04-11 上午9.37.56.png" alt="截屏2021-04-11 上午9.37.56" style="zoom:50%;" />

1.  V8提出了**三色标记法**。黑色和白色，还额外引入了灰色。黑色表示这个节点被 GC Root 引用到了，而且该节点的子节点都已经标记完成了。白色表示这个节点没有被访问到，如果在本轮遍历结束时还是白色，那 么这块数据就会被收回。

2.  灰色表示这个节点被 GC Root 引用到，但子节点还没被垃圾回收器标记处理，也表明目前正在处理这个节点;为啥会有灰?window.a ={};window.a.b ={}; window.a.b.c={};图2扫完一遍以后，window.a.b = [];导致b切开 了，但是d确实闲置。增量垃圾回收器添加了一个约束条件:不能让黑色节点指向白色节点。**写屏障 (Write- barrier) 机制，写屏障机制会强制将被引用的白色节点变成灰色的**，这样就保证了黑色节点不能指向白色节 点的约束条件。这个方法也被称为**强三色不变性**。因为在标记结束时的所有白色对象，对于垃圾回收器来 说，都是不可到达的，可以安全释放。在 V8 中，每次执行如 window.a.b = value的写操作之后，V8 会插入写屏障代码，强制将 value 这块内存标记为灰色。

##### 常见内存泄漏

Case1:无限制增长的数组 

Case2:无限制设置属性和值

Case3:任何模块内的私有变量和方法均是永驻 内存的 a = null

Case4: 大循环，无GC机会

内存泄漏分析

```cmd
node-inspector
console.log("Server PID", process.pid);
sudo node --inspect app.js
while true;do curl "http://localhost:1337/"; done
top -pid 2322
```

### 大规模node站点结构原理

#### 架构

MVC，NET多层架构，Java多层架构

##### **NET多层架构**

WebService对外服务

website静态资源服务

website.sln解决方案

websiteTest单元测试

App_data数据存放

BLL业务层，WebService和website调用，BLL找DALFactory

WebControllers渲染WebService和website，WebControllers找BLL

IDAL接口层

SQLServerDAL业务实现层，找Model和DBUtility

DALFactory靠反射将IDAL和SQLServerDAL合并，DALFactory找DataCache

DataCache缓存层

DLLibrary公共服务

Model

DBUtility数据层

<img src="Naixes阶段性学习笔记.assets/截屏2021-04-11 上午10.19.28.png" alt="截屏2021-04-11 上午10.19.28" style="zoom:30%;" />



<img src="Naixes阶段性学习笔记.assets/截屏2021-04-11 上午10.19.49.png" alt="截屏2021-04-11 上午10.19.49" style="zoom:50%;" />



##### JavaWeb多层架构

IOC（控制反转Inversion of Control）

>  NEST.js：node版spring

action路由层，找dao

ocmmon

po业务实体类，相当于model

dao数据库接口，结合了po和service

<img src="Naixes阶段性学习笔记.assets/截屏2021-04-11 上午10.29.15.png" alt="截屏2021-04-11 上午10.29.15" style="zoom:30%;" />

po+dao提供给service：service不主动引用dao，而是dao注入，action和service同理（和MVC的区别）

<img src="Naixes阶段性学习笔记.assets/截屏2021-04-11 上午10.48.06.png" alt="截屏2021-04-11 上午10.48.06" style="zoom:50%;" />

#### node集群应用

##### 预备上线

前端工程化的搭载动态文件的MAP分析压缩打 包合并至CDN

单测、压测 性能分析工具发现Bug 

编写nginx-conf实现负载均衡和反向代理 

PM2启动应用程序小流量灰度上线，修复BUG

##### 多线程

Master进程均为主进程，Fork可以创造主从进程。

通过child_process可以和NET模块组合，可以创建多个线程并监 听统一端口。通过句柄传递完成自动重启、发射自杀信号、 限量重启、负载均衡。

Node默认的机制是采用操作系统的抢占式策略。闲着的进程争 抢任务，但是会造成CPU闲置的IO暂时并未闲置。Node后来引 入了Round-Robin机制，也叫轮叫调度。主进程接受任务，在发

每个子进程做好自己的事，然后通过进程间通信来将他们连 接起来。这符合Unix的设计理念，每个进程只做一件事，并做 好。将复杂分解为简单，将简单组合成强大。

```js
var cluster = require('cluster');
var http = require('http');
var numCPUs = require('os').cpus().length;
if (cluster.isMaster) { 
  require('os').cpus().forEach(function(){
		cluster.fork(); 
  });
	cluster.on('exit', function(worker, code, signal) { 
    console.log('worker ' + worker.process.pid + ' died');
	});
	cluster.on('listening', function(worker, address) {
		console.log("A worker with #"+worker.id+" is now connected to " + address.address +
":" + address.port); 
  });
} else { 
  http.createServer(function(req, res) {
		res.writeHead(200);
		res.end("hello world\n");
		console.log('Worker #' + cluster.worker.id + ' make a response');
}).listen(8000); }
```

##### pm2

本机负载，进程守护，cluster、fork两种模式

pm2 是一个带有负载均衡功能的Node应用的进程管理器. 当你要把你的独立代码利用全部的服务器上的所有CPU，并保证进程永远都活 着，0秒的重载。

 1.内建负载均衡(使用Node cluster 集群模块)

 2.后台运行

 3.0秒停机重载

 4.具有Ubuntu和CentOS 的启动脚本

 5.停止不稳定的进程(避免无限循环)

 6.控制台检测

 7.提供 HTTP API

 8.远程控制和实时的接口API ( Nodejs 模块,允许和PM2进程管理器交互 )

测试过Nodejs v0.11 v0.10 v0.8版本，兼容CoffeeScript,基于Linux 和MacOS.

##### 服务器集群

<img src="Naixes阶段性学习笔记.assets/截屏2021-04-11 上午10.58.58.png" alt="截屏2021-04-11 上午10.58.58" style="zoom:50%;" />

nagios网络监控，nginx负载均衡，varnish/stupid缓存层

<img src="Naixes阶段性学习笔记.assets/截屏2021-04-10 下午9.12.19.png" alt="截屏2021-04-10 下午9.12.19" style="zoom:50%;" />

项目案例

MVC

<img src="Naixes阶段性学习笔记.assets/截屏2021-04-11 上午11.25.43.png" alt="截屏2021-04-11 上午11.25.43" style="zoom:50%;" />

经典代码

```js
router.get(/^\/(\d+)_(\d+)/, cModel.A,cModel.B,cModel.C);

var shaObj = new jsSHA(string, 'TEXT'); 
var hash = shaObj.getHash('SHA-1', 'HEX');

var forPound = req.headers['x-forwarded-for-pound'];

callback(new Error('Fail to parse http response to json, url:' + reqOptions.url + '), res, body);
                   
require(‘./middleware’)(app);
         
async( await ctx.render(‘index.html’));
```

### BFF

中间层：内容裁剪，天然支持跨域，ssr

文件结构

koa

环境区分

开发代码监听nodemon（supervisor较老），线上使用pm2

路由@koa/router

- 初始化
- api路由
- 渲染页面路由，koa-swig+co

静态资源：koa-static

真假路由：koa2-connect-history-api-fallback

容错处理

区分不支持es6的浏览器，用babel编译systmejs加载

> 模版冲突：swig配置项varControls: ['[[', ']]']
>
> npm i @babel/plugin-transform-modules-systemjs @babel/cli @babel/core -D

日志：log4js，日志时间，日志级别（ALL，TRACE，DEBUG，INFO，WARN，ERROR，FATAL，MARK，OFF），日志分类，保存到文件

ES6模块化语法修改，@babel/node+@babel/preset-env，开发环境代码运行之前进行转码或者后缀使用mj，snode12后支持或者package.json添加`"type": "module"`

model层

axios封装，容错

封装函数式库

- 阅读源码：lodash，underscore
- 参考

e2e测试

playWright+chai

rize pupteer

接口测试

mocha+supertest

> 工具：tree-cli，生成文件结构
>
> tree -L 2 -o README.md

#### webComponents

YouTube使用

框架：x-tag，polymerjs，omi

#### 前后端分离

库：scripty，使用sh文件管理命令

```json
// 修改前：
  "scripts": {
    "dev": "NODE_ENV=development nodemon --exec babel-node ./app.js",
    "build": "babel ./assets/js/testData.js -o ./assets/js/testData-bundle.js",
    "test:e2e": "node tests/e2e.test.js",
    "test:api": "mocha --file ./tests/api.test.js"
  },
// 修改后
  "scripts": {
    "client:dev": "scripty",
    "client:prod": "scripty",
    "server:dev": "scripty",
    "server:prod": "scripty",
    "test:e2e": "scripty",
    "test:api": "scripty",
    "dev": "NODE_ENV=development nodemon --exec babel-node ./app.js",
    "start": "pm2",
    "test": "",
    "build": "npm run client:prod & npm run server:prod",
    "build-systemjs": "babel ./assets/js/testData.js -o ./assets/js/testData-bundle.js"
  },
```

集群编译

钩子：

```json
    "demo": "echo helleo",
    "predemo": "predemo"
```

npm-run-all

jscpd：代码重复率检查

.jscpd.json

```json
{
  "threshold": 0,
  "reporters": ["html", "console"]
}
// 命令：jscpd './demo/test.js'
```

文件夹分离

mpa，服务器渲染多页面

webpack，多入口

```js
// webpack.config.js基本配置
module.exports = {
    entry: "",
    output: "",
    module: ""
}
```

区分打包环境：

库，yargs，处理命令参数

webpack-merge，合并配置文件

glob，多入口文件处理

babel：babel-loader

模版语法不能引入css和js，需要webpack处理

html-webpack-plugin：打包html并注入资源

多页面配置，解决引用多余js文件和js资源注入位置错误，抽离共通的runtime

```js
const {argv} = require('yargs')
const {merge} = require('webpack-merge')
// 文件匹配
const glob = require('glob')
const path = require('path')
const HtmlWebpackPlugin = require('html-webpack-plugin')

// 页面模板处理
const HtmlAfterPlugin =  require('./build/HtmlAfterPlugin')
// console.log(argv);

const mode = argv.mode || 'development'
const envConfig = require(`./build/webpack.${mode}.js`)
// 返回文件路径的数组
const files = glob.sync('./src/web/views/**/*.entry.js')
const entries = {}

// 多页面注入配置
const htmlPlugins = []

files.forEach(path => {
    if(/([a-zA-Z]+-[a-zA-Z]+)\.entry\.js/.test(path)) {
        const entryKey = RegExp.$1
        entries[entryKey] = path
        const [pagename, template] = entryKey.split('-')
        htmlPlugins.push(
            new HtmlWebpackPlugin({
                // 路径以output路径为准
                // 导出文件路径
                filename: `../views/${pagename}/pages/${template}.html`,
                // 模版路径
                template: `./src/web/views/${pagename}/pages/${template}.html`,
                // 引入的模块
                chunks: [entryKey],
                // 取消注入功能，用自定义插件HtmlWebpackPlugin替代
                inject: false
            })
        )
    }
})

const basicConfig = {
    mode,
    // 多入口
    entry: entries,
    // 压缩
    optimization: {
        // 抽离出公共部分
        runtimeChunk: 'single'
    },
    module: {
        rules: [
            {
                test: /\.js$/,
                use: ['babel-loader']
            }
        ]
    },
    plugins: [
        ...htmlPlugins,
        //  注意顺序，HtmlAfterPlugin是基于HtmlWebpackPlugin做的拦截
        new HtmlAfterPlugin()
    ],
    resolve: {
        alias: {
            "@": path.resolve('./src/web')
        }
    }
}

module.exports = merge(basicConfig, envConfig)
```

自定义插件解决js资源注入位置错误

```js
const HtmlWebpackPlugin = require("html-webpack-plugin");

const pluginName = 'HtmlAfterPlugin';

// 生成script标签
const assetHelp = (data) => {
  let js = []
  for(let item of data.js) {
    js.push(`<script src=${item}></script>`)
  }
  return {js}
}

class HtmlAfterPlugin {
  constructor() {
    this.jsArr = []
  }
  // compiler：相当于webpack的核心，挂载了很多东西
  apply(compiler) {
    // compilation：每个chunk都会生成一个
    compiler.hooks.compilation.tap(pluginName, (compilation) => {
        // HtmlWebpackPlugin提供的钩子
        HtmlWebpackPlugin.getHooks(compilation).beforeAssetTagGeneration.tapAsync(
          "HtmlAfterPlugin", // <-- Set a meaningful name here for stacktraces
          (data, cb) => {
            // 获取需要替换的js
            const {js} = assetHelp(data.assets)
            this.jsArr = js

            // Tell webpack to move on
            cb(null, data)
          }
        )
        HtmlWebpackPlugin.getHooks(compilation).beforeEmit.tapAsync(
          "HtmlAfterPlugin", // <-- Set a meaningful name here for stacktraces
          (data, cb) => {
            // 替换<!-- injectjs -->
            let _html = data.html
            _html = _html.replace('<!-- injectjs -->', this.jsArr.join(''))
            // 替换@layouts和@components
            _html = _html.replace(/@layouts/g, '../../layouts')
            _html = _html.replace(/@components/g, '../../../components')

            data.html = _html

            // Tell webpack to move on
            cb(null, data)
          }
        )
    });
  }
}

module.exports = HtmlAfterPlugin;
```

gulp代码打包清洗

> prepack，清洗比较极致

```js
const gulp = require('gulp')
const watch = require('gulp-watch')
const babel = require('gulp-babel')
const plumber = require('gulp-plumber')
const rollup = require('gulp-rollup')
const replace = require('@rollup/plugin-replace')

// 入口
const entry = "./src/server/**/*.js";
const cleanEntry = "./src/server/config/index.js";

// 开发环境
function buildDev() {
    // watch：出错后会马上停止，用gulp-plumber
    return watch(entry,{
        ignoreInitial: false
    }, () => {
        gulp.src(entry)
        .pipe(plumber())
        .pipe(
            babel({
                babelrc: false,
                // 将es6转换为commonjs
                "plugins": ["@babel/plugin-transform-modules-commonjs"]
            })
        )
        // 打包
        .pipe(gulp.dest('dist'))
    })
}

// 生产环境
function buildProd() {
    return gulp.src(entry)
        .pipe(
            babel({
                babelrc: false,
                ignore: [cleanEntry],
                // 将es6转换为commonjs
                "plugins": ["@babel/plugin-transform-modules-commonjs"]
            })
        )
        // 打包
        .pipe(gulp.dest('dist'))
}

// 流清洗
function buildConfig() {
    return gulp.src(entry)
        .pipe(rollup({
            input: cleanEntry,
            // 将es6转换为commonjs
            output: {
                format: 'cjs'
            },
            plugins: [
                // 删除多余配置
                replace({
                    'process.env.NODE_ENV': JSON.stringify('production')
                })
            ]
        }))
        // 打包
        .pipe(gulp.dest('dist'))
}

let build = gulp.series(buildDev)
 
if(process.env.NODE_ENV === 'production') {
    // 默认串行
    build = build.series(buildProd, buildConfig)
}

gulp.task('default', build)
```

## 测试题



top level await，webpack4可以写

tc39规范

while(true)：webworker或Concurrentt.thread

写屏蔽：

对象修改属性不会影响原型链-隐式

如果Object.defineProperty创建的原型链但是被标记为只读就无法创建写屏蔽，vue的双向绑定就是object.defaineProperty，所以不能直接改

如果原型链式存在set修改时也会执行

## 工程化

### Linux基础

#### 进程、线程、协程

属于操作系统的内容

**程序**是静态的，进程是动态的，一般说的关闭程序指的是进程，类似于类与实例。

**进程**执行在cpu和内存中。执行一个程序时，操作系统从硬盘上把程序的文件读到内存中，操作系统找到程序的执行入口，把其中的指令交给cpu去执行。单cpu单核cpu执行时不会一直跑一个程序的代码，操作系统要对cpu的时间进行调度，感觉上是并行执行，并发，实际上是在很小的时间间隔进行切换。

操作系统将cpu的时间分为时间片，非平均，按照优先级，抢占模式。写大循环/死循环时，会被分配较多的时间所以会卡，应该定期休眠，减少当前程序的时间，让出cpu。

操作系统也要分配内存资源，当程序到内存中时分配内存，执行时分配更大的内存。

内存管理：js带gc，带gc的程序是程序自己管理内存的。操作系统执行时会把操作系统自己放到内存中，叫做引导过程，一般它在内存中的位置是固定的，接下来引导程序会跳转到内核在内存的起始位置，内核开始执行，其他程序执行时会分配剩余的内存。不带gc的程序执行时向操作系统申请内存，不需要时要还给操作系统。带gc的程序启动时会被分配较大的内存，多余的内存作为程序自己的堆，自己管理，即gc维护。

进程代表cpu所能处理的单个任务，好比工程的车间，线程就像车间的工人，协作完成同一个任务。一个进程可以包含多个线程，进程内内存共享，所有线程都可以使用，但不能同时使用，此时的内存管理方法有互斥锁（mutex，一个锁一个钥匙）和信号量（semaphore，一个锁多把钥匙）

线程的容器，资源分配调度的最小单位，程序是指令数据，数据及其组织形式的描述，进程是程序的实体

进程是在操作系统中运行的基本单位，现在的操作系统多为多用户多任务，多任务指同时并发执行多个进程。

进程中的内存是逻辑内存是相互独立的

进程之间通过TCP/IP的端口实现

**文件/网络句柄**是进程共有的

**PC（program counter程序计数器）**操作系统真正运行的是线程，PC指向当前的指令，指令在内存中，每个线程都有一个自己的指针，指向当前所在内存

**TLS（thread local storage）**线程的独立内存，存储线程独有数据

**线程**是比进程更小的单位，进程直接受到操作系统直接管理创建维护，线程由操作系统调度，线程必须依附在进程上，线程代码是进程代码的一部分，创建线程需要调用操作系统的api，就是说线程也是由操作系统创建出来的，也由操作系统调度，但由进程进行管理。进程中至少有一个线程，进程结束时线程也会结束。

系统进行运算调度的最小单位，是进程中的实际运作单元，一条线程指进程中的一个单一顺序的控制流

早期的linux不提供线程的创建由第三方库提供，后来被纳入到linux中。

简单来说：

进程指系统运行的一个应用程序，是资源分配的最小单位

线程是系统分配处理器时间单元的基本单位，或者是程序执行的最小单位

线程可以创建撤销其他线程

**协程**是比线程更小的单位，也叫管程，微线程，纤程。协程是用户态的轻量级线程，进程和线程是内核态的调度单位。操作系统不能对协程进行调度，所以协程无法使用多核资源。

程序启动后跑的是程序自己的代码，叫用户态，当通过api调用内核功能，就进入到了内核态。

**发展**：早期实现并发，是父进程创建子进程由子进程进行处理，多一个连接就创建一个进程，即将调度任务交给操作系统。如果存在大量的连接，就会占用大量的资源，每个进程的管理都需要一定的资源（操作系统管理每个进程需要给每个进程附加一些数据），父进程创建子进程会完全复制父进程的数据（fork模式） ------> 线程是更加轻量级的解决方案，线程创建时也会复制代码和数据，但是线程可以从主线程共享进程中的一些代码和数据，占用的资源会少一些，多核的cpu也可以处理这些线程 ------> 进程和线程都需要操作系统调度，多了总会受到拖累，协程之间的切换没有进程和线程切换开销（操作系统的开销），即cpu时间，切换的时间什么事情都不能做，要保存当前状态，恢复切换的进程或线程的状态。操作系统的开销在cpu的内部，cpu内部有寄存器和缓存，切换时要复制寄存器中所有的状态到缓存或者内存中。协程的开销是程序中的变量，改的是内存中的状态，具体在cpu中是寄存器的状态，不需要复制，更快更轻量，但无法利用多核资源。，无法利用多核资源。

> nginx的配置中的worker_processes工作进程为1时，实际上能看到两个进程，另一个是主进程，用来监控子进程，杀死必须杀死主进程，否则主进程会不断重启子进程
>
> **多cpu服务器**，主板上有多个cpu，cpu通信协调贵，操作系统只能运行在一个cpu，操作系统可以把不同的程序分配到不同的cpu
>
> **多核cpu**，一个cpu中有多个核心，核也需要协调通信，cpu内部有专有的电路，和主板协调不同主板协调还需要芯片，减少成本。操作系统只能运行在一个核，操作系统可以把不同的程序分配到不同的核，类似于负载均衡
>
> 多核cpu之前有一个**超线程**技术，在一个核通过优化指令操作的流水线模拟多核，可以提高效率，伪多核。结合多核看起来可以翻倍
>
> cpu是通用型芯片，什么事都能干工艺复杂但不专，cpu运算分整数和浮点运算（还有矢量运算向量运算等）
>
> gpu是专用型芯片，只做浮点运算。并行处理单元
>
> 显卡有上千个核，更多的处理单元
>
> 阿姆（音译），用于移动设备，主核，俩个副核，多个小核，低功耗

程序分计算型和IO型（针对cpu和外设的输入输出），IO操作慢cpu计算多个数量级。任务分IO密集型和cpu密集型，服务器算是IO密集（读写网络），追求高并发，高实施，高可用（稳定），浏览器算cpu密集

现在的服务器一般多种手段

nginx：多进程+事件驱动

nodejs：多进程+多线程+事件驱动，js在主线程，其他工作线程执行api，事件驱动机制进行线程切换

操作系统的设计，可以归结为三点:

1、以多进程形式，允许多个任务同时运行;

2、以多线程形式，允许单个任务分成不同的部分运行;

3、提供协调机制，一方面防止进程之间和线程之间产生冲突，另一方面允许进程之间和 线程之间共享资源。

上半部分的内容都是在内存里，除了寄存器在cpu里，使用cpu时，保存的变量地址指令都是保存在寄存器中，当进程不占用cpu时寄存器的状态会被复制到内存

程序不能直接操作文件，程序调用操作系统的文件子系统api进行读写，操作文件时维护一个文件操作句柄（数字，背后维护一个数据结构），打开时生成。

linux所用的东西都看成文件，包括设备

栈是函数调用栈

fork模式创建进程时，会复制内存中的内容

多线程进程的代码数据文件是共享的

<img src="Naixes阶段性学习笔记.assets/截屏2021-04-21 上午10.58.36.png" alt="截屏2021-04-21 上午10.58.36" style="zoom:50%;" />

- 进程的目的就是担当分配系统资源(CPU时间、内存)的实体
- 线程是操作系统能够进行运算调度的最小单位
- 协程是一种用户态的轻量级线程，无法利用多核资源。
- IO（主要是网卡和存储器，存储器指外存）密集型应用的发展: 多进程->多线程->事件驱动->协程
- CPU密集型应用的发展:多进程->多线程
- 调度和切换的时间:进程 > 线程 > 协程

> https://mp.weixin.qq.com/s/PRQGyFKqFym5ncJcyVnZPw

#### 免密登录

原理：

使用ssh协议，ssh使用ssl协议作为加密会话层

ssh前身是telnet

telnet（不加密的远程连接，早期用来电话线连电脑）+ssl=ssh

服务器验证客户端，先创建加密连接，输入密码，免密使用公私钥

主要用在自动上传和自动下载，比如工程化的自动发布/部署

**配置免密登陆的步骤**

客户端发起请求

服务端找到对应公钥，做加密连接（私钥匹配）

1、生成秘钥对
 ssh-keygen -t rsa -C "你自己的名字" -f "你自己的名字_rsa" // t-算法 C-会出现在密钥中 f-文件名，不设密钥密码

2、上传配置公钥
上传公钥到服务器对应账号的home路径下的.ssh/中 ( ssh-copy-id -i "公钥文件路径" 用户名@服务器ip或域名 ) 配置公钥文件访问权限为 600

3、配置本地私钥把第一步生成的私钥复制到你的home目录下的.ssh/ 路径下 配置你的私钥文件访问权限为 600 chmod 600 你的私钥文件名

4、免密登陆功能的本地配置文件

编辑自己home目录的.ssh/ 路径下的config文件，配置config文件的访问权限为 644。单主机配置和多主机配置

```cmd
# 多主机配置
Host gateway-produce
HostName IP或绑定的域名
Port 22
Host node-produce
HostName IP或绑定的域名
Port 22
Host java-produce
HostName IP或绑定的域名
Port 22

Host *-produce
User root
IdentityFile ~/.ssh/produce_key_rsa
Protocol 2
Compression yes
ServerAliveInterval 60
ServerAliveCountMax 20
LogLevel INFO

#单主机配置
Host evil-cloud
User root
HostName IP或绑定的域名
IdentityFile ~/.ssh/evilboy_rsa
# 协议版本
Protocol 2
# 维护长连接
Compression yes
ServerAliveInterval 60
ServerAliveCountMax 20
# 消息等级
LogLevel INFO

#单主机配置
Host git.yideng.site
User git
IdentityFile ~/.ssh/evilboy_rsa
Protocol 2
Compression yes
ServerAliveInterval 60
ServerAliveCountMax 20
LogLevel INFO

```

#### 进程管理:pm2源码分析

PM2 是 node 进程管理工具，可以利用它来简化很多node应用管理的繁琐任务，如性能监控、自动重启、负载 均衡等，而且使用非常简单。



2、pm2 官网 https://pm2.io/

3、pm2 源码下载 https://github.com/Unitech/pm2

4、pm2 源码中能学到些什么

找到入口，API类

- Linux 进程管理的方法
  - 父进程创建子进程
- Linux 创建进程的两种方式：fork 与 exec 父子进程的管理机制
  - fork：复制自身
  - exec：在程序中执行另一个程序
- 父子进程的管理机制

demo：

```js
// worker：服务器
var http = require('http');
http.createServer(function(req, res) {
  res.writeHead(200);
  res.end("hello world\n");
}).listen(8000);

// master：pm2，fork
// 管理进程
var cluster = require('cluster');
// cpu数，4核超线程，8cpu，9个进程，一个主进程fork出8个
var numCPUs = require('os').cpus().length;
 
if (cluster.isMaster) {
  // 主进程代码
  console.log(numCPUs);
  for (var i = 0; i < numCPUs; i++) {
    // fork会把自身内存空间复制一份，但是重新执行
    // 每循环一次出一个子进程，和主进程代码一样，状态不一样执行的代码不一样
    var worker = cluster.fork();
  }
} else {
  // 子进程代码
  // 实例化worker
  // 子进程共享句柄，端口号不会冲突
  // 实际执行时访问的哪个子进程由
  require("./app.js");
}
```

### 持续集成

提交代码 -> CI拦截：重复率，语法校验 -> code RV -> CI防护 -> CI测试 -> Sonar/Eslint/htmllint/csslint（cssNano） -> 构建（gulp，webpack，swc-底层esbuild、swc-loader，rome，rollup，vite/snowpack-microbundle，parcel） -> 缺陷管理（trello，jira，ambition） -> 容器（docker，dockerfile，web容器-nginx/caddy快速构建应用） -> 文档管理（tsDoc，showDoc，markdown） -> cli核心

cli核心

- eDEX-UI
- Commanderjs
  - vorpal
- 终端图表
  - ervy
  - blessed
- shelljs
- inquirerjs
  - enquirer
  - prompts
- hotel，手动重启线上服务
- react-cli

CD

机器：

本机服务器

gitlab/svn机器

CI/CD机器

开发/测试机

svn开发阶段

trunk

branch

tags

模块化：微前端，UMD，SDK

cli

### Sonar-质量管理

## 前端性能优化与工程化

<img src="Naixes阶段性学习笔记.assets/截屏2021-05-07 上午10.47.39.png" alt="截屏2021-05-07 上午10.47.39" style="zoom:50%;" />

http请求和响应流程

### navigation timing

现代浏览器内部处理流程w3c，用来分析性能，有一套api在MDN可以查看

参考：

W3c.github.io/navigation-timing/

w3.org/TR/navigation-timing

<img src="Naixes阶段性学习笔记.assets/截屏2021-05-07 上午10.48.27.png" alt="截屏2021-05-07 上午10.48.27" style="zoom:50%;" />

输入url回车：

--- 提示卸载（卸载前一个页面） 

--- 重定向（包含本地重定向和http缓存协商后的重定向（获取缓存））&unload（瓶颈位置，事件内的一些处理，耗时，回收资源，发送请求，释放内存等） 

--- App cache（读取缓存即读文件，io操作，可能会发生瓶颈的位置，memory cache是谷歌浏览器对disk cache的优化，频繁读取的不是很大的资源会被缓存在内存，第一次请求本地没有缓存跳过重定向这两步）

- 浏览器处理步骤
- 标签用来计时
- 两个位置可能会发生瓶颈

--- DNS（瓶颈位置，传输层协议是UDP，使用CDN优化） 

--- TCP（瓶颈位置，受网络质量影响） 

--- req（没有requestEnd是因为不好界定，浏览器拿不到，请求时间过长说明服务器的响应时间太长）

> 授时服务，会在返回的时间上加上请求发出到的到响应之间的时间除以2来保证尽量的精确，但不一定精确，使用无线电比较精确

--- res（缓存协商，本地资源有效时又回到本地重定向，响应时间太长说明数据太大或者链路不好，可以压缩或者架设镜像服务器）

- 主要是网络操作

--- processing（主要是处理dom的过程，流转成文本，转成dom，处理dom，domLoading转化/domInteractive处理/domContentLoaded加载/domComplete完成，其他因素，嵌入js，css） 

--- onload（触发onLoad事件，loadEventStart/loadEventEnd）

- 后面两步是浏览器步骤
- 流转成文本，转成dom在内存中

> Spa加载时间更加复杂，目的是隐藏加载时间，是一种多任务策略，不占用等待时间在后台加载

### DNS

DNS 是Domain Name System, 域名系统，用于将域名转换为IP。 

顶级域名，.com .net .org，baidu.com二级域名，www.baidu.com二级域名

域名资源记录

| 记录类型                                           | 含义                                                         |
| -------------------------------------------------- | ------------------------------------------------------------ |
| SOA:(StartOf Authority, 起始授权记录)              | ⼀个区域解析库有且只能有一个SOA记录，⽽且必须放在第⼀条，域名供应商设置 |
| A记录(IPv4主机记录) A -- ip                        | 用于名称解析的重要记录，将特定的主机名映射到对应主机的IP地址上 |
| CNAME记录(别名记录) B -- A 内部跳转 解析出来还是ip | ⽤于返回另⼀个域名，即当前查询的域名是另一个域名的跳转， 主要用于域名的内部跳转，为服务器配置提供灵活性 |
| NS记录(域名服务器记录)                             | 用于返回保存下一级域名信息的服务器地址。该记录只能设置为域名，不能设置为IP地 址。 |
| MX(邮件记录)                                       | 用于返回接收电子邮件的服务器地址                             |
| IPv6主机记录(AAAA记录)                             | 与A记录对应，用于将特定的主机名映射到一个主机的IPv6地址。    |

域名服务器

内置，路由器中转，拨号时ppp服务器（连接服务器）会下发DNS服务器到路由器，路由器收到后进行设置，也可以手动设置，路由器将请求转发到DNS服务器，查找缓存，无缓存从根服务器开始

域名解析

2优化，缓存常用域名/数据库镜像

**解析过程**

域名很多为了加快解析，分到了多个服务器，不同等级的域名归不同的服务器管（分治），分根服务器，TLD服务器，名称服务器（负责一级域名以后的），客户端路由器收到DNS解析请求以后会把域名发到DNS服务器（路由器内置，经过路由器中转到DNS服务器），DNS服务器有一个缓存，先查看有没有缓存，没有的话先从根服务器处理顶级域名（全球有13个），查到以给定顶级域名结尾的一级域名归哪个TLD服务器，返回这个服务器ip给DNS服务器，DNS再给TLD服务器发送第二个请求，返回名称服务器ip，DNS再发送第三次请求，名称服务器会找到最终的ip返回。由于通信较多所以没有用TCP

其中的优化包括，DNS的缓存，还有大数据库的镜像，减少通讯，阿里云等买到域名设置好了ip之后会有一个提示，十分钟之内同步，就是将解析记录主动同步到镜像

<img src="Naixes阶段性学习笔记.assets/截屏2021-05-07 下午2.59.53.png" alt="截屏2021-05-07 下午2.59.53" style="zoom:50%;" />

### UDP

用户数据报协议，传输层，不会对报文进行操作

特点：

面向无连接：只加一个标识

有单播多播广播功能

面向报文：保留报文边界

不可靠：不保证收到，没有拥堵控制

高效：头部开销小，传输高效，8字节TCP20-60字节

对比TCP：

提供高效传输，不强调数据完整性时使用，比如音视频，DNS交换等

TCP提供可靠传输，需要数据完整，传输可控可靠时使用，比如文件传输，远程登录

### TCP

传输控制协议，传输层

特点：

面向连接：需要三次握手

支持单播传输：不支持多播和广播

面向字节流：不保留报文边界的情况下以字节流的方式进行传输

可靠传输：建立可靠连接，靠顺序号和应答号确保数据传送的可靠河顺序

提供拥塞控制：网络出现堵塞时，可以减小数据注入的速率和数量

提供双全工通信

#### 三次握手



<img src="Naixes阶段性学习笔记.assets/截屏2021-05-07 下午3.30.53.png" alt="截屏2021-05-07 下午3.30.53" style="zoom:50%;" />



<img src="Naixes阶段性学习笔记.assets/截屏2021-05-07 下午3.31.33.png" alt="截屏2021-05-07 下午3.31.33" style="zoom:50%;" />

TCP协议头：

源端口号，接收方端口号，各两个字节

发送方顺序号

应答号和对方的顺序号，必须连续，否则说明丢包了

...前面20个字节是固定的

后面是可变数据

<img src="Naixes阶段性学习笔记.assets/截屏2021-05-07 下午3.31.54.png" alt="截屏2021-05-07 下午3.31.54" style="zoom:50%;" />

**三次握手**

不包含数据

客户端发起连接请求，SYN指令，顺序号seq=x

服务端响应握手包发送SYN指令，顺序号seq=y，应答号ACK=x+1，客户端收到应答号，客户端能确认服务器能收到自己的数据，达到半连接，半连接不能保证服务器能收到客户端的数据

> TCP是全双工
>
> 单工：广播
>
> 半双工：对讲机
>
> 全双工：电话
>
> 两次握手：如果客户端不断发起连接请求，服务端需要维护的连接数据越来越多（因为服务器还需要遍历数组，维护连接超时，数据过多时服务器会拒绝服务，缩短超时时间可以缓解但是不能解决问题，比如DDOS分布式拒绝服务攻击，也叫分布式洪水攻击，解决：防火墙，堆硬件），这是拒绝服务攻击的一种，半连接攻击

客户端发送应答号ACK=y+1，服务器收到应答号，服务端能确认客户端能收到自己的数据，达到全连接

三次交互保证对方可以正确得接收自己的数据

**四次挥手**

一般是客户端发起断开

收到断开请求后马上返回，然后做收尾工作，最后再发送断开请求，所以响应和FIN请求分成两次发送

客户端发送FIN指令，顺序号seq=x+2，应答号ACK=y+1

服务器立刻响应，应答号ACK=x+3

服务器做完收尾工作后发送FIN指令，顺序号seq=y+1

客户端收到后响应，应答号ACK=y+2，至此连接断开



<img src="Naixes阶段性学习笔记.assets/截屏2021-05-07 下午3.32.13.png" alt="截屏2021-05-07 下午3.32.13" style="zoom:50%;" />



#### TCP滑动窗口（D324）

TCP的可靠传输是在传输层上完成的，但是发送报文等待确认确认后再发送下一个报文的效率非常低下，滑动窗口是为了解决这个问题

滑动窗口允许发送方连续发送多个报文，根据对方接受窗口大小限制发送方的发送速率，防止拥堵

本质是维护了几个变量，同时在发出或收到报文时对这几个变量进行维护

TCP是双全工，双方都包含了发送窗口和接收窗口

- 发送窗口，N，nextSeq，N+size

接收时N = ack，N + size = win

发送时移动nextSeq，发多少移动多少

- 接收窗口，J1，J2，J3

发送时ack = J2，J1移动到J2，Win = J3 - J2

接收时，顺序没出错时移动到J2，否则不移动，接下来发送的ack = J2

### CDN

解决问题：分散所有客户端请求同一个服务器的数据请求压力，使用镜像服务器，依赖DNS使用就近原则解析到最近的镜像，比如每个区域解析到的ip不是同一个，取决于网络环境

<img src="Naixes阶段性学习笔记.assets/截屏2021-05-07 下午3.24.59.png" alt="截屏2021-05-07 下午3.24.59" style="zoom:50%;" />

## 现代浏览器渲染过程

### 进化

- 1990年，蒂姆·伯纳斯·李开发了第一个网页浏览器WorldWideWeb，后改名为Nexus。WorldWideWeb浏览器支持早期的HTML标记 语言，功能比较简单，只能支持文本、简单的样式表、电影、声音、图片等资源的显示。

- 1993年，马克·安德森领导的团开发了一个真正有影响力的浏览器Mosaic，这就是后来世界上最流行的浏览器Netscape Navigator。

- 1995年，微软推出了闻名于世的浏览器Internet Explorer。**第一次浏览器大战开始**，持续两年
- 1998年，Netscape公司开放Netscape Navigator源代码，成立了Mozilla基金会。**第二次浏览器大战开始，持续八年** 
- 2003年，苹果公司发布了Safari浏览器。
- 2004年，Netscape公司发布了著名的开源浏览器Mozilla Firefox 2005年，苹果公司开源了浏览器中的核心代码，基于此发起了一个新的开源项目WebKit(Safari浏览器的内核)。

- 2008年， Google公司已WebKit为内核，创建了一个新的浏览器项目Chromium。以Chromium为基础，谷歌发布了Chrome浏览器。 至于这两者的关系，可以简单地理解为:Chromium为实验版，具有众多新特性;Chrome为稳定版。
  - Google现在的内核是blink是webkit的分支，走逐步替代的路线，从核心部分和V8
  - webkit分为两部分，处理html和css的部分和js引擎
  - V8用来替代js引擎

### 现代浏览器

现代浏览器特征，火狐先驱

- 网络
- 资源管理，从服务器下载下来的资源
- 网页浏览
- 多页面管理
- 插件和扩展
- 账户和同步
- 安全机制，跨域
- 开发者工具

现代浏览器结构

- 用户界面(User Interface)

- 浏览器引擎(Browser Engine)，是渲染引擎的高级接口

- 渲染引擎(Rendering Engine)，web core

- 网络(Networking)

- XML解析器(XML Parser)

- 显示后端(Display Backend)，给界面提供服务，单纯的html，字体支持

- 数据持久层(Data Persistence)，以文件的形式保存数据

<img src="Naixes阶段性学习笔记.assets/截屏2021-05-09 上午10.59.31.png" alt="截屏2021-05-09 上午10.59.31" style="zoom:50%;" />



### 渲染引擎

渲染引擎:能够能够将HTML/CSS/JavaScript文本及相应的资源文件转换成图像结果。 渲染引擎的种类:

| 渲染引擎           | 浏览器                           |
| ------------------ | -------------------------------- |
| Trident            | IE、Edge(旧)                     |
| Gecko              | Firefox                          |
| WebKit             | Safari                           |
| Blink(WebKit fork) | Chromium/Chrome，Opera，Edge(新) |

#### 结构与工作流程

以HTML/JavaScript/CSS等文件作为输入，以可视化内容作为输出

<img src="Naixes阶段性学习笔记.assets/截屏2021-05-09 上午11.17.20.png" alt="截屏2021-05-09 上午11.17.20" style="zoom:50%;" />

html文本 - dom树，结构化，使用html解析器

渲染树，基于css和dom树

布局树，计算位置

绘制渲染树，绘制像素点

<img src="Naixes阶段性学习笔记.assets/截屏2021-05-09 上午11.34.38.png" alt="截屏2021-05-09 上午11.34.38" style="zoom:50%;" />

具体就是浏览器获取到html后，先进行字节流解码把字节数据转换为字符，包括一些字符的预处理，然后通过词法分析将字符串转化为标记同时生成dom树

遇到css时解析css，结构化css，不是树结构，是按照一定的数据结构生成css片段，在dom树上找到对应的节点，与css片段进行关联匹配，生成渲染树

如果遇到js，html解析器会暂停工作，将js给js解释器解析，js可以以桥接机制影响dom树和渲染树，js解析完成后html解析器继续工作

在渲染树的基础上加上布局规则一层一层得叠加生成布局渲染树，就是一个排版的过程

最后绘制，调用显示后端，控件，字体，图形库，视频解码库等，计算像素点，将需要显示的内容（视口）映射（将数据转换成图片再通过显卡）到显示器上，一张图片就是一帧，刷新率就是一秒钟显示多少帧图片（目前最低50）

参与的模块：

html解析器

css解析器，先分解成css片段，再基于dom树生成渲染树，基于css以一定的数据结构描述渲染规则，将css渲染规则与dom树进行关联

js解释器（js core/v8），可以操作dom节点，可以调整页面样式，dom上的事件可以调用js引擎

> html解析器和js解释器不能并发执行，js一般往后放
>
> html和js操作dom的机制不同，html直接操作，js桥接操作

#### WebKit

WebKit 官网:https://webkit.org/

Blink 是未来 

Blink官方文档:http://www.chromium.org/blink

<img src="Naixes阶段性学习笔记.assets/截屏2021-05-09 上午10.07.53.png" alt="截屏2021-05-09 上午10.07.53" style="zoom:50%;" />

**webkit包括：**

webkit embedding api，浏览器引擎

web core，渲染引擎，核心

js core/v8，js引擎，核心

platform api

### Chrome 架构

开先河：将单进程模式扩展为多进程模式

单个进程：一个页面崩溃浏览器崩溃

- Browser:控制程序的“chrome”部分，包括地址栏，书签，后退和前进按钮。还处理Web浏览器的不可见的，和特权部分，例如网络请求和文件访问。

- Renderer:负责显示网站的选项卡内的所有内容。

- Plugin:控制网站使用的所有插件，例如flash。

- GPU:独立于其他进程的GPU处理任务。 它被 分成多个不同的进程，因为GPU处理来自多个程序的请求并将它们绘制在同一个面中。

<img src="Naixes阶段性学习笔记.assets/截屏2021-05-09 下午1.20.10.png" alt="截屏2021-05-09 下午1.20.10" style="zoom:50%;" />

浏览器进程（主进程），有多个线程，界面线程，数据持久化线程，网络线程

**渲染器进程（多个，子进程，属于webcore）**，一个进程负责一个域，一个页面崩溃同域页面崩溃。有性能问题，吃内存，但是现在硬件发展，不算大问题，Chrome也在不断优化，尽量节省内存，比如v8在64指针中放两个32指针，足够用。主线程（生成dom树），工作线程（多个，运行js，多个页面有         多个js解释器实例，web worker，service worker，每一个worker都是独立的js引擎的实例，不和页面js在一起防止争抢），排版线程，预渲染线程

<img src="Naixes阶段性学习笔记.assets/截屏2021-05-09 下午1.36.49.png" alt="截屏2021-05-09 下午1.36.49" style="zoom:50%;" />

- 渲染器进程负责选项卡内发生的所有事情。 在渲染器进程中，主线程处理你为用户编写的大部分代码。
- 如果你使用了web worker 或 service worker， 有时JavaScript代码的一部分将由工作线程处理。 排版和栅格线程也在渲染器进程内运行，以便高效、流畅地呈现页面。

> Web Workers：通过使用Web Workers，Web应用程序可以在独立于主线程的后台线程中，运行一个脚本操作。这样做的好处是可以在独立线程中执行费时的处理任务，从而允许主线程（通常是UI线程）不会因此被阻塞/放慢。
>
> pwa用到Web Worker
>
> ServiceWorker API 的[ ServiceWorker接口](https://developer.mozilla.org/en-US/docs/Web/API/ServiceWorker_API) 提供一个对一个服务工作者的引用。 多个浏览上下文（例如页面，工作者等）可以与相同的服务工作者相关联，每个都通过唯一的ServiceWorker对象。相当于用js写浏览器的后台

工具进程

GPU进程，绘制

插件进程（多个），不用的插件禁用或删除

> 浏览器可以查看任务管理器，查看进程

#### 渲染过程

**解析部分**

<img src="Naixes阶段性学习笔记.assets/截屏2021-05-09 下午1.48.19.png" alt="截屏2021-05-09 下午1.48.19" style="zoom:50%;" />

获取资源 - html解析（根据html结构生成dom树）

<img src="Naixes阶段性学习笔记.assets/截屏2021-05-09 下午1.48.34.png" alt="截屏2021-05-09 下午1.48.34" style="zoom:50%;" />

处理css生成数据结构 - 匹配关联dom树（生成渲染树）

<img src="Naixes阶段性学习笔记.assets/截屏2021-05-09 下午1.49.15.png" alt="截屏2021-05-09 下午1.49.15" style="zoom:50%;" />

计算位置排版，就是计算每个节点的大小坐标和相对位置，基于根节点计算（生成排版树）

- 构建DOM

- 子资源加载
  - 注意JavaScript可以阻止解析

- 提示浏览器如何加载资源

- 样式表计算
- 布局

- 绘制

注意：前端性能优化重点就是这部分

**合成部分**

把文档的结构、元素的样式、几何形状和绘制顺序转换为屏幕上的像素称为光栅化。

合成是一种将页面的各个部分分层，分别栅格化，并在一个被称为合成器线程的独立线程中合成为页面的技术。

<img src="Naixes阶段性学习笔记.assets/截屏2021-05-09 下午1.55.56.png" alt="截屏2021-05-09 下午1.55.56" style="zoom:50%;" />

生成渲染树

**GPU渲染**

一旦创建了层树并确定了绘制顺序，主线程就会将该信息提交给合成器线程。 合成器线程然后栅格化每个图层。 一个图层可能像页面的整个长度一样大，因此合成器线程会将它们分成图块，并将每个图块发送到光栅线程。 栅格线程栅格化每一个tile并将它们存储在GPU内存中。

通过IPC将合成器帧提交给浏览器进程。这时可以从UI线程添加另 一个合成器帧以用于浏览器UI更改，或者从其他渲染器进程添加扩充数据。 这些合成器帧被发送到GPU用来在屏幕上显示。 如果发生滚动事件，合成器线程会创建另一个合成器帧并发送到GPU。

合成的好处是它可以在不涉及主线程的情况下完成。 合成线程不需要等待样式计算或 JavaScript 执行。 这就是合成动画是平滑性能的最佳选择的原因。 如果需要再次计算布局或绘图，则必须涉及主线程。

<img src="Naixes阶段性学习笔记.assets/截屏2021-05-09 下午1.59.57.png" alt="截屏2021-05-09 下午1.59.57" style="zoom:50%;" />

> GPU（浮点处理器）是众核处理器，每个核都比较简单，因为GPU只负责浮点运算，是一种专用CPU，每个核都有一个浮点运算的单元，做并行运算。
>
> CPU（中央处理器）也能做浮点运算，但是能做浮点运算的单元少
>
> DirectX，win一个图形库，游戏引擎，除了图形，还有声音等
>
> openGL，开放的图形库，工业标准库，只负责图形，C语言写的
>
> webGL，封装的openGL

最终的渲染工作由GPU生成图，根据层树一个点一个点计算的，这里有一个优化，整个渲染会被GPU分解成若干个小工作，如图，一个小片就是一个tile（瓦）交给一个GPU核，算完后集中到显卡的显存上，显存把显存上的数据翻到显示器，数据结构很简单，一维，按照屏幕左上角依次排列，这个过程很快，取决于刷新率

<img src="Naixes阶段性学习笔记.assets/截屏2021-05-09 下午2.00.23.png" alt="截屏2021-05-09 下午2.00.23" style="zoom:50%;" />

> Open GL，工业标准库，开放的图形库

## 前端架构与性能优化

### 基础

#### 雅⻁军规

https://www.cnblogs.com/xianyulaodi/p/5755079.html

https://www.jianshu.com/p/4cbcd202a591

##### 页面加载方面

- 减少HTTP请求数

合并文件，合并图片，base64图片

- 减少DNS查找次数

DNS预解析，很多浏览器进行了优化即使不设置此属性，也能自动在后台进行预解析 。

```html
< meta  http-equiv="x-dns-prefetch-control" content="on">
< link  rel="dns-prefetch" href="//www.zhix.net">
< link  rel="dns-prefetch" href="//api.share.zhix.net">
< link  rel="dns-prefetch" href="//bdimg.share.zhix.net">
// 禁止隐式的 DNS Prefetch
< meta  http-equiv="x-dns-prefetch-control" content="off">
```

默认情况下浏览器会对页面中和当前域名（正在浏览网页的域名）不在同一个域的域名进行预获取，并且缓存结果，这就是隐式的 DNS Prefetch。如果想对页面中没有出现的域进行预获取，那么就要使用显示的 DNS Prefetch 了。

- 避免重定向

- 可缓存的ajax

使用etag和expires等浏览器缓存，gzip压缩

- 延迟加载组件

- 预加载组件

**preload**

```html
<link href=/js/chunk-vendors.5e63c7cf.js rel=preload as=script>
```

当浏览器解析到`preload`会立即进行资源的请求，需要注意的是使用`preload`进行预加载时需要指定文件的类型

**prefetch**

```html
<link href=/js/chunk-dca4e6ea.e4986a0a.js rel=prefetch>
```

当浏览器解析到`prefetch`时，不会立即请求资源，会等待浏览器空闲以后再进行资源的请求

现在前端都是基于`webpack`来实现构建，目前`webpack v4.6.0+` 实现了对预获取和预加载的支持

使用方式如下

```js
import(/* webpackPrefetch: true */ "LoginModal");
import(/* webpackPreload: true */ "ChartingLibrary");
```

当然我们也可以借助`preload-webpack-plugin`插件来实现

[https://www.npmjs.com/package/preload-webpack-plugin](https://link.zhihu.com/?target=https%3A//www.npmjs.com/package/preload-webpack-plugin)

`preload`初始模块

`prefetch`异步模块

```js
new PreloadWebpackPlugin(
    {
        rel: "preload",
        include: "initial",
        fileBlacklist: [
            /\.map$/,
            /hot-update\.js$/
        ]
    }
),
new PreloadWebpackPlugin({
    rel: 'prefetch',
    include: 'asyncChunks'
}),
```

- 减少dom数量
- 根据域名划分页面内容
- 少使用iframe
- 杜绝404
- 使用内容分发网络

js，html，css放到单独的静态资源服务器

- 使用get完成请求

post两步走，先发文件头再发数据，GET直接发一个TCP包

##### css和js

- 样式表置于顶部

会使页面有秩序得加载

- 避免使用css表达式
- 使用外部的js和css

会增加请求数量，但是有助于文件的缓存，适用于频繁访问并且变更较少的内容，既不会增加请求也不会增加文件大小

- 压缩js和css
- 避免使用滤镜
- 选择link舍弃@important

import会堵住加载

- js脚本放在底部
- 不引入重复脚本
- 减少dom访问

使用变量存储获取的dom

- 智能事件处理程序

有时候感觉页面反映不够灵敏，是因为有太多频繁执行的事件处理具柄被添加到了DOM树的不同元素上，这就是推荐使用事件委托的原因。如果一个div里面有10个按钮，应该只给div容器添加一个事件处理具柄，而不是给每个按钮都添加一个。事件能够冒泡，所以可以捕获事件并得知哪个按钮是事件源。

不需要为了处理DOM树而等待onload事件,通常只要目标元素在DOM树中可访问即可,而不必等待所有的图片下载完成。可以考虑用 DOMContentLoaded 来代替onload事件,但为了让它在所有浏览器中都可用,可以用 YUI Event 工具,它有一个onAvailable 方法。

- 文件小于25k
- 组件打包成复合文本

写在一起js和css，再用某种办法区分，现在不常用了

```js
1. CSS解析器 会忽略<!--符号，
2. JS解析器会把<!--当作注释符号，与// 注释相同。
<!-- /*
js
<!-- */

<!--
css
```



##### 图片

- 优化图片

压缩，格式转换为png

- 网站图标，小并且可缓存

##### cookie

- 减小cookie体积，可以使用localStorage代替
- 把组件放在无cookie域名下



<img src="Naixes阶段性学习笔记.assets/截屏2021-05-10 上午9.58.46.png" alt="截屏2021-05-10 上午9.58.46" style="zoom:50%;" />

**CDN：**

压缩合并的矛盾（压缩请求变多，合并文件变大），网站并发最多5个请求，加CDN

每个请求携带cookie，CDN可以去cookie，一个CDN下放不超过5个文件（页面上script不超过5个，超过就会等待）

webpack：超过30kb的文件才会被单独提取

控制一个script引用文件的大小，压缩后32kb（压缩前大概110kb），不够的话做懒加载或者缓存

**MD5:**

添加合适的md5，方便离线缓存

压缩：

**gzip**

br，针对于图片等的压缩协议

**离线缓存：**

前端ORM存储方案，关系映射表，库localForage，对现有的前端离线存储资源进行了封装，使用basketjs+localforage做离线缓存库

local storage，key-value，5m，部分机型超过2.5会卡顿（低端机型）

session strage，临时

indexed db，非关系型数据库

web sql，关系型数据库，50m

cookies，一般存储session id，不存储静态文件

trust tokens

<img src="Naixes阶段性学习笔记.assets/截屏2021-05-10 上午10.46.51.png" alt="截屏2021-05-10 上午10.46.51" style="zoom:50%;" />

1. webpack打一个全局的md5表

   ```js
   {
     "a.js": "a.53ddju3gy34.js",
       ...
   }
   ```

2. 启动js，加载到a时，先查看本地是否有缓存，localstorage中：

```js
function 注入缓存() {
  // "a.js"-> "a.53ddju3gy34.js"
	// "a.53ddju3gy34.js"-> "js内容"
}
if(本地是否有缓存) {
  if(是否过期) {
    // 加载文件
    // 清理缓存
    // 注入缓存
  }else {
    // 使用缓存
  }
}else {
  // 加载文件
  // 再次请求资源，fetch获取文件内容（已经etag缓存）
  // 注入缓存()
}
```

Service Workers：可以离线所有的文件，首先保证功能可用再进行提示

**检测用户网络：**

申请图片时判断用户网速

`navigator.connection`

多普勒测速法：

0kb图片请求，t2DNS有缓存，t3多路复用

<img src="Naixes阶段性学习笔记.assets/截屏2021-05-10 下午12.01.44.png" alt="截屏2021-05-10 下午12.01.44" style="zoom:50%;" />

网速达不到要求时，可以减少加载的组件和图片大小

百度的_WISE_INFO可以查看网速

#### 缓存策略 

缓存的优先级：cache-control expires etag last-modified

**cache-control**

设置过期的时间⻓度(秒)，在这个时间范围内，浏览器请求都会直 接读缓存。当 expires 和 cache-control 都存在时，cache-control 的 优先级更高。

**expires**

\* expires: Thu, 16 May 2019 03:05:59 GMT
 在 http 头中设置一个过期时间，在这个过期时间之前，浏览器的请求都不会发出，而是

自动从缓存中读取文件，除非缓存被清空，或者强制刷新。缺陷在于，服务器时间和用 户端时间可能存在不一致，所以 HTTP/1.1 加入了 cache-control 头来改进这个问题。

**etag / if-none-match**

这也是一组请求/相应头 响应头:
 etag: "D5FC8B85A045FF720547BC36FC872550" 请求头:
 if-none-match: "D5FC8B85A045FF720547BC36FC872550"

原理类似，服务器端返回资源时，如果头部带上了 etag，那么资源下 次请求时就会把值加入到请求头 if-none-match 中，服务器可以对比 这个值，确定资源是否发生变化，如果没有发生变化，则返回 304。

**last-modified / if-modified-since**

这是一组请求/相应头

响应头:

\* last-modified: Wed, 16 May 2018 02:57:16 GMT 01 请求头:

if-modified-since: Wed, 16 May 2018 05:55:38 GMT

服务器端返回资源时，如果头部带上了 last-modified，那么 资源下次请求时就会把值加入到请求头 if-modified-since 中，服务器可以对比这个值，确定资源是否发生变化，如果 没有发生变化，则返回 304。

#### 网站协议

http2多路复用：

浏览器请求//xx.cn/a.js-->解析域名—>HTTP连接—>服务器处理文件—>返回数据-->浏览器解析、渲染文件。Keep-Alive解决的核心问 题就在此，一定时间内，同一域名多次请求数据，只建立一次HTTP请求，其他请求可复用每一次建立的连接通道，以达到提高请求效率的问题。一定时间是可以配置的，HTTP1.1还是存在效率问题，第一个:串行的文件传输。第二个:连接数过多。HTTP/2对同一 域名下所有请求都是基于流，也就是说同一域名不管访问多少文件，也只建立一路连接。同样Apache的最大连接数为300，因为有了 这个新特性，最大的并发就可以提升到300，比原来提升了60倍!

<img src="Naixes阶段性学习笔记.assets/截屏2021-05-10 下午3.43.14.png" alt="截屏2021-05-10 下午3.43.14" style="zoom:50%;" />

### 渲染中的性能优化

#### 重绘重排影响

<img src="Naixes阶段性学习笔记.assets/截屏2021-05-10 下午5.24.50.png" alt="截屏2021-05-10 下午5.24.50" style="zoom:50%;" />

火焰图

loading

scripting，脚本执行

rendering，渲染

painting，绘制

system，系统执行js

ldle，空闲

<img src="Naixes阶段性学习笔记.assets/截屏2021-05-10 下午4.51.32.png" alt="截屏2021-05-10 下午4.51.32" style="zoom:50%;" />



<img src="Naixes阶段性学习笔记.assets/截屏2021-05-10 下午4.51.56.png" alt="截屏2021-05-10 下午4.51.56" style="zoom:50%;" />

网页是分层的

- 获取dom元素进行分层
- 对每个图层进行样式计算 recalcular style
- 对每个节点生成图形库的位置 layout
- 将每个节点绘制填充到图层的位图中 paint
- 图层作为纹理上传给GPU，CPU给GPU的最小的 bitmap GPU再进行偏移缩放等
- GPU将符合的图层生成屏幕图像，合成层 composite layers
- composite layers具体工作：
  - 主线程把绘制列表commit到合成线程
  - 合成线程根据视口切成tile
  - 将tile小图块生成位图，栅格化raster，保存到GPU中
  - 合成线程发送一个绘制图块的命令draw quad给浏览器进程
  - 浏览器viz组件处理drawquad
  - 首次会有一个低分辩的图，显示图片内容时全部显示

layout，paint，composite layers

#### 如何规避及高效渲染

独立生成层：根元素，position，transform，半透明，css滤镜，canvas，video，overflow

可以对独立的层加速，让GPU直接参与的元素或属性：css3d，video，webgl，transform，css滤镜，也可以使用will-change：transform

造成重排：读取offset，scroll，clientT，width会放弃优化立刻造成重排（优化：浏览器会维护一个回流重绘队列，到达一定数量或者时间就会flash批处理），盒子模型大小的变化（border-box的使用）

避免频繁flash，将读写分别放一起，一个简单的办法：写的时候放到requestAnimationFrame中（下一帧操作）

gpujs库，查看GPU性能， 优化费时操作

> css，js都会影响html的渲染不影响解析
>
> css的加载会影响js的执行，js会等css加载完成，因为js中可以使用CSS的类，造成重排
>
> css会不会阻塞domready，取决于css后面还有没有js，domContentLoaded事件
>
> css in js
>
> css inline
>
> （webkit相关）
>
> 减轻js对css的序列化：比如CSS.px(4)
>
> 
>
> spa
>
> 优：切页资源不重新加载，vuex公用
>
> 缺：白屏，seo
>
> index.html - vue.min.js - 相关库 - webpack公用文件 - main.js - fetch - 构建虚拟dom diff - patch页面 - 初始化事件引擎
>
> 白屏时间指的是页面准备加载到收到服务器返回的这段时间，这段时间过长就会产生白屏现象，在spa中尤为明显，以vue为例，浏览器加载完index.html后并不能看到页面，以为它只是一个框架没有实际内容，加下来还要加载vue，相关库，webpack公用文件，mainjs，发送请求，构建虚拟dom，diff，将虚拟dom patch到页面，初始化事件引擎等完成之后才能看到页面进行操作
>
> mpa
>
> 优：所见即所得，一次到位
>
> 缺：资源重复加载，index.html重（解决：bigpipe quicklink）
>
> mpa+spa真假路由混用
>
> mpa+spa真路由（自己开发，模版两套swig+vue），判断是否站内点击或刷新，相当于自己同构，也是next/nuxt原理
>
> nextjs，nuxtjs

### 页面加载性能优化

<img src="Naixes阶段性学习笔记.assets/截屏2021-05-17 上午9.18.19.png" alt="截屏2021-05-17 上午9.18.19" style="zoom:50%;" />

TTFB，用户收到第一个字节

FMP已废弃，需要手动mark有意义的点，造成一定的侵入性

FP，第一个像素点落点

FCP，首次内容绘制

TTI，可交互时间

#### 概念

18年google大会新出的指标

**最大内容绘制，LCP(Largest Contentful Paint)**，用于记录视窗内最大的元素绘制的时间，该时间会随着⻚面渲染变化而变化，因为⻚面中的最大元素在渲染过程中可能会发生改变，另外该指标会在用户`第一次交互后停止记录`。

**首次输入延迟，FID(First Input Delay)**，记录在 FCP 和 TTI 之间用户首次与⻚面交互时响应的延迟。react中的fiber专门解决FID

**阻塞总时间，TBT(Total Blocking Time)**，记录在 FCP 到 TTI 之间所有⻓任务的阻塞时间总和。

**累计位移偏移，CLS(Cumulative Layout Shift)**，记录了⻚面上非预期的位移波动。使用按钮动态添加某个元素，导致⻚面上其他位置的代码发生了偏移，造成了⻚面

**LCP 代表了⻚面的速度指标**， LCP 能体现的东⻄更多一些。一是指标实时更新，数据更精确，二是代表着⻚面最大元素的渲染时间，最大元素的快速载入能让用户感觉性能还挺好。
**FID 代表⻚面的交互体验指标**，交互响应的快会让用户觉得网⻚流畅。

**CLS 代表了⻚面的稳定指标**，尤其在**手机**上这个指标更为重要。因为手机屏幕挺小，CLS 值一大的话会让用户觉得⻚面体验做的很差。

<img src="Naixes阶段性学习笔记.assets/截屏2021-05-17 上午9.19.07.png" alt="截屏2021-05-17 上午9.19.07" style="zoom:50%;" />

FCP

<img src="Naixes阶段性学习笔记.assets/截屏2021-05-17 上午9.48.18.png" alt="截屏2021-05-17 上午9.48.18" style="zoom:50%;" />

LCP/FID

<img src="Naixes阶段性学习笔记.assets/截屏2021-05-17 上午9.48.46.png" alt="截屏2021-05-17 上午9.48.46" style="zoom:50%;" />

CLS

文本移动了 25% 的屏幕高度距离(位移距离)，位移前后影响了 75% 的屏幕高度面积(位移影响的面积)，那么 CLS 为0.25 * 0.75 = 0.1875。

CLS 推荐值为低于 0.1，越低说明⻚面跳来跳去的情况就越少，用户体验越好。

<img src="Naixes阶段性学习笔记.assets/截屏2021-05-17 上午9.49.36.png" alt="截屏2021-05-17 上午9.49.36" style="zoom:50%;" />

参考：web.dev/vitals

<img src="Naixes阶段性学习笔记.assets/截屏2021-05-17 上午9.58.47.png" alt="截屏2021-05-17 上午9.58.47" style="zoom:50%;" />

<img src="Naixes阶段性学习笔记.assets/截屏2021-05-17 上午10.40.00.png" alt="截屏2021-05-17 上午10.40.00" style="zoom:50%;" />

使用PerformanceObserver和performance.timing可以获取或计算这些指标

PerformanceObserver，统计异步数据

performance.timing，统计同步数据，通过节点的标签来获取对应的时间，可以计算获得DNS时间白屏时间等

```js
/**
 * Navigation Timing API provides performance metrics for HTML documents.
 * w3c.github.io/navigation-timing/
 * developers.google.com/web/fundamentals/performance/navigation-and-resource-timing
 */
const getNavigationTiming = () => {
  // There is an open issue to type correctly getEntriesByType
  // github.com/microsoft/TypeScript/issues/33866
  // 这里直接的物理赋值performance.timing 已被弃用
  const n = W.performance.getEntriesByType('navigation')[0] as any;
  // In Safari version 11.2 Navigation Timing isn't supported yet
  if (!n) {
    return {};
  }
  const responseStart = n.responseStart;
  const responseEnd = n.responseEnd;
  // We cache the navigation time for future times
  return {
    // fetchStart marks when the browser starts to fetch a resource
    // responseEnd is when the last byte of the response arrives
    fetchTime: responseEnd - n.fetchStart,
    // Service worker time plus response time
    workerTime: n.workerStart > 0 ? responseEnd - n.workerStart : 0,
    // Request plus response time (network only)
    totalTime: responseEnd - n.requestStart,
    // Response time only (download)
    downloadTime: responseEnd - responseStart,
    // Time to First Byte (TTFB)
    timeToFirstByte: responseStart - n.requestStart,
    // HTTP header size
    headerSize: n.transferSize - n.encodedBodySize || 0,
    //DNS解析时间
    dnsLookupTime: n.domainLookupEnd - n.domainLookupStart,
    //TCP建立时间
    tcpTime: n.connectEnd - n.connectStart || 0,
    // 白屏时间
    whiteTime: n.responseStart - n.navigationStart || 0,
    // dom渲染完成时间
    domTime: n.domContentLoadedEventEnd - n.navigationStart || 0,
    // 页面onload时间
    loadTime: n.loadEventEnd - n.navigationStart || 0,
    // 页面解析dom耗时
    parseDomTime: n.domComplete - n.domInteractive || 0,
  };
};
```

获取性能指标

```js
// window.performance.getEntriesByType("paint")

// 可以获取FP和FCP
const obs = new PerformanceObserver(list => {
  for(const entry of list.getEntries()) {
    console.log(entry)
  }
})
obs.observer({entryTypes: ['paint']})

// longtask
const obs = new PerformanceObserver(list => {
  for(const entry of list.getEntries()) {
    console.log(entry)
  }
})
obs.observer({entryTypes: ['longtask']})
// 定位到longtask后要把它挪走
// 下一帧
requestAnimationFrame()
// 空闲帧
// 1000/60 - 1000/30，1帧16.7 - 33.3毫秒system+程序时间
requestIdleCallback() // react 16.8 fiber的原理就用到了，利用空闲帧实现了调度算法

// FMP，需要mark收取值，侵入了业务逻辑
// 无侵入统计：？？？
<script>performance.mark('meaningful')</script>
...

<script>performance.clear('meaningful')</script>
...
const obs = new PerformanceObserver(list => {
  for(const entry of list.getEntries()) {
    console.log(entry)
  }
})
obs.observer({entryTypes: ['meaningful']})

// performance可以获取所有数据，根据navigation timing的流程
```

统计FP，FCP，浏览器中有很多FRP（响应式函数编程，比如rx.js）的指标证明，可以进行observe

PerformanceObserver，统计异步数据

performance.timming，统计同步数据

库web-vitals，避开了很多坑

<img src="Naixes阶段性学习笔记.assets/截屏2021-05-17 上午10.41.19.png" alt="截屏2021-05-17 上午10.41.19" style="zoom:50%;" />

白屏：

白屏时间：一般来说responseStart - navigationStart，但是这只是白屏里的前一半时间，不含代码执行和浏览器引擎渲染过程页面白屏的时间

首屏时间：loadEventEnd - navigationStart**首次全部完整下载和渲染完页面时间**

优化方式：quicklint，骨架屏，HTTP2等

qucklink库：利用了Intersection Observer API（监测视窗滚动）和window.requestIdleCallback()，当滚动到某个视窗以内时判断网络条件，好的话会在空闲帧把a连接进行预加载（cb），所有连接预加载成本有点大，还可以进行优化

guess.js：通过人工智能进行预测最有可能去的连接进行预加载，基于之前的统计数据

统计离线数据的内存使用情况

<img src="Naixes阶段性学习笔记.assets/截屏2021-05-17 上午11.03.02.png" alt="截屏2021-05-17 上午11.03.02" style="zoom:50%;" />

vue

老的生命周期

<img src="Naixes阶段性学习笔记.assets/截屏2021-05-17 上午11.05.50.png" alt="截屏2021-05-17 上午11.05.50" style="zoom:50%;" />

总结：

<img src="Naixes阶段性学习笔记.assets/截屏2021-05-17 上午11.13.44.png" alt="截屏2021-05-17 上午11.13.44" style="zoom:50%;" />

CSR：不依赖数据index的壳最先出来，webpack插件经常inline css，减少请求时间，FP最快

解决方案：预渲染，在构建时(build time)简单地生成针对特定路由的静态 HTML 文件。 不稳定，将html load到无头浏览器中，保存下来，每次上线都需要重新渲染

SSR：优化index重，bigpipe，将不重要的内容分成task利用流异步输出

### 错误捕获

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <!-- 1 -->
    <script>
        error
        console.log(1);
    </script>
    <script>
        // 会执行，每个script都是一个宏任务，互不影响
        console.log(2);
    </script>

    <!-- 2 -->
    <script>     
        try {
            console.log(error);
        } catch (e) {
            console.log(e);
        }
        // 异步的错误捕获不到，使用window.onerror
        try {
            setTimeout(() => {
                console.log(error);
            })
        } catch (e) {
            console.log('erroe:', e);
        }
    </script>

    <!-- 3 window.onerror -->
    <script>
        try {
            setTimeout(() => {
                console.log(error);
            })
        } catch (e) {
            console.log('erroe:', e);
        }
        // 捕捉不到html中的错误
        window.onerror = function(msg, url, row, col, error) {
            console.log(msg);
            // 禁止页面报红
            return true
        }
    </script>

    <!-- 4 -->
    <img src="./xx.png" alt="">
    <script>
        window.addEventListener("error", (msg, url, row, col, error) => {
            console.log(msg);
            return true
        }, true)
    </script>
    <!-- 以上都捕获不到Promise的错误 -->

    <!-- 5 -->
    <script>
        // 捕获异步错误
        window.addEventListener('unhandledrejection', function(e) {
            e.preventDefault()
            console.log(e.reason);
            return true
        })
        // 不catch就会报红
        new Promise((resolve, reject) => {
            reject("erroe1")
        })
        Promise.resolve().then(() => {
            throw "error3"
        })
        Promise.reject("error2")
      
      	// 全局错误uncatchException

        // 工具：fundebug
        // 接入
        // npm 安装

        // 用户录屏：sessionstack

        // 容错：zanePerfor （github）
    </script>
</body>
</html>
```

fundebug源码：

```js
// 兼容node错误
      
// 全局错误uncatchException
// unhandledrejection
// error

// 客户端
window.onerror
window.addEventListener("error", ...)
                        
// 录屏
// 记录用户的xpath，发送到服务端，生成gif
// 或者把用户操作的帧通过html2canvas发送给服务器，然后合成
```

存储容错数据时不要用ajax，会占用并发，使用navigator.sendBean("xxx.php")，专门用来做统计

参考项目：zanePerfor

#### SDK

参考：demo-collection-pro/performance项目

日志：

图片，img.src - "1*1.gif?data=序列化" 压缩，图片不占用业务逻辑并发，在独立的cdn

navigator.sendBeacon，传送

fetch，错误级别

ajax

> 注意sourcemap导致源码泄漏问题
>
> 包microbundle专门做sdk的
>
> 包api-extractor生成d.ts

##### 数据上报

方案一：xpath复杂，对纯文本节点支持不好，改为给每个节点添加id，但是文件太大

1. 代理用户的所有点击事件

2. 记录[xpath]，栈，LRU算法（缓存算法）维护，30fps确定栈长度

3. 压缩数据（工具：rrweb/src/packer/pack.ts），fetch（传送）
4. pupteer - 每还原一步都保存为png - node工具合成gif/mp4

> 微前端：国内，乾坤，国外，single-spa
>
> 乾坤：特性，路由代理成类似iframe[0] -> a/b -> content -> load，页面会有很多body

方案二：

图（htmlcanvas -> base64（太大））

方案三：

webrtc - js录制mp4 record（需要权限，只能给b端）

方案四：

只要是dom变动就触发MutationObserver，对form事件不起作用

方案五：

rrweb - 虚拟dom，添加id，事件触发时记录id - 还原播放

checkoutEveryNth不准确

不需要考虑fps

## vue/react ssr原理

参考项目：https://github.com/Naixes/sin-books

> jquery.pjax，代理请求，判断站内跳转还是刷新操作
>
> cheerio，在node中像jquery一样操作dom

### bigpipe

参考项目：https://github.com/Naixes/demo-collection/tree/master/learnNode/koa-bigpipe

当网页变得复杂整页渲染，内容太多

ssr - render 内容过大

bigpipe，使用文件/流输出页面而不是传统的render页面，或者将不重要的内容分成task利用流在服务端异步输出都属于bagpipe，响应头Transfer-Encoding: chunked，可以不使用koa-bigpipe等库，可以自己写，很简单

分段 chunked 串行输出，比如百度页面

> Transfer-Encoding: chunked

```js
const KOA = require('koa')
const Router = require('koa-router')
const render = require('koa-swig')
const co = require('co')
const {join, resolve} = require('path')
const fs = require('fs')

const app = new KOA()
const router = new Router()

app.context.render = co.wrap(
    render({
        root: join(__dirname, 'views'),
        autoescape: true,
        // ssr最关键的地方
        cache: false,
        ext: 'html',
        writeBody: false
    })
)

// task
const task1 = () => {
    return new Promise((res, rej) => {
        setTimeout(function () {
            resolve(`<script>addHtml("part1", "第一次传输<br/>")</script>`)
        }, 2000)
    })
}
const task2 = () => {
    return new Promise((res, rej) => {
        setTimeout(function () {
            resolve(`<script>addHtml("part2", "第二次传输<br/>")</script>`)
        }, 1000)
    })
}

// 基础页面传输
router.length('/test', async(ctx, next) => {
    ctx.body = await ctx.render('index')
})

// bigpipe
router.length('/', async(ctx, next) => {
    // 不是同步输出，没有按默认流程走会报404，要手动修正状态和类型
    ctx.status = 200
    ctx.type = 'html'

    // 4. 影响seo，但是影响不大，先渲染了主要内容
    const file = fs.readFileSync('./index.html', 'utf-8')
    ctx.res.write(file)
    const result1 = await task1
    ctx.res.write(result1)
    const result2 = await task2
    ctx.res.write(result2)

    ctx.res.end()

    // // 1. file传输，比render传输性能高
    // // 响应头：Transfer-Encoding: chunked
    // const file = fs.readFileSync('./index.html', 'utf-8')
    // ctx.res.write(file)
    // ctx.res.end()

    // // 2. 流，常见
    // const filename = resolve(join(__dirname, 'index.html'))
    // const stream = fs.createReadStream(filename)

	  // 需要封装一下，否则只返回一个ok
    // function createSsrStreamPromise() {
    //     return new Promise((resolve, reject) => {
    //         stream.on('error', err => {
    //             reject(err)
    //         }).pipe(ctx.res)
    //     })
    // }
    // await createSsrStreamPromise()

    // // 返回ok，koa需要像上面那样写
    // // stream.on('error', err => {
    // //     console.log('error', err);
    // // }).pipe(ctx.res)

    // // 3. 混合
    // const filename = resolve(join(__dirname, 'index.html'))
    // const stream = fs.createReadStream(filename)

    // function createSsrStreamPromise() {
    //     return new Promise((resolve, reject) => {
    //         stream
    //         .on('data', chunk => {
    //             ctx.res.write(chunk)
    //         }).pipe(ctx.res)
  	// 此时必须end
    //         .on('end', () => {
    //             ctx.res.end()
    //         })
    //     })
    // }
    // await createSsrStreamPromise()
})

app.use(router.routes()).use(router.allowedMethods())

app.listen(8085)
```

index

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>home</title>
</head>
<body>
    <!-- 同步输出 -->
    <h2>bigpipe输出</h2>
    <!-- 异步输出 -->
    <div id="part1">loadding</div>
    <div id="part2">loadding</div>
    <script>
        function addHtml(name, content) {
            document.getElementById(name).innerHTML(content)
        }
    </script>
</body>
</html>
```

### 面向切面编程

面向切面实现的主要目的是针对业务的切面进行提取

### SOLID

SOLID 是面向对象设计5大重要原则的首字母缩写

mvc，相互嵌套太深，类似齿轮

IOC，控制反转，依赖的技术手段DI（依赖注入），AOP的思想（面向切面编程），在constructor中工作

awilix，一个注入的框架

参考项目：https://github.com/Naixes/demo-collection/tree/master/learnSOLID/learnIOC

npm i awilix awilix-koa -D

> ts-node-dev，不用每次重启，ts版的nodemon
>
> modules-alias

