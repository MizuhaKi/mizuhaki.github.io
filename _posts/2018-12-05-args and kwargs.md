---
layout: post
title: \*args and \*\*kwargs for python
author: Mizuha Ki
date: 2018-12-05
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

## an example
```python
def func(*args, **kwargs):
    print ('args =', args)
    print ('kwargs = ', kwargs)
    print ('-----------', flush = True)

if __name__ == '__main__':
    func('name', 11, 'a', 4)
    func(a = 'name', b = 11, c = 'a',  d = 4)
    func('name', 11, 'a', 4, a = 'name', b = 11, c = 'a',  d = 4)
    func('name', 11, 'a', None, a = 'name', b = 11, c = 'a',  d = None)
```

## output
```python
args = ('name', 11, 'a', 4)
kwargs =  {}
-----------
args = ()
kwargs =  {'a': 'name', 'b': 11, 'c': 'a', 'd': 4}
-----------
args = ('name', 11, 'a', 4)
kwargs =  {'a': 'name', 'b': 11, 'c': 'a', 'd': 4}
-----------
args = ('name', 11, 'a', None)
kwargs =  {'a': 'name', 'b': 11, 'c': 'a', 'd': None}
-----------
-----------
```

## description
- **\*args** and **\*\*kwargs** are changeable function parameters
- **\*args** is a tuple 
- **\*\*kwargs** is a dict



