---
layout: "post.11ty.js"
title: "Intro to TypeScript 1.5 beta - Classes Part 1"
date: "2015-06-09"
tags: 
  - "Blog"
  - "Typescript"
slug: "intro-to-typescript-1-5-beta-classes-part-1"
---

![TypeScript](images/typescript_logo_small1.png)

> This is the sixth post in a series on getting to know TypeScript. If you missed the few posts feel free to go back and read them.
> 
> 1. [Intro to Typescript 1.5 beta - Types](/2015/05/29/intro-to-typescript-1-5-beta-types/)
> 2. [Intro to TypeScript 1.5 beta - Interfaces](/2015/06/01/intro-to-typescript-1-5-beta-interfaces/)
> 3. [Intro to TypeScript 1.5 beta - Functions Part 1](/2015/06/04/intro-to-typescript-1-5-beta-functions-part-1/)
> 4. [Intro to TypeScript 1.5 beta - Functions Part 2](/2015/06/05/intro-to-typescript-1-5-beta-functions-part-2/)
> 5. [Intro to TypeScript 1.5 beta - Functions Part 3](/2015/06/08/intro-to-typescript-1-5-beta-functions-part-3/)

If your new to JavaScript and have a background in C# or Java JavaScript's prototyped based inheritance can take some getting used to. To ease this pain TypeScript (and ECMAScript 6) uses a revolutionary concept to institute the ability to reuse components called **Classes**. Ok maybe it's not revolutionary but it's new(ish) in the world of JavaScript.

#### Enter the Classes

Classes can consist of `properties`, `methods`, and the `constructor`.

##### A Simple Class

```javascript
class Simple {  
    // property
    myNumber: number;
    // constructor
    constructor(startNumber: number) {
        this.myNumber = startNumber;
    }
    // method
    getMyNumber() {
        return this.myNumber;
    }
}
```

You may have noticed the use of the work `this.` when accessing the property `myNumber`. That is to specify you are referencing a class instance member.

The constructor is called when you `new` up the class.

##### `new` Class

```javascript
// New up Simple Class
var simple = new Simple(7);  
```

This example creates a new object that is shaped like our class and then calls the `constructor`. In this case it passes in the number `7` to be stored in our new objects `myNumber` member.

#### Lets Keep This Private

By default `properties` and `methods` are public but you can use the keyword `private` to restrict access to a either. If you feel so inclined you can use the `public` keyword to visually remind yourself that things are public but it's not necessary.

```javascript
// A Simple Class with private members
class SimplePrivate {  
    // private property
    private myNumber: number;
    // constructor
    constructor(startNumber: number) {
        this.myNumber = startNumber;
    }
    // method
    public getMyNumber() {
        return this.myNumber;
    }
}
```

#### Sometimes I Want Values to Hang Around Awhile (Read:Forever)

TypeScript also allows the use of `static` member properties. These are declared with the `static` keyword and are accessed by using the class name instead of `this.`

```javascript
// A Simple Class with a Static Property
class SimpleStatic {  
    // static property
    static multiplier: number = 10;
    // property
    myNumber: number;
    // constructor
    constructor(startNumber: number) {
        this.myNumber = startNumber;
    }
    // method
    multiplyMyNumberByTen() {
        return this.myNumber * SimpleStatic.multiplier;
    }
}
```

And that should be enough to start getting in trouble with for now. Check back next time as we cover Class [Inheritance and Accessors](/2015/07/14/intro-to-typescript-1-5-beta-classes-part-2/).
