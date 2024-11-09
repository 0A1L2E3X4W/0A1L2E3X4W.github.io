---
layout: post
title: Fcitx5 Install and Configure
date: 2024-11-09 00:11 +0800
categories: [Blogging, Tutorial]
tags: [Configuration]
---

## 1. download packages for chinese
```bash
# superuser
pacman -S fcitx5 fcitx5-configtool fcitx5-gtk fcitx5-qt fcitx5-chinese-addons
```

## 2. edit the environment file
```bash
# /etc/environment
QT_IM_MODULE=fcitx
XMODIFIERS=@im=fcitx
SDL_MOULE=fcitx
```
## 3. open fcitx5-configure tool and add "pinyin"
