---
title: 博主开发的软件 —— LinFax使用教程
date: 2017-08-03 20:23:24
tags:
  - Network
  - Linux
---
## LinFax
Linux原生的气象传真软件有ACFax，HamFax等，但是ACFax长期没有更新，HamFax支持ALSA和PulseAudio... 看起来HamFax就是最完美的解决方案，然而：扫描出来的图像像素比例失真，对比Windows上面的软件，KG-FAX可以看出不同。于是，博主在HamFax的基础上开发了LinFax

  ![ ](https://yiyangwang.us/2017-08-03/linfax-guide/0.jpg)

<!-- more -->
## 从GitHub下载项目源代码

HamFax使用GPL v3协议发布，LinFax使用相同的协议，源代码在GitHub上面公开，传送门：

  [https://github.com/YiyangVVang/LinFax](https://github.com/YiyangVVang/LinFax)

可以通过git clone到本地，也可以下载打包好的源码解压到本地，赋予"./configure"可执行权限，接下来执行Linux中的经典指令：

``` bash
./configure
make
```

然后运行编译后生成的文件：

``` bash
./hamfax
```

此时就已经进入LinFax本体了，但是程序默认从麦克风采集声音，对使用SDR的用户产生了很大的不便。但在Linux中可以使用PulseAudio将声音转录到麦克风，输入如下指令安装PulseAudio以及图形界面控制软件"PulseAudio 音量控制"

``` bash
sudo dnf install pulseaudio pavucontrol
```

然后打开"PulseAudio 音量控制"，同时确认LinFax打开"Receive from dsp"窗口，如图所示，调整PulseAudio设置

  ![ ](https://yiyangwang.us/2017-08-03/linfax-guide/1.jpg)
  ![Manual](https://yiyangwang.us/2017-08-03/linfax-guide/2.jpg)

以上设置确认无误后打开你的SDR，调整到指定的频率就可以接收了~
最后祝大家玩的开心~

## 博主通过WebSDR接收到的一些图

  ![共同社英语报纸](https://yiyangwang.us/2017-08-03/linfax-guide/3.jpg)
  ![JMH卫星云图](https://yiyangwang.us/2017-08-03/linfax-guide/4.jpg)
  ![气象传真0](https://yiyangwang.us/2017-08-03/linfax-guide/5.jpg)
  ![气象传真1](https://yiyangwang.us/2017-08-03/linfax-guide/6.jpg)
