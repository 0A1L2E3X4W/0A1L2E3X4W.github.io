---
layout: post
title: Zsh Configure
date: 2024-11-09 00:10 +0800
categories: [Blogging, Tutorial]
tags: [Configuration]
---

### install zsh and other packs
```bash
sudo pacman -S zsh zsh-autosuggestions zsh-syntax-highlighting zsh-completions zsh-theme-powerlevel10k-git
```

### change bash to zsh
```bash
 # 查看安装了哪些 Shell
chsh -l
 # 修改当前账户的默认 Shell
chsh -s /bin/zsh
```

### add to .zshrc
```bash
source /usr/share/zsh/plugins/zsh-autosuggestions/zsh-autosuggestions.zsh
source /usr/share/zsh/plugins/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh
source /usr/share/zsh-theme-powerlevel10k/powerlevel10k.zsh-theme
```
