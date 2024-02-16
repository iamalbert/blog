---
title: Managing Python environment
tags:
---


```sh
sudo apt install -y libssl-dev

# optional packages
sudo apt install -y libbz2-dev libncurses-dev libreadline-dev  libffi-dev libsqlite3-dev liblzma-dev tk-dev
```



```sh

pyenv install 3.11

pyenv virtualenv 3.11 ml
```

```sh
pyenv activate ml
pyenv deactivate

```

```sh
# .python-version
ml
```