## example for beamer
```latex
\documentclass{beamer}
\usepackage[english]{babel}   %如果去掉，中英混合会出错
\usepackage[noindent]{ctex}   %可使用 \usepackage{CJK}
\usepackage{beamerthemesplit}
% Or whatever. Note that the encoding and the font should match. If T1
% does not look nice, try deleting the line with the fontenc.
\usepackage[T1]{fontenc}
\usepackage{times}
 
\usetheme{Berkeley}
 
\title{XXXX}
 
\subtitle{XXXX}
 
\author{Ofey}
 
\institute{
  School of Computer Science\\
  Beijing Institute of Technology
}
 
% This is only inserted into the PDF information catalog. Can be left out.
\subject{OOO}
\keywords{OXOX}
 
\begin{document}
 
\begin{frame}{XXXX}
A normal frame.
\end{frame}
 
\end{document}
```
上面代码，便可以生成一夜的slides了，在我机器上测试是木有问题的。beamer中的frame有点相当于powerpoint中的一叶，要是想新建几页，再多加加个frame吧，也可以写成

```latex
\frame
{
  \frametitle{test}
  A normal frame.
}
```
至于frame和整个slides也都有相应的subtitle可以设置，随便看下文档就ok。

多个作者多个单位
有时，slides可能有多个作者，并且属于多个单位，会议论文作报告时，经常遇见此情况。如下代码解决

```latex
\author[Author, Another] % (optional, use only with lots of authors)
{F.~Author\inst{1} \and S.~Another\inst{2}}
% - Give the names in the same order as the appear in the paper.
% - Use the \inst{?} command only if the authors have different affiliation.
 
\institute[Beijing Institute of Technology] % (optional, but mostly needed)
{
  \inst{1}
  School of Computer Science\\
  Beijing Institute of Technology
  \and
  \inst{2}
  Department of Theoretical Philosophy\\
  University of Elsewhere
}
% - Use the \inst command only if there are several affiliations.
% - Keep it simple, no one is interested in your street address.
```
institute中写Email是可以直接识别出的，放心使用。至于经常出现的中括号可选项，用了乃就懂的～～

logo
有时，要插入个校徽神马的，吐槽下学校官方竟然每个矢量校徽。。。
导言区加：

```latex
% If you have a file called "university-logo-filename.xxx", where xxx
% is a graphic format that can be processed by latex or pdflatex,
% resp., then you can add a logo as follows:
 
% \pgfdeclareimage[height=0.5cm]{university-logo}{university-logo-filename}
% \logo{\pgfuseimage{bitlogo}}
\logo{\includegraphics[height=0.09\textwidth]{./pic/bitlogo.eps}} %这只是我的logo路径
```
目录(TOC)
LATEX生成目录这类实在是拿手戏。最简单的：

```latex
\begin{frame}
  \tableofcontents
\end{frame}
```
有时，可能目录太多，想分成两栏，可以使用multicol包

```latex
% This environment allows switching between one and multicolumn format on the same page
\usepackage{multicol}
 
\begin{frame}{Outline}
 
  \begin{multicols}{2}
    \tableofcontents
    % You might wish to add the option [pausesections]
  \end{multicols}
\end{frame}
```
有时，可能不想显示subsection之类，亦或者只想限制指定的几个section，如下：

```latex
\tableofcontents[hidesubsections,sections={<1-4>}] %显示1-4section，不显示subsection
\tableofcontents还有很多其他参数设置，详见文档。
```
若想在没个章节前显示下目录提示，可以如下代码：

```latex
\AtBeginSection[] { 
  \begin{frame}
    \frametitle{Outline} 
    \tableofcontents[currentsection,hideothersubsections] 
  \end{frame} 
  \addtocounter{framenumber}{-1}  %目录页不计算页码
}
```
不过没发现如何获得当前section的数值，这样我就可以自动在每张前插入目录，且使当前目录为第一。
当然，还可以做成一个个显示目录的动画效果，不过没啥实际意义- -！

slides中的链接
有时想在slides中加入超链接，可以跳转到指定的页面，这个也是很easy的。
给欲跳转到的frame加上label

```latex
\frame[label = XXX]
{
  \frametitle{OOO}
  \framesubtitle{XXX}
  OOXX
}
```
再在想加入超链接的地方加入：

```latex
\hyperlink{XXX}{\beamergotobutton{乃想显示的文本}} %\beamergotobutton可以选其他的按钮
```
显示时间+页数
这个根据不同的主题不一样，比如Berkeley默认就木有，而CambridgeUS就是有的，可以自己在导言区加入：

```latex
\setbeamertemplate{footline}{%
  \leavevmode%
  \hbox{%
    \begin{beamercolorbox}[wd=.333333\paperwidth,ht=2.25ex,dp=1ex,center]{author in head/foot}%
      \usebeamerfont{author in head/foot}\insertshortauthor
    \end{beamercolorbox}%
    \begin{beamercolorbox}[wd=.333333\paperwidth,ht=2.25ex,dp=1ex,center]{title in head/foot}%
      \usebeamerfont{title in head/foot}\insertshorttitle
    \end{beamercolorbox}%
    \begin{beamercolorbox}[wd=.333333\paperwidth,ht=2.25ex,dp=1ex,right]{date in head/foot}%
      \usebeamerfont{date in head/foot}\insertshortdate{}\hspace*{2em}
      \insertframenumber{} / \inserttotalframenumber\hspace*{2ex}
    \end{beamercolorbox}}%
  \vskip0pt%
}
```
其实就是抄其他主题代码。。。

页脚显示文本
有时希望在frame的左下角页脚能显示一些内容，并不是为了报告时如何，只是给其他途径看slides的人一点更详尽的解释、资料，但是又不想用脚注(脚注在beamer效果不咋的)。

