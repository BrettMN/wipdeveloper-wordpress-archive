---
layout: "post.11ty.js"
title: "Salesforce Mobile SDK and Ionic – Plugins"
date: "2017-09-05"
tags: 
  - "Blog"
  - "Cordova"
  - "IonicFramework"
  - "Salesforce"
  - "SalesforceDeveloper"
slug: "salesforce-mobile-sdk-ionic-plugins"
coverImage: "Screen-Shot-2017-09-06-at-11.55.00-PM.png"
---

One of the main benefits of creating an app to be installed on a device is you get to access device specific features.  What is a "Device Specific Feature" you say?  Well, good question.

## Device Specific Feature

A Device Specific Feature is a capability or feature built into a device through a combination of it's software and hardware.  Access to the Camera, File System, Geolocation, and the ability to ask the user to rate your app in the App Store or Google Play are examples of Device Specific Features.

Cordova allows us to access these features without the need to write native code through Plugins.

## Plugins

Cordova Plugins allow a Cordova apps to access these native capabilities through a JavaScript API.  This allows us to leverage our existing web skills to bridge the gap from what is capable in a web browser to make use of those native features.

At the time of this writing there are 2637 plugins so there is a chance there is one to help you with what you need.  Search at [Cordova Plugins](https://cordova.apache.org/plugins/) to see what is available.

## Ionic Native

Plugins to access native features are great but they will most likely require callbacks and accessing the global `cordova` object.  This doesn't go well with Ionics TypeScript nature.  To assist developers with plugins the Ionic Team has created a related collections of TypeScript wrappers of a number of Cordova Plugins called [Ionic Native](https://ionicframework.com/docs/native/).

Ionic Native uses uses Promises or Observables to map the callbacks of the plugins to a common interface that goes in line with change detection of Angular.

## Conclusion

With all that said, let's see if we can add a plugin to our sample app next time.

Don’t forget to sign up for [**The Weekly Stand-Up!**](https://wipdeveloper.wpcomstaging.com/newsletter/) to receive free the [WIP Developer.com](https://wipdeveloper.wpcomstaging.com/) weekly newsletter every Sunday!

Looking for the code and want to follow along?  Find it on [GitHub.com/BrettMN/salesforce-sdk-mobile-with-ionic-starter](https://github.com/BrettMN/salesforce-sdk-mobile-with-ionic-starter)
