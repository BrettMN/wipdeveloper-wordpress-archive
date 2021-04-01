---
layout: "post.11ty.js"
title: "Salesforce Mobile SDK 6.0.0 Consolidated Release Notes"
date: "2017-12-28"
tags: 
  - "Blog"
  - "Cordova"
  - "Salesforce"
  - "SalesforceDeveloper"
slug: "salesforce-mobile-sdk-6-0-0-consolidated-release-notes"
---

A little while ago there was a new release for the Salesforce Mobile SDK and I thought it would be easier to have one place to see the changes rather than having to look in the different repositories.  So here's a combined list of changes Salesforce Mobile SDK 6.0.0

## Android and iOS

#### Library Upgrades

We've updated React Native to version 0.50.4.

#### Login Enhancements

- In version 6.0, Mobile SDK enhances its authentication handling by adding identity provider services.
- Identity providers help known users avoid reentering their Salesforce credentials every time they log in to a Mobile SDK app.
- A Mobile SDK app can be used to provide authentication services to other Mobile SDK apps.
- We have created a template that can be used with `forcedroid` that demonstrates this functionality. This template can be found \[here\](https://github.com/forcedotcom/SalesforceMobileSDK-AuthTemplates).

#### SmartStore Enhancements

- Mobile SDK 6.0 introduces the ability to define your SmartStore schemas through configuration files rather than code.
- To define soups for the default global store, provide a file named `globalstore.json`.
- To define soups for the default user store, provide a file named `userstore.json`.

#### SmartSync Enhancements

- Beginning in Mobile SDK 6.0, you can define sync configuration files and assign names to sync configurations.
- You can use sync names to run, edit, or delete a saved sync operation.
- You can define “sync down” and “sync up” operations through configuration files rather than code.
- To define sync operations for the default global store, provide a file named `globalsyncs.json`.
- To define sync operations for the default user store, provide a file named `usersyncs.json`.

#### Mobile SDK Developer Tools

- The Developer Support dialog box is the launchpad for all available support screens and other useful actions.
- The dialog box presents only the options that are pertinent to the type of app you’re running.
- By default, these tools are available only in debug builds. However, you can use an API call to enable or disable the Developer Support screen at other times.

#### Other Technical Improvements

- Improvements to sample apps.
- Various bug fixes.

## Android

#### OS Version Support

- Android Oreo (API 27) is fully supported in Mobile SDK 6.0.
- The minimum Android OS version we support has been bumped up from KitKat (API 19) to Lollipop (API 21).

#### IDE Support

- Android Studio 3.0 and Gradle 4.1 are fully supported in Mobile SDK 6.0.

#### Library Upgrades

- We've updated Cordova to version 7.0.0.

#### Login Enhancements

- Mobile SDK 6.0 allows developers to use Chrome custom tabs for authentication instead of the system WebView.

#### Mobile SDK Developer Tools

- During debugging on a desktop, you can access the home screen through a keyboard shortcut or gesture (`⌘m` keyboard shortcut or `adb shell input keyevent 82`).

#### Forcedroid Changes

- The forcedroid utility no longer creates hybrid or React Native apps. Instead, install forcehybrid and forcereact npm packages for those use cases.

## iOS

#### OS Version Support

- iOS 11 is fully supported in Mobile SDK 6.0.
- The minimum iOS version we support has been bumped up from iOS 9 to iOS 10.

#### IDE Support

- Xcode 9 is the minimum version of Xcode required by Mobile SDK 6.0.

#### Library Upgrades

We've updated Cordova to version 4.5.4.

#### Mobile SDK Developer Tools

- During debugging on a desktop, you can access the home screen through a keyboard shortcut or gesture (`^⌘z` keyboard shortcut or `Shake Gesture` in the `Hardware` menu).

#### SDK Manager Classes

- The `SalesforceSDKManager` class welcomes several new SDK manager cousins that handle specific types of apps.
- This architecture now matches the analogous architecture in Mobile SDK for Android.

#### Other Technical Improvements

- Improvements to sample apps.
- Various bug fixes.

#### Deprecations

- `SFAuthenticationManager` and all its delegates are now deprecated and will be removed in Mobile SDK 7.0. Instead, use `SFUserAccountManager` for authentication related functionality.

#### Forceios Changes

- The forceios utility no longer creates hybrid or React Native apps. Instead, install forcehybrid and forcereact npm packages for those use cases.

## Conclusion

Don’t forget to sign up for [**The Weekly Stand-Up!**](https://wipdeveloper.wpcomstaging.com/newsletter/) to receive free the [WIP Developer.com](https://wipdeveloper.wpcomstaging.com/) weekly newsletter every Sunday!
