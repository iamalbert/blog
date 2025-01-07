---
title: Managing Python environment with Pyenv
date: 2025-01-07 22:47:18
tags:
---


# Install `pyenv`
https://github.com/pyenv/pyenv

# Install dependencies to compile python

```sh
sudo apt install -y libssl-dev gcc make

# Optional packages
sudo apt install -y libbz2-dev libncurses-dev libreadline-dev  libffi-dev libsqlite3-dev liblzma-dev tk-dev
```

# Install standalone python versions

```sh
pyenv install 3.13
```

## Use virtual env
For example, create a new virtual env call `ml`

```sh
pyenv virtualenv 3.13 ml
pyenv activate ml
pyenv deactivate
```

# Automatically switch python based on directory

```sh
pyenv local ml
```

This will create a file `.python-version` under current working directory. The content of the file is simply the name of the version (or virtualenv).

```sh
ml
```
