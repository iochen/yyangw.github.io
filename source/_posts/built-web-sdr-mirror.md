---
title: 搭建了一个共享sdr镜像站点
date: 2017-07-20 19:30:03
tags:
  - Linux
  - Network
---
## [sdr.hu](http://sdr.hu/)
在这个站点上面有来自全世界各地的在线sdr，但是其中大部分服务器都在国外，访问不稳定。同时不支持https，信息容易泄露。博主搭建了一个镜像站点。
  ![](https://yiyangwang.us/2017-07-20/built-web-sdr-mirror/0.jpg)
<!-- more -->

原始站点: [126.109.222.21:8073](http://126.109.222.21:8073)
镜像站点: [jpsdr.yiyangwang.us](https://jpsdr.yiyangwang.us)

## 一点小问题

原始站点使用http协议，镜像站点也就是博主的服务器nginx没有编译 ngx_http_substitutions_filter_module 模块，所以有一个请求还是基于http，需要加载不安全的脚本才可以使用。

## 承诺

 * 不会收集用户信息
 * 不会修改原始站点的内容

## 今天使用镜像站点收的几张JMH气象传真

  ![](https://yiyangwang.us/2017-07-20/built-web-sdr-mirror/1.jpg)
  ![](https://yiyangwang.us/2017-07-20/built-web-sdr-mirror/2.jpg)