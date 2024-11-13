---
title : 'ICPC 2024 杭州站 小黄鸭游记'
date : 2024-11-12T13:09:10+08:00
draft : false
url : 5c3701ff
math: true
---

## 摘要

3人场，7题。

~~虽然我寄了，但别人也都寄了，这何尝不是一种不寄~~

补题链接私信sua的人。

## 游记

### Day 1, Sat

由于杭州离南京较近，教练只订了一晚酒店，让周六早坐火车去杭州。但fyc正好要去杭州出差先走了，Dew老师要面基群友周五也走了。

我买的9:18的票。想着反正能报销，8点从学校打车去南京南站。司机的主业是起重，老家河南，曾在北京打工多年，因孩子上学问题移居南京。现在孩子在南航附中上高中，刚在南京买了一套房。

> 司机：南京三居室租一年两三万，在北京就要十万。北京不给孩子念高中，不像南京，有居住证就给孩子高中上。

> 司机：你们南京大学食堂不好吃吧？
>
> 我：你怎么知道？
>
> 司机：在别的学校干活都吃食堂。在南大干活对接人从外面买饭给我们吃，说食堂不好吃。

主办学校是杭州师范大学，离杭州西站很近。虽然实际占地面积和呢喃差不多，但呢喃一半是山，感觉上比呢喃大不少。

比赛地点在恕园的体育馆，据说承办过亚运会。

选手服藏蓝色，教练服大红色，都只有3xl和4xl，哪个尺码我都穿不了。

赞助商有华为，华为又整扫码填信息套圈的烂活。

教练碰见一个人，和这人说话，让我去套圈。

> 我：华为越来越抠了，去年江苏省赛还是扫码填信息就给电扇，这次居然需要套中了才给。
>
> 和教练说话的人：那我去给你要一个？
>
> 我：你谁啊？
>
> 和教练说话的人：我华为高管

（溜了溜了）

学校给每个人发支付宝电子校园卡，里面有84元。

之前打过杭州站的人说杭师大的食堂还不如呢喃食堂。我中午去尝逝，虽然味道还行，但全是凉的，确有呢喃风范。

学校里有个恕园宾馆离考场较近。结果教练嫌恕园不好听，订了学校另一端的勤园宾馆，离考场2km，幸好学校里可以扫哈罗电动车。~~也好，终于不搞订全季酒店的逝情了~~

宾馆的电梯十分抽象。新按上的楼层会覆盖之前人的楼层。

晚上不想吃食堂，拦了个学生问校外什么好吃，学生说这附近没什么好吃的。fyc大佬在高德地图上找到了个商场类似物，打车，到了才发现是个宾馆。还好附近有个真商场。

宾馆附近有个教超，里面还有瑞幸。晚上用卡里的钱去进了一些零食饮料和一瓶沐浴露。zf大佬说HIT的传统是比赛喝茶$\pi$，所以我也买了瓶柠檬红茶。

跟我住一间房的大一佬从下午就开始写segment beats，到晚上11点多还没调出来，在我的催促下睡觉。

### Day2, Sun

宾馆没有早餐，要去食堂吃饭。一般的糯米烧卖里面加的都是香菇+肉粒，这个食堂的烧卖居然是糯米+葱花。然后去教超买了三杯瑞幸。

物资给了小书包，还不错。

-------------------

开场后3分钟才进去系统，所以延时了3min。

我看M，感觉不难，但不会。

Dew看A，AC。然后看榜k有人过，让我看k，AC。

fyc跟榜做E，抓我当小黄鸭。开始想了个要写线段树二分的抽象贪心，我不确定这个贪心的正确性。fyc写完才发现这个贪心策略过不去样例，下机。

此时M也有人过，Dew会了M，抓我做小黄鸭。我看过M，觉得Dew的做法有道理。Dew写M，AC。

Dew写M时我去看H并有了初步思路，Dew AC M后和我讨论H，发现我H的思路有点问题。此时fyc又想了一个E用堆实现的贪心，又抓我做小黄鸭。Dew接着想H，AC。

我虽然不会证明fyc新做法的正确性，但觉得比上一个思路靠谱。fyc重写E，AC。

fyc写E时Dew看B。Dew抓我当小黄鸭，但我根本没听懂。Dew写B，AC。

