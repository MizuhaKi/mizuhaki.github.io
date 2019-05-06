---
layout: post
title: tensorflow and cuda version
author: Mizuha Ki
date: 2019-05-06
categories:
- computer science
- deep learning
- tensorflow
tags:
- computer science
- deep learning
- tensorflow
- blog
---

## tensorflow各个版本需要的CUDA版本以及Cudnn的对应关系
相应的网址为：
[tensorflow install for linux and macOS](https://www.tensorflow.org/install/source#common_installation_problems)
[tensorflow install for windows](https://www.tensorflow.org/install/source_windows)

版本 | Python 版本 | 编译器 | 编译工具 | cuDNN | CUDA
--- | --- | --- | --- | --- |---
tensorflow_gpu-2.0.0-alpha0 | 2.7、3.3-3.6 | GCC 4.8 | Bazel 0.19.2 | 7.4.1以及更高版本 | CUDA 10.0 (需要 410.x 或更高版本)
tensorflow_gpu-1.13.0 | 2.7、3.3-3.6 | GCC 4.8 | Bazel 0.19.2 | 7.4 | 10.0
tensorflow_gpu-1.12.0 | 2.7、3.3-3.6 | GCC 4.8 | Bazel 0.15.0 | 7 | 9
tensorflow_gpu-1.11.0 | 2.7、3.3-3.6 | GCC 4.8 | Bazel 0.15.0 | 7 | 9
tensorflow_gpu-1.10.0 | 2.7、3.3-3.6 | GCC 4.8 | Bazel 0.15.0 | 7 | 9
tensorflow_gpu-1.9.0 | 2.7、3.3-3.6 | GCC 4.8 | Bazel 0.11.0 | 7 | 9
tensorflow_gpu-1.8.0 | 2.7、3.3-3.6 | GCC 4.8 | Bazel 0.10.0 | 7 | 9
tensorflow_gpu-1.7.0 | 2.7、3.3-3.6 | GCC 4.8 | Bazel 0.9.0 | 7 | 9
tensorflow_gpu-1.6.0 | 2.7、3.3-3.6 | GCC 4.8 | Bazel 0.9.0 | 7 | 9
tensorflow_gpu-1.5.0 | 2.7、3.3-3.6 | GCC 4.8 | Bazel 0.8.0 | 7 | 9
tensorflow_gpu-1.4.0 | 2.7、3.3-3.6 | GCC 4.8 | Bazel 0.5.4 | 6 | 8
tensorflow_gpu-1.3.0 | 2.7、3.3-3.6 | GCC 4.8 | Bazel 0.4.5 | 6 | 8
tensorflow_gpu-1.2.0 | 2.7、3.3-3.6 | GCC 4.8 | Bazel 0.4.5 | 5.1 | 8
tensorflow_gpu-1.1.0 | 2.7、3.3-3.6 | GCC 4.8 | Bazel 0.4.2 | 5.1 | 8
tensorflow_gpu-1.0.0 | 2.7、3.3-3.6 | GCC 4.8 | Bazel 0.4.2 | 5.1 | 8

