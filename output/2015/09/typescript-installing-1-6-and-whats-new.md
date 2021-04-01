---
layout: "post.11ty.js"
title: "TypeScript - Installing 1.6 and What's New"
date: "2015-09-17"
tags: 
  - "Blog"
  - "Typescript"
slug: "typescript-installing-1-6-and-whats-new"
---

![TypeScript](images/typescript_logo_small1.png)

Today the Typescript team [announced](http://blogs.msdn.com/b/typescript/archive/2015/09/16/announcing-typescript-1-6.aspx) 1.6 with a few new features:

- [React/JSX support](#react)
- [Class expressions](#classexpressions)
- [User defined type guards](#typeguards)
- [Intersection types](#intersectiontypes)
- [Abstract classes](#abstractclasses)
- [Generic type aliases](#generictypealiases)
- [Breaking changes](#breakingchanges)

Lets take a look at a few of these but before we do be sure to update to the latest version for [Visual Studios 2015](http://download.microsoft.com/download/6/D/8/6D8381B0-03C1-4BD2-AE65-30FF0A4C62DA/TS1.6.2-D14OOB.23313.00/TypeScript_Full.exe), [Visual Studios 2013](http://download.microsoft.com/download/4/4/3/443F86B7-A89F-48E6-AC96-0AAC2A910A29/TS1.6.2-VUOOB.40914.00/TypeScript_Dev12.exe), [npm](https://www.npmjs.com/package/typescript) or just grab the [source](https://github.com/Microsoft/TypeScript/releases/tag/v1.6.2).

#### React/JSX Support

I haven't played around with React yet but this seems like a good thing. They have created a new file type (.tsx) that allows the use of JSX syntax with TypeScript. This allows for all the type checking and auto complete your used to with TypeScript while working with React/JSX in Visual Studios, VS Code and Sublime Text.

#### Class Expressions

Class expressions are now part of TypeScript. This allows you to create a new class similar to a class declaration but can be done wherever an expression could be used.

##### Class Expressions

```javascript
// Unnamed
class childClass extends class { doSomething() { return 'no' } } {  
    constructor(){
        super();
    }
}

let child = new childClass();  
console.log(child.doSomething());

// Named
let parentClass = class { doSomethingElse() { return 'maybe' } };

class babyClass extends parentClass {  
    constructor() {
        super();
    }
}

let baby = new babyClass();  
console.log(baby.doSomethingElse());  
```

#### User Defined Type Guards

Previously in TypeScript you could check the type of an object with an `if` statement:

##### if(typeof)

```javascript
if (typeof x === "String") {  
    ///Do Something fun here!
}
```

Of course to make this check you had to already be in your function. With **User Defined Type Guards** you can prevent going into a function.

##### x is a

```javascript
class Car {  
    name: string;
}
interface SportsCar extends Car {  
    revEngine();
}

function isSportsCar(a: Car): a is SportsCar {  
    return a.name === 'Tesla';
}

var x: Car;

if (isSportsCar(x)) {  
    x.revEngine(); // OK, x is SportsCar in this block
}
```

You may have noticed that not only can you use the `x is a` syntax with types but it also works with interfaces that you design allowing for even greater controller.

#### Intersection Types

Intersection types allows you to use the `&` operator, called intersection, to create an anonymous combination of types.

##### intersection

```javascript
function extend<T, U>(first: T, second: U): T & U {  
    let result = <T & U>{};
  for (let id in first) {
        result[id] = first[id];
    }

    for (let id in second) {
        if (!result.hasOwnProperty(id)) {
            result[id] = second[id];
        }
    }
    return result;
}

var extended = extend({ a: 'answer to everything' }, { b: 42 });  
console.log(extended.a); // works  
console.log(extended.b); // works  
```

#### Abstract Classes

Abstract classes may seem like a familiar topic if you have spent much time in another language but it's _brand new_ in TypeScript. With an abstract class it is possible to create a base class with default implementations that can be built on. Since these base classes are abstract the compiler will throw an exception if you attempt to instantiate one.

##### myAbstract

```javascript
abstract class myAbstract{  
    fiz(): number { return this.bang(); }
    abstract bang(): number;
}

var a = new myAbstract();  // error, Cannot create an instance of the abstract class 'myAbstract'

class myConcrete extends myAbstract {  
    bang() { return 1; }
}

var b = new b();  // Yay, it worked
```

#### Generic Type Aliases

In TypeScript 1.6 type aliases can now be generic allowing for more expressive capabilities.

##### reversOrder

```javascript
type reversOrder<A, B, C> = (c:C, b:B, a:A) => A;  
var example: reversOrder<number, string, boolean>;  
example(true, 'two', 99);  
```

#### Breaking Changes

Now with all these changes there may be some issues to be aware of, be sure to check the [breaking changes](https://github.com/Microsoft/TypeScript/wiki/Breaking-Changes) page to see what might effect you and your project.

Hopefully these changes enhance your type experience. If you would like to see the examples used in this post they are on available on [GitHub](https://github.com/BrettMN/IntroToTypescriptExamples). Just look for `1_6features.ts`.
