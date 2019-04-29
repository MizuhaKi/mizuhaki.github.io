---
layout: post
title: embedding representation visualization
author: Mizuha Ki
date: 2019-04-18
categories:
- computer science
- deep learning
- python
tags:
- computer science
- deep learning
- python
- blog
---

## a code example
```python
import numpy as np
from sklearn.manifold import TSNE
import matplotlib.pyplot as plt


#embedding = np.loadtxt('word_embedding.txt', skiprows = 1)
with open('word_embedding.txt', 'r') as fin:
    firstline = fin.readline().strip().split()
    idx, dims = int(firstline[0]), int(firstline[1])
    embedding = np.zeros([idx, dims], dtype = np.float)
    lines = fin.readlines()
    for line in lines:
        i = 1
        line = line.strip().split(' ')
        if len(line) > 1:
            embedding[i] = line[1:]
            i = i + 1

print('idx = {}, dims = {}, embedding = {}\n'.format(idx, dims, embedding.shape))

emb = TSNE(n_components = 2).fit_transform(embedding)

plt.switch_backend('pdf')
plt.figure(1)
plt.scatter(emb[:, 0], emb[:, 1])
plt.title('word_embedding')
plt.xlabel('dim 1')
plt.ylabel('dim 2')

plt.savefig('word_embedding.jpg')
```