---
title: Node.js项目部署到Linux
top: false
cover: false
toc: true
mathjax: true
date: 2021-04-25 16:06:39
password:
summary:
tags:
- 后端
- Node.js
categories:
- 技术
---
前言：使用此文前提是已经完全做好了一个本地的Node.js项目，现在只差部署到服务器。
<!--more-->

### 一、服务器准备：

服务器需要有Node环境，配置方法见[Linux上安装node.js](https://www.qianshibuwang.cn/2020/04/25/Linux上安装node-js/)



### 二、安装依赖：

进入项目根目录，输入：

> $ npm install

这个时候已经可以像在本地运行一样，运行服务器上的项目了，输入：

> $ node app.js

在浏览器打开：<ip>:<port>就可以看到了，和本地一模一样～

（最好测试一下，理由详见后文。）

但是一旦退出进程就看不到项目了，因此需要将目标文件永久启动。



### 三、使用pm2:

为了让项目随时随地可以浏览，这里选用了强大的pm2。

首先安装：

> $ npm install pm2 -g

安装好后别忘了创建软连接，不然使用pm2会找不到命令(不要照抄，路径不同。)

> $ ln -s /root/node-v14.0.0-linux-x64/bin/pm2 /usr/bin/pm2

现在可以使用pm2启动文件了(记得进入项目根目录)～

> $ pm2 app.js

![pm2](/img/pm2.png)

这个页面真是可爱



### 四、pm2的端口不监听问题

现在打开浏览器，并不会有预期的项目。但是使用node自己的启动方式，比如npm start和node app.js启动时，却发现程序可以访问。

查看原因：

node端口是否监听

> $ netstat -ntlp                   //比如node运行端口为3000，通过netstat -ntlp发现这个端口并未被监听

原来是通过pm2启动项目端口未被监听，而在这个项目中，start能启动监听是因为运行了

![startload](/img/startload.png)
然后直接简单粗暴的把启动文件也运行了：

> $ pm2 start bin/www



现在再来打开浏览器，随时随地都可以欣赏自己的项目了，大功告成～～～