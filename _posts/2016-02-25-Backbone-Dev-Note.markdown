---
layout: post
title:  "Backbone development node"
date:   2016-02-25 13:49:00 +0700
categories: Backbone, Javascript, Node.js
---

Short note on dev:

- Backbone.View doesn't have defaults, getter and setter.
- Using the *--save-dev* flag will cause npm to automatically add this package to the dev dependencies in your package.json file.
- npm *--save* vs *--save-dev* options are to put [dependency and devDependency] in package.json.
- CSS animation doesn't run on headless test using jsdom(maybe there are some others lib that do the job).
- `$.when` doesn't accept an array, you have to use `$.when.apply($, promises)` instead.
- Take an extra cation on `@trigger` under `->` of coffeescript. It should be `=>` most of the time. 

[dependency and devDependency]:http://stackoverflow.com/questions/18875674/whats-the-difference-between-dependencies-devdependencies-and-peerdependencies