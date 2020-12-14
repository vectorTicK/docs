---
sidebar: auto
---
# Ubuntu常用命令

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