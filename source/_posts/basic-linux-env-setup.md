---
title: Basic linux env setup
date: 2025-04-12 21:44:41
tags:
---

# Basic utilities

```sh
sudo apt update
sudo apt install -y vim tmux htop zsh curl wget openssh-client git jq unzip gnupg

mkdir ~/.bin
```

# Zsh

## Install

```sh
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```


## Change theme
```sh
sed -i 's/robbyrussell/gentoo/g' ~/.zshrc 
```

## Common plugins

Modify `~/.zshrc`
```sh
plugins=(git docker docker-compose common-aliases tmux)
```

Alternatively, run
```sh
sed -i 's/^plugins=/plugins=(git docker docker-compose common-aliases tmux)/g' ~/.zshrc
```

## SSH Agent
Modify ~/.zshrc and add 
```sh
plugins=(... ssh-agent ...)
zstyle :omz:plugins:ssh-agent lazy yes #allows to enter the password only on first use
```

## Settings

```sh
cat << EOF >> ~/.zshrc 
setopt noincappendhistory
setopt nosharehistory

export PATH="$USER/.bin:$PATH"
EOF
```


# Docker 

```sh
curl -fsSL https://get.docker.com  | sh
sudo groupadd docker 
sudo usermod -aG docker $USER
```

