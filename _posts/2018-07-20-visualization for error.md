---
layout: post
title: visualization for error
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
% error visualization
clear all; clc;

C = [80.72, 81.17, 80.45, 81.17, 80.81];
C_idx = [1, 2, 3, 4, 5];
C_e = [2.35, 3.25, 3.04, 2.14, 2.79];

figure(1)
errorbar(C_idx, C, C_e, '-s', 'LineWidth', 2, 'MarkerSize', 10, ...
    'MarkerEdgeColor', 'red', 'MarkerFaceColor', 'red');
%title('##');
xlabel('Gaussian components C');
ylabel('Accuracy');
legend('ACC');
axis([0 6 60 90]);
grid;
```