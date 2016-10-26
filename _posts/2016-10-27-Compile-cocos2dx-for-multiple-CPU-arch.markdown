---
layout: post
title:  "Compile cocos2dx for multiple architectures on android"
date:   2016-10-27 10:38:00 +0700
categories: cocos2dx, c++, CPU, android
---

For cocos2dx v3.13

Firstly, try to generate the cpp-tests apk which provided by frameworks.
Execute `android-build.py` in COCOS_X_ROOT/build 

Using `-n` parameter to indicate specific targets you need.

`python build/android-build.py -p android-21 -n armeabi:armeabi-v7a:x86 cpp-tests`

This may take a while.