---
layout: "post.11ty.js"
title: "ECMAScript 6 - Spread Syntax"
date: "2017-05-03"
tags: 
  - "Blog"
  - "ECMAScript6"
  - "Lightning"
  - "Salesforce"
  - "SalesforceDeveloper"
slug: "ecmascript-6-spread-syntax"
---

Have you head about the Spread Syntax? It a way to expand in place an iterable. Lets take a look.

## What?

The Spread Syntax allows you to expand an iterable in place. What this means is if you have an array and you use the spread syntax (`...`) om it the values in the array will expanded in place as individual objects. You would use this in function calls for the parameter list, and you can also use it to deconstruct arrays when creating new arrays.

#### Sample Spread Syntax Calling Function

\[js\] var fiveObjects = \[ 1, '2', 'three', {'four':'IV'}, 5 \]; console.log(...fiveObjects); \[/js\]

#### Sample Spread Syntax Array Assignment

\[js\] var twoObjects = \[ 1, '2' \];

var threeObjects = \[ 'three', {'four':'IV'}, 5 \];

var fiveObjects = \[...twoObjects, ...threeObjects\];

// fiveObjects would consist of // \[ 1, '2', 'three', {'four':'IV'}, 5\] \[/js\]

## Where Can I Use It?

If you check the compatibility tables at [http://kangax.github.io/compat-table](http://kangax.github.io/compat-table/es6/#test-spread_(...)_operator) you see good support on Desktop but it looks like Android may be an issue.

> On the [Mozilla website](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_operator#Browser_compatibility) it shows that android web-view and Chrome support the spread syntax.

No love for IE11 though so if you plan on supporting users still on Internet Explorer a transpiler will probably be required.

#### Can I Use `Rest Parameters`

[Can I Use rest-parameters?](http://caniuse.com/#feat=rest-parameters) Data on support for the rest-parameters feature across the major browsers from caniuse.com.

This means we will be able to use it when working with Frameworks like Angular, Vue.js, Aurelia, and React.

## What About In Lightning?

It works in Lightning! There are no saving or parsing issues. There shouldn't be an issue as long as your users are not holding on to IE11.

## What is it Good For?

One place I tend to use it is in a helper function to call Apex Remote Actions. When calling the `invokeAction` method it take a variable number of parameters depending on the Apex method. Passing the array makes it so I can have one definition for the helper and it can vary the parameters length with an empty array for no parameters or as many items in the array as the method requires.

#### Spread Syntax Example

\[js\] function callRemote(methodName, params, resolve, reject) { console.log(...params) Visualforce.remoting.Manager.invokeAction( methodName, ...params, //<== Spread Syntax in Action! function (result, event) { console.log({ event }) console.log({ result })

if (event.status) { resolve(result) } }, { //Options I am not setting } ); } \[/js\]

Hope that helps some!

## Conclusion

With a little understanding you may see more places to use the Spread Syntax. Are there places you tend to use it? Let me know by leaving a comment below or emailing [brett@wipdeveloper.com](mailto:brett@wipdeveloper.com).

<script src="//cdn.jsdelivr.net/caniuse-embed/1.1.0/caniuse-embed.min.js"></script>
