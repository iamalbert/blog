---
title: Setup WSL and work seaminglessly
tags:
  - windows
  - WSL
categories:
  - programming
date: 2024-02-16 18:21:10
---


# Network

Edit `/etc/wsl.conf` and add

```conf
[network]
generateResolvConf = false
```

Reboot computer and edit `/etc/resolv.conf`

```conf
nameserver 9.9.9.9
nameserver 1.1.1.1
```

# File system

Edit `/etc/wsl.conf` and add

```conf
[automount]
enabled = true 
# C-drive would be mounted to /c, rather than the default /mnt/c. 
root = /
```


# Reference

1. https://learn.microsoft.com/en-us/windows/wsl/wsl-config