---
layout: post
title: Arch Linux + Hyprland 配置
date: 2024-11-10 14:19 +0800
categories: [Blogging, Tutorial]
tags: [Configuration, Experience]
---

## 1. 安装必须包
1. Hyprland 相关
```bash
sudo pacman -S hyprland kitty
```

2. QT 和 GTK 相关
```bash
sudo pacman -S qt5ct qt6ct qt5-wayland qt6-wayland kvantum kvantum-qt5 nwg-look
sudo pacman -S xdg-desktop-portal-hyprland xdg-desktop-portal-gtk
```

3. 浏览器
```bash
sudo pacman -S firefox chromium
```
   - firefox chromium: 火狐和Chrome（前者基于GTK/Wayland，后者基于Xwayland）

4. BT 蓝牙
```bash
sudo pacman -S bluez bluez-utils blueman
```

5. 其他软件美化软件
```bash
sudo pacman -S hyprpicker rofi-wayland waybar dunst swww wlogout
```
   - hyprpicker: 截屏
   - rofi-wayland: 应用坞
   - waybar: 状态栏
   - dunst: 提醒
   - swww: 壁纸
   - wlogout: 退出菜单

## 2. 英伟达 Nvidia 显卡配置
```bash
sudo pacman -S nvidia-dkms nvidia-utils egl-wayland
```