然后我和fyc跟榜看F，F的前半部分是个大原题，但后半部分强制在线，fyc大佬想了主席树/分块都不行。此时无人上机，fyc先去抄前半部分的板子，我接着想F后半部分，发现了连续块性质，写后半部分，AC。

此时还剩80min。场上通过人数最多的是J，其次G，再次I。三人看J，但全无思路。

然后队友让我看G，我发现G是个只有码量的水题，于是与fyc大佬交流做法。fyc大佬认为无法在剩余时间内写完G。（事实证明fyc大佬十分有远见）

于是接着三人看J，但谁也没想到$O(m\cdot 2^m)$的做法。寄。

------

一群领导说了一堆，又来了个水平不怎么样的街舞表演，才开始滚榜。

滚榜由浙大王灿老师主持，该老师发表暴论“没人会做的题才是好题”。

滚榜过程中有些抽象队名，比如“队长十年单身换区域赛铜牌”，结果真铜牌了。还有“队长征婚+QQ号”，qq号我搜了是真的，且该队伍封榜后一直A题导致队名被念了几次。

滚榜结束后很晚了，fyc提议去高铁站吃晚饭。结果高铁站里面只有一家康师傅和一家德克士，还很贵。fyc吃了康师傅，我出站去美宜佳买了点吃的。

## 题解

### G

给定一个内向基环树森林，节点有颜色，问从每个点出发最先经过k次的颜色是哪种。

$n\leq 2\times 10^5,1\leq k\leq 10^9$。2s,1024M

---

fyc大佬是对的，这东西看着简单，实际上细节很多，不好调。杭州站讲题人也说有的队一开场就去写G，写了5h也没写出来。

容易想到维护一个数组，代表从当前节点出发，经过某种颜色k次的结束位置和走过的圈数，这样就可以$O(1)$比较某两种颜色经过k次的先后顺序。在dfs环上挂的子树时，对每个颜色维护一个栈。若栈的大小$\geq k$，则栈上的倒数第k个位置即为恰好经过k次该颜色的位置。否则需要上环。这样可以$O(1)$计算从当前位置经过某颜色k次的结束位置以及在环上走的圈数。由于在dfs当前节点的某个儿子时，只会让儿子节点的颜色结束位置变近，其他颜色的结束位置不变，所以可以用一个变量记录全局最小值，回溯时恢复数组和最小值。

但这样有个问题，对于环上挂着的不同子树，每种颜色在从不同树根出发的结束位置并不相同。~~所以我们需要数据结构维护不同树根的初始结束位置数组，吗？~~

官方题解给出了一个巧妙的解决方式。把环延长一倍，然后拆出一条链出来，这样不影响答案，且每个环只剩一个子树。

由于该题目只需求最先经过k次的颜色，且只输出所有点答案的和，所以即使有很离谱的bug也能过样例。既然暴力好写，应该写个对拍。

巨丑的代码（我的实现方式没有延长环）：

