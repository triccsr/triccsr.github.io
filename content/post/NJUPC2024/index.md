---
title : 'NJUPC2024 游寄'
date : 2024-05-06T22:06:40+08:00
draft : true
url : f22cd019
math : true
---
个人赛，4h。
## A
卡读入的模拟
## B
纯纯的签到
## C
### Problem
选择m个端点为1到n的整数的区间，使得满足条件：
- $l_i \leq r_i\text{ s.t.}\ i \in [1,m]$
- $\nexists i,j\in[1,m]\text{ s.t. }l_i\leq l_j\leq r_j\leq r_i$
问方案数。

### Sol

$\Theta(n)$的做法：问题转化为在值域$[1,n]$上选两个长度为m的序列，使得$l_i<l_{i+1},r_i<r_{i+1}\ i\in[1,m]$。然后枚举有多少个$l_i=r_j$的点，设有k个，然后剩下的$2m-2k$个数的坐标两两不同，每个括号序列代表一种$l$序列和$r$序列的分配方式，$\tbinom{n}{2m-2k}\cdot Catalan(m-k)$。

$\Theta(1)$的做法：折线法，不会。

## D

