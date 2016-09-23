---
layout: post
title:  "How to use pickle class to serialize any object in Python"
date:   2016-09-23 15:35:00 +0700
categories: python, pickle, serialization
---

I remember the day when I use java. It was very painful trying to make java class
serializable. IMHO, any object should be able to serial it current state to anywhere
seamlessly. Because it's just a binary after all.

My dream comes true when I got to know python pickle. With very convenience steps to use.
To serialize to file, you just have to:


1. import pickle
2. open file
3. dump to file
4. close file

To deserialize it, you just have to:


1. import pickle
2. open file which contains pickled data
3. load that file
4. close file and there you go.

Example serialize code:

```python
import pickle
filename = "stateFile.pickle"
file = open(filename, "wb")

arr = ["any","object","will","do",1,2,3]

pickle.dump(arr, file)

file.close()
```

Example deserialize code:

```python
import pickle
filename = "stateFile.pickle"
file = open(filename, "r")

loadedArr = pickle.load(file)

file.close()
```

Easy huh?