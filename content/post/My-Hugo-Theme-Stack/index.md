---
title : '我的hugo-theme-stack'
date : 2024-05-08T22:37:30+08:00
url : 54b10acc
---
## 背景

我以前用Hexo下的[NexT主题](https://theme-next.js.org/)，它很华丽，但打开图片多的文章时巨卡无比[比如这篇](https://triccsr.github.io/62a2ca63/)。

这次我选择了[hugo-theme-stack](https://github.com/CaiJimmy/hugo-theme-stack)，主要是看中了gallery功能。

## 更改

### 大更改

为了方便改主题，我使用了git-submodule安装方式，然后把[starter](https://github.com/CaiJimmy/hugo-theme-stack-starter)里的config文件夹复制到自己的站点文件夹里。

#### mermaid

我按照[hugo doc里的方法](https://gohugo.io/content-management/diagrams/#mermaid-diagrams)加了mermaid支持。

```mermaid
sequenceDiagram
    participant Alice
    participant Bob
    Alice->>John: Hello John, how are you?
    loop Healthcheck
        John->>John: Fight against hypochondria
    end
    Note right of John: Rational thoughts <br/>prevail!
    John-->>Alice: Great!
    John->>Bob: How about you?
    Bob-->>John: Jolly good!
```

```mermaid
graph TD
          A[Christmas] -->|Get money| B(Go shopping)
          B --> C{Let me think}
          B --> G[/Another/]
          C ==>|One| D[Laptop]
          C -->|Two| E[iPhone]
          C -->|Three| F[fa:fa-car Car]
          subgraph section
            C
            D
            E
            F
            G
          end
```

#### admonition(alert)

加了admonition，也叫alert。实现方式基于[DoIt](https://github.com/HEIGE-PCloud/DoIt)里的admonition。样式与github alert 接近。

现支持以下种类

github alert:

> [!NOTE]
> Useful information that users should know, even when skimming content.

> [!TIP]
> Helpful advice for doing things better or more easily.

> [!IMPORTANT]
> Key information users need to know to achieve their goal.

> [!WARNING]
> Urgent info that needs immediate user attention to avoid problems.

> [!CAUTION]
> Advises about risks or negative outcomes of certain actions.

部分mkdocs

> [!INFO]
> info

> [!question]
> question

> [!danger]
> danger

> [!bug]
> bug

##### github alert

无标题

```md
> [!NOTE]
> Useful information that users should know, even when skimming content.

> [!TIP]
> Helpful advice for doing things better or more easily.


```

有标题（真正的github alert不支持）

```md
> [!WARNING]+ Radiation hazard
> Do not approach or handle without protective gear.
```

> [!WARNING]+ Radiation hazard
> Do not approach or handle without protective gear.

##### hugo shortcode

```md
{{</* admonition  type=note title="This is a note" */>}}
A **note** banner
{{</* /admonition */>}}

{{</* admonition  type=tip title="This is a tip" */>}}
A **tip** banner
{{</* /admonition */>}}

```

也可以不加type和title，默认type为note，title为type，效果如下：

```md
{{</* admonition */>}}
Default
{{</* /admonition */>}}

{{</* admonition tip */>}}
default tip
{{</* /admonition */>}}
```
{{< admonition >}}
Default
{{< /admonition >}}

{{< admonition tip >}}
Default tip
{{< /admonition >}}

### 小更改

小的更改被我放在了site文件夹下。

把链接改成了蓝色，改了代码的字体和字号。

## 问题

- [ ] 暗色模式没法被dark reader识别。

- [x] mermaid的颜色没法随着亮色/暗色模式的切换而切换。（DoIt也有这个问题，于是我写了一个亮暗都能看清~~不过很丑~~的mermaid主题）

- [ ] 目录没法自动折叠。


