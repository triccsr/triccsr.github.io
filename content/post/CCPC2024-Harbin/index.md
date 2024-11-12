---
title : 'CCPC 2024 哈尔滨站 战犯寄录'
date : 2024-10-20T20:04:03+08:00
draft : false
url : 947b0acb
math: true
tags: 
    - XCPC
---

## 摘要

{{<admonition type=warning title="战犯寄语">}}
有返回值的函数必须return一个值，否则可能RE。
{{</admonition>}}

[补题链接](https://contest.ucup.ac/contest/1817?v=1)

3人场，~~队友过了~~7题，~~我只负责贡献罚时~~

大佬们只需要负责A题就行了，而战犯要考虑的可就多了。

以游客的视角参观自己生活了十多年的地方，但体验不怎么好。

## 题解（待续）

### L. A Game On Tree


给定一棵$n$个节点的树，边权都为1。两个人分别从树上的$\frac{n(n-1)}{2}$条路径中等概率随机选择一条，求两条路径的交的长度平方的期望。


#### 某菜鸡的补题做法

力大砖飞的树形dp。对于树上任意节点$u$，维护$u$子树内的点到$u$的所有长度$\geq 1$的“半路径”的0次项、1次项和2次项。将$u$的儿子$v$合并至$dp_u$时拼接两者内部的“半路径”。特判直上直下的路径。

（虽然强大的fyc认为这种维护多项式+拼接路径的做法没前途，但这做法确实能过）

两人的路径等概率选择，情况数有限。首先将期望转化为方案数。

对于每条从$w$到$u$的“半路径”（其中$u$为$w$的祖先），设其常数为$\sum_{x,y\in \mathrm{subtree}(w)}[\mathrm{LCA}(x,y)=w]$，记半路径$h$的常数为$k(h)$。k可以通过一个简单的dp求出。

对于终点同为点$u$且没有公共边的两条“半路径”$h_1$和$h_2$，路径$h_1+h_2$对总方案数的贡献为$k(h_1)\cdot k(h_2)\cdot (h_1+h_2)^2$。

按照正常的树上dp流程，对于每个节点$u$枚举儿子$v$，用$dp_v$更新全局答案和$dp_u$。则对全局答案的贡献为（下面的$\mathrm{subtree}(u)$为当前已加入的部分子树）：

$$
\begin{align*}
\Delta ans &=\sum_{h_1\in \mathrm{subtree}(u)}\sum_{h_2 从\mathrm{subtree}(v)到u}k(h_1)\cdot k(h_2)\cdot(\mathrm{len}(h_1)+\mathrm{len}(h_2))\\\\ 
&= \sum_{h_1\in \mathrm{subtree}(u)} k(h_1) \sum_{h_2 从\mathrm{subtree}(v)到u}k(h_2)\cdot(\mathrm{len}(h_1)+\mathrm{len}(h_2))\\\\
&= \sum k(h_1)\bigl(\sum k(h_2)\cdot \mathrm{len}^2(h_2)\bigr)+\sum k(h_2)\bigl(\sum k(h_1)\cdot \mathrm{len}^2(h_1)\bigr)+2(\sum k(h_1)\cdot \mathrm{len}(h_1))(\sum k(h_2)\cdot \mathrm{len}(h_2))
\end{align*}
$$

完美拆成了两部分的0次、1次、2次项形式。

代码：

```cpp
#include <bits/stdc++.h>
using namespace std;
typedef long long LL;
#define int long long 
const int N=1e5+11;
const LL MOD=998244353;
int n;
vector<int> e[N];
LL dp[N][3];//dp[u][i]表示u节点子树内所有到u的边非空“半路径”的i次项的和
LL sz[N],ss[N];
LL ksm(LL a,LL x){//求逆元
    LL ret=1;
    a=(a%MOD+MOD)%MOD;
    while(x){
        if(x&1)ret=ret*a%MOD;
        a=a*a%MOD;
        x>>=1;
    }
    return ret;
}
void dfs_pre(int now,int fa){//求k
    sz[now]=1;
    ss[now]=0;
    for(int to:e[now]){
        if(to==fa)continue;
        dfs_pre(to,now);
        sz[now]+=sz[to];
        ss[now]+=sz[to]*sz[to]%MOD;
    }
    ss[now]%=MOD;
}
void dfs(int now,int fa,LL &ans){
    memset(dp[now],0,sizeof(dp[now]));
    for(int to:e[now]){
        if(to==fa)continue;
        dfs(to,now,ans);
        LL t[3];
        t[0]=dp[to][0];
        t[1]=(dp[to][1]+dp[to][0])%MOD;
        t[2]=(dp[to][2]+2ll*dp[to][1]+dp[to][0])%MOD;//t[0...3]所有半路径的长度+1
        for(int i=0;i<3;++i){//加入v到u的“半路径”
            t[i]=(t[i]+sz[to]*sz[to]%MOD-ss[to])%MOD;
        }
        LL tmp=t[0]*dp[now][2]%MOD+dp[now][0]*t[2]%MOD+2ll*t[1]*dp[now][1]%MOD;
        tmp+=((n-sz[to])*(n-sz[to])%MOD-ss[now]+sz[to]*sz[to]%MOD-(n-sz[now])*(n-sz[now])%MOD)%MOD*t[2];
        ans+=tmp%MOD;
        for(int i=0;i<3;++i){
            dp[now][i]=(dp[now][i]+t[i])%MOD;
        }
    }
}
void work(){
    cin>>n;
    for(int i=1;i<=n;++i){
        e[i].clear();
    }
    for(int i=0;i<n-1;++i){
        int u,v;
        cin>>u>>v;
        e[u].push_back(v);
        e[v].push_back(u);
    }
    LL ans=0;
    dfs_pre(1,0);
    dfs(1,0,ans);
    ans=(ans%MOD+MOD)%MOD;
    LL ii=ksm(1ll*n*(n-1)/2ll,MOD-2);
    cout<<ans*ii%MOD*ii%MOD<<"\n";
}
signed main(){
    int T;
    cin>>T;
    while(T--){
        work();
    }
    return 0;
}
```

#### 强大的fyc的考场做法

考虑到所有边的边权都为1，路径长度的平方可以转化为路径上的点对数量-路径上的边数量。点对数量可以换根dp，边数量普通dp。

## 游记

### Day -1, Thu

12点从和园出发，3点半的飞机，18点到哈尔滨。坐机场大巴快线直达哈尔滨火车站，Dew买成了有经停站的1号线。

打车去我妈单位，在单位附近吃砂锅。

### Day 0, Fri

中午吃了博物馆松雷上面的老厨家，酸菜不酸，锅包肉也不够酸，地三鲜不咸，评价为假东北菜。（不过往酸菜里加黑胡椒的异端做法还挺好吃的）

下午fyc大佬被导师硬控在宾馆做ppt，我和Dew去了冰雪小世界。评价为100元一位的伊春水上公园。在2022年及之前，每年春节期间伊春水上公园都建冰雕房子和冰滑梯，冰雕免费看，冰滑梯收费，我小时候每年都去玩。但现在没有了，据说搬到离市区较远的东升去了。

以前哈尔滨地铁上的“大钻石选莱驰”没了，冬天的敷尓佳面膜广告也没了。看b站评论区说是莱驰已经凉了。

晚上按照某qq攻略的指示去了老俄楼（以前去过波特曼，但觉得价格较贵且没有特别好吃，所以打算换一家）。

- 蜂蜜芥末沙拉（20r）
    - 还行（不过这东西也很难不行）
- 红菜汤（12r）
    - 还行
- 两片煎马哈鱼（35r）
    - 味道不错，个人感觉性价比较高
- 红肠拼盘（30r）
    - 量有点少，只有8片
    - 味道比秋林和商委的红肠淡一些，形状也不同
- 俄式焖饭（28r）
    - 量很小，还不便宜
    - 就是西红柿青豆焖饭，没家里做的好吃
- 眼肉牛排（98r）
    - fyc点了7分熟
    - 实际上肉眼看着三分熟，吃起来全熟
    - fyc说能吃
- 西冷牛排（98r）
    - Dew点了7分熟
    - 实际上肉眼看着没熟，吃起来咬不动
    - 切牛排会发出类似锯木头的声音

~~结论：虽然贵的也没多好吃，但便宜的不一定能吃~~

### Day 1, Sat

fyc大佬继续被硬控。我和Dew佬中午吃了林大的俭德园，Dew老师带了一大盒牛奶，全洒在包里了。

豌杂面味道不错。2楼蜜雪冰城排了一车人，没买。

现场设备极其抽象。键盘键位是日式的，打起来很不习惯；椅子是生锈的塑料折叠椅，不太结实，场上有人把椅子坐塌了；鼠标在绒桌布上很难移动。

热身赛题目全原。T1大水题；T2 2024江苏省赛原，当时是由精通博弈论的xmj写的，Dew没做过，猜了很久结论；T3诈骗题，被强大的Dew佬A了；T4不会。

fyc解封，晚上先在乐松4楼吃饭，然后索菲亚教堂+中央大街+防洪纪念塔三连。索菲亚每走几步就有人追着问照不照相，中央大街的马迭尔冰棍感觉和以前味道不一样了，不好吃。

我问我爸为啥用这么抽象的设备，我爸说电脑、键鼠和桌椅都是ccpc组委会送来的，系统也是组委会的人装的，和他没关系。（我爸：群已经被我禁言了，在知乎上骂就骂吧，反正我不上知乎）

### Day2, Sun 

正式赛加上了鼠标垫，但椅子没换，场上一直有人坐塌椅子。

原定9点开始，结果网炸了，改成9点20开始。

我一眼看G，发现是大水题。其他队友去签更水的签到。

我写G，RE。改，RE；再改，RE；去掉流同步，RE；Dew重构，AC。

此时只剩A和E可开。我看A，发现是个大分类讨论构造。fyc写B，AC；Dew写E，过不去样例。

我去写A，此时离结束只剩20+min。Dew和fyc发现E的bug，此时剩10min左右，我还没写完A，于是交机。

最后E没AC，赛后发现是低级错误。

我、fyc、Dew分别反复观察我的G题代码，实在找不出RE在哪。最后在哈尔滨太平机场的候机厅照着赛时打印重敲代码，发现在自己的笔记本上居然连样例都RE了。

```cpp
int dfs(int now,vector<int> &top){
    vis[now]=true;
    top.push_back(now);
    for(int to:e[now]){
        if(vis[to])continue;
        dfs(to,top);
        ans[now].push_back(to);
    }
    if(!ans[now].empty())++cnt;
}
```

RE在上面一段代码的最后一行，确定没有数组越界的情况。我在后面加了个`return 0;`，**然 后 就 它 喵 的 跑 通 了**。

（其实在比赛时编译器有警告，但我没用到函数返回值，且在本机能跑通，就没管。结果评测机的编译器版本不同，就RE了）
