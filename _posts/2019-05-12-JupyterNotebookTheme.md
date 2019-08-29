---
layout: post
title: jupyter notebook theme
author: Mizuha Ki
date: 2019-05-12
categories:
- computer science
- python
- jupyter notebook
tags:
- computer science
- python
- jupyter notebook
- blog
---

## 修改 jupyter notebook 的主题，字体，字号
```bash
pip install jupyterthemes
jt -l
jt -t oceans16 -f anonymous -fs 12 -cellw 90% -ofs 11 -dfs 11 -T
```

## theme
- chesterish
- grade3
- gruvboxd
- gruvboxl
- monokai
- oceans16
- onedork
- solarizedd
- solarizedl

## Set Plotting Style (from within notebook)
jtplot.style() makes changes to matplotlib's rcParams dictionary so that figure aesthetics match those of a chosen jupyterthemes style. In addition to setting the color scheme, jtplot.style() allows you to control various figure properties (spines, grid, font scale, etc.) as well as the plotting "context" (borrowed from seaborn).

Note, these commands do not need to be re-run every time you generate a new plot, just once at the beginning of your notebook or whenever style changes are desired after that.

Pro-tip: Include the following two lines in ~/.ipython/profile_default/startup/startup.ipy file to set plotting style automatically whenever you start a notebook:

```python
# import jtplot submodule from jupyterthemes
from jupyterthemes import jtplot

# currently installed theme will be used to
# set plot style if no arguments provided
jtplot.style()
```

### jtplot.style() Examples
```python
# import jtplot module in notebook
from jupyterthemes import jtplot

# choose which theme to inherit plotting style from
# onedork | grade3 | oceans16 | chesterish | monokai | solarizedl | solarizedd
jtplot.style(theme='onedork')

# set "context" (paper, notebook, talk, poster)
# scale font-size of ticklabels, legend, etc.
# remove spines from x and y axes and make grid dashed
jtplot.style(context='talk', fscale=1.4, spines=False, gridlines='--')

# turn on X- and Y-axis tick marks (default=False)
# turn off the axis grid lines (default=True)
# and set the default figure size
jtplot.style(ticks=True, grid=False, figsize=(6, 4.5))

# reset default matplotlib rcParams
jtplot.reset()
```

## Monospace Fonts (code cells)

\-f arg | Monospace Font
:---: | :---:
anka | Anka/Coder
anonymous | Anonymous Pro
aurulent | Aurulent Sans Mono
bitstream | Bitstream Vera Sans Mono
bpmono | BPmono
code | Code New Roman
consolamono | Consolamono
cousine | Cousine
dejavu | DejaVu Sans Mono
droidmono | Droid Sans Mono
fira | Fira Mono
firacode | Fira Code
generic | Generic Mono
hack | Hack
hasklig | Hasklig
inconsolata | Inconsolata-g
inputmono | Input Mono
iosevka | Iosevka
liberation | Liberation Mono
meslo | Meslo
office | Office Code Pro
oxygen | Oxygen Mono
roboto | Roboto Mono
saxmono | saxMono
source | Source Code Pro
sourcemed | Source Code Pro Medium
ptmono | PT Mono
ubuntu | Ubuntu Mono

## Sans-Serif Fonts

\-nf/\-tf arg | Sans-Serif Font
:---: | :---:
opensans | Open Sans
droidsans | Droid Sans
exosans | Exo_2
latosans | Lato
ptsans | PT Sans
robotosans | Roboto
sourcesans | Source Sans Pro

## Serif Fonts

\-nf/\-tf arg | Serif Font
:---: | :---:
loraserif | Lora
ptserif | PT Serif
georgiaserif | Georgia
cardoserif | Cardo
crimsonserif | Crimson Text
ebserif | EB Garamond
merriserif | Merriweather
neutonserif | Neuton
goudyserif | Sorts Mill Goudy
