---
title: Is naming important?
date: "2017-12-03T16:51:00.000Z"
layout: post
draft: false
path: "/posts/naming-convention/"
category: "clean code"
tags:
  - "clean code"
  - "naming"
description: "What have I learned about naming?"
---

One of the first book that I read when I started my software apprenticeship journey was Clean Code.

At that time, I was super new to all concepts and principles so this book helped me tremendously in shaping my mindset. Of course, it was not an easy read that you could skim through in a week or two. It is also a book that is not easy to perceive thorougly first time around so I will definitely come back to it later on.

Naming convention is probably what made me realised how ugly my code had been. We have all named a variable like this:

```
var test = "We all been here"
```

or this:

```
public void ConvertSomething(){

}
```

We all planned to go back and change the name (or at least me) later on but never got to it.

So here are some of the key points about **Naming Conventions** that I learnt from Clean Code:
* Clearly reveal the its intent
* Explain the object clearly
* Could help others in maintaining your code
* Should not use single letter name for object
* Should have style for code format using tool such as Resharper
* Do not name two objects similarly. 
    * Eg: user and users
* Pick one word per concept. 
    * Eg: choose between send or post
