---
title: Mac汇编环境配置及自动挂载
top: false
cover: false
toc: true
mathjax: true
date: 2021-02-11 13:31:14
password:
summary:
tags:
- 计算机基础
categories:
- 技术
---

前言：每次使用DOSBox都要挂载一遍，故记录自动挂载方法。
<!--more-->

1.下载：在官网安装DOSBox，masm5（你可以放在任意文件夹，但要知道具体放在了哪里）

2.挂载：
1. 打开DOSBox，输入 mount c （注意c后面有空格）,然后跟上你masm5的文件目录，如果成功就会出现`Z：\>C:`，如果提示找不到文件，就再检查下文件目录写对没有。
> 例：mount c ～/desktop/DOSBOX/masm5
我是将masm5放在了桌面的DOSBOX文件夹里（～代表mac用户目录，就可以不用写/USers/xxx那一串）。
2. 输入 `c：`
3. 输入`debug`（只是打开debug这样的一个程序，你的程序名未必叫debug，可以直接进入masm5等汇编开发工具中查看程序名）
4. 让我们输入 `u `查看一下配置好了没有，如图说明已经可以使用了。
![1](/img/one.png)
3.设置初始登陆配置：这个时候，我们已经可以开始写汇编程序了，但是每次打开DosBox都需要重新挂载（即第二节中的1.2.3步），所以现在设置一下。
Mac的DOSBox配置文件在~/Library/Preferences/DOSBox 0.74 Preferences（注意！一定不要找错了。）在文件最下面有
![tip](/img/tip.png)
可以看到提示让你挂载，这个时候输入前文第一、二步中的命令，注意大小写不要错了。这里就相当于软件每次启动自己执行这两步，不需要你手动输入了。
配置好后重新打开DOSBox，如图，可以敲下debug后使用了～

![2](/img/2.png)

