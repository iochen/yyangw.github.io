---
title: Fedora 中使用 CloudFlare 实现 Dynamic DNS (动态DNS) 解析
date: 2017-06-08 11:50:05
tags:
  - Network
  - Linux
---
## Dynamic DNS 的作用
Dynamic DNS提供了一个轻量化机制，让本地DNS数据库可以即时的更新。它能把互联网域名指往一个可能经常改变的IP地址，让经常改变位置及配置的设备，能够持续性的更新IP地址。令互联网上的外界用户可以通过一个大家知道的域名，连接到一个可能经常动态改变IP地址的机器。其中一个常用的用途是在使用动态IP地址连接（例如在每次接通连接就会被分配一个新的IP地址的拨号连接，或是偶尔会被ISP变更IP地址的DSL连接等）的电脑上运行服务器软件。

  * ![ ](https://yiyangwang.us/2017-06-08/cloudflare-set-dynamic-dns/3.jpg)

<!-- more -->
## 使用 [ddclient](https://sourceforge.net/projects/ddclient/) 配置基于 Cloudflare 的 Dynamic DNS

首先，下载位于[SourceForge](https://sourceforge.net)的ddclient，地址如下：

``` bash
https://sourceforge.net/projects/ddclient/
```

点击"Download"即可下载，然后解压至任意目录，执行如下指令：

``` bash
$ cd /PATH TO DDCLIENT/                                      # 进入解压的目录
$ cp ddclient /usr/sbin/                                     # 拷贝文件
$ mkdir /etc/ddclient                                        # 创建目录
$ mkdir /var/cache/ddclient                                  # 创建目录
$ cp sample-etc_ddclient.conf /etc/ddclient/ddclient.conf    # 拷贝配置文件
```

接下来登入[CloudFlare](https://www.cloudflare.com)，访问[https://www.cloudflare.com/a/account/my-account](https://www.cloudflare.com/a/account/my-account)然后找到"API Key"，点击第一个"Global API Key"后面的"View API Key"查看并复制保存 API Key

  * ![Global API Key](https://yiyangwang.us/2017-06-08/cloudflare-set-dynamic-dns/0.jpg)

然后访问[https://www.cloudflare.com/login](https://www.cloudflare.com/login)，进入控制页面，切换到"DNS"一栏，新建一个A记录，"name"自定义为要分配给DDNS的名称，ip随意填写。

  * ![Global API Key](https://yiyangwang.us/2017-06-08/cloudflare-set-dynamic-dns/1.jpg)

然后输入如下指令编辑配置文件：

``` bash
vi /etc/ddclient/ddclient.conf
```

找到"ssl"这一行，确认值为"yes"

``` bash
ssl=yes
```

找到"use=web"这一行，去掉注释，替换：

``` bash
use=web, web=checkip.dns.he.net/, web-skip='IP address' # found after IP Address
```

找到"## CloudFlare (www.cloudflare.com)"这一行，内容如下：

``` bash
##
## CloudFlare (www.cloudflare.com)
##
protocol=cloudflare,        \                # 这里不用管
zone=example.us,            \                # 填写自己的域名
server=www.cloudflare.com,  \                # 这里不用管
login=mail@example.us,     \                 # 注册 CloudFlare 时的邮箱
password=cloudflare-api-key             \    # CloudFlare 的 Api Key
example.example.us                           # 分配给DDNS的域名
```

接下来按"ESC"输入":wq"保存并退出
尝试输入如下指令：

``` bash
$ ddclient -daemon=0 -debug -verbose -noquiet
```

如果看到如下输出则配置成功：

``` bash
DEBUG:    proxy  = 
DEBUG:    url    = checkip.dns.he.net/
DEBUG:    server = checkip.dns.he.net
CONNECT:  checkip.dns.he.net
CONNECTED:  using HTTP
SENDING:  GET / HTTP/1.0
SENDING:   Host: checkip.dns.he.net
SENDING:   User-Agent: ddclient/3.8.3
SENDING:   Connection: close
SENDING:   
RECEIVE:  HTTP/1.1 200 OK
RECEIVE:  Date: Thu, 08 Jun 2017 03:52:53 GMT
RECEIVE:  Server: Apache/2.4.18 (Ubuntu)
RECEIVE:  Vary: Accept-Encoding
RECEIVE:  Content-Length: 204
RECEIVE:  Connection: close
RECEIVE:  Content-Type: text/html; charset=UTF-8
RECEIVE:  
RECEIVE:  <!DOCTYPE html>
RECEIVE:  <html>
RECEIVE:  <head>
RECEIVE:   <meta http-equiv="Content-Type" content="text/html;charset=utf-8" />
RECEIVE:   <title>What is my IP address?</title>
RECEIVE:  </head>
RECEIVE:  <body>
RECEIVE:  Your IP address is : *your-ip*</body>
RECEIVE:  </html>
DEBUG:    get_ip: using web, checkip.dns.he.net/ reports *your-ip*
SUCCESS:  0.yiyangwang.us: skipped: IP address was already set to *your-ip*.
```

  * ![最终成果](https://yiyangwang.us/2017-06-08/cloudflare-set-dynamic-dns/2.jpg)

祝大家玩的开心~
