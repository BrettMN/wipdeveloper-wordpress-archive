---
layout: "post.11ty.js"
title: "TypeScript - What's New in 1.7"
date: "2015-12-03"
tags: 
  - "Blog"
  - "Typescript"
slug: "typescript-whats-new-in-1-7"
---

![TypeScript](images/typescript_logo_small1.png)

This week [Visual Studio 2015 Update 1](http://blogs.msdn.com/b/visualstudio/archive/2015/11/30/visual-studio-update-1-rtm.aspx) was released and with it [TypeScript 1.7](http://blogs.msdn.com/b/typescript/archive/2015/11/30/announcing-typescript-1-7.aspx). To get the update to TypeScript install the update for Visual Studio. Then you can use the following new features:

> Of course if you are not using Visual Studio to compile your TypeScript feel free to install it from an alternative source, such as npm `npm install -g typescript`

- [Async/Await for ES6 targets](#asyncawait)
- [Polymorphic `this` Typing](#this)
- [ES6 Module Emitting](#es6module)
- [ES7 Exponentiation](#es7exponentiation)

#### Async/Await for ES6 targets

The `async` keyword is used as a prefix to a function and will designate it as an asynchronous function. You can then use the `await` keyword when you call the function to stop execution until the `async`'s function's promise is fulfilled. This behavior seems similar how Async/Await works in C# so if you are familiar with that this should be _easy_.

##### Example Time

```javascript
"use strict";
// printDelayed is a 'Promise<void>'
async function printDelayed(elements: string[]) {  
    for (const element of elements) {
        await delay(200);
        console.log(element);
    }
}

async function delay(milliseconds: number) {  
    return new Promise<void>(resolve => {
        setTimeout(resolve, milliseconds);
    });
}

printDelayed(["Hello", "beautiful", "asynchronous", "world"]).then(() => {  
    console.log();
    console.log("Printed every element!");
});
```

> This example was provided by the TypeScript team

Of course the glory that is Async/Await does have a drawback. It's currently only available if you are targeting a platform that supports ES6 generators. That means right now just node.js v4 and up. They are working on bringing it to other targets but there is additional work that the TypeScript team will have to do to make that happen.

#### Polymorphic `this` Typing

##### TLDR

The Polymorphic `this` typing allows you to create a class that returns `this` and not mess up the typing's when the class inherited functions from a parent.

##### An Example

Lets say we have a base class called `Base` and a child class called `Child`. Before this change if we implemented a fluent style api within these classes a compiler error would occur when `Child` called a method that was defined on `Base`. Why? Well the method only _understood_ the type of class it was defined in, in this case `Base`. Lets look at it:

##### `Base` class

```javascript
export default class Base {  
    public constructor(protected something:string = '') { }

    public getCurrentSomething() {
        return this.something;
    }

    public setSomething(newSomething: string) {
        this.something = newSomething;
        return this;
    }
}
```

##### 'Child' class

```javascript
import Base from "./Base";

export default class Child extends Base {

    public constructor(something: string = '') {
        super(something);
    }

    public deleteSomething() {
        return this;
    }
}
```

##### Use It

```javascript
import Child from "./Child";

let child = new Child('something')  
    .setSomething('otherThing')
    .deleteSomething()           //ERROR HERE
    .getCurrentSomething();
```

On the line that says `.deleteSomething()` an error would occur because `.setSomething()` returned a type of `Base` and there is nor `.deleteSomething()` defined on `Base`.

This is no longer the case as the `this` is now considered a special type. They describe is as "the type of the left side of the dot in a method call".

#### ES6 Module Emitting

ES6 was added as an option for Module output. This will allow for more flexibility with module output.

#### ES7 Exponentiation

The last this is some sugar for your syntactic sweet tooth. you can now use `**` for exponents.

```javascript
let squared = 4 ** 2;  // same as: 4 * 4  
let cubed = 4 ** 3;  // same as: 4 * 4 * 4  
let num = 4;  
num **= 2; // same as: num = num * num;  
```

#### Conclusion

Maybe I need to get out more but I think this is some cool stuff. I can't wait to see what else the TypeScript team puts together, how about you? Let us know what you think by leaving a comment bellow or, if you are feeling shy, send an email to me at [brett@wipdeveloper.com](mailto:brett@wipdeveloper.com).
