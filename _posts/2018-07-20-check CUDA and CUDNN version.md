---
layout: post
title: check CUDA and CUDNN version
author: Mizuha Ki
date: 2018-07-20
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

## check command
cuda 版本 
cat /usr/local/cuda/version.txt

cudnn 版本 
cat /usr/local/cuda/include/cudnn.h | grep CUDNN_MAJOR -A 2

