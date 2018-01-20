---
title: 在 Fedora 系统下使用 wine 运行KG-FAX接收气象传真
date: 2017-07-08 13:24:52
tags:
  - Network
  - Linux
---
## 气象传真
世界各地气象部门经常利用无线电发送气象传真，为在海上航行的船只提供帮助，过去需要使用专业的气象传真接收机才可以接收，而SDR的出现，使得只要使用一台计算机和一个SDR接收机就可以接收气象传真。

  ![ ](https://yiyangwang.us/2017-07-08/receive-jmh-fax-on-fedora/6.jpg)
  
<!-- more -->
## 下载相关软件

由于市区无线电干扰比较严重，使用SDR接收机比较困难，故这次使用在线SDR接收机来接收气象传真。首先，访问：

  [http://www2.plala.or.jp/hikokibiyori/soft/kgfax/](http://www2.plala.or.jp/hikokibiyori/soft/kgfax/)

下载 KG-FAX 作为日本JMH气象传真的解调软件。将下载的安装包解压，然后使用wine打开，如官网图片所示：

  ![ ](https://yiyangwang.us/2017-07-08/receive-jmh-fax-on-fedora/7.jpg)

接下来单击“详细设定”旁边的那个按钮，选择“Monitor of 内置音频模拟立体声”。但是右上角还是没有任何信号，这是因为还没有打开SDR。

## 在线SDR

这次使用在线SDR接收，访问：

  [http://sdr.hu/](http://sdr.hu/)

挑选在线SDR，每一个SDR都有标记信息以及地理位置。
然后访问NOAA的站点下载[这份](http://www.nws.noaa.gov/os/marine/rfax.pdf)PDF，上面有全球范围气象传真的频率以及时间表，传送门:

  [http://www.nws.noaa.gov/os/marine/rfax.pdf](http://www.nws.noaa.gov/os/marine/rfax.pdf)

在第 II-1 页就找到了日本JMH的气象传真频率。气象传真使用 USB 制式，实际解调频率低于公布频率 1.9 Khz。例如：接收JMH4 13988.5 Khz的频率，需要13988.5 Khz - 1.9 Khz = 13986.6 Khz，在SDR中输入这个频率，单击“USB”，就可以接收JMH气象传真的信号了。

## KG-FAX

回到KG-FAX，单击右边第一个按钮，然后单击右边第二个按钮，选择自动保存的目录，接下来单击第三个按钮，使信号同步。当KG-FAX接收到启动信号时，第一个按钮就会被按下，然后开始解调。

## 博主接收到的一些图片

  ![萌妹纸](https://yiyangwang.us/2017-07-08/receive-jmh-fax-on-fedora/0.jpg)
  ![时间表](https://yiyangwang.us/2017-07-08/receive-jmh-fax-on-fedora/1.jpg)
  ![ ](https://yiyangwang.us/2017-07-08/receive-jmh-fax-on-fedora/2.jpg)
  ![ ](https://yiyangwang.us/2017-07-08/receive-jmh-fax-on-fedora/3.jpg)
  ![ ](https://yiyangwang.us/2017-07-08/receive-jmh-fax-on-fedora/4.jpg)

最后祝大家玩的开心~
如果有疑问可以在下方留言给我

## 版权

授权 “电波之旅” 微信公众号转载
