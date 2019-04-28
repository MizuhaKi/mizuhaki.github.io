---
layout: post
title: @ for python
author: Mizuha Ki
date: 2018-12-13
categories:
- computer science
- deep learning
- @
tags:
- computer science
- deep learning
- @
- blog
---

##  a example of code
```python
def func1(a): 
    def b(*args, **kwargs):
        print('a = ', a)
        output = a(*args, **kwargs)
        output = output ** 2
        print('func1 =', output)
        return output
    return b

@func1
def func2(b):
    output = b + 2
    print('func2 =', output)
    return output

if __name__ == '__main__' :
    output = func2(1)
    print('output = ', output)
```

## results
```python
a =  <function func2 at 0x7f67690f9ae8>
func2 = 3
func1 = 9
output =  9
```

## description
An @ symbol at the beginning of a line is used for class, function and method decorators.
Read more here:
[PEP 318: Decorators](http://www.python.org/dev/peps/pep-0318/)
[Python Decorators](http://wiki.python.org/moin/PythonDecorators)
The most common Python decorators you will run into are:
[@property](http://docs.python.org/library/functions.html#property)
[@classmethod](http://docs.python.org/library/functions.html#classmethod)
[@staticmethod](http://docs.python.org/library/functions.html#staticmethod)
If you see an @ in the middle of a line, that is a different thing, matrix multiplication.
