---
layout: post
title:  "Mocha and node require issues"
date:   2016-02-25 13:49:00 +0700
categories: Backbone, Javascript, Node.js, Mocha
---

Today, I ran into a problem which I've written a test for my Backbone.View but 
**require** function can resolve the alias specified.

Because my view consists of two classes:

- view/board
- view/cell

Board has a dependency on **Cell** class so I have to include a require statement  `require('view/cell')`.
The code is smoothly compiled into a single file using browserify. But when I try to write a test using
*mocha*, the problem arose.

The statement can't be resolved because mocha didn't read *package.json* configs just as 
browserifty did. The test on 'view/cell' itself had no problem because it has no dependency on another file.

My idea is to try to intercept the `require` function so it remap 'view/cell' to the right path under mocha's env.
Luckily, after I dug down stackoverflow, I had bumped to `mock-require` module which saved my day.
 
The solution looks like this:

```coffeescript
mock = require('mock-require')
mock('view/cell', '../../script/view/cell')
global.Board = require('../../script/view/board') #now I can load view/board.
```
 
phew..., that was easy.