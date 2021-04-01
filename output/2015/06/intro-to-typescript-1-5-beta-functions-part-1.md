---
layout: "post.11ty.js"
title: "Intro to TypeScript 1.5 beta - Functions Part 1"
date: "2015-06-03"
tags: 
  - "Blog"
  - "Typescript"
slug: "intro-to-typescript-1-5-beta-functions-part-1"
---

![TypeScript](images/typescript_logo_small1.png)

> This is the third post in a series on getting to know TypeScript. If you missed the first couple posts feel free to go back and read them.
> 
> 1. [Intro to Typescript 1.5 beta - Types](/2015/05/29/intro-to-typescript-1-5-beta-types/)
> 2. [Intro to TypeScript 1.5 beta - Interfaces](/2015/06/01/intro-to-typescript-1-5-beta-interfaces/)

Now lets take a look at functions. In TypeScript functions serve the role of how you "do" things. It is possible to create both named functions and anonymous functions. This allows you to decide the best way to implement a function for your use case.

##### Named vs Anonymous Function

```javascript
//Named function
function multiply(x, y) {  
    return x * y;
}

//Anonymous function
var multiply2 = function (x, y) {  
    return x * y;
};
```

Like JavaScript TypeScript functions can access, or capture, variables outside the scope, or body, of the function.

```javascript
//Capturing outside variable
var z = 100;

function multiplyWithZ(x, y) {

    return x * y * z;
}
```

#### What About the Types

To add types to a function definition you follow the name of your variable with a colon and the type `: number`. You can declare a return type by following the closing parenthesis of the values being passed in with a colon and the type as well.

```javascript
//Named function with Types
function multiplyWithTypes(x: number, y: number): number {  
    return x * y;
}

//Anonymous function with Types
var multiply2WithTypes = function (x: number, y: number): number {  
    return x * y;
};
```

> Since we are using types TypeScript can figure out the return values type based on the return statement so it is possible to leave the return type of the function off.

With the types assigned to the values of our functions we can define the complete type of of the function. When defining the function type the names of the parameters do not need to match the names of the function definition but it does make it easier to read. Once again we start defining the type by following the name of what we are assigning a type to, in this case the function, with a colon and than the type followed by the assignment.

##### Typed Function

```javascript
//Function Type defined
var multiplyTypedFunction: (x: number, y: number) => number =  
    function (x: number, y: number): number {
        return x * y;
    };
```

In this example you can see the type of the function is `(x: number, y: number) => number`. This means it takes 2 parameters of type number. The fat arrow `=>` precedes the return type, in this case `number`, and is required. If you have a function that returns nothing you would specify a return type of `void`. After the declaration the actual function is assigned.

> If you are using a captured variable in your function this is not declared and is effectively hidden as far as your functions api is concerned.

That's the basics of using types with functions. Check back later when we delve into [contextual typing; optional, default, and rest parameters](https://www.wipdeveloper.com/2015/06/05/intro-to-typescript-1-5-beta-functions-part-2/).
