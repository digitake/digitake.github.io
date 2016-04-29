---
layout: post
title:  "Gradle ShortNote 1"
date:   2016-04-30 00:55:00 +0700
categories: Gradle  
---

- Gradle is a build script.
- Based on Groovy which is fully compatible with Java.
- gradlew is a gradle wrapper that will download gradle automatically.
- to install gradle globally on OSX: `brew install gradle`
- normally, it looks for build.gradle file.
- but we can specify any file with option: `gradle -b <path-to-gradle-file>`
- `project` is an object that we can access form Gradle.
- to create task in gradle config: `task <task-name> {}`
- tasks dependencies can be assigned using: dependsOn, finalizedBy, shouldRunAfter
- Typed task is a predefined task. You can check it from: <https://docs.gradle.org/current/dsl/>
- UP-TO-DATE result means that no change have made to input and output.
- You create create you custom typed task.
- Build lifecycle is: initialization, configuration, execution
