---
layout: post
title: read .PFM images
author: Mizuha Ki
date: 2018-07-20
categories:
- computer science
- deep learning
- matlab
tags:
- computer science
- deep learning
- matlab
- blog
---

## matlab code
```matlab
function D = pfmread(filename_pfm)
 
fid = fopen(filename_pfm);
 
fscanf(fid,'%c',[1,3]);
cols = fscanf(fid,'%f',1);
rows = fscanf(fid,'%f',1);
fscanf(fid,'%f',1);
fscanf(fid,'%c',1);
D = fread(fid,[cols,rows],'single');
D(D == Inf) = 0;
D = rot90(D);
fclose(fid);
 
function pfmwrite(D, filename)
% assert(size(D, 3) == 1 & (isa(D, 'single') ));
 
[rows, cols] = size(D);
scale = -1.0/ max(max(D));
fid = fopen(filename, 'wb');
 
fprintf(fid, 'Pf\n');
fprintf(fid, '%d %d\n', cols, rows);
fprintf(fid, '%f\n', scale);
%fscanf(fid, '%c', 1);
 
fwrite(fid, D(end:-1:1, :)', 'single');
fclose(fid);
end
```

## description
关于pfm格式，从来没有官方权威的定义，但是常常在一些场合用到，如生物医学成像，红外成像等，尤其是其浮点方式的存储的位图使得其在科研和学习场合应用都很方便，Middlebury数据库中的视差图像就是以pfm格式进行存储的。

## PMF格式
PMF格式主要有两部分组成：头、元数据。

头有三行：
第一行，标识灰度、彩色的头，PF代表彩色三通道，Pf代表灰度单通道。
第二行，标识图像大大小，行-列。
第三行，标识数，正数标识大端存储，负数标识小端存储，其绝对值为scale。

元数据：
就是紧密排列的浮点数，每个四字节，总体来数，就是和bmp位图很像。

## PMF格式文件的查看

        推荐一款工具cvkit，非常好用，还可以直接处理Middleburry双目图像生成立体图

