---
layout: post
title: tensor shape
author: Mizuha Ki
date: 2019-05-06
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

## tf.shape()
```python
import tensorflow as tf
x = tf.constant([2,3,4,5])
shape = tf.shape(x)

with tf.Session() as sess:
	print(sess.run(shape))
```

## tensor.get_shape().as_list()
```python
import tensorflow as tf
x = tf.constant([2,3,4,5])
shape1 = x.get_shape()
shape2 = x.get_shape().as_list()

with tf.Session() as sess:
	print(sess.run(shape1))
	print(sess.run(shape2))
```

