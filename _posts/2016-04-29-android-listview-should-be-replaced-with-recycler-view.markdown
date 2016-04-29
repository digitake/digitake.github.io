---
layout: post
title:  "Android ListView should be replaced with RecyclerView"
date:   2016-04-29 22:21:00 +0700
categories: Android listview  
---

ListView in android has been working fine for its task. However, with more requirment
UI has to be more vivid as in material design or infinite scroll feature like in many social
network apps. seems like it's a time for its retirement.

Below is comparision from https://github.com/codepath/android_guides/wiki/Using-the-RecyclerView

> Compared to ListView
> RecyclerView differs from its predecessor ListView primarily because of the following features:

> Required ViewHolder in Adapters
    - ListView adapters do not require the use of the ViewHolder pattern to improve performance. In contrast, implementing an adapter for RecyclerView requires the use of the ViewHolder pattern.
    
> Customizable Item Layouts
    - ListView can only layout items in a vertical linear arrangement and this cannot be customized. In contrast, the RecyclerView has a RecyclerView.LayoutManager that allows any item layouts including horizontal lists or staggered grids.
    
> Easy Item Animations
    - ListView contains no special provisions through which one can animate the addition or deletion of items. In contrast, the RecyclerView has the RecyclerView.ItemAnimator class for handling item animations.
    
> Manual Data Source
    - ListView had adapters for different sources such as ArrayAdapter and CursorAdapter for arrays and database results respectively. In contrast, the RecyclerView.Adapter requires a custom implementation to supply the data to the adapter.
    
> Manual Item Decoration
    - ListView has the android:divider property for easy dividers between items in the list. In contrast, RecyclerView requires the use of a RecyclerView.ItemDecoration object to setup much more manual divider decorations.
    
> Manual Click Detection
    - ListView has a AdapterView.OnItemClickListener interface for binding to the click events for individual items in the list. In contrast, RecyclerView only has support for RecyclerView.OnItemTouchListener which manages individual touch events but has no built-in click handling.