---
layout: "post.11ty.js"
title: "Salesforce Mobile SDK and Ionic - Setup Remote Hybrid App"
date: "2017-10-17"
tags: 
  - "Blog"
  - "Cordova"
  - "IonicFramework"
  - "Salesforce"
  - "SalesforceDeveloper"
slug: "salesforce-mobile-sdk-ionic-setup-remote-hybrid-app"
coverImage: "Screen-Shot-2017-10-17-at-12.36.55-AM.png"
---

Since we covered the [difference between a Remote and a Local Hybrid app](https://wipdeveloper.wpcomstaging.com/2017/10/09/salesforce-mobile-sdk-ionic-local-vs-remote/) let set up our Remote Hybrid app.

## Create Visualforce Page

One things we will need is a Visualforce page to load inside our app.  I'm going to call my new page `ContactsApp` and we will set the `docType` to `html-5.0`, `showHeader` to `false`, and `sidebar` to `false`.  It should look something like this:

#### Empty `ContactsApp` Page

<apex:page docType="html-5.0" showHeader="false" sidebar="false">

</apex:page>

Since we are recreating our Local Hybrid app as a Remote Hybrid app the next step will be to copy everything from the `www/index.html` file except the `<!DOCTYPE html>` and paste it into our `ContactsApp.page`.

#### Filled `ContactsApp` Page

<apex:page docType="html-5.0" showHeader="false" sidebar="false">

    <html lang="en" dir="ltr">
    <head>
    <script data-ionic="inject">
        (function(w){var i=w.Ionic=w.Ionic||{};i.version='3.5.0';i.angular='4.1.3';i.staticDir='build/';})(window);
    </script>
    <meta charset="UTF-8" />
    <title>Ionic App</title>
    <meta name="viewport" content="width=device-width, initial-scale=1.0, minimum-scale=1.0, maximum-scale=1.0, user-scalable=no" />
    <meta name="format-detection" content="telephone=no" />
    <meta name="msapplication-tap-highlight" content="no" />

    <link rel="icon" type="image/x-icon" href="https://localhost/assets/icon/favicon.ico" />
    <link rel="manifest" href="https://localhost/manifest.json" />
    <meta name="theme-color" content="#4e8ef7" />
    
    <!-- cordova.js required for cordova apps -->
    <script src="https://localhost/cordova.js"></script>

    <!-- For testing purposes only  -->
    <script src="https://localhost/force.js"></script>

    <!-- un-comment this code to enable service worker
    <script>
        if ('serviceWorker' in navigator) {
        navigator.serviceWorker.register('service-worker.js')
            .then(() => console.log('service worker installed'))
            .catch(err => console.error('Error', err));
        }
    </script>-->

    <link href="https://localhost/build/main.css" rel="stylesheet" />

    </head>
    <body>

    <!-- Ionic's root component and where the app will load -->
    <ion-app></ion-app>

    <!-- The polyfills js is generated during the build process -->
    <script src="https://localhost/build/polyfills.js"></script>

    <!-- The bundle js is generated during the build process -->
    <script src="https://localhost/build/main.js"></script>

    </body>
    </html>

</apex:page>

One thing... ok a few things... that need to change is anything that is served from the root of the app wikl need it's url updated.  Since the root for the page is now in Salesforce we will add `https://localhost/` to any reference for a local resource.  So `cordova.js` becomes `https://localhost/cordova.js` and `manifest.json` becomes `https://localhost/manifest.json` and so on.

> Due to some the Visualforce requirement of closing all html tags I did have to add a few `/` to some of the `<link>` and `<meta>` elements.

With our Visualforce page ready we can create our app.

## Create Remote Hybrid App

Creating the RemoteHybrid app is going to be similar to how we [created the the Local Hybrid app](https://wipdeveloper.wpcomstaging.com/2017/06/27/saleforce-mobile-sdk-ionic-setup-mobile-sdk/).  This time though we will specify the `apptype` as `hybrid_remote`.

> I will also be using the `appname` of \`contacts\_remote\` as well as the `outputdir` of \`contacts\_remote\` just so things don't get mixed up.  I will also be using `forceios` this time but you can still use `forcedroid`.

#### Create New App

Bretts-MBP:blog brett$ forceios create
App type must be native, native\_swift, react\_native, hybrid\_local, hybrid\_remote.
Enter your application type (native, native\_swift, react\_native, hybrid\_local, hybrid\_remote): hybrid\_remote
/Library/Ruby/Gems/2.0.0/gems/cocoapods-1.3.1/lib/cocoapods/executable.rb:89: warning: Insecure world writable dir /Users/brett/Library/Android/sdk in PATH, mode 040777
Enter your application name: contacts\_remote
Enter the package name for your app (com.mycompany.myapp): com.wipdeveloper.contacts\_remote
Enter your organization name (Acme, Inc.): WIP Developer.com
Enter the start page for your app: apex/ContactsApp
/Library/Ruby/Gems/2.0.0/gems/cocoapods-1.3.1/lib/cocoapods/executable.rb:89: warning: Insecure world writable dir /Users/brett/Library/Android/sdk in PATH, mode 040777

\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*
\*
\*   Creating ios hybrid\_remote application using Salesforce Mobile SDK
\*     with app name:        contacts\_remote
\*          package name:    com.wipdeveloper.contacts\_remote
\*          organization:    WIP Developer.com
\*   
\*     in:                   salesforce-sdk-mobile-with-ionic-starter-remote
\*   
\*     from template repo:   https://github.com/forcedotcom/SalesforceMobileSDK-Templates#v5.2.0
\*          template path:   HybridRemoteTemplate
\*          start page:      apex/ContactsApp
\*          plugin repo:     https://github.com/forcedotcom/SalesforceMobileSDK-CordovaPlugin#v5.2.0
\*
\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*

Creating a new cordova project

...
...
some other things
...
...

\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*
\*
\*   Next steps:
\*   
\*   Your application project is ready in salesforce-sdk-mobile-with-ionic-starter-remote.
\*   To use your new application in XCode, do the following:
\*      - open salesforce-sdk-mobile-with-ionic-starter-remote/platforms/ios in XCode
\*      - build and run
\*   Before you ship, make sure to plug your OAuth Client ID and Callback URI, and OAuth Scopes into salesforce-sdk-mobile-with-ionic-starter-remote/www/bootconfig.json
\*
\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*

Bretts-MBP:blog brett$ 

We should now have a default Salesforce Mobile SDK app ready to get things copied and pasted into it.

## Conclusion

Don’t forget to sign up for [**The Weekly Stand-Up!**](https://wipdeveloper.wpcomstaging.com/newsletter/) to receive free the [WIP Developer.com](https://wipdeveloper.wpcomstaging.com/) weekly newsletter every Sunday!
