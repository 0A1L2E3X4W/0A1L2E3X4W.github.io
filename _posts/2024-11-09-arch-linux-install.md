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

3. 添加内容
```bash
blacklist pcspkr
```
{: file='/etc/modprobe.d/blacklist.conf'}

### 3. 检查是否为 UEFI 模式启动
```bash
ls /sys/firmware/efi/efivars
```

### 4. 连接 WiFi 网络
0. 解除 rfkill 禁用
```bash
rfkill unblock wifi
```

1. 进入 iwctl
```bash
iwctl
```

2. 用 iwctl 连接 WiFi
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

### 7. 使用 btrfs 文件格式 创建分区

我的配置使用了 Windows11 + Arch Linux
固态1(2TB) 是 Windows， 固态2(512GB) 是 Arch Linux
我的 Arch 分区方案如下：
- / (root): 445GB
  - /home (和 root 目录在同一 btrfs 文件系统中)
- /boot : 1GB
- /SWAP : 剩下所有空间

1. 使用命令查看分区情况
```bash
lsblk
```

2. 使用 cfdisk 在你需要的分区
```bash
cfdisk /dev/{partition}
```

3. 创建完分区后 格式化启动分区，为 fat 格式
```bash
mkfs.fat -F32 /dev/{partition}
```

4. 格式化 SWAP 分区
```bash
mkswap /dev/{partition}
```

5. 格式化为 btrfs (-f 为强制格式化)
```bash
mkfs.btrfs -f /dev/{partition}
```

6. 为了创建子卷，先挂在分区
```bash
mount -t btrfs -o compress=zstd /dev/{partition} /mnt
```
- -t：选项后指定挂载分区文件系统类型
- -o：选项后添加挂载参数
- compress=zstd：开启透明压缩

7. 创建子卷，后取消挂载
```bash
btrfs subvolume create /mnt/@
btrfs subvolume create /mnt/@home

umount /mnt
```

8. 挂载分区
```bash
# 挂载 / 目录
mount -t btrfs -o subvol=/@,compress=zstd /dev/{partition} /mnt

# 创建 /home 并挂载
mkdir /mnt/home
mount -t btrfs -o subvol=/@home,compress=zstd /dev/{partition} /mnt/home

# 创建 /root 并挂载
mkdir -p /mnt/boot
mount /dev/{partition} /mnt/boot

# 挂载交换分区
swapon /dev/{partition}
```

9. 使用 df 命令复查挂载情况
```bash
df -h
```

10. 使用 free 命令复查 Swap 分区挂载情况
```bash
free -h
```

### 安装必须包

1. 内核及 btrfs 文件系统必须包
```bash
pacstrap -K /mnt base base-devel linux linux-firmware btrfs-progs linux-headers
```

2. 如果提示 GPG 证书错误，可能是因为使用的不是最新的镜像文件，可以通过更新 archlinux-keyring 解决此问题
```bash
pacman -S archlinux-keyring
```

3. 通过如下命令使用 pacstrap 脚本安装其它必要的功能性软件
```bash
pacstrap -K /mnt networkmanager vim sudo neovim 
```

4. 安装对应芯片的驱动包
```bash
pacman -S intel-ucode
pacman -S amd-ucode
```

5. fstab 用来定义磁盘分区
```bash
genfstab -U /mnt >> /mnt/etc/fstab
```

6. 复查分区
```bash
cat /mnt/etc/fstab
```
