---
title: Setup WSL and work seaminglessly
categories:
    - programming
tags:
    - windows
    - WSL
---

# Network

```
# /etc/wsl.conf
[network]
generateResolvConf = false

# /etc/resolv.conf
nameserver 9.9.9.9
nameserver 1.1.1.1
```


# Docker 