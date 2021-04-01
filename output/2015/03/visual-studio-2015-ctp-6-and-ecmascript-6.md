---
layout: "post.11ty.js"
title: "Visual Studio 2015 CTP 6 and ECMAScript 6"
date: "2015-03-05"
tags: 
  - "Babel"
  - "Blog"
  - "ECMAScript6"
  - "Gulp"
  - "Visual Studio"
slug: "visual-studio-2015-ctp-6-and-ecmascript-6"
---

Did you realize it's possible to write and use ECMAScript 6 (ES6) today? Projects like Traceur and Babel make it possible to write JavaScript as described by the ES6 standard and use a _transpiler_ to _compile_ it to the JavaScript you may know and love (or hate) of today. Transpilers typically take the source of one language and convert it to the source of a different language or take an older version of a language and output as a newer version. In this instance we want to take the new JavaScript and make it old so modern web browsers can use it.

Why would we want to do this? Well, some of the features introduced with ES6 make it easier to write more succinct code that is easier to read with less boilerplate.

ES5:

```javascript
var wordSpliter2 = function(word){  
        return word.split('');
    }
    var letters2 = wordSpliter2('wipdeveloper');
    for(let letter in letters2){
      console.log(letters2[letter]);
    }
```

ES6:

```javascript
var wordSpliter = (word)=>{return word.split('')}  
var letters = wordSpliter('wipdeveloper');  
for(let letter of letters){  
  console.log(letter);
}
```

Also things like `let`, `const`, `for...of`, `template strings`, `map`, `set` and so on make intent more obvious and easier to manipulate datasets, strings and objects. The list of features is impressive and useful... or they would be useful features if we could use them in today's browsers.

Using a transpiler like Babel set up with a Gulp watch allows you to write in ES6 and update your client side code without much work after set up than saving your code. (You do save your code, right?) There are some catches though. Currently, Visual Studios 2015 CTP 6 doesn't recognize ES6 code as valid and will keep showing errors. VS will also try and reformat your code to be "correct" causing formatting errors for what is actually correct ES6 code. You can avoid the constant red squiggly lines by changing your file extension to .es or .es6 and Babel will still work correctly.

If you would like Visual Studio to Support the new JavaScript Language features Go and Vote for them at the [Visual Studio User Voice](https://visualstudio.uservoice.com).

An example project that uses Babel with Gulp can be found at [github.com/BrettMN/Visual-Studio-2015-CTP-6-and-ECMAScript-6](https://github.com/BrettMN/Visual-Studio-2015-CTP-6-and-ECMAScript-6),
