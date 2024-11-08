---
layout: post
title: Grub Theme install
date: 2024-11-09 00:08 +0800
categories: [Blogging, Tutorial]
tags: [Configuration]
---

(example: <a href="https://github.com/vinceliuice/grub2-themes">Grub2 Theme</a>)

### Examples:
 - Install Tela theme on 2k display device:
```sh
sudo ./install.sh -t tela -s 2k
```
 - Install Tela theme with custom resolution:
```sh
sudo ./install.sh -t tela -c 1600x900
```
 - Install Tela theme into /boot/grub/themes:
```sh
sudo ./install.sh -b -t tela
```
 - Uninstall Tela theme:
```sh
sudo ./install.sh -r -t tela
```

### Setting a custom background:
 - Make sure you have `imagemagick` installed, or at least something that provides `convert`
 - Find the resolution of your display, and make sure your background matches the resolution
   - 1920x1080 >> 1080p
   - 2560x1080 >> ultrawide
   - 2560x1440 >> 2k
   - 3440x1440 >> ultrawide2k
   - 3840x2160 >> 4k
