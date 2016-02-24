---
layout: post
title:  "Backbone.View what el, $el and tagName are for?"
date:   2016-02-24 19:44:00 +0700
categories: Backbone, Javascript
--------------------------------

tagName represents HTML tag 'type' of the current view object. If tagName is specified as 'li' then *el* property will be pointed 
to DOM Element of type 'li'. $el is just a jquery version of el object i.e. it's a synonym to $(this.el). However, el and tagName
are not forced to agree. For example, we can specify tagName as 'div' but assign an arbitrary element to el. Doing so they will no longer
agree on type.

The description of *el* from Backbone's official docs:

> *this.el* can be resolved from a DOM selector string or an Element; otherwise it will be created from the view's tagName, className, id and attributes properties. If none are set, this.el is an empty div, which is often just fine. An el reference may also be passed in to the view's constructor.

Note that the element created by Backbone view need to be added to DOM Tree before it can be seen by user.