---
layout: post
title: tensorflow share parameter 
author: Mizuha Ki
date: 2019-05-08
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

## tf.Variable()定义变量
```python
tf.Variable(
    initial_value=None,# 第一个参数是必填参数
    trainable=True,
    collections=None,
    validate_shape=True,
    caching_device=None,
    name=None,
    variable_def=None,
    dtype=None,
    expected_shape=None,
    import_scope=None)
```

[tf.Variable()](https://www.tensorflow.org/api_docs/python/tf/Variable)定义图的变量

- initial_value：变量的初始值，以下会有一个总结
- trainable：bool类型，如果为True，会把它加入到GraphKeys.TRAINABLE_VARIABLES，才能对它使用Optimizer
- collections：是一个list类型，指定该图变量的类型、默认为[GraphKeys.GLOBAL_VARIABLES]
- validate_shape：bool类型，如果为False，则不进行类型和维度检查
- name：是string类型，变量的名称，如果没有指定则系统会自动分配一个唯一的值（可选参数）

## tf.Variable()的初始化
```python
## random tensor
tf.random_normal(shape, mean=0.0, stddev=1.0, dtype=tf.float32, seed=None, name=None)
tf.truncated_normal(shape, mean=0.0, stddev=1.0, dtype=tf.float32, seed=None, name=None)
tf.random_uniform(shape, minval=0, maxval=None, dtype=tf.float32, seed=None, name=None)
tf.random_shuffle(value, seed=None, name=None)
tf.random_crop(value, size, seed=None, name=None)
tf.multinomial(logits, num_samples, seed=None, name=None)
tf.random_gamma(shape, alpha, beta=None, dtype=tf.float32, seed=None, name=None)
tf.set_random_seed(seed)

## constant value Tensor
tf.zeros(shape, dtype=tf.float32, name=None)
tf.zeros_like(tensor, dtype=None, name=None)
tf.ones(shape, dtype=tf.float32, name=None)
tf.ones_like(tensor, dtype=None, name=None)
tf.fill(dims, value, name=None)
tf.constant(value, dtype=None, shape=None, name='Const')
```

## tf.get_variable()
```python
tf.get_variable(
    name,   #name是一个必填参数，与之前见过的函数不一样！！！！
    shape=None,
    dtype=None,
    initializer=None,
    regularizer=None,
    trainable=True,
    collections=None,
    caching_device=None,
    partitioner=None,
    validate_shape=True,
    use_resource=None,
    custom_getter=None
)
```
[tf.get_variable()](https://www.tensorflow.org/api_docs/python/tf/get_variable)定义图的变量
 - name：新变量或现有变量的名称，这个参数是必须的，函数会根据变量名称去创建或者获取变量。
- shape：新变量或现有变量的形状或者维度。
- dtype：新变量或现有变量的类型（默认为 DT_FLOAT）。
- initializer：创建变量的初始化器，初始化变量。初始化的方式在下面会有一个归纳
- regularizer：一个函数（张量 - >张量或无）；将其应用于新创建的变量的结果将被添加到集合 tf.GraphKeys.REGULARIZATION_LOSSES 中，并可用于正则化。
- trainable：如果为 True，还将变量添加到图形集合：GraphKeys.TRAINABLE_VARIABLES。
- collections：要将变量添加到其中的图形集合键的列表。默认为 [GraphKeys.LOCAL_VARIABLES]。
- partitioner：（可选）可调用性，它接受要创建的变量的完全定义的 TensorShape 和 dtype，并且返回每个坐标轴的分区列表（当前只能对一个坐标轴进行分区）
- validate_shape：如果为假，则允许使用未知形状的值（也就是shape=[],方括号里面不填任何东西，包括空格）初始化变量。如果为真，则默认情况下，initial_value 的形状必须是已知的。
- use_resource：如果为假，则创建一个常规变量。如果为真，则创建一个实验性的 ResourceVariable，而不是具有明确定义的语义。默认为假（稍后将更改为真）。

## tf.get_variable()的初始化
```python
tf.constant_initializer #常量初始化函数
tf.random_normal_initializer  #正态分布
tf.truncated_normal_initializer  #截取的正态分布
tf.random_uniform_initializer  #均匀分布
tf.zeros_initializer  #全部是0
tf.ones_initializer  #全是1
tf.uniform_unit_scaling_initializer  ##满足均匀分布，但不影响输出数量级的随机值

## example

import tensorflow as tf
import numpy as np
import matplotlib.pyplot as plt
a1 = tf.get_variable(name='a1', shape=[2,3], initializer=tf.random_normal_initializer(mean=0, stddev=1))
a2 = tf.get_variable(name='a2', shape=[1], initializer=tf.constant_initializer(1))
a3 = tf.get_variable(name='a3', shape=[2,3], initializer=tf.ones_initializer())
 
with tf.Session() as sess:
	sess.run(tf.initialize_all_variables())
	print sess.run(a1)
	print sess.run(a2)
	print sess.run(a3)
```

## tf.variable_scope()
嵌套的作用域附加名字所用的规则和文件目录的规则很类似：
```python
with tf.variable_scope("foo"):
    with tf.variable_scope("bar"):
        v = tf.get_variable("v", [1])
assert v.name == "foo/bar/v:0"
```
当前变量作用域可以用tf.get_variable_scope()里面不需要参数进行检索并且reuse 标签可以通过调用tf.get_variable_scope().reuse_variables()里面也不需要参数设置为True .设置方法在上面有举例。注意你不能设置reuse标签为False。即使你不能直接设置 reuse 为 False ,但是你可以输入一个重用变量作用域,然后就释放掉,就成为非重用的变量.当打开一个变量作用域时,使用reuse=True 作为参数是可以的.但也要注意，同一个原因，reuse 参数是不可继承.所以当你打开一个重用变量作用域，那么所有的子作用域也将会被重用.
```python
with tf.variable_scope("root"):
    # At start, the scope is not reusing.
    assert tf.get_variable_scope().reuse == False
    with tf.variable_scope("foo"):
        # Opened a sub-scope, still not reusing.
        assert tf.get_variable_scope().reuse == False
    with tf.variable_scope("foo", reuse=True): 这里打开共享
        # Explicitly opened a reusing scope.
        assert tf.get_variable_scope().reuse == True
        with tf.variable_scope("bar"):
            # Now sub-scope inherits the reuse flag.
            assert tf.get_variable_scope().reuse == True
    # Exited the reusing scope, back to a non-reusing one.
    assert tf.get_variable_scope().reuse == False
```

## description
### name
使用tf.Variable时，如果检测到命名冲突，系统会自己处理。使用tf.get_variable()时，系统不会处理冲突，而会报错。实际上由于tf.Variable() 每次都在创建新对象，所有reuse=True 和它并没有什么关系。对于get_variable()，来说，在某个作用域下如果已经有创建的变量对象，同时要满足标签reuse=True ，就把那个对象返回（也就是共享）没有创建变量；如果没有存在想要创建的变量对象的话，同时标签reuse=False(默认），就创建一个新的（这个时候才创建新对象）。
####  variable可以创建两个name相同（都为w_1）的变量
```python
import tensorflow as tf
w_1 = tf.Variable(3,name="w_1")
w_2 = tf.Variable(1,name="w_1")
print w_1.name
print w_2.name
#输出实际上创建了两个不同的变量
#w_1:0
#w_1_1:0
```
#### get_variable在同一个作用域下（这个作用域是默认的）不能创建两个name相同（都为w_1）的变量

```python
import tensorflow as tf
w_1 = tf.get_variable(name="w_1",initializer=1)
w_2 = tf.get_variable(name="w_1",initializer=2)
#下面是错误信息
#ValueError: Variable w_1 already exists, disallowed. Did
#you mean to set reuse=True in VarScope?
```

### reuse
tf.get_variable()它的工作方式根据当前的变量域（Variable Scope）的reuse属性变化而变化，我们可以通过tf.get_variable_scope().reuse来查看这个属性，它默认是False。
#### 变量的实际名称=作用域+name的字符窜
```python
with tf.variable_scope("foo"): # reuse默认是False
    v = tf.get_variable("v", [1])
assert v.name == "foo/v:0"
```
#### tf.get_variable_scope().reuse == True时，作用域是为重用变量所设置
这种情况下，调用就会搜索一个已经存在的变量，他的全称和当前变量的作用域名+所提供的名字是否相等.如果不存在相应的变量，就会抛出ValueError 错误.如果变量找到了，就返回这个变量.
```python
with tf.variable_scope("foo"):
    v = tf.get_variable("v", [1])
with tf.variable_scope("foo", reuse=True):
    v1 = tf.get_variable("v", [1])
assert v1 == v 
## 输出可以知道
v1.name==v.name=='foo/v:0'
```


