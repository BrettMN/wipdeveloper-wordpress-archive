---
layout: "post.11ty.js"
title: "Intro to TypeScript 1.5 beta - Functions Part 3"
date: "2015-06-07"
tags: 
  - "Blog"
  - "Typescript"
slug: "intro-to-typescript-1-5-beta-functions-part-3"
---

![TypeScript](images/typescript_logo_small1.png)

> This is the third post in a series on getting to know TypeScript. If you missed the first couple posts feel free to go back and read them.
> 
> 1. [Intro to Typescript 1.5 beta - Types](/2015/05/29/intro-to-typescript-1-5-beta-types/)
> 2. [Intro to TypeScript 1.5 beta - Interfaces](/2015/06/01/intro-to-typescript-1-5-beta-interfaces/)
> 3. [Intro to TypeScript 1.5 beta - Functions Part 1](/2015/06/04/intro-to-typescript-1-5-beta-functions-part-1/)
> 4. [Intro to TypeScript 1.5 beta - Functions Part 2](/2015/06/05/intro-to-typescript-1-5-beta-functions-part-2/)

#### () => { return "What's a Lambda"; }

In TypeScript Lambdas can be used to define a function. This makes writing a function much more verbose and binds `this` at the time of creation instead of the time of execution.

> `this` is confusing, or it is in JavaScript. I would recommend spending some time learning about how `this` behaves if you don't have an understanding of it already. One article that might be worth a read is [Understanding JavaScript Function Invocation and "this"](http://yehudakatz.com/2011/08/11/understanding-javascript-function-invocation-and-this/) by Yahuda Katz.

#### Overloading Functions

With JavaScript being such a dynamic language it is not uncommon to use one function that returns different value types based on what is passed in.

##### Overloaded without Types

```javascript
// Overloaded Function without types
function overloadedWithOutTypes(letterOrNumber) :any {  
    if (typeof letterOrNumber === 'string') {
        return 'my string was: ' + letterOrNumber;
    }
    else if (typeof letterOrNumber === 'number') {
        return letterOrNumber * letterOrNumber;
    }
}
```

TypeScript allows for this as well all allows for for the values to be strongly typed. This is accomplished though overloading the function type.

##### Overloaded with Types

```javascript
// Overloaded Function with types
function overloadedWithTypes(letterOrNumber: string): string;  
function overloadedWithTypes(letterOrNumber: number): number;  
function overloadedWithTypes(letterOrNumber): any {  
    if (typeof letterOrNumber === 'string') {
        return 'my string was: ' + letterOrNumber;
    }
    else if (typeof letterOrNumber === 'number') {
        return letterOrNumber * letterOrNumber;
    }
}
```

I mentioned in [Intro to TypeScript 1.5 beta - Interfaces](/2015/06/01/intro-to-typescript-1-5-beta-interfaces/) I would cover the interfaces for function when covering functions. And if you are still following along this will be easy, of course if your not following along you probably are not reading this.

To define our functions interface we give the interface a function call signature.

##### My Function Interface

```javascript
// Function Interface definition
interface myFunctionInterface {  
    (word: string, myNumber: number, ...everythingElse: string[]): void;
}
```

##### Using My Function Interface

```javascript
// Using a function interface definition
var myFunctionBasedOnMyInterface: myFunctionInterface;  
myFunctionBasedOnMyInterface = function (thisWord, thisNumber, ...rest) {  
    // TODO: Do something magical with a string, a number and zero or more strings
};
```

And that's how you type your functions in TypeScript in a nutshell. Now that we can type a function, lets type a Class.
