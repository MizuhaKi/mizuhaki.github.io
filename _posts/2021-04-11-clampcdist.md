---
layout: post
title: clamp cdist where poisson
author: Mizuha Ki
date: 2021-04-11
categories:
- clamp 
- cdist 
- where
- poisson
- pytorch
- docker
tags:
- clamp 
- cdist 
- where
- poisson
- pytorch
- docker
- blog
---


### clamp
- [torch.clamp](https://pytorch.org/docs/stable/generated/torch.clamp.html?highlight=clamp#torch.clamp): Clamp all elements in input into the range [min, max]. Let min_value and max_value be min and max, respectively.

```bash
>>> a = torch.randn(4)
>>> a
tensor([-1.7120,  0.1734, -0.0478, -0.0922])
>>> torch.clamp(a, min=-0.5, max=0.5)
tensor([-0.5000,  0.1734, -0.0478, -0.0922])

>>> a = torch.randn(4)
>>> a
tensor([-0.0299, -2.3184,  2.1593, -0.8883])
>>> torch.clamp(a, min=0.5)
tensor([ 0.5000,  0.5000,  2.1593,  0.5000])

>>> a = torch.randn(4)
>>> a
tensor([ 0.7753, -0.4702, -0.4599,  1.1899])
>>> torch.clamp(a, max=0.5)
tensor([ 0.5000, -0.4702, -0.4599,  0.5000])
```


### cdist 
- [torch.cdist](https://pytorch.org/docs/stable/generated/torch.cdist.html?highlight=cdist#torch.cdist): Computes batched the p-norm distance between each pair of the two collections of row vectors.

```bash
>>> a = torch.tensor([[0.9041,  0.0196], [-0.3108, -2.4423], [-0.4821,  1.059]])
>>> a
tensor([[ 0.9041,  0.0196],
        [-0.3108, -2.4423],
        [-0.4821,  1.0590]])
>>> b = torch.tensor([[-2.1763, -0.4713], [-0.6986,  1.3702]])
>>> b
tensor([[-2.1763, -0.4713],
        [-0.6986,  1.3702]])
>>> torch.cdist(a, b, p=2)
tensor([[3.1193, 2.0959],
        [2.7138, 3.8322],
        [2.2830, 0.3791]])
```


### where
- [torch.where](https://pytorch.org/docs/stable/generated/torch.where.html?highlight=where#torch.where): Return a tensor of elements selected from either x or y, depending on condition.

```bash
>>> x = torch.randn(3, 2)
>>> y = torch.ones(3, 2)
>>> x
tensor([[-0.4620,  0.3139],
        [ 0.3898, -0.7197],
        [ 0.0478, -0.1657]])
>>> torch.where(x > 0, x, y)
tensor([[ 1.0000,  0.3139],
        [ 0.3898,  1.0000],
        [ 0.0478,  1.0000]])
>>> x = torch.randn(2, 2, dtype=torch.double)
>>> x
tensor([[ 1.0779,  0.0383],
        [-0.8785, -1.1089]], dtype=torch.float64)
>>> torch.where(x > 0, x, 0.)
tensor([[1.0779, 0.0383],
        [0.0000, 0.0000]], dtype=torch.float64)
```


### poisson
- [torch.poission](https://pytorch.org/docs/stable/generated/torch.poisson.html?highlight=poisson#torch.poisson): Returns a tensor of the same size as input with each element sampled from a Poisson distribution with rate parameter given by the corresponding element in input.

```bash
>>> rates = torch.rand(4, 4) * 5  # rate parameter between 0 and 5
>>> torch.poisson(rates)
tensor([[9., 1., 3., 5.],
        [8., 6., 6., 0.],
        [0., 4., 5., 3.],
        [2., 1., 4., 2.]])
```