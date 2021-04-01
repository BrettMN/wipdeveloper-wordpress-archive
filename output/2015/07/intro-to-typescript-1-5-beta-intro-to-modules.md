---
layout: "post.11ty.js"
title: "Intro to TypeScript 1.5 beta - Intro to Modules"
date: "2015-07-27"
tags: 
  - "Blog"
  - "Typescript"
slug: "intro-to-typescript-1-5-beta-intro-to-modules"
---

![TypeScript](images/typescript_logo_small1.png)

> This is the eighth post in a series on getting to know TypeScript. If you missed the few posts feel free to go back and read them.
> 
> 1. [Intro to TypeScript 1.5 beta - Types](/2015/05/29/intro-to-typescript-1-5-beta-types/)
> 2. [Intro to TypeScript 1.5 beta - Interfaces](/2015/06/01/intro-to-typescript-1-5-beta-interfaces/)
> 3. [Intro to TypeScript 1.5 beta - Functions Part 1](/2015/06/04/intro-to-typescript-1-5-beta-functions-part-1/)
> 4. [Intro to TypeScript 1.5 beta - Functions Part 2](/2015/06/05/intro-to-typescript-1-5-beta-functions-part-2/)
> 5. [Intro to TypeScript 1.5 beta - Functions Part 3](/2015/06/08/intro-to-typescript-1-5-beta-functions-part-3/)
> 6. [Intro to TypeScript 1.5 beta - Classes Part 1](/2015/06/10/intro-to-typescript-1-5-beta-classes-part-1/)
> 7. [Intro to TypeScript 1.5 beta - Classes Part 2](/2015/06/05/intro-to-typescript-1-5-beta-functions-part-2/)

Sometime when working with JavaScript things can get a little busy on the global scope, unless you are using certain design patterns. TypeScript helps prevent global scope pollution with modules. Modules allow you, the developer, to logically organize your code similar to namespaces in other languages. With modules you can choose what to expose for use outside of the module.

## Without Modules

Without the use of modules you might write some code to get a path to your app like follows:

##### `module-before.ts`

```javascript
var rootPath: string = "www.wipdeveloper.com/",  
    defaultController = "home",
    defaultAction = "index";


interface GetPath {  
    (id: number, controller: string, action?: string): string
}

var getPath: GetPath;  
getPath = function (id: number, controller: string, action: string) {

    if (!controller) {
        controller = defaultController;
    }
    if (!action) {
        action = defaultAction;
    }

    return rootPath + controller + '/' + action + '/' + id;
}
```

Most of what we have is needed for the implementation but the only thing that would be needed from code that calls it is access to the `getPath` function. And with everything outside of a class we are just adding things to the global scope. That's not something we should be doing.

If we modify our code to use modules we can expose only the method, like so:

##### `module-base.ts`

```javascript
module Paths {  
    var rootPath: string = "www.wipdeveloper.com/",
        defaultController = "home",
        defaultAction = "index";


    interface GetPath {
        (id: number, controller: string, action?: string): string
    }

    export var getPath: GetPath;
    getPath = function (id: number, controller: string, action: string) {

        if (!controller) {
            controller = defaultController;
        }
        if (!action) {
            action = defaultAction;
        }

        return rootPath + controller + '/' + action + '/' + id;
    }
}
```

A couple of things to notice here. We wrapped our previous code inside a module declaration with a the name `Path`: `module Paths {}`. We also `export` the function `getPath` declaration so that is may be used outside of our module. Now we can all it similar to Accessing things inside a Namespace:

##### Calling All Paths

```javascript
Paths.getPath(1, 'home', 'index');  
```

## That's Great but Wont the Module File Get Too Big Like This Heading?

If you are creating a large app it is possible for your module to grow in size beyond what is comfortable with just one file. So it's a good thing we can split modules up in multiple files.

##### `module-extended.ts`

```javascript
module Paths {

    //Api path
    export var getApiPath: GetPath;
    getApiPath = function (id: number, controller: string, action: string) {

        if (!controller) {
            controller = defaultController;
        }
        if (!action) {
            action = defaultAction;
        }

        return rootPath +'api/' + controller + '/' + action + '/' + id;
    }
}
```

With the module in two files we can still access values declared in the other file since it is the same module.

With this basic understanding of modules we can begin to logically separate our code into smaller units that are easy to manage. Check out the next post in this series, [Intro to TypeScript 1.5 - External Modules](/2015/07/30/intro-to-typescript-1-5-external-modules/).
