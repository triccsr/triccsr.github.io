---
title : '一只菜鸡的Konsole坏了，这是它的archlinux发生的变化'
date : 2024-05-07T15:49:41+08:00
tags :
    - 日常
    - archlinux
    - bug
url : 0e1b1d21
---
## 背景

某菜鸡有一只装了archlinux+kde的笔记本电脑。一天，某菜鸡什么都没干，仅仅进行了日常的`# pacman -Syu`，Konsole就坏掉了。具体症状表现为打开konsole需要15秒，占用100%cpu和13g内存。

神奇的是，这个问题只在x11下出现，wayland下没有问题。并且，某菜鸡还有一台也装了archlinux+kde的台式机，也没有出现问题。

## 尝试

某菜鸡分别在archlinux forum和LUG@NJU qq群内询问，得到的建议都是`~/.zshrc`运行时间过长，建议清理。

菜鸡卸载了使用已久的oh-my-zsh，发现问题没有解决。

菜鸡在LUG@NJU群大佬的建议下安装了终端模拟器kitty，发现kitty没有问题。菜鸡猜测是kde自身的问题。

菜鸡新建了一个空账户，发现空账户里没有问题。那么基本可以确定是账户内部settings出了问题。

我清空kde的settings，然后重新装修，发现是Win11图标的问题，换成breeze或tela就好了。

有些离谱，不过我又看到[archlinux forum上的另一篇帖子](https://bbs.archlinux.org/viewtopic.php?id=294921)，也是使用了flattery图标然后打不开dolphin，换成默认图标就好了。

~~还是老话，fuck U kde :rage:。~~

## 后续

问题解决了，虽然不是oh-my-zsh的问题，但oh-my-zsh已经被我删了。我尝试了一下powerlevel10k主题，发现还不错。

powerlevel10k的完全体需要MesloLGS NF字体，我尝试在fontconfig中设置nerd字体的fallback，但失败了。无奈之下还是安装了MesloLGS NF。

powerlevel10k好看且速度快，但它毕竟只是一个主题。一些oh-my-zsh开箱自带的功能现在需要手动配。

我安装了zsh-history-substring-search插件以实现按up键历史搜索功能。它不仅可以匹配前缀，还可以匹配子串。

zsh-history-substring-search与zsh-vi-mode有点冲突，在台式机上按照推荐设置
```zsh
bindkey '^[[A' history-substring-search-up
bindkey '^[[B' history-substring-search-down
```
无法正常工作。参考[issue](https://github.com/zsh-users/zsh-history-substring-search/issues/140)，需要使用：
```zsh
zvm_after_init_commands+=("bindkey '^[[A' history-substring-search-up && bindkey '^[[B' history-substring-search-down")`
```
但推荐设置在安装了相同的插件的笔记本上就能正常工作，我不明白:confused:。

我现在的`~/.zshrc`:

```zsh
# Enable Powerlevel10k instant prompt. Should stay close to the top of ~/.zshrc.
# Initialization code that may require console input (password prompts, [y/n]
# confirmations, etc.) must go above this block; everything else may go below.
if [[ -r "${XDG_CACHE_HOME:-$HOME/.cache}/p10k-instant-prompt-${(%):-%n}.zsh" ]]; then
  source "${XDG_CACHE_HOME:-$HOME/.cache}/p10k-instant-prompt-${(%):-%n}.zsh"
fi


source /usr/share/zsh-theme-powerlevel10k/powerlevel10k.zsh-theme

# To customize prompt, run `p10k configure` or edit ~/.p10k.zsh.
[[ ! -f ~/.p10k.zsh ]] || source ~/.p10k.zsh

# plugins installed by pacman/yay/paru
source /usr/share/zsh/plugins/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh
source /usr/share/zsh/plugins/zsh-autosuggestions/zsh-autosuggestions.zsh
source /usr/share/zsh/plugins/zsh-vi-mode/zsh-vi-mode.zsh

# zsh history substring search
source /usr/share/zsh/plugins/zsh-history-substring-search/zsh-history-substring-search.zsh
: ${HISTORY_SUBSTRING_SEARCH_ENSURE_UNIQUE='true'}

# make zsh history substring search work with zsh-vi-mode
zvm_after_init_commands+=("bindkey '^[[A' history-substring-search-up && bindkey '^[[B' history-substring-search-down")
# may not work 
#bindkey '^[[A' history-substring-search-up
#bindkey '^[[B' history-substring-search-down

# zsh set history, based on oh-my-zsh https://github.com/ohmyzsh/ohmyzsh/blob/master/lib/history.zsh
HISTFILE=$HOME/.zsh_history
HISTSIZE=50000
SAVEHIST=10000
setopt extended_history
setopt hist_expire_dups_first
setopt hist_ignore_all_dups
setopt hist_ignore_space
setopt hist_verify
setopt share_history
setopt inc_append_history

```