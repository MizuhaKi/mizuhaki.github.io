---
layout: post
title: Vim for latex
author: Mizuha Ki
date: 2019-05-19
categories:
- computer science
- vim
- latex
tags:
- computer science
- vim
- latex
- blog
---

最近 Vim 和 LaTex 用的都比较多，如果你也经常使用 Vim来编辑 LaTex 文档，不妨尝试一下。

## 快捷键
1. = 自动格式化对齐样式，对于有代码洁癖强迫症的人来说绝对是福音。
2. gq家族 根据 textwidth 自动换行。gqgq: 换行当前段。gqap: 格式化整个段。{Visual}gq: 格式化选定的部分。对于每行字符数量不能超过 80 的人来说，又一个福音。最后你的文章会非常整齐，就像这样：
```tex
Vim (an acronym for Vi IMproved) is a text editor written by Bram Moolenaar and
first released publicly in 1991. Based on the vi editor common to Unix-like
systems, Vim is designed for use both from a command line interface and as a
standalone application in a graphical user interface. Vim is free and open
source software and is released under a license that includes some charityware
clauses, encouraging users who enjoy the software to consider donating to
children in Uganda. The license is compatible with the GNU General Public
License.
```

## 命令 & .vimrc
1. :set spell 经常写英文的人会用得到的，一不小心打错单词了，Vim 会在单词上加一个下划线提示。你还可以把你认为正确的特殊单词加到字典里面。
2. autocmd BufNewFile,BufRead *.tex set spell 把这句话加到 .vimrc 里面可以在打开 .tex 文件的时候自动进行拼写检查。
3. let g:tex_indent_items=0 估计大家都打开了换行时自动对齐的功能，但是有没有发现这样一个问题，在用 itemize 的时候，每一个 item 都会自动缩进两个，非常麻烦。如果你懒得搞的话，最后就变成了这个样子：
```tex
\begin{itemize}
  \item fist ...
    \item second ...
      \item third ...
\end{itemize}
```
如果在 .vimrc 里面加入 let g:tex_indent_items=0 一句话，自动缩进终于变得正常了。

## 插件
1. UltiSnips 无论是编辑 LaTex 文档还是写代码，UltiSnips 绝对是利器。他可以自动补全常用的代码结构。拿 Tex 举例，输入 item 就会出来：
```tex
item
\begin{itemize}
    \item
\end{itemize}

fig
\begin{figure}[htpb]
  \centering
  \includegraphics[width=0.8\linewidth]{name.ext}
  \caption{Name}
  \label{fig:name}
\end{figure}

lp
\left(contents\right)
```
还有非常多的自动补全，\begin{}…\end{} \section{}…。当然，你还可以编写自己的 snippets。用了这个插件，写东西的时候有一种畅快淋漓的感觉，再也不用纠结乱起八糟的命令了。可以看一下作者录制的四个 screencasts，了解 UltiSpips 更强大的功能。

2. Align 用 [Align](https://github.com/vim-scripts/Align) 来对齐表格，又一个强迫症的福音。
```tex
\begin{tabular}{cccc}
  a & b & c & d \\
  Ef & long long & ss & a \\
  test & n & long content & small \\
\end{tabular}
" 选中表格内容，按 tt，就可以对齐了，豁然开朗。
\begin{tabular}{cccc}
  a    & b         & c            & d     \\
  Ef   & long long & ss           & a     \\
  test & n         & long content & small \\
\end{tabular}
```
3. [Syntastic](https://github.com/scrooloose/syntastic)是语法检查的利器。对于 Tex 文档来说，你总不想到编译的时候才发现 & 符号没有用转移字符 \& 吧。Syntastic 会动态的检查 Tex 文档的语法，除了语法错误的提示，他还会有一些语法的建议。附一张官方的图，这是多么的方便啊！ 

4. [ale](https://github.com/w0rp/ale)(Asynchronous Lint Engine)是一款语法检查的插件，与syntastic类似，但有两个明显的优势，一个是语法检查是异步执行的，因此基本上不会出现卡顿的情况，另外一个是ale默认会使用所有检查工具并发的进行检查，但它只支持Vim 8.0以上的版本。
```bash
"异步语法检查
Plug 'w0rp/ale'

" ale-setting {{{
let g:ale_set_highlights = 0
"自定义error和warning图标
let g:ale_sign_error = 'chacha'
let g:ale_sign_warning = 'leidian'
"在vim自带的状态栏中整合ale
let g:ale_statusline_format = ['chacha %d', 'leidian %d', 'gou OK']
"显示Linter名称,出错或警告等相关信息
let g:ale_echo_msg_error_str = 'E'
let g:ale_echo_msg_warning_str = 'W'
let g:ale_echo_msg_format = '[%linter%] %s [%severity%]'
"打开文件时不进行检查
let g:ale_lint_on_enter = 0

"普通模式下，sp前往上一个错误或警告，sn前往下一个错误或警告
nmap sp <Plug>(ale_previous_wrap)
nmap sn <Plug>(ale_next_wrap)
"<Leader>s触发/关闭语法检查
nmap <Leader>s :ALEToggle<CR>
"<Leader>d查看错误或警告的详细信息
nmap <Leader>d :ALEDetail<CR>
"使用clang对c和c++进行语法检查，对python使用pylint进行语法检查
let g:ale_linters = {
\   'c++': ['clang'],
\   'c': ['clang'],
\   'python': ['pylint'],
\}
" }}}
```

## 其他
还有一些不在强烈建议的列表当中，但是也非常的有用。比如说单词补全的插件：neocompletecache。或者直接从 markdown 转成 tex 文档，让你完全专注于写作: [pandoc](http://johnmacfarlane.net/pandoc/)。剩下的都是是看个人喜好了。

Update: 还有一个非常重要的工具，latexmk，是 LaTex 的 Makefile。好像 tex-live 的包里面直接就带了。有了他，就可以左边开一个 Vim，右边放一个 PDF。然后在 Vim 中保存修改，右面 PDF 就会自动更新。想达到这样的效果，首先要建立一个配置文件 .latexmkrc，里面写上：
```bash
$pdf_previewer = "start evince %O %S";
```
这里是为了制定默认的 PDF 浏览器。设置完之后，只要运行 latexmk 命令就能自动监控 tex 文件的修改，然后重新编译。
```bash
latexmk -pdf -pvc xxx.tex      // 用 pdflatex 编译，同时打开 PDF 浏览，并监控修改
latexmk -xelatex -pvc xxx.tex  // 用 xelatex 编译，同时打开 PDF 浏览，并监控修改
latexmk -c     // 删除生成的中间文件
```