---
layout: post
title:  "Mystery error on jquery, jsdom and mocha initialization."
date:   2016-02-27 15:54:00 +0700
categories: DOM, Mocha, JSDOM, jQuery 
---

Today, I bumped into another mystery issue on my dev journey.

I set up a test suite using mocha and use jsdom to mock up a DOM env.
I put a jsdom env setup code `before()` the tests are executed. 
My setup code looks like this:

```coffeescript
...
global.window = window
global.document = window.document
global.Backbone = require('backbone');
global.Backbone.$ = global.$ = require('jquery')
...
```

**window** is an object produced by jsdom env and it's assigned to the `global`.
It represents a global scope in HTML env. And then, I can use `require('jquery')` just as
running on the normal browser. The code worked perfectly fine with IntelliJ test console.
And it worked when I executed **mocha** test individually.

The issue arose when I used --recursive option of mocha to test the whole suite in test dir.

```
...
2 failing
  1) Board.View.Board "before all" hook:
     Uncaught Error: jQuery requires a window with a document
    at module.exports (/Users/work/Dev/node_modules/jquery/dist/jquery.js:29:12)
    at Object.jsdom.env.done (test/view/boardTest.coffee:29:7)
    at /Users/work/Dev/node_modules/jsdom/lib/jsdom.js:275:18
  2) Board.View.Cell "before all" hook:
       Uncaught Error: jQuery requires a window with a document
      at module.exports (/Users/work/Dev/node_modules/jquery/dist/jquery.js:29:12)
      at Object.jsdom.env.done (test/view/cellTest.coffee:24:9)
      at /Users/work/Dev/node_modules/jsdom/lib/jsdom.js:275:18
...
```

I ain't really sure what the hell was happening. I try to test if window
that produced by jsdom was not there, but it was. So my guess was that something's
wrong with the way jQuery trying to capture **window** object from global scope.
So I try to supply the **window** object to jquery directly.

`global.Backbone.$ = global.$ = require('jquery')(window)`

Bam! `Error $ is not a function!?`. Then I dug stackoverflow. Many ppl just 
execute that fine. My *educated* guess was that it might be about the way jQuery captures things from global.
So, I changed the code order to do `require('jquery')(window)` before `global.window = window`.

Finally, it works! Surely, somethings is mess on how jsdom manage its scope.

Have any suggestion or did I miss anything? Pls twitt me.