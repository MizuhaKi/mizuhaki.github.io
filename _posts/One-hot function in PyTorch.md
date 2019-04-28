# One-hot function implementation in [PyTorch](https://pytorch.org/docs/stable/index.html)
---
## Method1: use scatter_ function
```python
labels = [0, 1, 4, 7, 3, 2]
one_hot = torch.zeros(6, 8).scatter_(dim = 1, index = labels, value = 1)
```

## Method2: use index_select() funtion
```python
labels = [0, 1, 4, 7, 3, 2]
index = torch.eye(8)
one_hot = torch.index_select(index, dim = 0, index = labels)
```

## Method3: use Embedding module
```python
emb = nn.Embedding(8, 8)
emb.weight.data = torch.eye(8)
```
then we can get
```
emb(Variable(torch.LongTensor([1, 2], [3, 4])))
Variable containing:
(0,.,.) = 
0 1 0 0 0 0 0 0 
0 0 1 0 0 0 0 0
(1 ,.,.) =
0 0 0 1 0 0 0 0
0 0 0 0 1 0 0 0
```

## Method4: create  a module
```python
class One_Hot(nn.Module):
    def __init__(self, depth):
        super(One_Hot,self).__init__()
        self.depth = depth
        self.ones = torch.sparse.torch.eye(depth)
    def forward(self, X_in):
        X_in = X_in.long()
        return Variable(self.ones.index_select(0,X_in.data))
    def __repr__(self):
        return self.__class__.__name__ + "({})".format(self.depth)
```
