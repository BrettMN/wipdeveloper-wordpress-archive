---
layout: "post.11ty.js"
title: "Aurelia and ASP.NET 5 - Understanding the Aurelia Parts - The Basics"
date: "2015-07-27"
tags: 
  - "ASP.NET 5"
  - "Aurelia"
  - "Blog"
slug: "aurelia-and-asp-net-5-understanding-the-aurelia-parts-the-basics"
---

Last time, [Getting Started with Aurelia and ASP.NET 5](/2015/07/24/getting-started-with-aurelia-and-asp-net-5/), we set up an ASP.NET 5 project with Aurelia. We sort of glossed over what we did with Aurelia so I thought we could go back, take a look at it and get a better understanding of it.

Lets get started by looking at the scripts we referenced.

##### Look At My Head Again

```markup
<head>  
    <meta charset="utf-8" />
    <title></title>
    http://jspm_packages/system.js
    http://config.js
    System.import('aurelia-bootstrapper');
</head>  
```

The file `jspm_packages/system.js` loads [SystemJS](https://github.com/systemjs/systemjs) on the page. If you are not familiar with SystemJS it is dynamic module loader. The `config.js` loads the configuration settings for SystemJS. A lot of the options in the `config.js` were determined for us when we ran `jspm init` and answered those few questions. The `System.import('aurelia-bootstrapper');` tells SystemJS to load the `aurelia-bootstrapper` that is specified in the `config.js`.

We also specified some markup on our index page.

##### Index.html

```markup
<body>
```

</body>

The `aurelia-app` attribute tells Aurelia where the base of the Aurelia app is located in the hierarchy of your html. This is the location that the `aurelia-bootstrapper` will inject the `app.html` and `app.js` after they have been data-binded together.

Our `app.js` contained a `configureRouter` that we passed in a `config` and a `router`.

##### app.js

```javascript
export class App {  
    configureRouter(config, router){
        config.title = 'Aurelia-Setup';
        config.map([
          { route: ['','main'], name: 'main',      moduleId: './main',      nav: true, title:'Main Page' }
        ]);

        this.router = router;
    }
}
```

On the `config` we set the title, this is optional, and configured the one route we currently have. Each route requires a `route`, the url pattern that must be matched, and a `moduleId`, the relative path to the module id that is to be used for that route. Additional route properties include `name`, that can be used to generate a link to the route, a `title`, that can be used to generate the documents title, `nav`, that specifies if the route should be included in the navigation model, and a `href` that could be used the bind in the navigation model.

In the `app.html` file you may have noticed a few thing. First it's not a full html file as it has a root element of `template` and second we only added a `router-view` element to it.

##### app.html

```markup
<template>  
        <router-view></router-view>
</template>  
```

The `template` element is a [W3 spec](http://www.w3.org/TR/html5/scripting-1.html#the-template-element) used to declare fragments of html that may be loaded/inserted after page load. The `router-view` is where the router will inject the currently active view based on the url path and configuration.

## But There is Still Nothing to Look At

The last pair of things we added were the `main.js` and `main.html`.

##### main.js

```javascript
export class Main{  
    message = 'Hello';
}
```

We kept things simple in `main.js` as it is just a JavaScript class that has one property, `message` that is set to `"Hello"`. Granted it's a ECMAScript 6 class so it may seem a little different from what you have seen in JavaScript in the past.

##### main.html

```markup
<template>  
    <h1>main page</h1>
    <h4>${message}</h4>
</template>  
```

In `main.js` we see it's a `template` again but contains some standard html stuff that we see everyday but what's the `${message}`? That is Aurelia's databinding syntax in html. The `${}` is similar to ES6 template strings placeholders so JavaScript developers can feel/get comfortable with it notion of replacing those with the properties of the same name. In this case the `message` property we set on the `main.js` class and why we see "Hello" when we run the app.

![Results](images/00-final2.png)

With this better understanding of what we did last time we can move forward with making a more complex application with Aurelia and ASP.NET 5.
