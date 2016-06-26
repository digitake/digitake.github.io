---
layout: post
title:  "How to fix psycopg2 Symbol not found: _PQbackendPID on osx"
date:   2016-06-26 22:24:00 +0700
categories: Python, psycopg2, pip, postgresql
---

I've been having this problem for long time. And I couldn't fix it until today.
Let me lay it out things.
psycopg2 is a library that you will use to connect and interact with Postgresql.
Usually, you can install it by `pip install psycopg2` command. This library currently 
support both 32bit and 64bit versions. Python also has both 32 and 64bit versions.

Actually, I think the source of problem comes from the way OSX integrates python as part of the system 
and yet allow you to install another python in some other location. And when versions are mismatch.
There you see the msg that looks like below:


```bash
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "/Library/Python/2.7/site-packages/psycopg2/__init__.py", line 50, in <module>
    from psycopg2._psycopg import BINARY, NUMBER, STRING, DATETIME, ROWID
ImportError: dlopen(/Library/Python/2.7/site-packages/psycopg2/_psycopg.so, 2): Symbol not found: _PQbackendPID
  Referenced from: /Library/Python/2.7/site-packages/psycopg2/_psycopg.so
  Expected in: flat namespace
 in /Library/Python/2.7/site-packages/psycopg2/_psycopg.so
```

To fix this problem:

1. Make sure that you have a correct version of python(or you can have both):
    Check it by this command ``` file `which python` ```.
    On my machine, it yields:


        /Library/Frameworks/Python.framework/Versions/2.7/bin/python: Mach-O universal binary with 2 architectures
        /Library/Frameworks/Python.framework/Versions/2.7/bin/python (for architecture ppc):	Mach-O executable ppc
        /Library/Frameworks/Python.framework/Versions/2.7/bin/python (for architecture i386):	Mach-O executable i386
                
    which means python that I normally use is the one I installed, not the one bundled with osx.
    Now, you can see that there's no x64 version. And that's the true cause of the problem.

2. Solution: I can fix it in two ways:
    1. I can install python2.7 x64 version
    2. I can try python that comes with OSX by execute `/usr/bin/python`.
    
It should fix the problem.
