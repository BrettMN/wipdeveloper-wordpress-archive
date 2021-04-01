---
layout: "post.11ty.js"
title: "TypeScript - Accessing Other .ts Files"
date: "2015-10-15"
tags: 
  - "Blog"
  - "Typescript"
slug: "typescript-accessing-other-ts-files"
---

![TypeScript](images/typescript_logo_small1.png)

Recently I was asked about how to access other TypeScript files from within the file you are working on. The individual had some compiler issues and was trying to figure it out. So here are some tips to maybe help out.

Sometimes it may be necessary to use a `/// <reference path="" />` tag to help the compiler understand what files you are working with. If we had a project that had a folder called `app` with a file named `config` and we were accessing it from our `main.ts` it would look like this:

##### Reference in `main.ts`

```javascript
/// <reference path="app/config.ts" />
```

This will help the compiler resolve issues with the type system.

#### Script Tags

It is possible to use your TypeScript without a fancy module loader and just reference the files you want access to inside your `html`. This has the benefit of being quick and easy with smaller projects (read: examples), but lacks the sophistication of a module loading system that allows the modules to self define dependencies.

Given a project that has a `main.ts` and `config.ts` in root and a `service.ts` in a folder `app` all files could be referenced on the index page in 3 lines:

##### `index.html`

```markup
<!DOCTYPE html>  
<html>  
<head>  
    http://app/service.js
    http://config.js
    http://main.js
</head>  
<body>  
</body>  
</html>  
```

> Of course all standard notions of JavaScript script references apply so you can not load a script before a dependency without errors.

For this to work we will also need a complete

##### `main.ts`

```javascript
/// <reference path="config.ts" />
/// <reference path="app/service.ts" />

let config = new Config();  
let service =  new Service(config.settings.address);

let address = service.getAddress();

if(address === config.settings.address){  
    console.log(`The service returned ${config.settings.address}`)
}else{
    console.log(`The service did not return ${config.settings.address}`)
}
```

##### a `config.ts`

```javascript
class Config{  
    settings = {
        address :'www.WIPDeveloper.com'
    }
}
```

##### and a `service.ts`

```javascript
class Service{

    address:string;

    constructor(address:string){
        this.address = address;
    }

    getAddress(){
        return this.address;
    }
}
```

Now when our overly simple example loads we should see something like this in the developer console.

![success message in console](images/00-success2.png)

This example is just like working with multiple JavaScript files and making calls to other objects that have been added to the global scope from being loaded. The only special markup is if you have to add the `/// <reference path="" />` tags to help identify the proper types.

> I'm using Visual Studio 2015 with TypeScript 1.6 and don't actually need the `reference` tags but the handbook says they help.

#### SystemJS

Another way to work with multiple TypeScript files is to use a module loading system. For this example we will be using (SystemJS)\[https://github.com/systemjs/systemjs\]. Our files are largely the same but rather than trusting that items will be available on the global scope we will use `import` and `require` to specify what modules we will be needing as dependencies.

A few changes were necessary:

##### Updated `index.html`

```markup
<!DOCTYPE html>  
<html>  
<head>  
    http://system.js
</head>  
<body>  
    
        System.config({
            paths: {
                '*' :'*.js'
            }
        });

        System.import('main');
    
</body>  
</html>  
```

Using SystemJS we are able to import `system.js` file, do any require configuration and tell it the starting module for our 'app'.

##### `main.ts`

```javascript
import Config = require('app/config');  
let config = new Config();

import Service = require('app/services/service');

let service = new Service.Service(config.settings.address);

let address = service.getAddress();

if(address === config.settings.address){  
    console.log(`The service returned ${config.settings.address}`)
}else{
    console.log(`The service did not return ${config.settings.address}`)
}
```

The main module of our app has a few changes. You may notice that we are using `import` and `require` keywords to gain access to our other modules. This provides access to the modules that contain the classes we are exporting in the following `.ts` files.

##### `app/config.ts`

```javascript
export = class Config{  
    settings: { address: string };

    constructor() {
        this.settings = {
            address: 'www.WIPDeveloper.com'
        }
    }
}
```

##### and a `service.ts`

```javascript
export = class Service{

    address:string;

    constructor(address:string){
        this.address = address;
    }

    getAddress(){
        return this.address;
    }
}
```

The primary difference for the `config.ts` and `service.ts` is we added the `exports` before the class declaration so we can allow access to the class in other modules.

Now if we load our `index.html` we should see the same results as before in the console.

![success message in console](images/00-success2.png)

This was just 2 examples of using `.ts` files from different locations within your project. All source code is available at [https://github.com/BrettMN/TypeScriptSamples](https://github.com/BrettMN/TypeScriptSamples) in the `FilesByReference` and the `SystemJSModules` directories.

If you have more questions feel free to leave a comment and I will get back to you as soon as I can
