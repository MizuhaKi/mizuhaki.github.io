---
layout: post
title: How to use the ubuntu for GPU server
author: Mizuha Ki
date: 2019-03-12
categories:
- computer science
- ubuntu
- command
tags:
- computer science
- ubuntu
- command
- blog
---

## 窗口操作：
创建窗口： screen -S xxx (screen's name)
激活窗口： screen -r xxx (screen's name)
查看窗口序列： screen -ls
退出窗口： Ctrl + A + D
kill窗口：
- screen -S screenname -X quit
- screen -S yourname -> 新建一个叫yourname的session
- screen -ls -> 列出当前所有的session
- screen -r yourname -> 回到yourname这个session
- screen -d yourname -> 远程detach某个session
- screen -d -r yourname -> 结束当前session并回到yourname这个session

## 常用文件操作指令：
显示当前目录下的文件列表：ls
显示当前目录下的隐藏文件列表：ls -a
拷贝文件夹：  cp -r 文件夹 目标路径
拷贝文件夹：  cp 文件 目标路径
删除文件： rm 文件
删除文件夹： 
- rm -r 文件夹
- rm -rf 文件夹

新建文件夹：mkdir 文件夹名
移动文件：mv
显示当前路径：pwd
显示文件大小： du -sh *
显示问价夹大小：du -sh */

如何修改文件为可执行状态：chmod 777 文件名

查询GPU状态: nvidia-smi

查看内存和gpu消耗情况：nvidia-smi
查看文件大小 du –sh 文件夹   或者 du -sh *      sudo du -h --max-depth=1 xxxx    du -h  --max-depth=1
百分比： df
编译： make  make -j8
清空编译：make clean

定位文件名，直接gf，即可直接打开另外一个文件。

查找文件：locate filename
查找文件：
- 查找当前目录下的指定的core文件 find . -name "core"
- 查找根目录下的指定的core文件 find / -name "core"
- 查找根目录下的指定的大小core文件 find / -name "core" - size +1024c
- 查找文件中是否含有指定的字符 "10.71.110.89" find / -name "*.tar.gz" - type f -exec rm -rf {} /;


## vim常用快捷键
- 打开文件：vim 文件名
- 进入编辑模式：i
- 编辑文件：Esc ：wq
- 退出文件： Esc :q
- 退出文件，不编辑： Esc :q!
- h 每次按下光标就会向左移动
- l 每次按下光标就会向右移动
- j 每次按下光标就会向下移动
- k 每次按下光标就会向上移动 
- dd 删除一行
- de 删除到空格前的词
- dw 删除知道空格的词
- gg 光标到行文件首
- G 光标到文件尾
- :!command 用于执行一个外部命令 command

## ubuntu终端常用命令
- ctrl + l - 清屏
- ctrl + c - 终止命令
- ctrl + d - 退出 shell,好像也可以表示EOF
- ctrl + z - 将当前进程置于后台，fg还原。
- ctrl + r - 从命令历史中找
- ctrl + a - 光标移到行首
- ctrl + e - 光标移到行尾
- ctrl + u - 清除光标到行首的字符
- ctrl + w - 清除光标之前一个单词
- ctrl + k - 清除光标到行尾的字符
- ctrl + t - 交换光标前两个字符
- ctrl + y - 粘贴前一ctrl+u类命令删除的字符
- ctrl + p - 上一条命令
- ctrl + n - 下一条命令
- ctrl + v - 输入控制字符 如ctrl+v <ENTER> ,会输入^M
- ctrl + f - 光标后移一个字符
- ctrl + b - 光标前移一个字符
- ctrl + h - 删除光标前一个字符
- N+<ESC>+f - 光标后移N个单词，N为1时可省略
- N+<ESC>+b - 光标前移N个单词，N为1时可省略
- ctrl + s - 挂起当前shell
- ctrl + q - 重新启用
- <ESC>+d 从光标开始处删除到行尾。挂起的shell
- !! - 上一条命令
- !-n - 倒数第N条历史命令
- !-n:p - 打印上一条命令（不执行）
- !?string?- 最新一条含有"string"的命令 # !-n:gs/str1/str2/ - 将倒数第N条命令的str1替换为str2,并执行（若不加g,则仅替换第一个）


