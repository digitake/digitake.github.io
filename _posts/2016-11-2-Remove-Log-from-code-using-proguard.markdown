---
layout: post
title:  "Remove Log from code using proguard"
date:   2016-11-2 22:13:00 +0700
categories: android, proguard, debugging
comments: yes
---

Android **Log** class is a great tool for debugging. However, leaving your code
full of log messages in released version of your app might not be such a good practice.
Let alone security perspective, it just introduce a bit of overheads to code.

So what to do?

Android framework comes with such great tools for fine-tuning your app.
and `proguard` is one of the great tool to reduce you code size.
And, of course, remove `Log` code.

In order to use it to remove `Log` we first have to use `proguard-android-optimize.txt` as a default proguard file.
This setting is in build.gradle of app. As the name implied, it's an optimized version of proguard script which allows
us to remove unused(i.e. no side effect code).

After we have change the default proguard file, then we can just add these lines to proguard's rules:

```
    -assumenosideeffects class android.util.Log {
        public static boolean isLoggable(java.lang.String, int);
        public static int d(...);
        public static int w(...);
        public static int v(...);
        public static int i(...);
    }
```

And there you go.