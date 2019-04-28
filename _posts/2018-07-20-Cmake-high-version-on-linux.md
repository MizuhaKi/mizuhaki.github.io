---
layout: post
title: cmake high version on linux
author: Mizuha Ki
date: 2018-07-20
categories:
- computer science
- ubuntu
- cmake
tags:
- computer science
- ubuntu
- cmake
- blog
---

## uninstall older version
```bash
sudo apt-get udpate
sudo apt-get autoremove cmake
```

## download files
```bash
wget [cmake](https://cmake.org/files/v3.9/cmake-3.9.1-Linux-x86_64.tar.gz)
```

## unzip
```bash
tar zxvf cmake-3.9.1-Linux-x86_64.tar.gz
```

## create soft url
```bash
mv cmake-3.9.1-Linux-x86_64 /opt/cmake-3.9.1
ln -sf /opt/cmake-3.9.1/bin/*  /usr/bin/
```