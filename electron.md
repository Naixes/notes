# vim

windows必须安装git bush才能使用

进入：vim

退出：依次esc:q!

- vim：编辑器之神，可以配置成ide
  - Linux自带，也自带nano但是不好用
  - 键盘控制
  - 支持宏，插件
  - 等等

- Emacs：神的编辑器，相当于一个操作系统

### 官方教程

命令：vimtutor

命令都是单词的首字母

yank：拷贝，paste：向后粘贴，P：向前粘贴

undo：撤销，redo：撤销撤销（ctrl+r，r是replace）

insert：插入（在前面插入，append：在后面插入，I：行首插入，A：行尾插入）进入**插入模式**

**正常模式**下输入冒号进入**命令行模式**，write：保存

**delete：表示删除**：

dd：删除一整行（ctrl+d/u：翻页），3dd：删除3行（其他操作也适用数字），x：向后删除一个字符，delete word：向后删除单词，db：向前删除一个单词，di(：删除括号里面的内容，da(：删除括号包括内容，di{，dit：删除tag中的内容

# electron

- 一个个性化浏览器
- 支持nodejs和浏览器js

### 开始

#### 安装

```js
npm init -y
npm i electron --dev
// 在本地目录寻找，不写就是在全局寻找
npx electron -v
```

创建index.html和main.js

#### 配置

添加脚本命令：`"start": "electron ."`

修改main：`"main": "main.js"`

编写main.js打开index.html

#### 打包

安装electron-builder

添加命令脚本`"build": {xxx} ...`，从github上面拷贝

`npm run build`

也可以直接打开一个网站，win.loadURL()

dist --win可以打包一个windows



移植vue项目，开一个服务，gitbash打开命令行，http-server打开一个服务，打包到根目录，将文件拖到electron项目中，打包

#### 缺点

功能不全面，安装包体积大，程序占用内存大，不能做大型游戏