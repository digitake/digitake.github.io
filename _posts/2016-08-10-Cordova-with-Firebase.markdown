---
layout: post
title:  "How to use cordova with firebase on android"
date:   2016-08-10 19:29:00 +0700
categories: cordova, google-firebase, android
---

To use firebase with cordova-android, one can follow these steps:

1. create a new cordova build.

        cordova create <path> <app-id> <project-name>

2. add android platform.

        cordova platform add android

3. modify `platforms/android/build.gradle` file.
add line given from firebase console to this file.

4. add android-services.json to `platforms/android` path.

5. run `gradle sync` to resync gradle.

6. now you can run cordova app with firebase `cordova run android`

