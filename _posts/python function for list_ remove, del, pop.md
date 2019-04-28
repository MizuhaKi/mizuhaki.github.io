# python function for list
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
