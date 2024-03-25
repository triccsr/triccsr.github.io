---
title: cmake的奇怪问题
tags:
  - bug
  - c++
abbrlink: 8aacde4
date: 2024-03-26 00:22:30
---


若一个library `A_LIB`中只有头文件，即使`CMakeLists.txt`中加入了`target_link_libraries(A_LIB ... B_LIB)`，`#include SOME_HEADER_IN_B_LIB`时也会报错 missing headers。

解决方法：在`A_LIB`中加入一个空`.cpp`文件。

一个有趣的问题是在clion下不会报这个错，但使用vscode+clangd+cmake会报错。
