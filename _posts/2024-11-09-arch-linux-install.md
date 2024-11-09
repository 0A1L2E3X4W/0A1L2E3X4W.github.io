---
layout: post
title: Arch Linux Install
date: 2024-11-09 22:22 +0800
categories: [Blogging, Tutorial]
tags: [Configuration, Experience]
---

### 1. 禁用 reflector 服务

1. 停止检查 reflector 当前状态服务
```bash
systemctl stop reflector.service
```

2. 检查 reflector 当前状态
```bash
systemctl status reflector.service
```

### 2. 禁用蜂鸣器 buzzer

1. 暂时禁用（下次重启会开启）
```bash
rmmod pcspkr
```

2. 永久禁用
首先创建文件 /etc/modprobe.d/blacklist.conf
```bash
sudo vim /etc/modprobe.d/blacklist.conf
```

添加内容
```bash
blacklist pcspkr
```
{: file='/etc/modprobe.d/blacklist.conf'}

### 3. 检查是否为 UEFI 模式启动
```bash
ls /sys/firmware/efi/efivars
```

### 4. 连接 WiFi 网络
1. 解除 rfkill 禁用
```bash
rfkill unblock wifi
```

1. 进入 iwctl
```bash
iwctl
```

1. 用 iwctl 连接 WiFi
```bash
device list
station wlan0 scan
station wlan0 get-networks
station wlan0 connect {wifi-name}
exit
```

### 5. 更新系统时间
```bash
timedatectl set-ntp true
timedatectl status
```

### 6. 更新镜像源
1. 修改 /etc/pacman.d/mirrorlist
```bash
vim /etc/pacman.d/mirrorlist
```

2. 添加内容
```text
Server = https://mirrors.ustc.edu.cn/archlinux/$repo/os/$arch # 中国科学技术大学开源镜像站
Server = https://mirrors.tuna.tsinghua.edu.cn/archlinux/$repo/os/$arch # 清华大学开源软件镜像站
Server = https://repo.huaweicloud.com/archlinux/$repo/os/$arch # 华为开源镜像站
Server = http://mirror.lzu.edu.cn/archlinux/$repo/os/$arch # 兰州大学开源镜像站
```
