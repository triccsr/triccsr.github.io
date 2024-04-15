---
title: ICPC2023 南京站 打星游寄(附M题题解)
tags: 
    - XCPC
    - 线段树
url: 86d723f2
date: 2023-11-05 18:00:55
math: true
---

## 摘要


> **BITTER LESSON**  
> C++ `std::map.insert()` **DOES NOT** insert the key value pair if an equivalent key already existed. [Example](https://www.geeksforgeeks.org/map-insert-in-c-stl/)
{.warning}

3 人，打星，6 题，还是寄。

[补题链接，需要私信 SUA-时庆钰要权限](https://qoj.ac/contest/1414)
没去现场赛的可以等 12 月 2 号的[ucup](http://ucup.ac/)

<!--more-->

## 题解

### M 接雨水 Trapping Rain Water

#### Problem

Given an integer sequence $a_1, a_2, \dots a_n\ (1 \leq n \leq 10^5)$, perform $q\ (1 \leq q \leq 10^5)$ modifications on the array above, the ith one increases $a_{x_i}$ by $v_i$. After each modification, calculate the value of:
$$\sum_{i=1}^n (\min(f_i,g_i)-a_i)$$

where

$$

\begin{gathered}
f_i=\max_{j=1}^i a_j \\
g_i=\max_{j=i}^n a_j
\end{gathered}
$$

#### Solution

分类讨论+线段树

$\sum_{i=1}^n (\min(f_i,g_i)-a_i)=\sum \min(f_i,g_i)-\sum a_i$

$\sum a_i$可以容易地用变量维护。难点在于维护$\sum \min(f_i,g_i)$，设其为$sum$。

不妨设$f_0=0,g_{n+1}=0$。每次修改形如$a_p+=v$，下文中的$a_p$都指更新后的值。

若$f_{p-1} \geq a_p \land g_{p+1} \geq a_p$，则$sum$不变。

若$f_{p-1} \geq a_p > g_{p+1}$，设$l=\max_{i\in[1,p-1]\land a_i \geq a_p} i, r=\argmax_{i=p+1}^n a_i$（即$l=p$前面第一个$a_i \geq a_p$的$i$，$r=a_{p+1},a_{p+2}\dots a_n$的最大值的下标），则$\forall i \in [l,p]\bigl(\min(f_i,g_i)=a_p\bigr)$，其他部分的$\min(f_i,g_i)$值不变。

若$f_{p-1}<a_p\leq g_{p+1}$同理。

若$f_{p-1}<a_p>g_{p+1}$，设$l=\argmax_{i=1}^{p-1} a_i, r=\argmax_{i=p+1}^n a_i$，则$\forall i \in [l,p-1]\bigl(\min(f_i,g_i)=a_l\bigr),\forall i \in [p+1,r]\bigl(\min(f_i,g_i)=a_r\bigr)$，同时$\min(f_p,g_p)=a_p$

可以发现上述操作都是对某个区间的$\min(f_i,g_i)$赋值，所以可用区间赋值区间和的线段树维护$\min(f_i,g_i)$

区间赋值的边界（即上文的$l,r$）只有两种情况：

1. 区间最大值坐标
2. 区间第一个/最后一个满足$a_i\geq v$的$i$

用线段树维护$a_i$，情况一就是区间最大值坐标，情况二在线段树上二分。

code:

```cpp
#include <bits/stdc++.h>
const int N = 1e5 + 11;
typedef long long LL;
const LL LLINF = 1e10;
using std::map;
int n;
LL a[N];
#define ls(x) ((x) << 1)
#define rs(x) (((x) << 1) | 1)
#define mid ((l + r) >> 1)
namespace S1 {
LL sum[N << 2], tag[N << 2];
void build(int l, int r, int now) {
  tag[now] = sum[now] = 0;
  if (l == r) return;
  build(l, mid, ls(now));
  build(mid + 1, r, rs(now));
}
void add_tag(int l, int r, int now, LL v) {
  tag[now] = v;
  sum[now] = v * (r - l + 1ll);
}
void push_down(int l, int r, int now) {
  if (l < r && tag[now] != 0) {
    add_tag(l, mid, ls(now), tag[now]);
    add_tag(mid + 1, r, rs(now), tag[now]);
  }
  tag[now] = 0;
}
void push_up(int now) { sum[now] = sum[ls(now)] + sum[rs(now)]; }
void interval_mask(int l, int r, int now, int st, int en, LL v) {
  if (st > en) return;
  if (st <= l && r <= en) {
    add_tag(l, r, now, v);
    return;
  }
  push_down(l, r, now);
  if (st <= mid) {
    interval_mask(l, mid, ls(now), st, en, v);
  }
  if (en > mid) {
    interval_mask(mid + 1, r, rs(now), st, en, v);
  }
  push_up(now);
}
LL interval_sum(int l, int r, int now, int st, int en) {
  if (st > en) return 0;
  if (st <= l && r <= en) {
    return sum[now];
  }
  push_down(l, r, now);
  LL ret = 0;
  if (st <= mid) ret += interval_sum(l, mid, ls(now), st, en);
  if (en > mid) ret += interval_sum(mid + 1, r, rs(now), st, en);
  return ret;
}
}  // namespace S1
namespace S2 {
std::pair<LL, int> mx[N << 2];
void build(int l, int r, int now) {
  mx[now] = std::make_pair(0, l);
  if (l == r) return;
  build(l, mid, ls(now));
  build(mid + 1, r, rs(now));
}
void push_up(int now) { mx[now] = std::max(mx[ls(now)], mx[rs(now)]); }
void modify(int l, int r, int now, int index, LL v) {
  if (index < l || index > r) return;
  if (l == r) {
    mx[now] = std::make_pair(v, l);
    return;
  }
  if (index <= mid) {
    modify(l, mid, ls(now), index, v);
  } else {
    modify(mid + 1, r, rs(now), index, v);
  }
  push_up(now);
}
std::pair<LL, int> interval_max(int l, int r, int now, int st, int en) {
  if (st > en) return std::make_pair(-LLINF, -1);
  if (st <= l && r <= en) {
    return mx[now];
  }
  auto ret = std::make_pair(-LLINF, -1);
  if (st <= mid) {
    ret = std::max(ret, interval_max(l, mid, ls(now), st, en));
  }
  if (en > mid) {
    ret = std::max(ret, interval_max(mid + 1, r, rs(now), st, en));
  }
  return ret;
}
int first_notless_index(int l, int r, int now, int st, int en, LL v) {
  if (st > en) return -1;
  if (l == r) {
    return (mx[now].first >= v) ? l : -1;
  }
  // pushdown()
  int ret = -1;
  if (st <= mid && mx[ls(now)].first >= v) {
    ret = first_notless_index(l, mid, ls(now), st, en, v);
  }
  if (ret != -1) return ret;
  if (en > mid) {
    return first_notless_index(mid + 1, r, rs(now), st, en, v);
  }
  return -1;
}
int last_notless_index(int l, int r, int now, int st, int en, LL v) {
  if (st > en) return -1;
  if (l == r) {
    return (mx[now].first >= v) ? l : -1;
  }
  // pushdown()
  int ret = -1;
  if (en > mid && mx[rs(now)].first >= v) {
    ret = last_notless_index(mid + 1, r, rs(now), st, en, v);
  }
  if (ret != -1) return ret;
  if (st <= mid) {
    return last_notless_index(l, mid, ls(now), st, en, v);
  }
  return -1;
}
}  // namespace S2

#undef ls
#undef rs
#undef mid
void myk(int idx, LL v) {
  S2::modify(1, n, 1, idx, v);
  int leftLastNotLess = S2::last_notless_index(1, n, 1, 1, idx - 1, v);
  int rightFirstNotLess = S2::first_notless_index(1, n, 1, idx + 1, n, v);
  if (leftLastNotLess != -1 && rightFirstNotLess != -1) {
    return;
  }
  S1::interval_mask(1, n, 1, idx, idx, v);
  if (leftLastNotLess == -1 && rightFirstNotLess == -1) {
    auto leftMax = S2::interval_max(1, n, 1, 1, idx - 1);
    if (leftMax.second != -1) {
      S1::interval_mask(1, n, 1, leftMax.second, idx - 1, leftMax.first);
    }
    auto rightMax = S2::interval_max(1, n, 1, idx + 1, n);
    if (rightMax.second != -1) {
      S1::interval_mask(1, n, 1, idx + 1, rightMax.second, rightMax.first);
    }
  } else if (leftLastNotLess == -1) {
    S1::interval_mask(1, n, 1, idx + 1, rightFirstNotLess - 1, v);
  } else if (rightFirstNotLess == -1) {
    S1::interval_mask(1, n, 1, leftLastNotLess + 1, idx - 1, v);
  }
}
void work() {
  scanf("%d", &n);
  S1::build(1, n, 1);
  S2::build(1, n, 1);
  LL suma = 0;
  for (int i = 1; i <= n; ++i) {
    scanf("%lld", &a[i]);
    suma += a[i];
    myk(i, a[i]);
  }
  int m;
  scanf("%d", &m);
  while (m--) {
    int x;
    LL v;
    scanf("%d%lld", &x, &v);
    a[x] += v;
    suma += v;
    myk(x, a[x]);
    LL ans = S1::interval_sum(1, n, 1, 1, n) - suma;
    printf("%lld\n", ans);
  }
}
int main() {
  int T;
  scanf("%d", &T);
  while (T--) {
    work();
  }
  return 0;
}
```

## 游寄

### Day1 热身赛

NUAA 江宁，地铁来回，校园巴士和 HIT 的一样。

衣服不错，上面的 floyd 代码是对的。

发了三只袋鼠，两银一灰锡。

中文题面，四道袋鼠原题。去年打南京站的时候卡袋鼠卡死，今年在热身赛上 AC 了去年的袋鼠，发现代码其实挺短的。

晚上回到学校收到短信，要求正式赛前全员补照队伍照片。

### Day2 正式赛

6:30 醒了睡不着了，吃了个金拱门，8 点南门打车。

带了 Claris 的板子和[qkoqhh 大佬](https://qkoqhh.github.io/)的[没有思考，没有灵感，扎爆气球板子](https://github.com/qkoqhh/ACM-template)，然后在比赛现场活捉了 qkoqhh 大佬。

由于队员人数增加到了 3 个，我无法全面复盘比赛情况。占坑。

开场我第一个看的 M，感觉是个可做的数据结构，但没想好怎么做。然后看榜有人过 I，zzq 看 I，自己接着想 m。

然后发现 M 还是没人过，倒是 G 过了不少人。我放下 M 和 xmj 看 G,~~过了亿会~~两人~~同时~~想出 G 的做法，然后 xmj 去写 G。

此时 zzq 已经 AC 了 I 在想 C，并且已经有了不少思路。我按照 zzq 的思路往下想想出了 C 的做法，然后我去写 C。由于~~我太菜了~~C 题的细节较多，我 wa 了一发并且调了很长时间才 AC，机时罚时两开花。

我写 C 的过程中队友们想出了 A 的做法，最终 AC。

然后我和 zzq 接着想 M，中途发现 L 过的比 M 多然后 zzq 去和 xmj 想 L。M 是数据结构，而队友们说 L 代码较简单，优先写 L。LM 双线程并行，L 先 AC。

我写完 M 时离比赛结束只剩 20min 了，由于线段树写假了一度过不去样例，样例通过后 WA 了一发。队友们提供了一组样例卡掉了我的代码，然后三人一起 gdb 调试，发现问题出在`std::map.insert(std::make_pair(k,v))`当`k`已经在`map`里时不会更新`map[k]=v`。但此时离比赛结束只剩 1min，最终没能改完。(update on 2023.11.08 改完也没用，做法假了)
