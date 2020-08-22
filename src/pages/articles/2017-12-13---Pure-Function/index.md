---
title: Pure function
date: "2017-12-13T16:51:00.000Z"
layout: post
draft: false
path: "/posts/pure-function/"
category: "functional programming"
tags:
  - "functional programming"
description: "What are pure functions?"
---

**Pure functions** are functions that:
* Return values depend solely on their arguments
* Return the same result when using the same arguments
* No side effects such as database call (insert into database)
* Do not modify arguments that are passed in to maintain immutability

*Example*:
```javascript
//x and y are not being modified
//no side effects since always returns sum of x and y
function add(x, y){
    return x + y;
}
```

On the other hand, **Impure functions** are functions that:
* Have side effects such as database or network call which might alter the results everytime the function is executed
* Modify arguments that are passed in

*Example*:
```javascript
//items have been modified inside the function
function appendTest(items){
    for(let i = 0; i < items.length; i++>){
        items[i] = items[i] + "Test";
    }
}
```
