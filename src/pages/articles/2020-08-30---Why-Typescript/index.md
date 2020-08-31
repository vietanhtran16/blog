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

## Advantages of Typescript

### Easier to understand/maintain
Types clearly express questions such as:
  * What arguments does this function accept?
  * What would I get back from this function?
  * What is the shape of this object?

Without the support from Typescript, to answer correctly all the questions above, you need to try method such as using `console.log`, read other places where this function is used or even check its implementation to figure out.

In my opion, **code written is Typescript is easier to understand/maintain since it expresses your intention** in the code and helps other people (including your future self) which leads to maintainable code and fewer bugs.

### Refactor is simple and easy
For example, we have this object below:
```typescript
const profile = {
    name: "Luis",
    age: 19
}
```
In Javascript, if we want to change `name` to `fullName`, it is not so safe since it could be anywhere in the code and your best option to do it might be a search and replace which could easily replaces something else by mistake.

This tedious work in Typescript is way simpler, it could help you rename it with ease and alert of any error even before you build the code.

### Encourage type first approach
Define your interface/contract before going deep into the implementation as types would drive your program specification.

If we go deep in implementation without clear type definition, the implementation might not be suitable for the actual type we are receiving.

```typescript
// User
const user: { fullName: string } = {
    fullName: "Viet"
};

// our implementation
const getUserName = (user) =>
    user.name;

getUserName(user); // Oops name does not exist in user
```

Also, defining type first is useful when having two teams agreeing on a contract so that when both team are done (given that they followed the agreed contract), there is a higher likelihood that their implementation would integrate a lot better compared to when not having an agreed contract beforehand.

### Other benefits
* Less bugs.
* Less boilerplate tests (since type check is done by Typescript).
* Save developers time from debugging, reading code, etc.

## Does it have any cons?
### Extra transpiling step
Browser cannot interpret Typescript code directly so it needs to be transpiled to Javascript before running. However, this step is automated and quite fast so it is not a major con compared to the values it brings

### Some third party libraries do not have type definition
When this happens, you normally have to write type definition yourself and include it in your project or even better, you could contribute back your type definitions to the community by open sourcing it (which is a good way to learn Typescript). I am sure that the project owner would happily accept and help you with refining your type definition.
