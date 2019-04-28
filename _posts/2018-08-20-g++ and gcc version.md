---
layout: post
title:  check g++ and gcc version in Ubuntu
author: Mizuha Ki
date: 2018-08-20
categories:
- computer science
- ubuntu
- check version
tags:
- computer science
- ubuntu
- check version
- blog
---

## check version
```bash
gcc --version
g++ --version
```
## Install version
```bash
sudo apt-get install -y gcc-4.7
sudo apt-get install -y g++-4.7
```
## Update version 
```bash
cd /usr/bin
sudo rm gcc
sudo ln -s gcc-4.7 gcc
sudo rm g++
sudo ln -s g++-4.7 g++
```
## check version
```bash
ls –al gcc g++
gcc --version
g++ --version
```
