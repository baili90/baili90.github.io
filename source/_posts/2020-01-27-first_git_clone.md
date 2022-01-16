---
title: 记录第一次成功git-clone的过程
top: false
cover: false
toc: true
mathjax: true
date: 2020-01-27 00:15:11
password:
summary:
tags:
- git
categories:
- 技术
---
一直以来我都无法使用github，这个也就算了，解决方法不难。可是很多远程操作都无法执行，实在忍不下去了，网上设置git代理的方法看起来有些散，就自己记录一下过程吧～

<!-- more -->

1.查看localhost：
先吐槽一下这个`git config --global https.proxy http://127.0.0.1:1080`命令。
按照网上的资料还以为是需要代理服务器地址，后面才发现是要本机localhost。也怪我拿着就用，后面又折腾了好久如何取消。localhost可以用这个查看：

> $ nslookup localhost


2.查看监听端口：
在代理软件上查看自己的本地监听端口,要注意的是，http代理要使用http的监听端口。

3.配置git代理
这个时候可以使用你查到的localhost和端口来输入命令了，为了方便，也可以直接输入`local host:`后跟着你的端口号（下面`8001`是博主的端口号，不要照抄！）。

> $ git config --global http.proxy "localhost:8001"

> $ git config --global https.proxy "localhost:8001"

现在尝试`git clone`就能下载远程仓库了，终于成功，太感动了。
然后摸索了一下，发现不使用代理就无法使用`git clone`等操作，大概有了些推测但尚需深入学习，就不描述了。

4.取消代理：

> $ git config --global --unset http.proxy

> $   git config --global --unset https.proxy

之前错误了输入了一些别的，取消：

> $  git config --global --unset https.https://github.com.proxy

> $ git config --global --unset http.https://github.com.proxy

