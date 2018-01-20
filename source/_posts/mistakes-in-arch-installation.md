---
title: 悉数 Arch Linux 安装过程中踩过的那些坑
date: 2018-01-17 17:05:15
tags: Linux
---

## 0. 软件源

在 USB引导的 Arch Linux 环境中默认的软件源在美国，由于中国是一个神奇的国度，所以需要替换为 中国的镜像  [这篇简书上的教程](https://www.jianshu.com/p/fe2165cc6af8) 的作者推荐用 nano 编辑器 手动将软件源复制粘贴到前方，但实际操作中比较复杂，所以博主推荐另一种方法：
使用如下指令从 Arch Linux Wiki 下载并替换 /etc/pacman.d/mirrorlist ：

``` bash
wget -O /etc/pacman.d/mirrorlist https://www.archlinux.org/mirrorlist/all/https/
```

接下来编辑 /etc/pacman.d/mirrorlist ，找到 China 部分，将软件源前面的注释去掉，然后使用如下指令：

``` bash
pacman -Syy
pacman -S --force pacman-mirrorlist
```

<!-- more -->

## 1. 磁盘分区

在这一部分按照 Arch Linux Wiki 上面的 [Installation Guide](https://wiki.archlinux.org/index.php/Installation_guide) 即可，唯一要注意的地方：

* 如果使用UEFI引导，EFI系统分区需要参考 [EFI System Partition](https://wiki.archlinux.org/index.php/EFI_System_Partition) 进行格式化

使用如下指令：

``` bash
mkfs.fat -F32 /dev/sdxY
```

## 2. 网络连接

博主在安装完基本操作系统，进入到了 Plasma 桌面环境，但是连接到网络必须使用 netctl 手动配置，需要切换到 NetworkManager ，使用如下指令：

``` bash
pacman -S network-manager-applet plasma-nm
sudo systemctl disable netctl
sudo systemctl enable NetworkManager 
```

* 注意大小写

## 3. 桌面环境中文化

恭喜你，进入了桌面环境，同时可以使用 NetworkManager 连接到互联网，可以参考 [这篇简书上的教程](https://www.jianshu.com/p/fe2165cc6af8) ，"系统中文化" 之前的部分

### 安装中文字体

使用如下指令安装中文字体，在此处博主推荐 “思源黑体”

``` bash
sudo pacman -S adobe-source-han-sans-cn-fonts adobe-source-han-serif-cn-fonts
```

### KDE 设置全面的中文

参考 [Arch Linux Localization](https://wiki.archlinux.org/index.php/Arch_Linux_Localization_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)) ，在 ~/.xprofile 文件前端添加：

``` bash
export LANG=zh_CN.UTF-8
export LC_ALL="zh_CN.UTF-8"
```

* **注意: **该方法适用登陆管理器用户，KDE用户按此方法可以设置较为全面的中文

## 4. 中文输入法

博主从 Fedora 迁移过来，所以更习惯使用 ibus 作为中文输入法，安装过程可以参考 Arch Linux Wiki [IBus](https://wiki.archlinux.org/index.php/IBus_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)) ，但是单独写入 ~/.bashrc 并不能在启动时自动运行，需要在 ~/.xprofile 中写入：

``` bash
export GTK_IM_MODULE=ibus
export XMODIFIERS=@im=ibus
export QT_IM_MODULE=ibus

ibus-daemon -x -d
```

此时，ibus 输入法 已经可以使用了，按照 [官方Wiki](https://wiki.archlinux.org/index.php/IBus_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)) 进行配置即可

## 尾声

至此，带有图形界面和中文环境的 Arch Linux 安装完毕，附上一张博主的桌面~

![](https://yiyangwang.us/2018-01-17/mistakes-in-arch-installation/0.jpg)