---
title: Immutability
date: "2018-02-04T16:51:00.000Z"
layout: post
draft: false
path: "/posts/immutability/"
category: "functional programming"
tags:
  - "functional programming"
  - "immutability"
description: "It is about how to handle change and not about avoiding change."
---

It is about how to handle change and not about avoiding change. 

## But what is mutation?
Mutation is simply overwriting the current object. Due to that, object can be mutated anywhere in the application so in one line it can be an object of one type, and in the following line it can be another type. This is what makes objects unpredictable since they are different at different point in time.

```javascript
//mutating model property of car
let car = {make: "Tesla", model: "X"};
car.model = "Fiesta";
```

## Why is mutation bad? 
* Unpredictable. Object can be mutated anywhere in the application so in one line it can be an object of one type, and in the following line it can be another type. This is what makes objects unpredictable since they are different at different point in time.
* Only provides current state
* Objects are overwritten so the history of that objects are not kept in memory. 
* Hard to track down bugs since objects are mutated everywhere and only the current state is presented

## What is immutability
* It is about how to handle change
* Create something new with change instead of mutating the current version. This creates a history of the object which allows us to debug in the future
* Nothing can be mutated - unchangeable
* Create trust since every other path of the code can be confidence that the value is always the same
* Provide a solid contract compared to using memory pointers
* Change is reflected in the new value

```javascript
//create new object with change
let modelX = {make: "Tesla", model: "X"};
let model3 = {...modelX, model: "3"};
```

## Why we need immutability?
* Create trust in object value
* A lot more predicatable since nothing is mutated
* Provides a history of object values which enables time travel debugging
