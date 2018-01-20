---
title: 接收上海海岸电台气象传真
date: 2017-07-24 16:14:05
tags:
  - Linux
---
博主在位于北京丰台南苑的家中面对瀑布图，发现了一个奇怪的气象传真信号，于是开始了一番搜寻，且听我慢慢道来...

  ![ ](https://yiyangwang.us/2017-07-24/receive-shanghai-radio-fax/0.jpg)

<!-- more -->
## Day 1

7月22日上午，博主来到北京南苑的家中，重新开始使用期中之后就在睡觉的SDR。面对瀑布图，我发现在20.5Mhz附近的一个奇怪的气象传真信号，便打开KG-FAX，同时在NOAA的气象传真频率表中查找，一无所获。然而图片只收了一半，而且图片发送完毕后信号就消失了，由于没有时间表，只能放弃。
下午，听完朝鲜之声之后，在8.3Mhz附近再次发现这个奇怪的气象传真，便打开KG-FAX，由于使用rtl-sdr接收，14.4Mhz两边镜像，zjveal分析上午的20.5Mhz是镜像，他的PCR1000也印证了这一点。但这次图片也不完整，博主开始Google，发现了[这样](http://t.m.china.com.cn/convert/c_mBBMj3.html)一篇新闻“[中国首套海上无线电气象传真系统投入试运行](http://t.m.china.com.cn/convert/c_mBBMj3.html)”，传送门：[http://t.m.china.com.cn/convert/c_mBBMj3.html](http://t.m.china.com.cn/convert/c_mBBMj3.html)。
结合信号强度以及频率，于是博主致电上海海岸电台，成功要到了时间和频率表，如下
频率：（kHz）

  * 4170
  * 8302
  * 12382
  * 16559

时间（试运行阶段），UTC+8

  * 09:30
  * 10:00
  * 10:30
  * 11:00
  * 13:30
  * 14:00
  * 14:30
  * 15:00

## Day 2

在今天（7.23.2017），成功接收上海海岸电台气象传真，图片如下，感谢zjveal提供：

  ![ ](https://yiyangwang.us/2017-07-24/receive-shanghai-radio-fax/1.jpg)
  ![ ](https://yiyangwang.us/2017-07-24/receive-shanghai-radio-fax/2.jpg)

接收地点：江苏镇江
接收设备：Icom PCR1000

## The End

通过进一步Google，博主发现早在1974年10月，中国已经拥有了自己的气象传真广播——北京气象传真广播，呼号为BAF。然而博主最后找到的关于BAF的记载却截止在1990年代。然而无论如何，BAF才是真正的“首家”气象传真广播，新闻却报道上海海岸电台为“首家”气象传真广播。具体背后的原因，却不为人知

最后，祝大家玩的开心~