---
layout: "post.11ty.js"
title: "Intro to TypeScript 1.5 beta - Functions Part 2"
date: "2015-06-04"
tags: 
  - "Blog"
  - "Typescript"
slug: "intro-to-typescript-1-5-beta-functions-part-2"
---

![TypeScript](images/typescript_logo_small1.png)

> This is the third post in a series on getting to know TypeScript. If you missed the first couple posts feel free to go back and read them.
> 
> 1. [Intro to Typescript 1.5 beta - Types](/2015/05/29/intro-to-typescript-1-5-beta-types/)
> 2. [Intro to TypeScript 1.5 beta - Interfaces](/2015/06/01/intro-to-typescript-1-5-beta-interfaces/)
> 3. [Intro to TypeScript 1.5 beta - Functions Part 1](/2015/06/04/intro-to-typescript-1-5-beta-functions-part-1/)

#### But I Don't Want To Type That Much

If you feel that typing the whole function out like that gets a little redundant and would like to save a few keystrokes you do have options. It is possible to leave types off of one side of the equation and the compiler will be able to determine the types on the other side. This is called "contextual typing" and can help save some work to type your program.

##### Contextual Typing

```javascript
// multiplyInferredType has the full function type
var multiplyInferredType = function (x: number, y: number): number { return x * y; };

// The parameters 'x' and 'y' have the type number
var multiplyInferredType2: (baseValue: number, increment: number) => number =  
    function (x, y) { return x * y; };
```

#### Parameters Are Not Optional

Unlike in JavaScript the parameters of a function are not optional. This means if you call a functions with the incorrect number of parameters the compiler will throw an error.

If you would like to be able to call a function but have the option to omit some parameters the they would have to be made optional. To make a parameter optional you use a question mark after the name before the colon `myNumber?: number`. Optional parameters must come after the required parameters.

##### Optional Parameter

```javascript
// Optional Parameters
function add2Or3Numbers(one: number, two: number, three?: number): number {  
    if (three) {
        return one + two + three;
    } else {
        return one + two;
    }
}
```

#### But I Always Want it to Be X Unless I Tell it to Be Y

It is also possible to specify default values for parameters. This is down with assigning a value in the parameter definition list.

##### Default Parameter

```javascript
// Default Parameters
function add2Or3NumbersWithDefault(one: number, two: number, three = 0): number {  
        return one + two + three;
}
```

#### What About the Rest (of the) Parameters

Now that we know how to deal with optional and default parameters you may be wondering how to deal with an unknown number of parameters. Well just like JavaScript had `Arguments` to gather all unspecified arguments into a single accessible parameter, TypeScript has the `Rest Parameter`. The Rest Parameter is defined by an ellipsis (...) before it's name `...restParameter` and the compiler will build an array of the arguments you pass into the function that you can access from the specified name.

##### Rest Parameter

```javascript
// Rest Parameters
function sumAllTheThings(...numbers: number[]): number {  
    var results = 0;
    for (var num of numbers) {
        results += num;
    }
    return results
}
```

When defining a function type of a function that uses Rest Parameters don't forget to use the ellipsis's.

##### Rest Parameter Typed

```javascript
// Typing a function that uses Rest Parameters
var sumAllTheThingsFunction: (...rest: number[]) => number = sumAllTheThings;  
```

Now that we have an understanding of contextual typing; optional, default, and rest parameters lets take a little break to let it all soak in. Check back later when we look into [lambdas, overloaded functions and function interfaces](/2015/06/08/intro-to-typescript-1-5-beta-functions-part-3/).
