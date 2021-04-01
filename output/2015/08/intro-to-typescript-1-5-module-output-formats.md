---
layout: "post.11ty.js"
title: "Intro to TypeScript 1.5 - Module Output Formats"
date: "2015-08-20"
tags: 
  - "Blog"
  - "Typescript"
slug: "intro-to-typescript-1-5-module-output-formats"
---

![TypeScript](images/typescript_logo_small1.png)

> This is the eleventh post in a series on getting to know TypeScript. If you missed the few posts feel free to go back and read them.
> 
> 1. [Intro to TypeScript 1.5 beta - Types](/2015/05/29/intro-to-typescript-1-5-beta-types/)
> 2. [Intro to TypeScript 1.5 beta - Interfaces](/2015/06/01/intro-to-typescript-1-5-beta-interfaces/)
> 3. [Intro to TypeScript 1.5 beta - Functions Part 1](/2015/06/04/intro-to-typescript-1-5-beta-functions-part-1/)
> 4. [Intro to TypeScript 1.5 beta - Functions Part 2](/2015/06/05/intro-to-typescript-1-5-beta-functions-part-2/)
> 5. [Intro to TypeScript 1.5 beta - Functions Part 3](/2015/06/08/intro-to-typescript-1-5-beta-functions-part-3/)
> 6. [Intro to TypeScript 1.5 beta - Classes Part 1](/2015/06/10/intro-to-typescript-1-5-beta-classes-part-1/)
> 7. [Intro to TypeScript 1.5 beta - Classes Part 2](/2015/06/05/intro-to-typescript-1-5-beta-functions-part-2/)
> 8. [Intro to TypeScript 1.5 beta - Intro to Modules](/2015/07/28/intro-to-typescript-1-5-beta-intro-to-modules/)
> 9. [Intro to TypeScript 1.5 - External Modules](/2015/07/30/intro-to-typescript-1-5-external-modules/)
> 10. [Intro to TypeScript 1.5 - Modules Remainders](/2015/08/07/intro-to-typescript-1-5-modules-remainders/)

With TypeScript 1.5 you have the options of choosing 4 different output formants, `AMD`, `CommonJS`, `SystemJS` and `UMD`. In [Intro to TypeScript 1.5 beta - Intro to Modules](/2015/07/28/intro-to-typescript-1-5-beta-intro-to-modules/) we configured our project to use `commonjs` in our `tsconfig.json` file. So if we are targeting ECMAScript 5 and have a TypeScript module like this:

##### TypeScript Paths Module

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

The output with `commonjs` as the module target would look like this:

##### Paths Module As CommonJS

```javascript
var rootPath = "www.wipdeveloper.com/", defaultController = "home", defaultAction = "index";  
exports.getPath;  
exports.getPath = function (id, controller, action) {  
    if (!controller) {
        controller = defaultController;
    }
    if (!action) {
        action = defaultAction;
    }
    return rootPath + controller + '/' + action + '/' + id;
};
```

If we change the module target to `amd` we would get this:

##### Paths Module As AMD

```javascript
define(["require", "exports"], function (require, exports) {  
    var rootPath = "www.wipdeveloper.com/", defaultController = "home", defaultAction = "index";
    exports.getPath;
    exports.getPath = function (id, controller, action) {
        if (!controller) {
            controller = defaultController;
        }
        if (!action) {
            action = defaultAction;
        }
        return rootPath + controller + '/' + action + '/' + id;
    };
});
```

Of course id the module target is set to `system` it is different again:

##### Paths Module As SystemJS

```javascript
System.register([], function(exports_1) {  
    var rootPath, defaultController, defaultAction, getPath;
    return {
        setters:[],
        execute: function() {
            rootPath = "www.wipdeveloper.com/", defaultController = "home", defaultAction = "index";
            exports_1("getPath", getPath);
            exports_1("getPath", getPath = function (id, controller, action) {
                if (!controller) {
                    controller = defaultController;
                }
                if (!action) {
                    action = defaultAction;
                }
                return rootPath + controller + '/' + action + '/' + id;
            });
        }
    }
});
```

And if we set ithe module target to `umd` we get a different result again:

##### Paths Module As UMD

```javascript
(function (deps, factory) {
    if (typeof module === 'object' && typeof module.exports === 'object') {
        var v = factory(require, exports); if (v !== undefined) module.exports = v;
    }
    else if (typeof define === 'function' && define.amd) {
        define(deps, factory);
    }
})(["require", "exports"], function (require, exports) {
    var rootPath = "www.wipdeveloper.com/", defaultController = "home", defaultAction = "index";
    exports.getPath;
    exports.getPath = function (id, controller, action) {
        if (!controller) {
            controller = defaultController;
        }
        if (!action) {
            action = defaultAction;
        }
        return rootPath + controller + '/' + action + '/' + id;
    };
});
```

By now you may be wondering witch output you should choose for your project. Well it depends. All four formats have their particular uses. `CommonJS` is used with Node.js. `AMD` implements the [RequireJS](http://requirejs.org/) module loader format. [`UMD`](https://github.com/umdjs/umd) is a module loader that attempts to meet the needs of both `CommonJS` and `RequireJS`. [`SystemJS`](https://github.com/systemjs/systemjs) is a "Universal dynamic module loader" that can work with "ES6 modules, AMD, CommonJS and global scripts".

So it depends on what you are working with and how you want to manage your modules. I would read through how each module works and choose the one that best suits your needs.

#### ECMAScript 6?

All these examples were given with the target set to `es5`. If we change the target to `es6` we get more terse out put but then we wouldn't be able to rely on browsers to reliably consume the JavaScript we have outputted. At some point in the future we will be able to trust consumers of our code to be able to use all the ECMAScript 6 stuff but by then we will probably be using features from ECMAScript 7 or 2016 or whatever it's going to be called.
