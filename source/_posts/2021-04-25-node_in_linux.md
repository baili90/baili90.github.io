---
title: Linux上安装node.js
top: false
cover: false
toc: true
mathjax: true
date: 2021-04-25 14:18:13
password:
summary:
tags:
- Linux
categories:
- 技术
---
前言：此篇博文用的直接部署方法，简单好懂。
<!-- more -->


#### 1.安装wget

> $ yum install -y wget

如果已经安装了可以跳过该步



#### 2.下载nodejs最新的bin包

可以在下载页面https://nodejs.org/en/download/中找到下载地址。然后执行指令：

> $ wget https://npm.taobao.org/mirrors/node/v14.0.0/node-v14.0.0-linux-x64.tar.xz

这里注意选择合适的版本，比如linux的64位版本就无法在32位系统上运行。



#### 3.解压安装包

依次执行

> $ xz -d node-v14.0.0-linux-x64.tar.xz
> $ tar -xf node-v14.0.0-linux-x64.tar



#### 4. 部署bin文件

这一步相当于建立了一个链接。

先确认node.js的路径，我是在根目录下载解压的。确认后依次执行

> $ ln -s ~/node-v14.0.0-linux-x64/bin/node /usr/bin/node
> $ ln -s ~/node-v14.0.0-linux-x64/bin/npm /usr/bin/npm
>
> $ ln -s ~/node-v14.0.0-linux-x64/bin/node /usr/local/bin/node
> $ ln -s ~/node-v14.0.0-linux-x64/bin/npm /usr/local/bin/npm

在这里，如果之前有安装过node而没有卸载干净，可能会报错如：

> -bash: /usr/local/bin/node: No such file or directory

进入 `/usr/local/bin/`把`node`删除了就好，其余报错同理 。



#### 5.测试

> $ node -v
> $ npm

如果正确输出版本号，则部署完成。