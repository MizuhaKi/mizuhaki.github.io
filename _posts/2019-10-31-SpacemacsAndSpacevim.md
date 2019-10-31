---
layout: post
title: Spacemacs and Spacevim
author: Mizuha Ki
date: 2019-10-31
categories:
- editor
- emacs
- vim
tags:
- editor
- emacs
- vim
- blog
---

## Introduction 
- A community-driven Emacs distribution - The best editor is neither Emacs nor Vim, it's Emacs *and* Vim! http://spacemacs.org
- A community-driven modular vim distribution - The ultimate vim configuration https://spacevim.org

## Installation
- Spacemacs
```bash
sudo add-apt-repository ppa:kelleyk/emacs
sudo apt install emacs26
sudo mv .emacs.d .emacs.d.bak
sudo git clone https://github.com/syl20bnr/spacemacs ~/.emacs.d
emacs
```

- Spacevim
```bash
sudo apt instal vim
curl -sLf https://spacevim.org/cn/install.sh | bash
curl -sLf https://spacevim.org/install.sh | bash -s -- --install vim
curl -sLf https://spacevim.org/install.sh | bash -s -- --install neovim
vim
```
