---
layout: "post.11ty.js"
title: "Intro to Typescript 1.5 beta - Types"
date: "2015-05-29"
tags: 
  - "Blog"
  - "Typescript"
slug: "intro-to-typescript-1-5-beta-types"
---

Sometimes when working on large scale JavaScript applications it would be nice to have a type checking system. Or perhaps you work in Visual Studio and would like to be able to refactor your JavaScript with ease and a little more peace of mind that a global find and replace. Or maybe you want to use the syntax of ECMAscript 2015 without a transpiler. All three of these scenario are possible if you use TypeScript today.

#### Ready

Before getting started a quick background on TypeScript is probably in order. TypeScript is an open source superset of JavaScript primarily developed by Microsoft that compiles to plain JavaScript. One of the main features that set it apart from JavaScript is the type system.

#### Get Set

To get started you will need to install TypeScript 1.5 beta, as this will have the closest feature set to ECMAscript 2015. Links to install for your environment of choice can be found at [www.TypeScriptLang.org](http://www.typescriptlang.org/#Download). I will be using Visual Studio 2015 RC and using an ASP.NET 5 empty template with static files enabled. To find out how to set this up on your own feel free to read [ASP.NET 5 and Static Files](/2015/04/02/asp-net-5-and-static-files/).

#### Type All the Things

There are 7 basic types: Boolean, Number, String, Array, Enum, Any, and Void. A variable gets a type assigned to it either by inference or explicit annotation. Explicit type declaration occurs when you use a colon and the type after declaring the variable name `var myVariable : Number`. Type inference  
occurs when a type isn't declared and the but the compiler determines a type based on the following rules: - [Basics](http://www.typescriptlang.org/Handbook#type-inference-basics) using the type of the value that is assigned during initializing. - [Best common type](http://www.typescriptlang.org/Handbook#type-inference-best-common-type) tries to match based on the type that matches all the provided values. - [Contextual Type](http://www.typescriptlang.org/Handbook#type-inference-contextual-type) happens "when the type of an expression is implied by its location."

##### Explicit Type Declarations

```javascript
var bool: boolean;  
var number: Number;  
var string: String;  
var array: Array<Number>;

enum myEmuns { one, two, three };  
var anEnum: myEmuns;  
var myAny: any;  
var myVoid: void;  
```

##### Inferred Type Declarations

```javascript
//inferred type declaration
var bool2 = true;  
var numberArray = [1, 2, 3];  
var stringArray = ['test', null];

window.onclick = function (mouseEvent) {  
    // MouseEvent is type is MouseEvent because the window.onclick
    // accepts a function that takes a variable of type MouseEvent.
};
```

#### Compile this

Now that the variables have had their types set we can 'trust' the compiler to check types when we assign new values. This means not putting numbers in our strings and keeping our Booleans away from our arrays (unless, of course, it's an array of Booleans).

##### This Works

```javascript
bool = true;  
number = 1 + 1;  
string = 'Typescript';  
array = [1, 2];  
anEnum = myEmuns.three;  
myAny = "what ever" + 1 + true;  
```

If you try to assign a value that is not of the declared type your compiler tell you there is an error but it will still build the JavaScript file. The error is TypeScripts way of letting you know that things may now work as you expect them to.

##### This Doesn't

```javascript
bool = 1;  
number = 1 + 'typescript';  
string = true;  
array = [1, 'two'];  
anEnum = 'one';  
bool2 = number;  
numberArray.push('5');  
stringArray.push(5);
```

And that's the basic of TypeScript types. Come back next time for [Interfaces](/2015/06/01/intro-to-typescript-1-5-beta-interfaces/).
