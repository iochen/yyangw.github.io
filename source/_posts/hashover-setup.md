---
title: 在 Hexo 静态博客系统中安装 Hashover 评论系统
date: 2017-05-27 21:06:05
tags:
  - Network
  - Linux
---
Hexo作为一个很成熟的静态博客系统, 有着静态博客的众多优点，部署方便，反应迅速。但同时静态博客也有一个缺点——

  * 没有自带的评论系统

这篇文章就将介绍，如何搭建Hashover评论系统
<!-- more -->
可用的第三方评论系统在国内有多说，友言等，国外则有Disqus等。而今天这篇文章将主要面向想拥有自己评论系统的博主们。开源的评论系统，主要有:

  * Isso
  * Hashover

这两个，isso基于Python，数据库使用SQLite。这样的配置方案需要有独立的VPS才可以实现，而Hashover基于php，使用xml管理评论。这个博客也是采用了Hashover。~~其实是配置完isso，Nginx反代死活不成功，懒得折腾罢了~~
好啦，现在就进入Hashover的搭建教程

## 安装上传

  * 官方站点：[tildehash.com/?page=hashover](http://tildehash.com/?page=hashover)
  * GitHub项目：[github.com/jacobwb/hashover](https://github.com/jacobwb/hashover)
  * 下一代Hashover：[github.com/jacobwb/hashover-next](https://github.com/jacobwb/hashover-next)

从官网上面的介绍，目前的Hashover稳定版本为*1.0.2*，正在开发的版本为*2.0*，在这篇教程中使用的是*1.0.2*版，如果使用正在开发的*2.0*版也可以参考本教程，**大部分**配置基本相同。安装教程十分简单：
  * 官网下载[Hashover压缩包](http://tildehash.com/hashover.zip)然后在你的网站目录解压。
  * 赋予（chmod）“0644” 权限给站点所有文件（所有者可写，所有人可读）
  * 赋予 “0755” 权限给目录和PHP文件（所有人可读，所有者可写，可执行）
  * 赋予 "0777" 权限给 "hashover/pages" 目录（所有人可读，可写，可执行）
如果使用VPS，指令如下 假定 "站点根目录" 在 “/data/wwwroot/example/”，执行如下指令

``` bash
# chmod -R 0755 /data/wwwroot/example/
# chmod -R 0777 /data/wwwroot/example/hashover/pages
```

安装过程到此结束

## 配置

``` bash
# cd /data/wwwroot/example/ #进入站点根目录
# vi hashover/scripts/secrets.php
```

打开vi编辑器后，按 "i" 进入编辑模式，配置以下变量：

``` php
  $encryption_key = ' ';                       // 8 ~ 32 个字符设置加密密钥
  $notification_email = 'username@example.us'; // 通知新评论的电子邮件地址
  $admin_nickname = 'example';                 // 管理员昵称
  $admin_password = 'your_passwd';             // 管理员密码
```
按 ":" 之后输入 "wq" 保存并退出。
至此，配置结束。

## 在 Hexo 中使用Hashover

官网给出的JavaScript代码：

``` javascript
<script type="text/javascript" src="/hashover.php"></script>
<noscript>You must have JavaScript enabled to use the comments.</noscript>
```
官网给出的PHP代码：

``` php
<?php $mode = 'php'; include('hashover.php'); ?>
```

在相关网页中插入代码就可以使用 Hashover 评论系统了，在Hexo中配置如下：
进入Hexo目录，输入如下指令：

~~$ vi themes/landscape/layout/post.ejs~~

``` bash
$ vi themes/landscape/layout/_partial/article.ejs
```
打开vi编辑器后，按 "i" 进入编辑模式，在：

``` bash
</footer>
```

前面添加如下代码加载Hashover：

```
<% if (!index){ %>
  <script type="text/javascript" src="https://yiyangwang.us/hashover.php"></script>
  <noscript>You must have JavaScript enabled to use the comments.</noscript>
<% } %>
```

在 "example.us" 的位置填入hashover的**绝对路径**，然后按 ":" 之后输入 "wq" 保存并退出。
至此，Hexo中配置结束。

```
$ hexo g
```

然后上传至服务器就可以看到效果了~
