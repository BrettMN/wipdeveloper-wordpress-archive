---
layout: "post.11ty.js"
title: "Intro to TypeScript 1.5 - Mixins"
date: "2015-08-28"
tags: 
  - "Blog"
  - "Typescript"
slug: "intro-to-typescript-1-5-mixins"
---

![TypeScript](images/typescript_logo_small1.png)

> This is the eleventh post in a series on getting to know TypeScript. If you missed the few posts feel free to go back and read them.
> 
> 1. [Intro to TypeScript 1.5 beta - Types](/2015/05/29/intro-to-typescript-1-5-beta-types/)
> 2. [Intro to TypeScript 1.5 beta - Interfaces](/2015/06/01/intro-to-typescript-1-5-beta-interfaces/)
> 3. [Intro to TypeScript 1.5 beta - Functions Part 1](/2015/06/04/intro-to-typescript-1-5-beta-functions-part-1/)
> 4. [Intro to TypeScript 1.5 beta - Functions Part 2](/2015/06/05/intro-to-typescript-1-5-beta-functions-part-2/)
> 5. [Intro to TypeScript 1.5 beta - Functions Part 3](/2015/06/08/intro-to-typescript-1-5-beta-functions-part-3/)
> 6. [Intro to TypeScript 1.5 beta - Classes Part 1](/2015/06/10/intro-to-typescript-1-5-beta-classes-part-1/)
> 7. [Intro to TypeScript 1.5 beta - Classes Part 2](/2015/06/05/intro-to-typescript-1-5-beta-functions-part-2/)
> 8. [Intro to TypeScript 1.5 beta - Intro to Modules](/2015/07/28/intro-to-typescript-1-5-beta-intro-to-modules/)
> 9. [Intro to TypeScript 1.5 - External Modules](/2015/07/30/intro-to-typescript-1-5-external-modules/)
> 10. [Intro to TypeScript 1.5 - Modules Remainders](/2015/08/07/intro-to-typescript-1-5-modules-remainders/)
> 11. [Intro to TypeScript 1.5 - Module Output Formats](/2015/08/20/intro-to-typescript-1-5-module-output-formats/)

Previously we have seen the that TypeScript allows the uses of traditional object oriented inheritance where a child class `extends` a parent class. TypeScript also allows for building up complex classes by combining more basic partial classes. This concept is usually referred to as "Mixins".

We will start with 2 smaller classes:

##### Greeter Mixin

```javascript
class Greeter {  
    message: string;
    greet() {
        return this.message;
    }
}
```

The first class `Greeter` has just a message and a function that returns that message.

##### TakesBreaks Mixin

```javascript
class TakesBreaks {  
    onBreak: boolean;
    startBreak() {
        this.onBreak = true;
    }
    endBreak() {
        this.onBreak = false;
    }
}
```

The second class has a boolean for whether it's on break and two functions to change the on break status.

With these two smaller classes we will combine them into a more complex class:

##### BreakTakingGreeter Class

```javascript
class BreakTakingGreeter implements Greeter, TakesBreaks {  
    constructor() {
        setInterval(() => console.log(this.interact()), 500);
    }

    interact() {
        if (!this.onBreak) {
            return this.greet();
        }
        return "I'm on Break";
    }

    // Greeter
    message: string = 'Hello';
    greet: () => string;
    // TakesBreaks
    onBreak: boolean = false;
    startBreak: () => void;
    endBreak: () => void;
}
```

You might have noticed that instead of using the `extends` keyword we used the `implements` keyword. Using the `implements` keyword causes the c classes to be treated like they were interfaces. Since they are treated like interfaces the new class has to be able to implement the smaller classes. However we don't want to copy the classes over manually so we create standing properties to satisfy the complier.

#### Mix it All Together

To get the full functionality of our smaller classes we will need to have an `applyMixins` function somewhere in our code that looks library that looks like this:

##### applyMixins

```javascript
function applyMixins(derivedCtor: any, baseCtors: any[]) {  
    baseCtors.forEach(baseCtor => {
        Object.getOwnPropertyNames(baseCtor.prototype).forEach(name => {
            derivedCtor.prototype[name] = baseCtor.prototype[name];
        })
    });
}
```

We will also need to call if before we create any of our new class.

##### Mixin it up

```javascript
applyMixins(BreakTakingGreeter, [Greeter, TakesBreaks])

var halfTimeWorker = new BreakTakingGreeter();

setInterval(() => halfTimeWorker.onBreak ? halfTimeWorker.endBreak() : halfTimeWorker.startBreak(), 1000);  
```

There we have it. A `BreakTakingGreeter` class that we can use to sometime say hello to an imaginary customer.
