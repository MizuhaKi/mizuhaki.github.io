---
layout: post
title: Vim Setting
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

## a vim config
``` vim
source $VIMRUNTIME/vimrc_example.vim
source $VIMRUNTIME/mswin.vim
behave mswin

set diffexpr=MyDiff()
function MyDiff()
  let opt = '-a --binary '
  if &diffopt =~ 'icase' | let opt = opt . '-i ' | endif
  if &diffopt =~ 'iwhite' | let opt = opt . '-b ' | endif
  let arg1 = v:fname_in
  if arg1 =~ ' ' | let arg1 = '"' . arg1 . '"' | endif
  let arg2 = v:fname_new
  if arg2 =~ ' ' | let arg2 = '"' . arg2 . '"' | endif
  let arg3 = v:fname_out
  if arg3 =~ ' ' | let arg3 = '"' . arg3 . '"' | endif
  if $VIMRUNTIME =~ ' '
    if &sh =~ '\<cmd'
      if empty(&shellxquote)
        let l:shxq_sav = ''
        set shellxquote&
      endif
      let cmd = '"' . $VIMRUNTIME . '\diff"'
    else
      let cmd = substitute($VIMRUNTIME, ' ', '" ', '') . '\diff"'
    endif
  else
    let cmd = $VIMRUNTIME . '\diff'
  endif
  silent execute '!' . cmd . ' ' . opt . arg1 . ' ' . arg2 . ' > ' . arg3
  if exists('l:shxq_sav')
    let &shellxquote=l:shxq_sav
  endif
endfunction


filetype off  
" Vundle path 
set rtp+=$VIM/vimfiles/bundle/vundle/  
call vundle#rc('$VIM/vimfiles/bundle/')  
Bundle 'gmarik/vundle'  
filetype plugin indent on  
  
" usr add
Bundle 'Solarized'
" set the menu & the message to English
set langmenu=en_US
let $LANG= 'en_US'
source $VIMRUNTIME/delmenu.vim
source $VIMRUNTIME/menu.vim
colorscheme solarized
set filetype=python  
au BufNewFile,BufRead *.py,*.pyw setf python  
syntax enable  
syntax on " 自动语法高亮  
set number"显示行号  
set tabstop=4 "表示Tab代表4个空格的宽度  
set expandtab "表示Tab自动转换成空格  
set autoindent "表示换行后自动缩进  
set autoread " 当文件在外部被修改时，自动重新读取  
set history=400 "vim记住的历史操作的数量，默认的是20  
set nocompatible"使用vim自己的键盘模式,而不是兼容vi的模式  
set confirm"处理未保存或者只读文件时,给出提示  
set smartindent"智能对齐  
set shiftwidth=4  
set nobackup
set noundofile
if has('gui_running')
    set guioptions-=T  " no toolbar
    set lines=55 columns=108 linespace=0
    if has('gui_win32')
      set guifont=Consolas:h12:cANSI
    else
      set guifont=Consolas\ 12
    endif
  endif

filetype plugin indent on     " required!   
```