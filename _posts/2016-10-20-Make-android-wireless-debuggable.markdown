---
layout: post
title:  "Make android device becomes remotely debuggable"
date:   2016-10-20 18:29:00 +0700
categories: android, debug, command-line
---

To enable debug over TCP:


1. Connect to android device via USB cable.
2. Execute `adb tcpip <port-number>`
3. There you go!


To connect to a device over TCP:

1. Get device IP address
2. Execute `adb connect <device-IP>`
3. Awesome!


Now a bit less worry about USB port wearing out.