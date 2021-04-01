---
layout: "post.11ty.js"
title: "Angular Directive to wrap a jQuery plugin"
date: "2015-02-19"
tags: 
  - "Angular Directive"
  - "AngularJs"
  - "Blog"
  - "jQuery"
slug: "angular-directive-to-wrap-a-jquery-plugin"
---

The other day at work I started working on a project that had made heavy use of a jQuery plugin for masking date inputs. I was re-implementing some things with Angular and had to maintain the same behavior that the users had come to expect as the norm. There were strange issues with how the previous implementation used its jQuery selector (it was looking to a data-mask attribute used by the library) and getting the date to display properly on page load.

Now I've not used a jQuery plugin inside an Angular app before so I have not done this before. It's also been a few months since I worked with Angular so I'm a little out of practice. I know Angular uses jQuery if jQuery is loaded on the page first but I didn't understand how before this little exercise.

All that said here are some things I learned to keep in mind when wrapping a jQuery plugin in an Angular directive.

- Load jQuery and the plugin before Angular on the page.
- Use angular.element not $ to select the dom element.
- Keep it simple.
- If the element you are binding to is not the base element of your template don't forget to select the proper child.
- If you need use a similar value for the plugin and an Angular feature pass both values in.

A sample project is available on GitHub at [https://github.com/BrettMN/jQuery-Plugin-Wrapper-for-Angular](https://github.com/BrettMN/jQuery-Plugin-Wrapper-for-Angular)

### First things first: Load the libraries in the proper order.

JQuery, plugin than Angular. For my sample app that makes the head look similar to this:

```markup
<head>  
  http://js/libs/jquery/dist/jquery.js
  http://js/libs/maskerade/jquery.maskerade.js
  http://js/libs/angular/angular.js
  // other scripts here or there or anywhere
</head>  
```

### Don't use '$'

If for some reason you feel the need to wrap an element with jQuery user 'angular.element' not '$'. This is because when jQuery is loaded first it is pulled into Angular for use and can be referenced from 'angular.element'. The [Angular documentation](https://docs.angularjs.org/api/ng/function/angular.element)(v1.4.0-build.3807) says 'angular.element' is an alias for the jQuery function but if for some reason you load jQuery and a plugin then Angular and jQuery gets loaded again the plugin is still present at 'angular.element' even though '$' has been freshly reloaded. Page2.html in the sample project has console logs that show how these are 2 different functions.

### Keep it Simple

If your making a Directive that effects one input element **do not** add a label and an area for validation messages. Your directive will be more reusable if it's smaller, more focused on it's task than if it's trying to be all that it can and might not need to be.

### Get the proper element from your $element

If for some reason things are not working out for you be sure you are working with the element you think you are working with. I became too focused on the end results and forget that the element I was binding to was not the root element.

```javascript
//Inside your directive link use this to get the third element inside of the root element
$element[2]
```

Finally, don't try to get good enough by using one value for 2 purposes that are similar. In this case Angular $filter and Maskerade masks use similar letter but are cased differently so toLowerCase() would have only cause more problems in the long run as you try to reuse the directive with different patterns.

[Sample Project on GitHub](https://github.com/BrettMN/jQuery-Plugin-Wrapper-for-Angular)
