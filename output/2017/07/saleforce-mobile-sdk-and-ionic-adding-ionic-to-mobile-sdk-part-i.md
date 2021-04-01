---
layout: "post.11ty.js"
title: "Saleforce Mobile SDK and Ionic – Adding Ionic to Mobile SDK - Part I"
date: "2017-07-04"
tags: 
  - "Blog"
  - "Cordova"
  - "IonicFramework"
  - "Salesforce"
  - "SalesforceDeveloper"
slug: "saleforce-mobile-sdk-and-ionic-adding-ionic-to-mobile-sdk-part-i"
coverImage: "mobile-05-header.png"
---

We've already set up an app to that can [talk to our Salesforce Org](https://wipdeveloper.wpcomstaging.com/2017/06/29/saleforce-mobile-sdk-ionic-first-run/) and we have set up an app that [has the Ionic Framework](https://wipdeveloper.wpcomstaging.com/2017/07/03/saleforce-mobile-sdk-ionic-setup-ionic-framework/).  Now we need to setup up an app with Ionic.  To do that we will create an app with the Salesforce Mobile SDK and add Ionic to it through the use of our computers handy dandy copy and paste feature.  So get your `Ctrl+c` and `Ctrl+v` or `command+c` and `command+v` ready as we they are about to get a work out.

## To start

First thing we will need is the base app generated with `forcedroid`.  We have a working example of this in [Saleforce Mobile SDK and Ionic – Setup the Mobile SDK](https://wipdeveloper.wpcomstaging.com/2017/06/27/saleforce-mobile-sdk-ionic-setup-mobile-sdk/) and completed in [Saleforce Mobile SDK and Ionic – First Run](https://wipdeveloper.wpcomstaging.com/2017/06/29/saleforce-mobile-sdk-ionic-first-run/) so you can either use that app or create a new one following the same steps.

> I will be creating a new one and calling it `ionicContacts` and referencing it from this point forward.

One of the first things I will be doing is adding the `.gitignore` from the Ionic app we created in [Saleforce Mobile SDK and Ionic – Setup the Ionic Framework](https://wipdeveloper.wpcomstaging.com/2017/07/03/saleforce-mobile-sdk-ionic-setup-ionic-framework/) and then I'm going to initialize a git repository.  I am going to do this now so I can see what all the differences you may choose to wait but I don't recommend working in the long run that way.

Now lets start moving the working stuff.

## Update `package.json`

Let's start by updating the `package.json`.  We will do this by opening the `package.json` from our [pure Ionic app](https://wipdeveloper.wpcomstaging.com/2017/07/03/saleforce-mobile-sdk-ionic-setup-ionic-framework/) and copying some things over to the `package.json` in our `ionicContacts` app.

Let's look at what we are staring with

#### Pure Ionic `package.json`

{
  "name": "pureIonic",
  "version": "0.0.1",
  "author": "Ionic Framework",
  "homepage": "http://ionicframework.com/",
  "private": true,
  "scripts": {
    "clean": "ionic-app-scripts clean",
    "build": "ionic-app-scripts build",
    "lint": "ionic-app-scripts lint",
    "ionic:build": "ionic-app-scripts build",
    "ionic:serve": "ionic-app-scripts serve"
  },
  "dependencies": {
    "@angular/common": "4.1.3",
    "@angular/compiler": "4.1.3",
    "@angular/compiler-cli": "4.1.3",
    "@angular/core": "4.1.3",
    "@angular/forms": "4.1.3",
    "@angular/http": "4.1.3",
    "@angular/platform-browser": "4.1.3",
    "@angular/platform-browser-dynamic": "4.1.3",
    "@ionic-native/core": "3.12.1",
    "@ionic-native/splash-screen": "3.12.1",
    "@ionic-native/status-bar": "3.12.1",
    "@ionic/storage": "2.0.1",
    "ionic-angular": "3.5.0",
    "ionicons": "3.0.0",
    "rxjs": "5.4.0",
    "sw-toolbox": "3.6.0",
    "zone.js": "0.8.12"
  },
  "devDependencies": {
    "@ionic/app-scripts": "1.3.12",
    "@ionic/cli-plugin-ionic-angular": "1.3.1",
    "typescript": "2.3.4"
  },
  "description": "An Ionic project"
}

#### Salesforce Mobile SDK `package.json`

{
    "name": "com.wipdeveloper.ioniccontacts",
    "displayName": "contacts",
    "version": "1.0.0",
    "description": "A sample Apache Cordova application that responds to the deviceready event.",
    "main": "index.js",
    "scripts": {
        "test": "echo \\"Error: no test specified\\" && exit 1"
    },
    "author": "Apache Cordova Team",
    "license": "Apache-2.0",
    "dependencies": {
        "shelljs": "^0.7.0"
    }
}

Looking at them line 13 of the `forcedroid` `package.json` is really the only thing we need to worry about keeping.

#### Line 13

"shelljs": "^0.7.0"

Everything else is generic information or things we entered when we created the app.  Feel free to copy things over to your `ionicContacts` app's `package.json` in whatever manner suits you best.

#### Final `package.json`

{
    "name": "com.wipdeveloper.ioniccontacts",
    "displayName": "Ionic Contacts",
    "version": "1.0.0",
    "description": "A sample Salesforce Mobile SDK app that integrates with the Ionic Framework.",
    "homepage": "https://wipdeveloper.wpcomstaging.com/",
    "private": true,
    "scripts": {
        "clean": "ionic-app-scripts clean",
        "build": "ionic-app-scripts build",
        "lint": "ionic-app-scripts lint",
        "ionic:build": "ionic-app-scripts build",
        "ionic:serve": "ionic-app-scripts serve",
        "test": "echo \\"Error: no test specified\\" && exit 1"
    },
    "author": "Brett Nelson <brett@wipdeveloper.com> (http://wipdeveloper.wpcomstaging.com/)",
    "license": "Apache-2.0",
    "dependencies": {
        "@angular/common": "4.1.3",
        "@angular/compiler": "4.1.3",
        "@angular/compiler-cli": "4.1.3",
        "@angular/core": "4.1.3",
        "@angular/forms": "4.1.3",
        "@angular/http": "4.1.3",
        "@angular/platform-browser": "4.1.3",
        "@angular/platform-browser-dynamic": "4.1.3",
        "@ionic-native/core": "3.12.1",
        "@ionic-native/splash-screen": "3.12.1",
        "@ionic-native/status-bar": "3.12.1",
        "@ionic/storage": "2.0.1",
        "ionic-angular": "3.5.0",
        "ionicons": "3.0.0",
        "rxjs": "5.4.0",
        "sw-toolbox": "3.6.0",
        "zone.js": "0.8.12",
        "shelljs": "^0.7.0"
    },
    "devDependencies": {
        "@ionic/app-scripts": "1.3.12",
        "@ionic/cli-plugin-ionic-angular": "1.3.1",
        "typescript": "2.3.4"
    }
}

 

> I took this as a chance to update a few other values in the `package.json` but you can keep the default values if you like.   Noticeably the `displayName`, `description`, `homepage`, and `author`.

## Conclusion

With our `package.json` updated we can start moving to copying files and folders from the pure Ionic app to our `forcedroid` generated app.

Don't forget to sign up for [**The Weekly Stand-Up!**](https://wipdeveloper.wpcomstaging.com/newsletter/) to receive free the [WIP Developer.com](https://wipdeveloper.wpcomstaging.com/) weekly newsletter every Sunday!
