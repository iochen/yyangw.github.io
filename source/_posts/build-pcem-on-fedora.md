---
title: 在 Fedora 系统下编译 PC 模拟器 PCem
date: 2017-06-11 14:00:21
tags:
  - Old School Computer
  - Computer History
---
## 简介

PCem 是一款完美模拟老硬件环境的模拟器,如果你是古董游戏/软件的爱好者,那么千万不要错过它。
  * ![](https://yiyangwang.us/2017-06-11/build-pcem-on-fedora/0.jpg)
<!-- more -->

## 编译运行

访问PCem官网[https://pcem-emulator.co.uk/]下载模拟器
解压压缩包,进入目录
打开 Readme-LINUX,依赖要求如下:

  * Allegro 4.x
  * OpenAL
  * ALut

安装依赖：

``` bash
sudo dnf install allegro allegro−devel openal−soft openal−soft−
devel freealut freealut−devel
```

确定在解压文件所在目录执行:

``` bash
./configure
make && sudo make install
```

发现报错如下:

``` bash
Making all in src
make[1]: Entering directory ’/home/Tony/ 下 载 /PCemV12Linux/src’
source=’386.c’ object=’pcem−386.o’ libtool=no \
DEPDIR=.deps depmode=none /bin/sh ../depcomp \
gcc −DPACKAGE_NAME=\”PCem\” −DPACKAGE_TARNAME=\”pcem\” −
DPACKAGE_VERSION=\”v12\” −DPACKAGE_STRING=\”PCem\ v12\” −
DPACKAGE_BUGREPORT=\”Sarah\ Walker\ \<pcem−emulator@pcem−
emulator.co.uk\>\” −DPACKAGE_URL=\”\” −DPACKAGE=\”pcem\” −
DVERSION=\”v12\” −DHAVE_LIBOPENAL=1 −DHAVE_LIBALUT=1 −
DHAVE_LIBPTHREAD=1 −I.
−I/usr/include −O3 −c −o pcem−386.o
‘test −f ’386.c’ || echo ’./’‘386.c
/bin/sh: ../depcomp: No such file or directory
Makefile:737: recipe for target ’pcem−386.o’ failed
make[1]: *** [pcem−386.o] Error 127
make[1]: Leaving directory ’/home/Tony/ 下 载 /PCemV12Linux/src’
Makefile:337: recipe for target ’all−recursive’ failed
make: *** [all−recursive] Error 1
```

由于链接已断,重新链接：

``` bash
automake −−add−missing
```

重新执行：

``` bash
make && sudo make install
```

编译通过
在这里编译就基本完成了,可以选择在官网上下载没有版权限制的 rom 放置到 roms 文件夹内,然而在中文的操作环境下有出现了新的问题: 放置到 roms 文件夹后报错：

``` bash
Set fullspeed − 0 0 0
No ROMs present!
AL lib: (WW) FreeContext: (0x4358fe0) Deleting 2 Source(s)
AL lib: (WW) FreeDevice: (0x4349310) Deleting 8 Buffer(s)
You must have at least one romset to use PCem.
```

这个是由于 PCem 本身 Linux 版本存在众多缺陷(后面会讲),不支持中文目录就是其中之一,将 PCem 目录移动至英文目录即可解决,示例：

``` bash
mv PCem/ /home/username/PCem
```

## 获取更多的 roms

上文也提及,在官网上面有部分没有版权限制的 rom 可以免费下载,更多的 rom 因为版权原因需要使用搜索引擎获取,在这里推荐一个博客[http://retro-roms.blogspot.com](http://retro-roms.blogspot.com),在这里提供更多 roms 的下载,
链接：
[http://retro-roms.blogspot.com/2016/09/pcem-v11-bios-update.html](http://retro-roms.blogspot.com/2016/09/pcem-v11-bios-update.html)
请勿用于商业用途

## 相较于 Windows 版本,Linux 版本的缺陷

  * 无法显示菜单,需要使用 CTRL-ALT-PGDN 打开
  * 鼠标不能很好的工作
  * 无法实现全屏
  * 无法运行视频加速,所以性能不如 Windows 版本

## 最终成果

  * ![](https://yiyangwang.us/2017-06-11/build-pcem-on-fedora/1.jpg)

