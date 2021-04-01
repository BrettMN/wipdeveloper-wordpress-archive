---
layout: "post.11ty.js"
title: "Intro to TypeScript 1.5 beta - Interfaces"
date: "2015-06-01"
tags: 
  - "Blog"
  - "Typescript"
slug: "intro-to-typescript-1-5-beta-interfaces"
---

> This is the second post in a series on getting to know TypeScript. If you missed the first post feel free to go back and read it. [Intro to Typescript 1.5 beta - Types](/2015/05/29/intro-to-typescript-1-5-beta-types/)

Now that we have an understanding of how the type system works we can start using that knowledge to limit our type errors. In a function declaration you can specify what type each value is rather than hoping the correct type is passed in.

```javascript
//Hopes for a number
function hopesForANumber(iHopeIGetANumber) {  
}

//Only takes a number
function takesANumber(myNumber: number) {  
}
```

#### But if I Want to Pass a Function a More Complex Object than a Simple Value

Glad you asked. You can use an [Interface](http://www.typescriptlang.org/Handbook#interfaces) to define an object "shape." This is a concept sometimes called "duck typing" or "structural subtyping". You declare an interface with the `interface` keyword, give it a name and then define what names of values should be and what types those names should be.

##### Like so

```javascript
// My first interface
interface IMyFirstInterface {  
    myNumber: number;
}
```

> As for the naming convention I am not sure if it is common to preface interfaces with `I` but I am used to doing it with C# so I will do it with TypeScript until I learn otherwise.

Now if we want our function to accept an object that contains a number named `myNumber` we can define the type of the object being passed in as our new interface. Inside the function body you can access `myNumber` they way you would access any values of a JavaScript object.

```javascript
//Using IMyFirstInterface
function takesIMyFirstInterfaceAndAddsMyNumber(someValue: IMyFirstInterface) {  
    console.log(someValue.myNumber + someValue['myNumber']);
}
```

#### Keeping Your Options Open

Interfaces can also have optional properties. These would be defines with a question mark + colon `?:` before specifying the type.

##### My Optional Option

```javascript
//Optional Properties
interface IOptional{  
    option?: boolean;
}
```

#### Extending A Helping Interface

An Interfaces can also extend another Interface. This means it is possible to define a "base" interface and "add" properties to it with a new Interface rather than duplicating the properties on multiple Interface declarations.

##### Extend IMyFirstInterface

```javascript
//Extend IMyFirstInterface
interface IExtended extends IMyFirstInterface {  
    myString: string;
}

//Using IExtended
function takesIExtendedAndLogsMyStringAndTheSquareOfMyNumberToConsole(value: IExtended) {  
    console.log(value.myString);
    console.log(value.myNumber * value.myNumber);
}
```

And that's the basics of Interfaces. We didn't cover a few things here like using interfaces to define [Function Types](http://www.typescriptlang.org/Handbook#interfaces-function-types), [Array Types](http://www.typescriptlang.org/Handbook#interfaces-array-types), [Class Types](http://www.typescriptlang.org/Handbook#interfaces-class-types), or  
[Hybrid Types](http://www.typescriptlang.org/Handbook#interfaces-hybrid-types).

> For Function and Class Types I am planning of covering them when we talk about Functions and Classes. Since it might be easier to understand how to define an interface for a thing after you know more about how that thing is defined itself.

This should be enough to make you dangerous with Interfaces. Check back next time as we start getting to know [Functions](/2015/06/04/intro-to-typescript-1-5-beta-functions-part-1/).
