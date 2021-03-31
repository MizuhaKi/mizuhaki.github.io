---
layout: post
title: Locale in Docker
author: Mizuha Ki
date: 2021-03-31
categories:
- locale
- spacemacs
- docker
tags:
- locale
- spacemacs
- docker
- blog
---


## Introduction
Although Python 3 has officially started to use UTF-8 encoding for text files, I still sometimes got errors regarding ASCII/UTF-8 in Docker container. Surprisingly, there is no such issue in the native system. It turns out that it is the system locale problem. In the native system, the locale is usually properly set from the GUI during installation. In Docker container, usually the system locale was not set, and therefore UTF-8 could not be properly read and display in the terminal.

In this blog post, I will talk about how to set the locale properly in Docker container so that there will be no UTF-8 problems at all.


## Check System Locale
```bash
locale
locale -a

LANG=en_US.UTF-8
LANGUAGE=en_US.UTF-8
LC_CTYPE="en_US.UTF-8"
LC_NUMERIC="en_US.UTF-8"
LC_TIME="en_US.UTF-8"
LC_COLLATE="en_US.UTF-8"
LC_MONETARY="en_US.UTF-8"
LC_MESSAGES="en_US.UTF-8"
LC_PAPER="en_US.UTF-8"
LC_NAME="en_US.UTF-8"
LC_ADDRESS="en_US.UTF-8"
LC_TELEPHONE="en_US.UTF-8"
LC_MEASUREMENT="en_US.UTF-8"
LC_IDENTIFICATION="en_US.UTF-8"
LC_ALL=en_US.UTF-8
```

## Install
```bash
locale-gen en_US.UTF-8
dpkg-reconfigure locales    # all
echo en_US.UTF-8 UTF-8 > /etc/locale.gen && locale-gen
```

### Add to bashrc
```bash
export LANG=en_US.UTF-8
export LANGUAGE=en_US.UTF-8
export LC_CTYPE=en_US.UTF-8
export LC_ALL=en_US.UTF-8
```
