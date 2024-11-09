---
layout: post
title: Arch Linux Needed Packages
date: 2024-11-09 15:55 +0800
categories: [Blogging, Tutorial]
tags: [Configuration]
---

### before nvidia packages installed
```text
qt5ct qt6ct qt5-wayland qt6-wayland kvantum kvantum-qt5 nwg-look
xdg-desktop-portal-hyprland xdg-desktop-portal-gtk

hyprland hyprpicker kitty
rofi-wayland waybar dunst
firefox chromium
```

### nvidia packages
```text
nvidia-dkms nvidia-utils egl-wayland
```

### after nvidia installed
```text
swww wlogout slurp swappy cliphist
ark dolphin vim neovim code
sddm qt5-quickcontrols qt5-quickcontrols2 qt5-graphicaleffects
zsh zsh-autosuggestions zsh-completions zsh-syntax-highlighting zsh-theme-powerlevel10k-git
pipewire pipewire-alsa pipewire-audio pipewire-jack pipewire-pulse gst-plugin-pipewire
networkmanager network-manager-applet
polkit-gnome pacman-contrib parallel jq imagemagick qt5-imageformats ffmpegthumbs kde-cli-tools
bluez bluez-utils blueman
man-db man-pages clash-verge
brightnessctl udiskie fastfetch cava
```

### aur packages
```text
swaylock-effects-git libnotify grimblast-git
```
