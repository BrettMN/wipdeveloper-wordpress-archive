---
layout: "post.11ty.js"
title: "Intro to TypeScript 1.5 - Modules Remainders"
date: "2015-08-06"
tags: 
  - "Blog"
  - "Typescript"
slug: "intro-to-typescript-1-5-modules-remainders"
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
> 9. [Intro to TypeScript 1.5 - External Modules](/2015/07/30/intro-to-typescript-1-5-external-modules/)

In the last two posts we covered some basics of TypeScript Namespace and Modules. And while you can import an entire Namespace into your working file that may not be necessary for your needs. In which case an _Aliase_ might be useful.

#### Aliases

Given a Namespace structured as follows:

##### Colors Namespace

```javascript
namespace Colors {  
    export namespace Warm {
        export class Red { }
        export class Yellow { }
    }
    export namespace Cold {
        export class Blue { }
    }
}
```

We could import the entire namespace has we previously had even if we are just going to use the `Warm` colors.

##### Previously Way

```javascript
import colors = Colors;  
var red0 = new colors.Warm.Red();  
```

To make it easier to use the `Warm` colors we can import `Colors.Warm` to a distinct object and reference it from there.

##### Aliase Way

```javascript
import warmColors = Colors.Warm;  
var red1 = new warmColors.Red();  
```

> When using aliases in this manner we don't use the `require` keyword.

So far we have only discussed using our own TypeScript code in a project but what if we want to use a third party library? Wouldn't TypeScript a lack of type information about the library?

#### Ambient Definitions

It is possible to use Namespaces and Modules to define the declarations that a library uses without implementing the definition. Doing this allows us to load the library normally but still have type checking while we are coding. These defined but not implemented TypeScript Namespaces and Modules are called Ambient and generally kept in a `*.d.ts` file. The `*.d.ts` file is similar in nature to a header file you might be familiar with from C/C++.

##### Ambient Namespace

```javascript
declare namespace wip {  
    export interface actions {
        send: {
            (data: WipData): void;
        }
    }

    export interface WipData {
        id: number,
        message: string
    }
}

declare var wipActions: wip.actions;  
```

Here we have a namespace that just provide the typing for our fake 'WIP' library. With this in place we can now get gain the benefit of type checking in in TypeScript for our custom library and load the library on the page with a standard `<script>` tag.

##### Ambient Modules

```javascript
declare module "url" {  
    export interface Url {
        protocol?: string;
        hostname?: string;
        pathname?: string;
    }

    export function parse(urlStr: string, parseQueryString?, slashesDenoteHost?): Url;
}

declare module "someOtherModule" {  
    export function separate(phrase: string, indexToSeperateAt: number): string;
    export function join(separator: string, ...words: string[]): string;
    export var count: number;
}
```

With Ambient Modules it is possible to declare multiple modules in the same `*.d.ts` file so you only need to use one `/// <reference/>` tag in your working file.

> We haven't talked about it but you can use `/// <reference/>` comments to gain intellisense in you TypeScript files.

##### Ambient Modules in Work

```javascript
/// <reference path="ambientmodule.d.ts" />
import url = require("url");  
var myUrl = url.parse("http://www.wipdeveloper.com");  
```

Here we use our custom definition to gain intellisense for use with the Node.js Url module.

#### Something to Watch out for

Namespaces and Modules add conveniences to aspects of working with TypeScript but they are not with their potential pitfalls.

#### Namespacing a modules

In the following `.ts` file we create a namespace.

##### Colors.ts

```javascript
export namespace Colors {  
    export class Red { /* ...Something boring here... */ }
    export class Blue { /* ...Something interesting here... */ }
}


This is all well and good if we were just going to use the Namespace convention but we plan on importing this as a module.

#####Colors.ts
```

language-javascript import colors = require('./needlessNamespace'); var red = new colors.Colors.Red(); // Oh so not clear \`\`\`

As you can see this causes some excessive namespacing to go on. If we remove the namespace from our `Colors.ts` file we can access remove one of those `Colors`.

That's all for now. Join us next time for some more TypeScript fun!
