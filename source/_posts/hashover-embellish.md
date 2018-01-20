---
title: Hashover 美化教程
date: 2017-05-30 19:28:18
tags:
  - Network
  - Linux
---
在之前的[文章](https://yiyangwang.us/2017-05-27/hashover-setup/)中已经介绍了Hashover以及搭建的方法，那么在这篇文章中将介绍使用[GIMP](https://zh.wikipedia.org/zh-hans/GIMP)编辑Hashover中的图片（例如icon）对Hashover进行美化。
<!-- more -->
Hashover的目录结构是这样的：
``` bash
hashover/
├── changelog.txt
├── comments.css
├── GNU\ Affero\ General\ Public\ License.txt
├── html-templates
│   └── default.html
├── images
│   ├── avatar.png
│   ├── bubble-tick.png
│   ├── bubble-tick-reply.png
│   ├── delicon.png
│   ├── edit.png
│   ├── email.png
│   ├── first-comment.png
│   ├── has-email.png
│   ├── liked.png
│   ├── like.png
│   ├── login.png
│   ├── name.png
│   ├── no-email.png
│   ├── password.png
│   ├── place-holder.png
│   ├── rss.png
│   └── website.png
├── pages
├── scripts
│   ├── deletion_notice.php
│   ├── encryption.php
│   ├── global_variables.php
│   ├── javascript-mode.php
│   ├── like.php
│   ├── locales.php
│   ├── parse_comments.php
│   ├── php-mode.php
│   ├── read_comments.php
│   ├── rss-output.php
│   ├── secrets.php
│   ├── settings.php
│   ├── urlwork.php
│   └── write_comments.php
└── template.xml
```
评论框的icon都在hashover/images/目录下，如图所示：

  * ![Hashover](https://yiyangwang.us/2017-05-30/hashover-embellish/0.jpg)

分辨率均为 45*45 ，修改是裁剪至相应分辨率即可。
那么，我们开始编辑美化图标吧~

  * ![原图](https://yiyangwang.us/2017-05-30/hashover-embellish/1.jpg)

打开GIMP编辑，裁剪图像，然后为新的图像起一个文件名

  * ![GIMP](https://yiyangwang.us/2017-05-30/hashover-embellish/2.jpg)

最终效果：

  * ![icon0](https://yiyangwang.us/hashover/images/icon0.png)

然后上传至 hashover/images/
``` bash
cd /PATH TO YOUR WWWROOT/    //进入站点根目录
vi hashover.php              //编辑 hashover.php
```
输入 "//avatar.png" 找到用户留言时的图标，按 "i" 进入编辑模式，替换成重新上传的图片的路径，按 "ESC"，输入 ":wq" 写入并保存。
刷新一下网页，效果就出来了~
以此类推，就可以编辑Hashover的其他图标

  * "delicon.png" 被 "hashover/scripts/deletion_notice.php" 引用
  * "first-comment.png" 被 "javascript-mode.php" 以及 "php-mode.php" 引用

祝各位玩的开心~