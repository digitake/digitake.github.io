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

After you successfully compiled and installe cpp-tests on your test device.
Now you are ready to create your own project.

Cocos2dx 3.x provides a handy command line. To create new project:

`cocos new <project name> -p <package path e.g. com.yourcompany.yourproject> -l cpp`

and follow by a compilation of your new project in debug mode.

`cocos compile -s <project-dir> -m debug -p android --app-abi armeabi:x86 --ap android-13`

You might not need option `--ap` on your machine. This is environment specific. If you found out that
cocos keep using a default android API version lover than 13. You'd better keep is option on.