---
layout: post
title:  "Python in-memory file using StringIO"
date:   2017-06-27 03:30:00 +0700
categories: Python, Python3
comments: yes
---

StringIO is a class that represents an in-memory file. In Python3, this class is moved into
`io` module. There are two IO type class in `io` namely `io.StringIO` and `io.BytesIO` for text and
data respectively.

Normally we use BytesIO if we don't want to interpret the data.


```python3
from io import BytesIO

in_memory_file = BytesIO()
in_memory_file.write(b'hello world')
    
print(in_memory_file.getvalues())

in_memory_file.close() # will lose all data.
```