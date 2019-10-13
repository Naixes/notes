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

### 安装

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

