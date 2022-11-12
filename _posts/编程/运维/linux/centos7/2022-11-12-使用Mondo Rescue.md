---
layout: article
title: 使用Mondo Rescue
mathjax: true
---
参考博客  https://my.oschina.net/u/4113630/blog/4524807

Mondo Rescue 的安装

```shell
1.cd /etc/yum.repos.d

2.wget ftp://ftp.mondorescue.org/centos/7/x86_64/mondorescue.repo

3.将gpgcheck=0

 more mondorescue.repo

[mondorescue]

name=centos 7 x86_64 - mondorescue Vanilla Packages

baseurl=ftp://ftp.mondorescue.org//centos/7/x86_64

enabled=1

gpgcheck=0

gpgkey=ftp://ftp.mondorescue.org//centos/7/x86_64/mondorescue.pubkey

4.yum install mondo

root用户下输入mondoarchive，然后就都是图形操作了
```



图形界面参考 上面的链接

打包成ISO镜像后  使用Xftp传出到相应目录

使用此镜像做系统时  在boot 命令行界面输入nuke 即可恢复系统


