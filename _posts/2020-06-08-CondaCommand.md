---
layout: post
title: Conda Command
author: Mizuha Ki
date: 2020-06-08
categories:
- tools
- conda
- command
tags:
- tool
- conda
- command
- blog
---

## Introduction 
- A tool for python environment.

## Command
```bash
conda list
conda update conda
conda install python
conda info -e
conda activate environment
conda deactivate
conda remove -n environment --all
conda env export -n environment > environment.yml
conda env create -n environment -f environment.yml
```
## Tsinghua Source 
```bash
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/conda-forge/
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/msys2/
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/pytorch/
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/r/
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main/

conda config --set show_channel_urls yes
```

