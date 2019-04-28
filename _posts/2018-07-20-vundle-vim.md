---
layout: post
title: Vundle + Vim
author: Mizuha Ki
date: 2018-07-20
categories:
- computer science
- tool
- vim
tags:
- computer science
- tool
- vim
- blog
---

## 安装 Vim
在 Ubuntu 上安装 Vim 很简单，在终端敲入如下命令即可
```bash
sudo apt-get install vim
```

## 安装 Vundle
由于 vim 缺乏默认的插件管理器，所有插件的文件都散布在 ~/.vim 下的几个文件夹中，这样导致各种插件的安装、更新、删除都需要自己手动处理，既麻烦费事，又可能出现错误。所以我们需要插件管理器的帮忙，常见的插件管理器有 vundle、pathogen 等等，我们这里使用 vundle。
Vundle 托管在 Github 上，所以使用 git 下载 vundle ，并将其存放于 /etc/vim/bundle/vundle 即可。使用如下命令直接将源代码检出到该目录： 
```bash
git clone https://github.com/gmarik/vundle.git /etc/vim/bundle/vundle
```
下载完了 vundle 后，还需要配置 .vimrc 文件。 

配置vundle插件：
可以在终端通过vim打开~/.vimrc文件，
```bash
vim /etc/vim/.vimrc
```
也可以直接在目录中打开（快捷键ctrl+H显示隐藏文件）。 
将以下加在.vimrc文件中，加入之后保存之后就可以使用vundle了。
```vim
" Define bundles via Github repos "
Bundle 'christoomey/vim-run-interactive'
Bundle 'Valloric/YouCompleteMe'
Bundle 'croaky/vim-colors-github'
Bundle 'danro/rename.vim'
Bundle 'majutsushi/tagbar'
Bundle 'kchmck/vim-coffee-script'
Bundle 'kien/ctrlp.vim'
Bundle 'pbrisbin/vim-mkdir'
Bundle 'scrooloose/syntastic'
Bundle 'slim-template/vim-slim'
Bundle 'thoughtbot/vim-rspec'
Bundle 'tpope/vim-bundler'
Bundle 'tpope/vim-endwise'
Bundle 'tpope/vim-fugitive'
Bundle 'tpope/vim-rails'
Bundle 'tpope/vim-surround'
Bundle 'vim-ruby/vim-ruby'
Bundle 'vim-scripts/ctags.vim'
Bundle 'vim-scripts/matchit.zip'
Bundle 'vim-scripts/tComment'
Bundle 'mattn/emmet-vim'
Bundle 'scrooloose/nerdtree'
Bundle 'Lokaltog/vim-powerline'
Bundle 'godlygeek/tabular'
Bundle 'msanders/snipmate.vim'
Bundle 'jelera/vim-javascript-syntax'
Bundle 'altercation/vim-colors-solarized'
Bundle 'othree/html5.vim'
Bundle 'xsbeats/vim-blade'
Bundle 'Raimondi/delimitMate'
Bundle 'groenewege/vim-less'
Bundle 'evanmiller/nginx-vim-syntax'
Bundle 'Lokaltog/vim-easymotion'
Bundle 'tomasr/molokai'
Bundle 'klen/python-mode'
```

## 安装需要的插件
将想要安装的插件，按照地址填写方法，将地址填写在vundle#begin和vundle#end之间就可以
保存之后，有两种方法安装插件。 
(1) 运行 vim ,再运行 :PluginInstall
```bash
vim
:PluginInstall
```
(2) 通过命令行直接安装 vim +PluginInstall +qall
```bash
vim +PluginInstall +qall
```
安装完成之后，插件就可以使用。

## 移除不需要的插件
编辑.vimrc文件移除的你要移除的插件所对应的plugin那一行。
保存退出当前的vim
重新打开vim，输入命令BundleClean。
其他常用命令
更新插件BundleUpdate
列出所有插件BundleList
查找插件BundleSearch
YouCompleteMe —— 代码补全
Syntastic —— 语法检查
SuperTab —— 使 Tab 快捷键具有更快捷的上下文提示功能
Ctags —— 实现变量名、函数名的跳转（需遍历源代码文件生成 tags 文件）
Cscope —— 升级版 Ctags
TagList —— 显示当前文件中的宏、全局变量、函数等 tag（类似于 SourceInsight 的功能）
Tagbar —— TagList 的替代品（更适合于 C++）
AutoPairs —— 自动插入和格式化括号
Powerline —— 状态栏
Vim-airline —— Powerline 的替代品
Echofunc —— 自动显示函数声明
Snipmate —— 自动插入代码（代码重用工具）
NERDTree —— 文件浏览器（树形目录）
Ctrlp —— 文件浏览器（重新定义打开目录和文件的方式，更适用于大规模项目文件的浏览）
MiniBufferExplorer —— 缓冲区文件管理器
NERDCommenter —— 快速注释
Undotree —— 支持 undo 和 redo
Gdbmgr —— 调试器
Molokai —— 颜色主题

