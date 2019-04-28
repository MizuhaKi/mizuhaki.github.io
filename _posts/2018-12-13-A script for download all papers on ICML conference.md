---
layout: post
title: A script for download all papers on ICML conference
author: Mizuha Ki
date: 2018-12-13
categories:
- computer science
- tool
- script
tags:
- computer science
- tool
- script
- blog
---

## script code
```python
# coding=utf-8
from multiprocessing import Pool
import requests
from bs4 import BeautifulSoup
import traceback
import re
import os
import pdb

prefix = 'http://proceedings.mlr.press/v80/'
save_dir = 'icml2018'

def get_pdf(data):
    href, title = data
    name = re.sub(r'[\\/:*?"<>|\bx0\u2019\u2014\xb0\u2013]', ' ', title) 
    if os.path.isfile(save_dir+"/icml18-%s.pdf" % name):
        print("File already exsists, skip %s" % name)
        return
    try:
        content = requests.get(href).content
        with open(save_dir+"/icml18-%s.pdf" % name, 'wb') as f:  # You may change to "path/to/your/folder"
            f.write(content)
        print("Finish downloading %s" % title)
    except:
        print('Error when downloading %s' % href)
        print(traceback.format_exc())
        
pool = Pool(100)
if not os.path.exists(save_dir):
    os.mkdir(save_dir)
html = requests.get(prefix).content
soup = BeautifulSoup(html, "lxml")
a_list = soup.findAll("p", {"class": "links"})
title_list = soup.findAll("p", {"class": "title"})
title_list = [_.text for _ in title_list]
pdf_list = []
for everya in a_list:
    if everya.contents[3].text == "Download PDF":
        href = everya.contents[3].get("href")
        pdf_list.append(href)
assert len(pdf_list) == len(title_list), "numbers of title and pdf not euqal"
print("Find %d papers" % len(pdf_list))
pool.map(get_pdf, zip(pdf_list, title_list))
print("Find %d papers" % len(pdf_list))
```
