---
title: 高端局-修复archlinux网络
tags:
  - 日常
  - archlinux
abbrlink: b5a75f7a
date: 2024-03-11 21:50:06
---

## 摘要
archlinux没有设置休眠，但误点休眠键后无法唤醒电脑，只能长按电源键关机。再次开机后发现有线网络一直显示connecting但一直连不上。

执行`# systemctl status dhcpcd`发现dhcpcd.service not found。

使用安装了archlinux镜像的u盘archroot挂载原来的根目录重新安装dhcpcd包，问题解决。

~~fuck you kde, fuck you nvidia~~:rage:
## 起因