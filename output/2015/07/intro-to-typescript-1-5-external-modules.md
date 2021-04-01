---
layout: "post.11ty.js"
title: "Intro to TypeScript 1.5 - External Modules"
date: "2015-07-29"
tags: 
  - "Blog"
  - "Typescript"
slug: "intro-to-typescript-1-5-external-modules"
---

![TypeScript](images/typescript_logo_small1.png)

> This is the ninth post in a series on getting to know TypeScript. If you missed the few posts feel free to go back and read them.
> 
> 1. [Intro to TypeScript 1.5 beta - Types](/2015/05/29/intro-to-typescript-1-5-beta-types/)
> 2. [Intro to TypeScript 1.5 beta - Interfaces](/2015/06/01/intro-to-typescript-1-5-beta-interfaces/)
> 3. [Intro to TypeScript 1.5 beta - Functions Part 1](/2015/06/04/intro-to-typescript-1-5-beta-functions-part-1/)
> 4. [Intro to TypeScript 1.5 beta - Functions Part 2](/2015/06/05/intro-to-typescript-1-5-beta-functions-part-2/)
> 5. [Intro to TypeScript 1.5 beta - Functions Part 3](/2015/06/08/intro-to-typescript-1-5-beta-functions-part-3/)
> 6. [Intro to TypeScript 1.5 beta - Classes Part 1](/2015/06/10/intro-to-typescript-1-5-beta-classes-part-1/)
> 7. [Intro to TypeScript 1.5 beta - Classes Part 2](/2015/06/05/intro-to-typescript-1-5-beta-functions-part-2/)
> 8. [Intro to TypeScript 1.5 beta - Intro to Modules](/2015/07/28/intro-to-typescript-1-5-beta-intro-to-modules/)

UPDATE: Thanks to Yahiko Uzumaki on Twitter for pointing out that TypeScript Internal Modules are now called Namespace and External Modules are just called 'Modules'. This Change can be seen in the [release notes](http://blogs.msdn.com/b/typescript/archive/2015/07/20/announcing-typescript-1-5.aspx) and the [handbook on GitHub](https://github.com/Microsoft/TypeScript-Handbook/blob/master/pages/Namespaces%20and%20Modules.md). Please keep that in mind as you read.

<blockquote class="twitter-tweet" lang="en"><p dir="ltr" lang="en"><a href="https://twitter.com/BrettMN">@BrettMN</a> External modules should be simply called modules now, since internal modules are officially "namespaces".</p>— Yahiko Uzumaki (@YahikoUzumaki2) <a href="https://twitter.com/YahikoUzumaki2/status/627203641716404224">July 31, 2015</a></blockquote>[//platform.twitter.com/widgets.js](//platform.twitter.com/widgets.js)

Last time in [Intro to TypeScript 1.5 beta - Intro to Modules](/2015/07/28/intro-to-typescript-1-5-beta-intro-to-modules/) we talked about basic TypeScript modules features. In those examples we used only 'internal' modules. TypeScript has a concept called 'external' modules for use with Node.js or RequireJS. External modules specify relationships using `import` statements that consist of the keyword `import` a name that will be used for the module in the current file and the `require` keyword with the path the the file.

##### Referance Internal Module

```javascript
Module.exportedFunctionOrClass();  
```

##### Referance External Module

```javascript
import localName = require('./ExternalModuelFileName');  
```

With external modules the `module` keyword is not needed. The module is defined by what is in the one file. We still use the `export` keyword to make a class or function available for use outside of the module.

> To configure the project to use modules I added a `tsconfig.json` file to the root of the project folder and added `"module": "commonjs"` to the list of options.

If we redid our previous `Paths` module as external modules they might look like this:

##### `Paths.ts`

```javascript
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
```

##### `PathsExtended.ts`

```javascript
import paths = require('externalModules/Paths');

export var getPath = paths.getPath;

export var getApiPath: GetPath;  
getApiPath = function (id: number, controller: string, action: string) {

    if (!controller) {
        controller = defaultController;
    }
    if (!action) {
        action = defaultAction;
    }

    return rootPath + 'api/' + controller + '/' + action + '/' + id;
}
```

You may notice that the first this we do with the `PathsExtended` module `import`s the `Paths` module and then `export`s a function from it. This way the user of the `PathsExtended` module only needs to import one module to get all the functionality that was present before.

> For a better understanding of the differences between the [node.js (commonjs)](http://www.commonjs.org/) or [require.js (AMD)](http://requirejs.org/) please feel free to visit their respective websites for further reading.

Now we can import these modules and access the their functions.

```javascript
import paths = require('externalModules/Paths');  
import extendedPaths = require('externalModules/PathsExtended');


var homePath = paths.getPath(1, 'home');  
var homePath2 = extendedPaths.getPath(1, 'home', 'index');  
var apiPath = extendedPaths.getApiPath(1, 'home');  
```

## Exports = what?

With that last example we exported one function from the `Paths` module. To use that function we had to use the dot notation to access it. In situations like this we could us the `export =` syntax to simplify access. When the `export =` symbol is imported it is consumed directly and does not need the dot notation to get access to it.

Lets try it with our `Paths` module.

##### `Paths2.ts`

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

export = getPath;  
```

You can see the (big) difference here at the end where we `export = getPath`. Now if we import this we can consume it directly.

##### `Paths2.ts`

```javascript
import paths2 = require('externalModules/Paths2');  
var homePath3 = paths2(1, 'home', 'index');  
```

> This would probably make more sense if our module exported a class. Oh well, maybe next time.

Now we have an understanding of External modules and the `export =` syntax use it wisely. And be sure to stop by again soon as we will go over a few more details on TypeScript Modules in [Intro to TypeScript 1.5 - Modules Remainders](/2015/08/07/intro-to-typescript-1-5-modules-remainders/).