```cpp
#include <bits/stdc++.h>

using namespace std;
const int N=4e5+11,inf=0x3f3f3f3f;

int n,k,t[N],a[N],v[N];

vector<int> r[N];
deque<int> loop[N];
int lTail;
vector<int> posOnPath[N];
deque<int> posOnLoop[N];

bool onLoop[N];

struct M{
    int pathDep;
    int cntPath;
    int cntLoop;
    int type;
    bool operator <(const M &m)const{
        if(pathDep!=m.pathDep)return pathDep>m.pathDep;
        if(cntLoop==0)return false;
        if(m.cntLoop==0)return true;
        int cr=(k-cntPath-1)/cntLoop,mcr=(k-m.cntPath-1)/m.cntLoop;
        if(cr!=mcr)return cr<mcr;
        return posOnLoop[type].at((k-cntPath)-cr*cntLoop-1)<posOnLoop[m.type].at((k-m.cntPath)-mcr*m.cntLoop-1);
    }
    M()=delete;
    M(int pathDep,int cntPath,int cntLoop,int type):pathDep(pathDep),cntPath(cntPath),cntLoop(cntLoop),type(type){}
};


void dfs(int now,int d,vector<M> &mushrooms,M &pathMin){
    M oldValue=mushrooms[t[now]];
    M oldMin=pathMin;
    posOnPath[t[now]].push_back(d);
    if((int)posOnPath[t[now]].size()>=k){
        mushrooms[t[now]].pathDep=posOnPath[t[now]][(int)posOnPath[t[now]].size()-k];    
    }
    mushrooms[t[now]].cntPath=(int)posOnPath[t[now]].size();
    pathMin=min(pathMin,mushrooms[t[now]]);
    v[now]=pathMin.type;
    for(int to:r[now]){
        if(onLoop[to])continue;
        dfs(to,d+1,mushrooms,pathMin);
    }
    mushrooms[t[now]]=oldValue;
    pathMin=oldMin;
    posOnPath[t[now]].pop_back();
}
namespace J{
    int get_v(int u){
        static int c[N];
        vector<int> used;
        int ret=0;
        while(1){
            c[t[u]]+=1;
            used.push_back(t[u]);
            if(c[t[u]]==k){
                ret=t[u];
                break;
            }
            u=a[u];
        }
        for(int type:used){
            c[type]=0;
        }
        return ret;
    }
}
void work(){
    cin>>n>>k;
    for(int i=0;i<=n;++i){
        r[i].clear();
        loop[i].clear();
        posOnPath[i].clear();
        posOnLoop[i].clear();
        onLoop[i]=false;
        v[i]=0;
    }
    for(int i=1;i<=n;++i)cin>>t[i];
    for(int i=1;i<=n;++i){
        cin>>a[i];
        r[a[i]].push_back(i);
    }

    lTail=0;
    vector<bool> vis(n+1,false),inStack(n+1,false);
    vector<int> stk;
    for(int i=1;i<=n;++i){
        if(!vis[i]){
            int now=i;
            stk.clear();
            while(1){
                inStack[now]=true;
                vis[now]=true;
                stk.push_back(now);
                if(inStack[a[now]]){
                    while(!stk.empty()){
                        loop[lTail].push_front(stk.back());
                        onLoop[stk.back()]=true;
                        if(stk.back()==a[now])break;
                        inStack[stk.back()]=false;
                        stk.pop_back();
                    }
                    lTail+=1;
                    break;
                }
                if(vis[a[now]])break;
                now=a[now];
            }
            while(!stk.empty()){
                inStack[stk.back()]=false;
                stk.pop_back();
            }
        }
    }

    vector<M> info(n+1,M(-inf,0,0,0));
    for(int i=1;i<=n;++i)info[i].type=i;

    for(int l=0;l<lTail;++l){
        vector<int> loopTypes;
        for(int i=0;i<(int)loop[l].size();++i){
            posOnLoop[t[loop[l][i]]].push_back(i);
            loopTypes.push_back(t[loop[l][i]]);
        }

        M pathMin=M(-inf,0,0,0);
        for(int type:loopTypes){
            info[type].pathDep=-inf;
            info[type].cntPath=0;
            info[type].cntLoop=(int)posOnLoop[type].size();
            pathMin=min(pathMin,info[type]);
        }

        for(int i=(int)loop[l].size()-1;i>=0;--i){
            dfs(loop[l][i],1,info,pathMin);
            posOnPath[t[loop[l][i]]].push_back(-i);
            if((int)posOnPath[t[loop[l][i]]].size()>=k){
                info[t[loop[l][i]]].pathDep=posOnPath[t[loop[l][i]]].at(posOnPath[t[loop[l][i]]].size()-k);
            }
            info[t[loop[l][i]]].cntPath=(int)posOnPath[t[loop[l][i]]].size();
            pathMin=min(pathMin,info.at(t[loop[l][i]]));
        }

        for(int type:loopTypes){
            posOnLoop[type].clear();
            posOnPath[type].clear();
            info[type]=M(-inf,0,0,type);
        }

    }
    long long ans=0;
    for(int i=1;i<=n;++i){
        ans+=1ll*i*v[i];
    }
    cout<<ans<<"\n";
}
int main(){
    //freopen("g.in","r",stdin);
    // ios::sync_with_stdio(0);
    // cin.tie(0);
    int T;
    cin>>T;
    while(T--){
        work();
    }
    return 0;
}

```
