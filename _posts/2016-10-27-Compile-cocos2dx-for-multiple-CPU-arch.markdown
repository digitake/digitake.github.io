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
cocos keep using a default android API version lower than 13. You'd better keep is option on.
Or another solution is to uninstall all your APIs which version are lower than 13, then you can omit this option.

-----
The other way to build native image for Cocos2D without using command line is to use gradle to hook `ndk-build` command.
Doing so first thing you need to know is that android-studio will auto-generate `Android.mk` file to build native image.
That means whatever config in jni folder is meaningless. Hence, we have to disable this default behavior by add `jni.srcDirs = []`
under `sourceSets.main` config. Then we create a gradle Exec task `ndkBuild`. 

```gradle
task ndkBuild(type: Exec) {
    def ndkDir = android.ndkDirectory.getAbsolutePath() //Because gradle hates environment variable.
    if (Os.isFamily(Os.FAMILY_WINDOWS)) {
        commandLine ndkDir+'/ndk-build.cmd', '-C', file('src/main').absolutePath
    } else {
        commandLine ndkDir+'/ndk-build', '-C', file('src/main').absolutePath
    }
}
```

And then make it run before java compilation.

```gradle
tasks.withType(JavaCompile) {
    compileTask -> compileTask.dependsOn ndkBuild
}
```

From this point, gradle will build ndk regarded to jni/Android.mk and jni/Application.mk.
Go to Application.mk and make sure that `APP_ABI := armeabi armeabi-v7a x86`.

You may also want to separated `productFlavors` to create multiple apks.
Just go back to `build.gradle` and add abiFilter as shown below:

```gradle
    productFlavors {
        x86 {
            ndk {
                abiFilter "x86"
            }
        }
        armv7 {
            ndk {
                abiFilter "armeabi-v7a"
            }
        }
        arm {
            ndk {
                abiFilter "armeabi"
            }
        }
        fat
    }
```

Now you are ready to use android-studio to build Cocos game without hopping forth and back to console.


Full build.gradle file is shown below:
```gradle
import org.apache.tools.ant.taskdefs.condition.Os

apply plugin: 'com.android.application'

android {
    compileSdkVersion 22
    buildToolsVersion '24.0.3'

    defaultConfig {
        applicationId "com.package.app"
        minSdkVersion 10
        targetSdkVersion 22
        versionCode 10002
        versionName "1.0.2"
    }

    sourceSets.main {
        java.srcDir "src"
        res.srcDir "res"
        jniLibs.srcDir "libs"
        manifest.srcFile "AndroidManifest.xml"
        assets.srcDir "assets"
        jni.srcDirs = []   //disable automatic ndk-build call
    }

    signingConfigs {

        release {
            if (project.hasProperty("RELEASE_STORE_FILE")) {
                storeFile file(RELEASE_STORE_FILE)
                storePassword RELEASE_STORE_PASSWORD
                keyAlias RELEASE_KEY_ALIAS
                keyPassword RELEASE_KEY_PASSWORD
            }
        }
    }

    buildTypes {
        release {
            minifyEnabled true
            proguardFiles getDefaultProguardFile('proguard-android-optimize.txt'), 'proguard-rules.pro'
            if (project.hasProperty("RELEASE_STORE_FILE")) {
                signingConfig signingConfigs.release
            }
        }
    }

    productFlavors {
        x86 {
            ndk {
                abiFilter "x86"
            }
        }
        armv7 {
            ndk {
                abiFilter "armeabi-v7a"
            }
        }
        arm {
            ndk {
                abiFilter "armeabi"
            }
        }
        fat
    }
}

dependencies {
    compile fileTree(dir: 'libs', include: ['*.jar'])
    compile project(':libcocos2dx')
    compile 'com.android.support:appcompat-v7:22.2.1'
}

task cleanAssets(type: Delete) {
    delete 'assets'
}
task copyAssets(type: Copy) {
    from '../../Resources'
    into 'assets'
}

// call regular ndk-build(.cmd) script from app directory
task ndkBuild(type: Exec) {
    def ndkDir = android.ndkDirectory.getAbsolutePath()
    if (Os.isFamily(Os.FAMILY_WINDOWS)) {
        commandLine ndkDir+'/ndk-build.cmd', '-C', file('src/main').absolutePath
    } else {
        commandLine ndkDir+'/ndk-build', '-C', file('src/main').absolutePath
    }
}

tasks.withType(JavaCompile) {
    compileTask -> compileTask.dependsOn ndkBuild
}


clean.dependsOn cleanAssets
preBuild.dependsOn copyAssets
```