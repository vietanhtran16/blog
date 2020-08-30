---
title: Why Typescript over Javascript?
date: "2020-08-30T06:10:00.000Z"
layout: post
draft: false
path: "/posts/why-typescript/"
category: "typescript"
tags:
  - "typescript"
  - "javascript"
description: "Typescript vs Javascript"
---

## What is Typescript?
In short, Typescript is a superset of Javascript with type support. 

It is basically still the normal Javascript that is running everywhere on the internet but with the power to describe the shape of an object, a function or just a variable in your code.

## Examples of Typescript

```typescript
// Arguments
const add = (first: number, second, number) => 
    first + second;
```

```typescript
// Object
interface IUser {
    firstName: string;
    lastName: string;
    age: number;
}

const user: IUser = {
    firstName: "Lionel";
    lastName: "Messi";
    age: 33;
};
```

```typescript
// Function Return Type
const greeting = (name: string): string => 
    `Hello there ${name}`
```