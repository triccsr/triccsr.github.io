---
title: cmake的奇怪问题
tags:
  - bug
  - c++
url: 8aacde4
date: 2024-03-26 00:22:30
---
## 问题

若一个library `A_LIB`中只有头文件，即使`CMakeLists.txt`中加入了`target_link_libraries(A_LIB ... B_LIB)`，`#include SOME_HEADER_IN_B_LIB`时也会报错 missing headers。

解决方法：在`A_LIB`中加入一个空`.cpp`文件。

一个有趣的问题是在clion下不会报这个错，但使用vscode+clangd+cmake会报错。

~~So fuck vscode+clangd+cmake~~

<!--more-->

## 参考资料

[Working on a header-only library with cmake](https://www.reddit.com/r/cpp_questions/comments/qabln0/working_on_a_headeronly_library_with_cmake_and/)

截止到2024.3.26的最高赞回答，作者[the_poope](https://www.reddit.com/user/the_poope/):

>"This is a well-known 'problem'. Cmake creates a compilation database for each file that is compiled - but header files are not compiled directly, they are just included in files that are compiled. In fact you could in principle include the header file in different files that are compiled very differently.
>Anyway, the solution is to add a post-processing step that adds the header files to the generated .json using e.g. compdb.
>See https://stackoverflow.com/questions/68401578/youcompleteme-c-not-finding-headers-using-compile-commands-json 
>and many other posts and guides."

我选择了第二高赞的更加简单粗暴的做法，作者[Nihili0](https://www.reddit.com/user/Nihili0/)

>"Try to put some tests that include your headers and `add_executable`/"
>
>"You don't have to do anything, just a main and include them.
>Also it could be a good idea to include each headers in separate files to compile them in isolation."