```latex
% add text to beamer footline
 
\makeatletter
% add a macro that saves its argument
\newcommand{\footlineextra}[1]{\gdef\insertfootlineextra{#1}}
\newbox\footlineextrabox
 
% add a beamer template that sets the saved argument in a box.
% The * means that the beamer font and color "footline extra" are automatically added. 
\defbeamertemplate*{footline extra}{default}{
  \begin{beamercolorbox}[ht=2.25ex,dp=1ex,leftskip=\Gm@lmargin]{footline extra}
    \insertfootlineextra
    % \par\vspace{2.5pt}
  \end{beamercolorbox}
}
 
\addtobeamertemplate{footline}{%
  % set the box with the extra footline material but make it add no vertical space
  \setbox\footlineextrabox=\vbox{\usebeamertemplate*{footline extra}}
  \vskip -\ht\footlineextrabox
  \vskip -\dp\footlineextrabox
  \box\footlineextrabox%
}
{}
 
% patch \begin{frame} to reset the footline extra material
\let\beamer@original@frame=\frame
\def\frame{\gdef\insertfootlineextra{}\beamer@original@frame}
\footlineextra{}
\makeatother
```
使用很简单：

```latex
\footlineextra{XXXX}
```

参考文献
LATEX最爽的几点之一就是参考文献的管理使用啊，毕设论文得用doc的泪奔T.T
一般用的比较多的是bibtex，首先，自己搞定bib文件，然后slides中加上一页来放引用文献

```latex
%一般的引用样式只是[1]类，paper中这样没啥，slides这样不够友好
%apalike：美国心理学学会期刊样式，显示作者名+年份
\bibliographystyle{apalike}   
\bibliography{XXX}   %引用的XXX.bib文件
此外，reference可能较多，slides一页一般都不够用，beamer是可以自动分成多页的，如下：

% If there are too many of them to fit on the frame, 
% you must manually split them among additional frames or use the allowframebreaks option.
\begin{frame}[allowframebreaks]{References} 
  \scriptsize
  \bibliographystyle{apalike}
  \bibliography{XXX}
\end{frame}
```
引用，自然是\cite{}命令了

表格
有时，需要画一些表格，可能比较复杂，比如可能需要合并几行，或者几列，下面一个示例：
导言区加上

```latex
\usepackage{multirow}
% The \cline command draws horizontal lines across the columns specified,
ginning in column i and ending in column j, which are identified in the mandatory argument.
% \cline{i-j}
  \begin{table}
    \begin{tabular}{c|c|c|c}
      \hline
      % \multicolumn{2}{c}{\backslashbox{Name}{Numer}} &  \multicolumn{2}{c}{}\\ \hline
      \multirow{2}{*}{CleanEval} & \multirow{2}{*}{CleanEval-Eng} & training set & 60 \\ \cline{3-4} 
      \multirow{2}{*}{}          & \multirow{2}{*}{}              & evaluation set &   864 \\ \hline 
 
      \multirow{6}*{CETD} & NYTimes      & \multicolumn{2}{c}{100} \\ \cline{2-4} 
      \multirow{6}*{}     & Yahoo!       & \multicolumn{2}{c}{100} \\ \cline{2-4} 
      \multirow{6}*{}     & Wikipedia    & \multicolumn{2}{c}{100} \\ \cline{2-4}
      \multirow{6}*{}     & BBC          & \multicolumn{2}{c}{100} \\ \cline{2-4}
      \multirow{6}*{}     & Ars Technica & \multicolumn{2}{c}{100} \\ \cline{2-4}
      \multirow{6}*{}     & Chaos        & \multicolumn{2}{c}{200} \\ \hline 
    \end{tabular}
  \end{table}
```
效果如图
table 
其中，\multirow{6}*{CETD} 6代表占用6行，CETD是其内容，其实下面的\multirow{6}*{}是可以去掉的，只是为了代码排版更清晰
\multicolumn{2}{c}{100}值合并两列，并且居中。
\cline的解释见代码注释
至于有时候可能会想要斜线的效果，不过latex中表格斜线分割看上去不舒服，还是不推荐，尤其科技论文中，文档直接明说不推荐
更多设置，详见Tables in LaTeX: packages and methods

sidebar
Berkeley主题中的sidebar默认显示所有的subsection，并且在显示对应的页时，高亮相应的section。对此可以作一些自定义。
一般章节较多时，sidebar就很不友好了，显示不全，间距还大，别扭，只是取消显示subsection,一句话搞定

```latex
\usetheme[hideallsubsections]{Berkeley}
```
一种更好的sidebar显示方式：

```latex
% By default, the current entry of the table of contents in the sidebar will be highlighted by using a more vibrant color.
% A good alternative is to highlight the current entry by using a different color for the background of the current point.
% The color theme sidebartab installs the appropriate colors
 
\usecolortheme{sidebartab}
```
图表、算法编号
beamer仿佛默认是不显示图标标号的默认值是Figure：XXX

```latex
% show fig and table number
\setbeamertemplate{caption}[numbered]
% show theorems and example number
\setbeamertemplate{theorems}[numbered]
```
字体大小
beamer中某人的一些项目字体太大，比如样例example，可以在导言区自定义

```latex
\setbeamerfont{example}{size=\tiny}
\setbeamerfont{algorithm}{size=\scriptsize}
Chaos
```
至于关于动画之类的，其实更多的涉及到的是LATEX的画图，扯起来就太多了，不扯了，直接照着各文档来吧。
一般这些画图包都有各式各样的样例供参考。
转发

http://ofey.me/2011/12/beamer使用笔记/
