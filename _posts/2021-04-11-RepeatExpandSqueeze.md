---
layout: post
title: squeeze unsqueeze size view repeat expand expand_as cat split transpose permute matmul mul mm einsum
author: Mizuha Ki
date: 2021-04-11
categories:
- squeeze
- unsqueeze
- size
- view
- repeat
- expand
- expand_as
- cat
- split
- transpose
- permute
- matmul
- mul
- mm
- einsum
- pytorch
- docker
tags:
- squeeze
- unsqueeze
- size
- view
- repeat
- expand
- expand_as
- cat
- split
- transpose
- permute
- matmul
- mul
- mm
- einsum
- pytorch
- docker
- blog
---


## Introduction
- The torch package contains data structures for multi-dimensional tensors and defines mathematical operations over these tensors. Additionally, it provides many utilities for efficient serializing of Tensors and arbitrary types, and other useful utilities.
- Some frequently used tools for deep networks on pytorch.

## Example and Description
### squeeze and unsqueeze
- [torch.squeeze](https://pytorch.org/docs/stable/generated/torch.squeeze.html?highlight=squeeze#torch.squeeze)(.squeeze()): Returns a tensor with all the dimensions of input of size 1 removed.
- [torch.unsqueeze](https://pytorch.org/docs/stable/generated/torch.unsqueeze.html?highlight=unsqueeze#torch.unsqueeze)(.unsqueeze()): Returns a new tensor with a dimension of size one inserted at the specified position.

### example 
```bash
>>> x = torch.tensor([1, 2, 3, 4])
>>> torch.unsqueeze(x, 0)
tensor([[ 1,  2,  3,  4]])
>>> torch.unsqueeze(x, 1)
tensor([[ 1],
        [ 2],
        [ 3],
        [ 4]])

>>> x = torch.zeros(2, 1, 2, 1, 2)
>>> x.size()
torch.Size([2, 1, 2, 1, 2])
>>> y = torch.squeeze(x)
>>> y.size()
torch.Size([2, 2, 2])
>>> y = torch.squeeze(x, 0)
>>> y.size()
torch.Size([2, 1, 2, 1, 2])
>>> y = torch.squeeze(x, 1)
>>> y.size()
torch.Size([2, 2, 1, 2])
```

### size and view
- [size](https://pytorch.org/docs/stable/tensors.html?highlight=size#torch.Tensor.size): Returns the size of the self tensor. The returned value is a subclass of tuple.
- [view](https://pytorch.org/docs/stable/tensors.html?highlight=view#torch.Tensor.view):Returns a new tensor with the same data as the self tensor but of a different shape.

### example
```bash
>>> torch.empty(3, 4, 5).size()
torch.Size([3, 4, 5])

>>> x = torch.randn(4, 4)
>>> x.size()
torch.Size([4, 4])
>>> y = x.view(16)
>>> y.size()
torch.Size([16])
>>> z = x.view(-1, 8)  # the size -1 is inferred from other dimensions
>>> z.size()
torch.Size([2, 8])

>>> a = torch.randn(1, 2, 3, 4)
>>> a.size()
torch.Size([1, 2, 3, 4])
>>> b = a.transpose(1, 2)  # Swaps 2nd and 3rd dimension
>>> b.size()
torch.Size([1, 3, 2, 4])
>>> c = a.view(1, 3, 2, 4)  # Does not change tensor layout in memory
>>> c.size()
torch.Size([1, 3, 2, 4])
>>> torch.equal(b, c)
False
```

### repeat, expand and expand_as
- [repeat](https://pytorch.org/docs/stable/tensors.html?highlight=torch%20repeat#torch.Tensor.repeat): Repeats this tensor along the specified dimensions.
- [expand](https://pytorch.org/docs/stable/tensors.html?highlight=expand#torch.Tensor.expand): Returns a new view of the self tensor with singleton dimensions expanded to a larger size.
- [expand_as](https://pytorch.org/docs/stable/tensors.html?highlight=expand#torch.Tensor.expand): Expand this tensor to the same size as other. self.expand_as(other) is equivalent to self.expand(other.size()).

### example 
```bash
>>> x = torch.tensor([1, 2, 3])
>>> x.repeat(4, 2)
tensor([[ 1,  2,  3,  1,  2,  3],
        [ 1,  2,  3,  1,  2,  3],
        [ 1,  2,  3,  1,  2,  3],
        [ 1,  2,  3,  1,  2,  3]])
>>> x.repeat(4, 2, 1).size()
torch.Size([4, 2, 3])

>>> x = torch.tensor([[1], [2], [3]])
>>> x.size()
torch.Size([3, 1])
>>> x.expand(3, 4)
tensor([[ 1,  1,  1,  1],
        [ 2,  2,  2,  2],
        [ 3,  3,  3,  3]])
>>> x.expand(-1, 4)   # -1 means not changing the size of that dimension
tensor([[ 1,  1,  1,  1],
        [ 2,  2,  2,  2],
        [ 3,  3,  3,  3]])
```
 
### cat and split
- [torch.cat](https://pytorch.org/docs/stable/generated/torch.cat.html?highlight=torch%20cat#torch.cat): Concatenates the given sequence of seq tensors in the given dimension. All tensors must either have the same shape (except in the concatenating dimension) or be empty.
- [torch.split](https://pytorch.org/docs/stable/generated/torch.split.html#torch.split): Splits the tensor into chunks. Each chunk is a view of the original tensor.

### example
```bash
>>> x = torch.randn(2, 3)
>>> x
tensor([[ 0.6580, -1.0969, -0.4614],
        [-0.1034, -0.5790,  0.1497]])
>>> torch.cat((x, x, x), 0)
tensor([[ 0.6580, -1.0969, -0.4614],
        [-0.1034, -0.5790,  0.1497],
        [ 0.6580, -1.0969, -0.4614],
        [-0.1034, -0.5790,  0.1497],
        [ 0.6580, -1.0969, -0.4614],
        [-0.1034, -0.5790,  0.1497]])
>>> torch.cat((x, x, x), 1)
tensor([[ 0.6580, -1.0969, -0.4614,  0.6580, -1.0969, -0.4614,  0.6580,
         -1.0969, -0.4614],
        [-0.1034, -0.5790,  0.1497, -0.1034, -0.5790,  0.1497, -0.1034,
         -0.5790,  0.1497]])

>>> a = torch.arange(10).reshape(5,2)
>>> a
tensor([[0, 1],
        [2, 3],
        [4, 5],
        [6, 7],
        [8, 9]])
>>> torch.split(a, 2)
(tensor([[0, 1],
         [2, 3]]),
 tensor([[4, 5],
         [6, 7]]),
 tensor([[8, 9]]))
>>> torch.split(a, [1,4])
(tensor([[0, 1]]),
 tensor([[2, 3],
         [4, 5],
         [6, 7],
         [8, 9]]))
```

### transpose and permute
- [torch.transpose](https://pytorch.org/docs/stable/generated/torch.transpose.html?highlight=transpose#torch.transpose)(.transpose()): Returns a tensor that is a transposed version of input. The given dimensions dim0 and dim1 are swapped.
- [permute](https://pytorch.org/docs/stable/tensors.html?highlight=torch%20permute#torch.Tensor.permute): Returns a view of the original tensor with its dimensions permuted.

### example
```bash
>>> x = torch.randn(2, 3)
>>> x
tensor([[ 1.0028, -0.9893,  0.5809],
        [-0.1669,  0.7299,  0.4942]])
>>> torch.transpose(x, 0, 1)
tensor([[ 1.0028, -0.1669],
        [-0.9893,  0.7299],
        [ 0.5809,  0.4942]])

>>> x = torch.randn(2, 3, 5)
>>> x.size()
torch.Size([2, 3, 5])
>>> x.permute(2, 0, 1).size()
torch.Size([5, 2, 3])
```

### matmul, mul and mm
- [matmul](https://pytorch.org/docs/stable/generated/torch.matmul.html?highlight=matmul): Matrix product of two tensors.
- [mul](https://pytorch.org/docs/stable/generated/torch.mul.html?highlight=mul#torch.mul): Multiplies each element of the input input with the scalar other and returns a new resulting tensor.
- [mm](https://pytorch.org/docs/stable/generated/torch.mm.html?highlight=mm#torch.mm): Performs a matrix multiplication of the matrices input and mat2.

### example
```bash
>>> # vector x vector
>>> tensor1 = torch.randn(3)
>>> tensor2 = torch.randn(3)
>>> torch.matmul(tensor1, tensor2).size()
torch.Size([])
>>> # matrix x vector
>>> tensor1 = torch.randn(3, 4)
>>> tensor2 = torch.randn(4)
>>> torch.matmul(tensor1, tensor2).size()
torch.Size([3])
>>> # batched matrix x broadcasted vector
>>> tensor1 = torch.randn(10, 3, 4)
>>> tensor2 = torch.randn(4)
>>> torch.matmul(tensor1, tensor2).size()
torch.Size([10, 3])
>>> # batched matrix x batched matrix
>>> tensor1 = torch.randn(10, 3, 4)
>>> tensor2 = torch.randn(10, 4, 5)
>>> torch.matmul(tensor1, tensor2).size()
torch.Size([10, 3, 5])
>>> # batched matrix x broadcasted matrix
>>> tensor1 = torch.randn(10, 3, 4)
>>> tensor2 = torch.randn(4, 5)
>>> torch.matmul(tensor1, tensor2).size()
torch.Size([10, 3, 5])

>>> a = torch.randn(3)
>>> a
tensor([ 0.2015, -0.4255,  2.6087])
>>> torch.mul(a, 100)
tensor([  20.1494,  -42.5491,  260.8663])
>>> a = torch.randn(4, 1)
>>> a
tensor([[ 1.1207],
        [-0.3137],
        [ 0.0700],
        [ 0.8378]])
>>> b = torch.randn(1, 4)
>>> b
tensor([[ 0.5146,  0.1216, -0.5244,  2.2382]])
>>> torch.mul(a, b)
tensor([[ 0.5767,  0.1363, -0.5877,  2.5083],
        [-0.1614, -0.0382,  0.1645, -0.7021],
        [ 0.0360,  0.0085, -0.0367,  0.1567],
        [ 0.4312,  0.1019, -0.4394,  1.8753]])

>>> mat1 = torch.randn(2, 3)
>>> mat2 = torch.randn(3, 3)
>>> torch.mm(mat1, mat2)
tensor([[ 0.4851,  0.5037, -0.3633],
        [-0.0760, -3.6705,  2.4784]])

```

### einsum
- [einsum](https://pytorch.org/docs/stable/generated/torch.einsum.html?highlight=einsum#torch.einsum): Sums the product of the elements of the input operands along dimensions specified using a notation based on the Einstein summation convention.

### example
```bash
# trace
>>> torch.einsum('ii', torch.randn(4, 4))
tensor(-1.2104)

# diagonal
>>> torch.einsum('ii->i', torch.randn(4, 4))
tensor([-0.1034,  0.7952, -0.2433,  0.4545])

# outer product
>>> x = torch.randn(5)
>>> y = torch.randn(4)
>>> torch.einsum('i,j->ij', x, y)
tensor([[ 0.1156, -0.2897, -0.3918,  0.4963],
        [-0.3744,  0.9381,  1.2685, -1.6070],
        [ 0.7208, -1.8058, -2.4419,  3.0936],
        [ 0.1713, -0.4291, -0.5802,  0.7350],
        [ 0.5704, -1.4290, -1.9323,  2.4480]])

# batch matrix multiplication
>>> As = torch.randn(3,2,5)
>>> Bs = torch.randn(3,5,4)
>>> torch.einsum('bij,bjk->bik', As, Bs)
tensor([[[-1.0564, -1.5904,  3.2023,  3.1271],
        [-1.6706, -0.8097, -0.8025, -2.1183]],

        [[ 4.2239,  0.3107, -0.5756, -0.2354],
        [-1.4558, -0.3460,  1.5087, -0.8530]],

        [[ 2.8153,  1.8787, -4.3839, -1.2112],
        [ 0.3728, -2.1131,  0.0921,  0.8305]]])

# batch permute
>>> A = torch.randn(2, 3, 4, 5)
>>> torch.einsum('...ij->...ji', A).shape
torch.Size([2, 3, 5, 4])

# equivalent to torch.nn.functional.bilinear
>>> A = torch.randn(3,5,4)
>>> l = torch.randn(2,5)
>>> r = torch.randn(2,4)
>>> torch.einsum('bn,anm,bm->ba', l, A, r)
tensor([[-0.3430, -5.2405,  0.4494],
        [ 0.3311,  5.5201, -3.0356]])
```


