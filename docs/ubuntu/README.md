---
sidebar: auto
---
# Ubuntu

## 安装配置ubuntu18.04

### 准备材料

> 我的电脑是联想拯救者Y7000，配置i5-8300H, 1050Ti, 8G内存， 512G固态。安装Ubuntu的主要影响是显卡驱动问题会导致安装过程死机，wifi模块默认关闭，安装过程中不能立刻使用无线联网。

* Ubuntu桌面版iso镜像文件，从Ubuntu官网下载：<https://www.ubuntu.com/download/desktop>

* 8G以上U盘

* rufus软件，用于将Ubuntu镜像烧录到U盘

### 安装

1. 使用rufus软件，将下载好的Ubuntu镜像烧录到U盘
1. 重启电脑，选择从USB启动
1. 进入按照启动画面后选择`ubuntu install`，（解决安装过程中的死机问题：按'e'键，将`quiet splash ---`修改为 `quiet splash nomodeset`）
1. 进入图形化安装界面，正常逐步操作
1. 重启后选择`ubuntu`，（解决安装过程中的死机问题：按'e'键，添加：`nomodeset`）

> 重启后基本可以正常使用，但本机wifi不能使用，显卡驱动为装，登录、关机都会出现死机情况，下面在配置部分逐项解决

### 配置

1. 开启无线网卡：

```bash
sudo gedit /etc/modprob.d/ideapad.conf
blacklist ideapad_laptop
sudo touch /etc/modprobe.d/ideapad.conf
sudo modprobe -r ideapad_laptop
```

2. 连接网络后打开软件更新，更新软件

1. 安装显卡驱动：

```bash
nvidia drivers:ubuntu-drivers devices
sudo ubuntu-drivers autoinstall
```

### 美化

> ubuntu18.10开始，Ubuntu默认主题已足够美观，进一步美化可参照以下步骤

1. 安装**ubuntu tweak tool**

1. 安装**gnome-shell**

1. 在gnome-look下载各类主题，安装主题的按照说明进行安装使用

### 我的Ubuntu桌面

*桌面*

<img src="img/screenshot1.png"  width="640" height="360">

*打开应用*

<img src="img/screenshot2.png"  width="640" height="360">

> 可以愉快的使用了，需要什么软件搜索就可以了

## 解除端口占用

1.查看已经连接的服务端口

> netstat -a

2.查看所有的服务端口

> netstat -ap

3.查看指定端口，可以结合grep命令：

>  netstat -ap | grep 8080

4.根据端口查找进程

> sudo lsof -i:端口号

5.杀掉进程

> sudo kill pid号



## 安装Windows字体

1. 从 Win10 系统下字体文件夹（C:\Windows\Fonts） ，拷贝如下文件到当前Ubuntu用户目录 /usr/software/fonts/Fonts

```
宋体：simsunb.ttf 和 simsun.ttc
微软雅黑：msyhbd.ttf
Courier New：courbd.ttf、courbi.ttf、couri.ttf 和 cour.ttf
WPS Office 所需字体：wingding.ttf、webdings.ttf、symbol.ttf、WINGDNG3.TTF、WINGDNG2.TTF、MTExtra.ttf
1234
```

2. 新建字体存放目录 windows-font

```bash
sudo mkdir /usr/share/fonts/truetype/windows-font
```

3. 拷贝字体到wiondow-font目录下

```bash
sudo cp /usr/software/fonts/Fonts/* /usr/share/fonts/truetype/windows-font
```

4. 修改权限，并更新字体缓存

```bash
sudo chmod -R 777  /usr/share/fonts/truetype/windows-font
cd /usr/share/fonts/truetype/windows-font
sudo mkfontscale
sudo mkfontdir
sudo fc-cache -fv
```

5. 重启下系统吧！

```bash
sudo reboot
```