# yield for python

## a example of code
```python
def fun():
    for i in range(20):
        x = yield i
        print('good', x, i)

if __name__ == '__main__':
    a = fun()
    a.__next__()
    a.__next__()
    x1 = a.send(5)
    x2 = a.send(3)
    next(a)
    next(a)
    print(x1, x2)
```

## results
```python
good None 0
good 5 1
good 3 2
good None 3
good None 4
2 3
```

## description
[**yield**](https://wiki.python.org/moin/Generators) generator functions allow you to declare a function that behaves like an iterator. 
