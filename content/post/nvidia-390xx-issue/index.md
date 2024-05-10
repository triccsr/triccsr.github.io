---
title : '低端局-nvidia又双叒叕坏了'
date : 2024-05-10T22:41:13+08:00
tag : 
    - 日常
    - archlinux
    - bug
    - 修电脑
draft : true
url : cae3365c
---
{{<admonition warning>}}
我真傻，真的。我单知道linux内核大更新可能导致显卡挂掉，我不知道内核小更新+gcc更新也会。Donec massa lacus, ultricies a ullamcorper in, fermentum sed augue. Nunc augue augue, aliquam non hendrerit ac, commodo vel nisi.Sed adipiscing elit vitae augue consectetur a gravida nunc vehicula. Donec auctor odio non est accumsan facilisis. Aliquam id turpis in dolor tincidunt mollis ac eu diam.
{{</admonition>}}

## 背景

插播LUG@NJU笑话一则:

> 是什么错觉让你觉得 ArchLinux 容易挂，是NVIDIA吗？

我在工位的古董台式用的显卡是NVS 315，普通的nvidia驱动不支持，用的驱动一直是aur里的nvidia-390xx-dkms。

我前一天晚上例行`# pacman -Syu`然后关机，今天早上开机发现卡在target reached graphical interface了，进不去图形界面，但按<kbd>Ctrl</kbd> + <kbd>Alt</kbd> + <kbd>F3</kbd>能进去终端。

考虑到原来也出现过类似问题，我立刻想到是nvidia驱动出了问题，`#journalctl -b`了下也确实是nvidia-uvm出了问题。

然后用手机查aur forum，发现不只我一个有这个问题，并且已经有大佬写好了patch，但是是以代码块渲染的方式呈现的，而不是文件。我只能`wget -np https://bbs.archlinux.org/viewtopic.php?id=295600`，然后手动找到patch的代码块。一个问题是引号`"`全变成了`\&quot;`，需要手动`sed`。

然后参考了[wiki的patch教程](https://wiki.archlinux.org/title/Patching_packages#Applying_patches)，makepkg，然后`# pacman -U NAME.tar.zst`。

