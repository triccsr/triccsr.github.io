---
title: 高端局-修复archlinux网络
tags:
  - 日常
  - archlinux
abbrlink: b5a75f7a
date: 2024-03-11 21:50:06
---

## 摘要

{%note danger%}
### BITTER LESSON

若在linux下手滑点到休眠键，**不要手动关机，等机器自己关**。

没配置休眠的结果最多是正在进行的任务丢失，但此时手动关机可能导致系统损坏。

{%endnote%}

archlinux没有设置休眠，但手滑点到了休眠键，于是长按电源键关机。**（危险操作，请勿模仿）**

再次开机后发现有线网络一直显示connecting但一直连不上。

执行`# systemctl status dhcpcd`发现unit dhcpcd.service not found。

使用安装了archlinux镜像的u盘archroot挂载原来的根目录重新安装dhcpcd包，问题解决。

~~Fuck you kde, fuck you nvidia~~:rage:

<!--more-->

## 起因
