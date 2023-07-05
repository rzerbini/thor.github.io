---
title: "ArchLinux Notes"
date: 2023-07-04T19:01:40-03:00
description: "Sample article"
tags: [archlinux]
---

this is post 11

## ArchLinux Notes

------------------------------
### ArchlinuxInstall

use systemctl restart systemd-networkd

editar /etc/systemd/network/20-wired.network incluir

[Network]

DNS=8.8.8.8

DNS=8.8.4.4

DNS=1.1.1.1

add to /etc/resolv.conf the nameserver=8.8.8.8

-------
* 1
* 2
* 3


```
sudo pacman -Syyu && sudo pacman -U package.tar.gz
```

update hoje
