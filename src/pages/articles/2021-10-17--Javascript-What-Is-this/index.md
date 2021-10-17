---
title: Javascript - What is `this`?
date: "2021-10-17T16:51:00.000Z"
layout: post
draft: false
path: "/posts/javascript-what-is-this/"
category: "javascript"
tags:
  - "fundamentals"
description: "What does `this` refer to in Javascript?"
---


## Is `this` confusing?
Yes, it is extremely confusing at least to me. `this` keyword in Javascript refers to different things such as how the function is called, whether it is using a normal `function` keyword or arrow function, etc. I got asked about this the other day and was not too sure on what `this` would be in some scenario so let's dive into it.

## `this` in different scenario
### In global context
This one is simple. `this` would refer to the global object.

### In object method
Let's look an example below

```javascript
const car = {
    brand: "Pagani",
    hello: function(){
        return this.brand;
    }
};
console.log(car.hello()); // print "Pagani"

function sayHello(){
    return this.brand;
}

const anotherCar = {
    brand: "Bugatti",
    hello: sayHello
}
console.log(anotherCar.hello()); // print "Bugatti"
```

In the two examples above, `this` would refer to the `car` object itself whether the `hello` method was defined inline or reference an outer function.

### In function context

```javascript
const car = {
    brand: "Pagani",
    hello: function(){
        return this.brand;
    }
};
const { hello } = car;
console.log(hello() === undefined); // print true

function giveMeThis() {
    return this;
}
console.log(giveMeThis() === window) // print true for browser
console.log(giveMeThis() === globalThis) // print true for node
```

`this` in the first example is no longer refering to the `car` object itself when it is being called as a standalone function not as a method on the object. `this` is now refering to the global object which is `window` in a browser or `globalThis` in node. Because of that, `this.brand` is `undefined`. As a note, when strict mode is on, if `this` is not set, it will be `undefined`.

### In arrow function

For arrow function, `this` always remains the `this` of the enclosing lexical scope of when it was created.

```javascript
var globalObject = this;
var giveMeThis = (() => this);
console.log(giveMeThis() === globalObject); // print true
```

Arrow function is not suitable to be used for object method since the object does not create a new scope itself so `this` would be the global object

```javascript
const car = {
    brand: "Pagani",
    hello: () => {
        return this.brand;
    }
};
console.log(car.hello() === undefined) // print true
```

### How could I provide `this`?
You would be able to provide `this` using [call](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/call), [apply](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/apply), and [bind](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/bind). However, they would not have any effect on `this` for an arrow function. Here are examples of how they work:

```javascript
const car = {
    brand: "Bentley"
};

function getBrandName(message){
    return `${message} ${this.brand}`;
}

const message = "This is a";
console.log(getBrandName(message)) // print 'This is a undefined'
console.log(getBrandName.call(car, message)) // print 'This is a Bentley'
console.log(getBrandName.apply(car, [message])) // print 'This is a Bentley'
console.log(getBrandName.bind(car)(message)) // print 'This is a Bentley'
```

## Bonus: Can you tell what would be printed out?
```javascript
const car = {
  brand: "Pagani",
  hello: function () {
    const insideArrow = () => console.log(`This is a ${this.brand}`);
    insideArrow();
  },
};
console.log(car.hello());

const { hello } = car;
console.log(hello());
console.log(hello.call(car));
```

```javascript
const anotherCar = {
  brand: "Pagani",
  hello: function () {
    const insideFunc = function () {
      console.log(`This is a ${this.brand}`);
    };
    insideFunc();
  },
};
console.log(anotherCar.hello());

const { hello } = anotherCar;
console.log(hello());
console.log(hello.call(anotherCar));
```

*Reference:* 
- [MDN's doc on this](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/this)
- [MDN's doc on arrow function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions)