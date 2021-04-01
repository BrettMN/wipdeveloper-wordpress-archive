---
layout: "post.11ty.js"
title: "Cordova - Single Page Application Setup"
date: "2016-02-09"
tags: 
  - "AngularJs"
  - "Aurelia"
  - "Blog"
  - "Cordova"
slug: "apache-cordova-single-page-application-setup"
---

Last post we did a set up for using Aurelia with Apache Cordova. One thing we didn't cover is that before you start your Single Page Application (spa) you should wait till the device is ready. Not waiting till it's ready may cause errors to occur in your app.

### The `deviceready` Event

It is possible to add an event listener to the `deviceready` event. This is the same as registering a listener to any other event:

```javascript
document.addEventListener("deviceready", function(){  
    ///Something gets done here
}, false);
```

This will allow to execute code after the device is ready.

> Don't worry if your code to add the listener is executed after the device is already ready. Cordova will execute your callback function immediately.

Now Lets see how to use the `deviceready` event with a couple different frameworks.

### Aurelia

To prevent Aurelia from loading and making calls to the Cordova Apis before they are ready you can have the `deviceready` call back event call the `SystemJS.import` of the `aurelia-bootstrapper` like so:

```javascript
document.addEventListener("deviceready", function(){  
    SystemJS.import('aurelia-bootstrapper');
}, false);
```

### Angular

To allow the device and Cordova to get ready before starting up your Angular app don't put a `ng-app="appname"` attribute in the html and instead use the `angular.bootstrap()` function.

```javascript
document.addEventListener("deviceready", function(){  
      angular.bootstrap(document.body, ['appname']);
}, false);
```

You can use a different dom element besides the `document.body` you will just need to use select the element and pass it in and that will become the root of you Angular application.

### Conclusion

Have you set up your SPA in Cordova differently? I would like to hear about it, leave a comment below or send an email to me at [brett@wipdeveloper.com](mailto:brett@wipdeveloper.com).
