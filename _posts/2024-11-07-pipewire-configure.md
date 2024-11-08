---
layout: post
title: Pipewire Configure
date: '2024-11-07 21:15:09 +0800'
categories: [Blogging, Tutorial]
tags: [Configuration]
---

### For Helvum (GTK patchbay for PipeWire):
```bash
sudo pacman -S pipewire pipewire-alsa pipewire-pulse pipewire-jack wireplumber helvum
```

### For qpwgraph (PipeWire Graph Qt GUI Interface):
```bash
sudo pacman -S pipewire pipewire-alsa pipewire-pulse pipewire-jack wireplumber qpwgraph
```

### To enable the system service:
```bash
systemctl --user enable --now pipewire.socket
systemctl --user enable --now pipewire-pulse.socket
systemctl --user enable --now wireplumber.service
```
