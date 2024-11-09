---
layout: post
title: Arch Linux Install
date: 2024-11-09 22:22 +0800
categories: [Blogging, Tutorial]
tags: [Configuration, Experience]
---

### 1. stop reflector service

1. stop service
```bash
systemctl stop reflector.service
```

2. check service status
```bash
systemctl status reflector.service
```

### 2. stop buzzer

#### stop buzzer now
```bash
rmmod pcspkr
```

#### permanently stop buzzer
1. first make file
```bash
sudoedit /etc/modprobe.d/blacklist.conf
```

2. add these content
```bash
blacklist pcspkr
```

### 3. check UEFI mode
```bash
ls /sys/firmware/efi/efivars
```

### 4. connect to wifi/internet
unblock wifi function
```bash
rfkill unblock wifi
```

1. use command enter iwctl
```bash
iwctl
```

2. connect wifi
```bash
device list
station wlan0 scan
station wlan0 get-networks
station wlan0 connect {wifi-name}
exit
```

### 5. update clock
```bash
timedatectl set-ntp true
timedatectl status
```

### 6. Update Mirrorlist
```bash
vim /etc/pacman.d/mirrorlist
```

mirror source
```text
Server = https://mirrors.ustc.edu.cn/archlinux/$repo/os/$arch # 中国科学技术大学开源镜像站
Server = https://mirrors.tuna.tsinghua.edu.cn/archlinux/$repo/os/$arch # 清华大学开源软件镜像站
Server = https://repo.huaweicloud.com/archlinux/$repo/os/$arch # 华为开源镜像站
Server = http://mirror.lzu.edu.cn/archlinux/$repo/os/$arch # 兰州大学开源镜像站
```
