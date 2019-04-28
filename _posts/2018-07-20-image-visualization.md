---
layout: post
title: image visualization
author: Mizuha Ki
date: 2018-07-20
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
import cPickle
import numpy as np
import matplotlib.pyplot as plt
from matplotlib.patches import Rectangle
#from src import api as vg
from PIL import Image as PIL_Image
import requests
from StringIO import StringIO

obj = []  # 201
rel = []  # 100
index = 120

with open('C:/Users/Administrator/Desktop/python/obj.txt', 'r') as fin:
    for line in fin.readlines():
        line = line.strip().split()
        obj.append(line)
    fin.close()
    
with open('C:/Users/Administrator/Desktop/python/rel.txt', 'r') as fin:
    for line in fin.readlines():
        line = line.strip().split()
        rel.append(line)
    fin.close()


with open('C:/Users/Administrator/Desktop/python/train.pkl', 'rb') as fin:
    anno = cPickle.load(fin)
    img_path = 'C:/Users/Administrator/Desktop/python/visual_genome_python_driver-master/VG_dataset/Version_1.2/' + anno[index]['img_path'][21:]
    boxs = anno[index]['boxes']
    classes = anno[index]['classes']
    ix1 = anno[index]['ix1']
    ix2 = anno[index]['ix2']
    rel_classes = anno[index]['rel_classes']
    fin.close()

    print('anno: {}, boxs = {}, classes = {}, ix1 = {}, ix2 = {}, rel_classes = {}, \nover'.format(anno[index], boxs[0], 
                                                                                        classes[0], ix1[0], ix2[0], rel_classes[0]))

fig = plt.gcf()
fig.set_size_inches(18.5, 10.5)
def visualize_regions(img_path, boxs=None, classes=None, ix1=None, ix2=None, rel_classes=None, obj = None, rel = None):
    #response = requests.get(img_path)
    img = PIL_Image.open(img_path)
    size = img.size
    plt.imshow(img)
    ax = plt.gca()
    print(classes, ix1, ix2, rel_classes, size)
    for i in range(len(classes)):
        classes[i] = obj[classes[i]]
    for i in range(len(ix1)):
        ix1[i] = classes[ix1[i]]
        ix2[i] = classes[ix2[i]]
        for j in range(len(rel_classes[i])):
            rel_classes[i][j] = rel[rel_classes[i][j]]
    print(classes, ix1, ix2, rel_classes)
    for i in range(len(boxs)):
        box = boxs[i]
        cla = classes[i]
        if i == 0:
            ax.add_patch(Rectangle((box[0], box[1]), box[2] - box[0], box[3] - box[1], fill=False, edgecolor='green', linewidth=7))
        elif i == 1:
            ax.add_patch(Rectangle((box[0], box[1]), box[2] - box[0], box[3] - box[1], fill=False, edgecolor='red', linewidth=7))
        elif i == 2:
            ax.add_patch(Rectangle((box[0], box[1]), box[2] - box[0], box[3] - box[1], fill=False, edgecolor='blue', linewidth=7))
        else:
            ax.add_patch(Rectangle((box[0], box[1]), box[2] - box[0], box[3] - box[1], fill=False, edgecolor='yellow', linewidth=7))
        phrase = str(cla)
        ax.text(box[0], box[1], phrase, style='italic', bbox={'facecolor':'white', 'alpha': 0.7, 'pad': 1}, fontsize = 24)
    
    for i in range(len(ix1)):
        if i == 0:
            phrase = ix1[i] + ix2[i] + rel_classes[i]
        else:
            phrase = phrase + ix1[i] + ix2[i] + rel_classes[i]
    #ax.text(12, 16, phrase, style='italic', bbox={'facecolor':'white'})
    fig = plt.gcf()
    plt.tick_params(labelbottom='off', labelleft='off')
    plt.subplots_adjust(top=1,bottom=0,left=0,right=1,hspace=0,wspace=0)
    plt.savefig('giraffe.png', dpi=100)
    plt.show()

    
visualize_regions(img_path, boxs, classes, ix1, ix2, rel_classes, obj = obj, rel = rel)    
```