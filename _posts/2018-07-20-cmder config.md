---
layout: post
title: cmder config
author: Mizuha Ki
date: 2018-07-20
categories:
- computer science
- tool
- cmder
tags:
- computer science
- tool
- cmder
- blog
---

Cmder是款解压即可用的软件，解压后将cmder文件夹放到你想放的位置，直接进入文件夹双击Cmder.exe即可使用。

## ls命令不支持中文
- Cmder右下角下拉列表中，打开settings面板，找到Startup -> Envrioment选项
- 在下面的文本框里添加一行：set LANG=zh_CN.UTF-8
- 然后重启cmder，使用ls命令查看目录下的文件，带中文的文件名都能正常显示了。

## 添加 Cmder 到右键菜单
- 以管理员身份打开Cmder，在Cmder命令窗口中使用快捷键Ctrl + t，在弹出界面上确保Run as current user和 Run as administrator这两项已勾选（PS：勾选new window可以打开多窗口功能），然后点start
- 在命令行输入：Cmder.exe /REGISTER ALL
- 然后在文件夹上右键点击Cmder here，就能在Cmder里进入该目录

## 修改命令提示符号：cmder默认的命令提示符是 λ ，如果想改成常见的 $ ,具体操作如下：
- 打开cmder安装目录下的\vendor\clink.lua文件
- 找到lambda = "λ"和lambda = "("..env..") λ"把λ替换成$
- 重启cmder
- powerShell需要另行设置，打开cmder安装目录下的\vendor\profile.ps1文件
- 找到λ <PostPrompt> <repl input>和λ <PostPrompt> |和Microsoft.PowerShell.UtilityWrite-Host "`nλ " -NoNewLine -ForegroundColor "DarkGray"把λ替换成$
- 重启cmder

## 自定义aliases
  cmder还增加了alias功能，它让你用短短的指令执行一些常见但指令超长又难以记忆的语法;比如 ls cls等等
  打开cmder安装目录下的\config\user-aliases.cmd文件，根据自己的需要进行编辑快捷语句。
  如：..=cd .. 表示输入..回车即返回上一级目录

## 添加至环境变量
- 右键我的电脑，单击“属性”，单击左侧“高级系统设置”，单击最下面的“环境变量”
- 在下面的窗口中找到path，选中后点击“编辑”，将你的Cmder文件夹的全路径（如：D:\Cmder）放进去，然后一路点击确定
- win + r打开运行窗口，输入cmder即可打开cmder了

## 常用快捷键
双Tab，用于补全
Ctrl+T，建立新页
Ctrl+W，关闭标签页
Ctrl+Tab，切换标签页
Alt+F4，关闭所有标签页
Ctrl+1，切换到第一个页签，Ctrl+2同理
Alt + enter，切换到全屏状态

