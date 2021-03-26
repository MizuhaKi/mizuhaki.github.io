---
layout: post
title: Emacs on Debian
author: Mizuha Ki
date: 2021-03-26
categories:
- tools
- emacs
- debian
tags:
- tools
- emacs
- debian
- blog
---


## Introduction 
- A txt [editor](https://www.emacswiki.org/emacs/EmacsSnapshotAndDebian) for debian system.

## Command
```bash
sudo apt-get install software-properties-common
sudo apt-get update 
sudo apt-get install gnupg2      # gnupg, gnupg1, gnupg2
wget -q http://emacs.ganneff.de/apt.key -O- | sudo apt-key add
sudo add-apt-repository "deb http://emacs.ganneff.de/ buster main"
sudo apt-get update
sudo apt-get install emacs-snapshot
sudo update-alternatives --config emacsclient
```
