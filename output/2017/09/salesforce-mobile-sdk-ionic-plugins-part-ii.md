---
layout: "post.11ty.js"
title: "Salesforce Mobile SDK and Ionic – Plugins Part II"
date: "2017-09-12"
tags: 
  - "Blog"
  - "Cordova"
  - "IonicFramework"
  - "Salesforce"
  - "SalesforceDeveloper"
slug: "salesforce-mobile-sdk-ionic-plugins-part-ii"
coverImage: "Screen-Shot-2017-09-12-at-12.10.41-AM.png"
---

Since we already covered what a [plugin](https://wipdeveloper.wpcomstaging.com/2017/09/04/salesforce-mobile-sdk-ionic-plugins/) was we should try to implement it in our app.  One this we may want to do is send an email to a contact from our app without having to enter the email address.  We can do this by calling the default mail client and populating the address, subject line and even body of the message.

## Install Plugin

Since we want to call the OS specific capability of opening the email client we can use a plugin to do this.  We will be using the [Cordova Email Plugin](https://www.npmjs.com/package/cordova-plugin-email-composer) to provide this functionality.  So the first this we should do is install it with npm.

#### Install plugin

ionic cordova plugin add cordova-plugin-email-composer

Or source since we are using Ionic we can also use the Ionic Native wrapper to get all the features exposed through promises and observables without having to handle callbacks ourselves.

Since we installed a new plugin we will have to reinstall the Salesforce Mobile SDK plugin as well.  We do this by removing it and then re-adding it.

#### Remove Salesforce Mobile SDK plugin

cordova plugin remove com.salesforce

#### Add Salesforce Mobile SDK plugin

cordova plugin add https://github.com/forcedotcom/SalesforceMobileSDK-CordovaPlugin --force

> Anytime you are adding or removing plugins you will need to re-install the Salesforce Mobile SDK plugin as the last step to ensure it continues to function properly

#### Install Ionic Native Wrapper

npm install --save @ionic-native/email-composer

With the plugin and the wrapper installed we can add an email button to out action list in the `contact-details.ts` class.

## Update App Module

Before we can start using the Ionic Native wrapper for the plugin we will have to tell the app that we want to.  In the `src/app/app.module.ts` we will need to import it and then add it to our list of `providers`

#### Updated Imports

import { BrowserModule } from '@angular/platform-browser';
import { ErrorHandler, NgModule } from '@angular/core';
import { IonicApp, IonicErrorHandler, IonicModule } from 'ionic-angular';
import { EmailComposer } from '@ionic-native/email-composer';

I added it at line `4` after the imports from `ionic-angular`.

#### Updated Providers

providers: \[
  StatusBar,
  SplashScreen,
  {provide: ErrorHandler, useClass: IonicErrorHandler},
  EmailComposer,
  ContactsServiceProvider
\]

Towards the end of the `@NgModule` declaration I the `providers` are listed.  I added the `EmailComposer` after the Ionic specific handlers here as well on what will be line `43`

## Conclusion

Now we are ready to make use of the email composer in our app next time.

Don’t forget to sign up for [**The Weekly Stand-Up!**](https://wipdeveloper.wpcomstaging.com/newsletter/) to receive free the [WIP Developer.com](https://wipdeveloper.wpcomstaging.com/) weekly newsletter every Sunday!

Looking for the code and want to follow along?  Find it on [GitHub.com/BrettMN/salesforce-sdk-mobile-with-ionic-starter](https://github.com/BrettMN/salesforce-sdk-mobile-with-ionic-starter)
