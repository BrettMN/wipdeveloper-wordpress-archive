---
layout: "post.11ty.js"
title: "Salesforce Mobile SDK and Ionic - Offline - Intro"
date: "2017-12-04"
tags: 
  - "Blog"
  - "Cordova"
  - "IonicFramework"
  - "Salesforce"
  - "SalesforceDeveloper"
slug: "salesforce-mobile-sdk-and-ionic-offline-intro"
coverImage: "Screen-Shot-2017-12-06-at-12.07.08-AM.png"
---

One of the main reasons a mobile app would be preferred over a website is the ability to function offline.  With people on the go with variably reliable internet connections this can be a big concern.  Luckily we haven't been building a website so we can deal with this using the tools that the Salesforce Mobile SDK provides: SmartStores and SmartSync!

## SmartStore

SmartsStore is a plugin for mobile projects to safely store Salesforce Data on a device in encrypted databases.  This allows users to access data even after their device has lost it's internet connection and provides security for the data.

SmartStores come in 2 varieties: user-based and global.

A user-based store is used for a specific log in to Salesforce and the lifecycle of the store is managed by the plugin.  This means that you don't have to worry about cleaning up your data store when the user logs out or the session end another way, SmartSync handles that for you.

A global store is not tied to a specific Salesforce login.  This means that the data will persist if the user logs out of Salesforce and it is up to the developer to manage the clean up.

## SmartSync

SmartSync is two different things used to synchronize changes that were made while offline with Salesforce. The SmartSync plugin uses the device native SmartSync to provide `syncup` and `syncdown` but does now return an model objects.  SmartSync.js is a JavaScript library build on Backbone.js and provides easy-to-use model objects.  Smartsync.js also requires writing your own `syncup` function.

## Conclusion

Don’t forget to sign up for [**The Weekly Stand-Up!**](https://wipdeveloper.wpcomstaging.com/newsletter/) to receive free the [WIP Developer.com](https://wipdeveloper.wpcomstaging.com/) weekly newsletter every Sunday!
