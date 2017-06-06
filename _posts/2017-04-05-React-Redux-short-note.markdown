---
layout: post
title:  "React-redux short notes"
date:   2017-04-05 17:10:00 +0700
categories: React, Redux, note
comments: yes
---

Redux components are:
    - Action
    - Reducer
    - Store
    - Data flow
    

**Action** is the pure javascript object that contains information of the action needed to be done.
The action object will be sent to `store` by using `store.dispatch(<action-object>)`.
Actions must have a `type` property that indicates the type of action being performed.
The `type` property should be string though can be of any type. Other than the `type`, 
actions can contain arbitrary structure. Action is created by `Action creator` which is simply a 
function that return an `action` object.


**Reducer** is the thing that perform real actions. It `reduce` actions and combine into single state.
A reducer can be splitted and combined since it's a pure functional style.


**Store** is the place to keep state. There will be only one store in Redux application.
A store can be created by `createStore` function. `createStore` function takes reduced state as
its first argument. Also one can supply initial state to the optional second argument.