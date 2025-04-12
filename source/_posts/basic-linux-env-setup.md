---
title: Basic linux env setup
date: 2025-04-12 21:44:41
tags:
---

```sh
sudo apt update
sudo apt install -y vim tmux htop zsh curl wget net-tools openssh-client git jq unzip gnupg

mkdir ~/.bin
```

# zsh


```sh
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

Modify `~/.zshrc`

```sh
plugins=(git python docker docker-compose ssh-agent command-not-found common-aliases tmux)
zstyle :omz:plugins:ssh-agent lazy yes #allows to enter the password only on first use


# End of file

setopt noincappendhistory
setopt nosharehistory

export PATH="$USER/.bin:$PATH"
```


# Docker 

```sh
curl -fsSL https://get.docker.com  | sh
sudo groupadd docker && usermod -aG docker $USER
```

