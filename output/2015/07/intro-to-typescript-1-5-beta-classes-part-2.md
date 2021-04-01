---
layout: "post.11ty.js"
title: "Intro to TypeScript 1.5 beta - Classes Part 2"
date: "2015-07-13"
tags: 
  - "Blog"
  - "Typescript"
slug: "intro-to-typescript-1-5-beta-classes-part-2"
---

![TypeScript](images/typescript_logo_small1.png)

> This is the seventh post in a series on getting to know TypeScript. If you missed the few posts feel free to go back and read them.
> 
> 1. [Intro to Typescript 1.5 beta - Types](/2015/05/29/intro-to-typescript-1-5-beta-types/)
> 2. [Intro to TypeScript 1.5 beta - Interfaces](/2015/06/01/intro-to-typescript-1-5-beta-interfaces/)
> 3. [Intro to TypeScript 1.5 beta - Functions Part 1](/2015/06/04/intro-to-typescript-1-5-beta-functions-part-1/)
> 4. [Intro to TypeScript 1.5 beta - Functions Part 2](/2015/06/05/intro-to-typescript-1-5-beta-functions-part-2/)
> 5. [Intro to TypeScript 1.5 beta - Functions Part 3](/2015/06/08/intro-to-typescript-1-5-beta-functions-part-3/)
> 6. [Intro to TypeScript 1.5 beta - Classes Part 1](/2015/06/10/intro-to-typescript-1-5-beta-classes-part-1/)

One major feature of classes you may be wondering about it `inheritance`. In JavaScript you you can use the `Object.create` to create a new object with your first object as the prototype. While this allows for some reuse wouldn't it be nice to just extend the first object (or the class it came from) into the new object (or class you want it to be)?

#### Enter `extends`

TypeScript allows inheritance of classes by uses the `extends` keyword. This allows you to take one class and add (or extend) new properties or functions onto it and form a new class. You use the `extends` keyword following the new class name and follow it with the parent class name. Like so: `class newClass extends oldClass`

##### Extending a Parent Class

```javascript
// A Base Class
class Parent {  
    id: string;
    constructor(id: string) {
        this.id = id;
    }

    public getId() {
        return this.id;
    }
}

// Child Class with added function
class Child extends Parent{

    constructor(id: string) {
        super(id);
    }

    public setId(id: string) {
        this.id = id;
    }
}
```

#### Calling All Supers

The previous example shows adding just one function but it's possible to add multiple functions, properties and override functions. When calling a function defined on the parent class the `super` keyword is used instead of `this`.

##### Overriding Parents Function

```javascript
// Child Class that overrides a Parent class function
class Grandchild extends Child {  
    // new public property
    public idChanged: Boolean;

    constructor(id: string) {
        this.idChanged = false;
        super(id);
    }

    // Sets the id but requires a user confirm it first
    public setId(id: string) {
        if (confirm('Are you sure you want to change this Id?')) {
            this.idChanged = true;
            super.setId(id);
        }
    }
}
```

You may have noticed that we added a public property to indicate if the `id` had been changed and update it in the overridden `setId` function. The new `setId` function still calls the `setId` function that was defined in the `Child` class using the `super` keyword.

#### Accessors or HEY DON'T TOUCH THAT!

Sometimes you would like to control the flow of logic around certain properties, like the `id` in the previous example. The function and provide one way to do this but wouldn't it be better with accessors similar to what is possible in other languages? That's where `Accessors` come in. Using `get` and `set` to define function that intercept access to properties on an object access can be limited or controlled based on your program requirements.

```javascript
// No Accessors
class NoAccessor {  
    public id: string;
}

// With Accessors get only
class WithAccessorsGetOnly {  
    private _id: string;

    constructor(id: string) {
        this._id = id;
    }

    get id(): string {
        return this._id;
    }
}

// With Accessors get and set
class WithAccessorsGetAndSet {  
    private _id: string;

    get id(): string {
        return this._id;
    }

    set id(id: string) {
        if (confirm('Are you sure you want to change this Id?')) {
            this._id = id;
        }
    }
}
```

That's it for TypeScript Classes for now. Check back later for [Intro to TypeScript 1.5 beta - Classes Part 2](/2015/07/28/intro-to-typescript-1-5-beta-intro-to-modules/)
