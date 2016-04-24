---
layout: post
title:  "Installing MongoDB by homebrew on El Capitan"
date:   2016-04-23 24:55:00 +0700
categories: MongoDB Installation Homebrew 
---

Today, I just installed MongoDB for my Parse local dev.
The follows are step-by-step guide which shouldn't cause any issue.

1. `brew update`
    to update homebrew to the lastest state.
2. `brew install mongodb --with-openssl`
    to install MongoDB with openssl which you are likely to use it for parse API.
3. `sudo mkdir -p /data/db`
    to create data directory for MongoDB to work with. But it will be created under root.
4. ```sudo chown -R `id -u` /data/db```
    to change owner of the directory back to currect user.
5. `mongod`
    to start the mongo deamon.
    
Done!