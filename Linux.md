## linux

linux和mac都是类unix

主要是内核

linux和windows：windows作为服务器成本高，性能不如linux

linux发行版：简单来说就是linux内核和应用软件的打包，常用linux发行版：CentOS，ubuntu，redhat，Debain，Fedora等

### 内核

linux内核：kernel

操作系统的核心，第一层基于硬件的扩充，最核心最基础的服务

应用通过内核进行系统调用使用硬件，内核代码简洁高效，基本没有bug

Linux是一种开源电脑操作系统内核，c语言编写，符合POSIX标准的类Unix操作系统

**Linux内核的主要模块**

储存管理

CPU和进程管理

文件系统

设备管理和驱动

网络通信

系统的初始化

系统调用

### 虚拟机

vmware

virtualbox 

virtualpc

### cygwin

在windows下运行的uniux环境

安装，完整安装full

### 安装

#### 发行版

CentOS：使用redhat的源代码，redhat：商业系统，Fedora：桌面好用，在CentOS的基础上      ===     rpm安装包

ubuntu：桌面好用（可以用来开发），在Debain的基础上，Debain：国外用的多     ===    deb安装包

#### ubuntu

#### CentOS

mini版：没有图形界面，一般用在服务器

1. vmware：注册后安装

2. centos：linux的安装镜像

3. 创建虚拟机：注意路径，处理器：1，内核：1，内存推荐2g以上，桥接网络，默认，最大磁盘大小20g，存为单个文件（需要复制时可以选多个，拷贝比较快）

4. 打开虚拟机：安装centos，默认，选择图形界面和安装软件

   > 问题：此主机支持 Intel VT-x，但 Intel VT-x 处于禁用状态。
   >
   > 解决：在bios中配置
   >
   > 可以在任务管理器的性能页签查看是否已经开启虚拟化

### 目录

- root：根

- bin：可执行程序，没有后缀

  判断是否可执行文件：命令：ls -l：以x结尾说明可执行

- etc：配置文件，重要脚本

- hom：多用户系统的用户信息，相当于windows的users

- lib/lib64：系统的库，二进制，相当于windows

- mnt/media：u盘等

- dev：开发用的东西

- proc：动态数据，系统的信息，内存中，关机会清空

  命令：cat cpuinfo：可以显示cpu信息

- boot：引导文件，脚本，配置文件，内核等
- opt：可以放绿色软件等自己安装的软件，相当于programfiles，yum install xxx可以安装软件
- root：root用户的home
- sbin：和bin类似（历史原因遗留）
- sys：扩展目录（历史原因遗留）

### 命令行

```cmd
ls #默认在home路径下，ls显示当前路径下所有文件
dir #和ls效果一样
ls -l #长格式目录
ls -a #显示隐藏文件，.表示当前目录，..表示上一级目录
ls -al
cd xxx #切换目录，文件名严格区分大小写
cd .. #上级目录
cd ~ # 当前用户路径
cd / #根路径 
cat xxx # 查看当前文件
mkdir xxx # 创建目录                                                       md # windows
touch xxx # 创建文件
cp copyname path/newname # cp bb.bb aaa/bb.bc 拷贝文件到指定目录并重命名    copy copyname filename # 拷贝文件到指定目录   rename filename newname # 重命名
cp -R copyname newname # 拷贝目录
pwd # 显示完整路径
rm filename # 删除文件                                                     del # 直接删除文件
rm -r filename # 删除文件夹
rm -rf # 删除所有文件 
mv # 移动文件

init [0123456] # 0：关机，1：单用户，2：多用户有网络，3：多用户无网络，4：系统未使用保留给用户，5：图形界面，6：重启
```

#### 文件夹权限

文件类型：1链接d目录-文件

文件所有者权限：r可读4，w可写2，x可执行1

文件所在组对该文件权限

其他组用户对该文件的权限

### 远程登录Linux

#### win

##### putty

##### xshell

##### cmder终端使用ssh命令

安装cmder：绿色软件，配置环境变量，使用

#### linux和mac

##### ssh命令

```cmd
ssh 用户名@ip #ssh root@192.168.0.21  回车
输入密码 # 输入密码  回车
# #表示超级管理员 $普通用户 ubuntu是禁用root用户的 centos不会禁用
```

### 常用命令

#### vi/vim

见下

#### 其他

**服务管理命令**

systemctl：

**网络管理命令**

ifconfig：显示网络配置

ip：

router：

## vim

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

> 命令都是单词的首字母

**yank：拷贝**，paste：向后粘贴，P：向前粘贴

**undo：撤销**，**redo：撤销撤销**（ctrl+r，r是replace）

**insert：插入**（在前面插入，append：在后面插入，I：行首插入，A：行尾插入）进入**插入模式**

**正常模式**下输入冒号进入**命令行模式**，write：保存

**delete：表示删除**：

dd：删除一整行（ctrl+d/u：翻页），3dd：删除3行（其他操作也适用数字），x：向后删除一个字符，delete word：向后删除单词，db：向前删除一个单词，di(：删除括号里面的内容，da(：删除括号包括内容，di{，dit：删除tag中的内容

```cmd
vi 文件名 # 打开文件
# i ：插入
# esc: ：底线命令行模式
# esc:w ：保存
# esc:wq ：保存并退出
# /xxx ：检索xxx，下一个n，上一个shift+n
```

