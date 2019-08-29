---
layout: post
title:  list method for python
author: Mizuha Ki
date: 2018-10-09
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

## remove()
list.remove(value)
```python
list = [2, 3, 4, 5, 6, 3] 
print(list)
>> [2, 3, 4, 5, 6, 3]
list.remove(3)
print(list)
>>[2, 4, 5, 6, 3]
```

## del()
del list[index]
```python
list = [2, 3, 4, 5, 6, 3] 
print(list)
>> [2, 3, 4, 5, 6, 3]
del list[2]
print(list)
>>[2, 3, 5, 6, 3]
```

## pop()
list.pop(index)
```python
list = [2, 3, 4, 5, 6, 3] 
print(list)
>> [2, 3, 4, 5, 6, 3]
top = list.pop(2)
print(top, list)
>>4 [2, 4, 5, 6, 3]
```
