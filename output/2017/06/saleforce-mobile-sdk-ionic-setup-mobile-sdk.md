---
layout: "post.11ty.js"
title: "Saleforce Mobile SDK and Ionic – Setup the Mobile SDK"
date: "2017-06-28"
tags: 
  - "Blog"
  - "Cordova"
  - "Salesforce"
  - "SalesforceDeveloper"
slug: "saleforce-mobile-sdk-ionic-setup-mobile-sdk"
coverImage: "mobile-01-header.png"
---

Last time we looked at the tools we would be working with to make an mobile app.  Let's start getting those tools ready to use.

## Install Things

Ok so the install is pretty easy.  `npm install forcedroid -g` and your done.

#### `npm install forcedroid -g`

PS D:\\Workspace\\Blog\\salesforce\\ionic> npm install forcedroid -g
C:\\Users\\brettmn\\AppData\\Roaming\\npm\\forcedroid -> C:\\Users\\brettmn\\AppData\\Roaming\\npm\\node\_modules\\forcedroid\\forcedroid.js
C:\\Users\\brettmn\\AppData\\Roaming\\npm
\`-- forcedroid@5.1.0
  \`-- shelljs@0.7.8
    +-- glob@7.1.2
    | +-- fs.realpath@1.0.0
    | +-- inflight@1.0.6
    | | \`-- wrappy@1.0.2
    | +-- inherits@2.0.3
    | +-- minimatch@3.0.4
    | | \`-- brace-expansion@1.1.8
    | |   +-- balanced-match@1.0.0
    | |   \`-- concat-map@0.0.1
    | +-- once@1.4.0
    | \`-- path-is-absolute@1.0.1
    +-- interpret@1.0.3
    \`-- rechoir@0.6.2
      \`-- resolve@1.3.3
        \`-- path-parse@1.0.5

PS D:\\Workspace\\Blog\\salesforce\\ionic>

As I mentioned last time this depends on having Apache Cordova install so let's get that as well

#### `npm install cordova@6.4.0`

PS D:\\Workspace\\Blog\\salesforce\\ionic> npm install cordova@6.4.0 -g
npm WARN deprecated node-uuid@1.4.8: Use uuid module instead
C:\\Users\\brettmn\\AppData\\Roaming\\npm\\cordova -> C:\\Users\\brettmn\\AppData\\Roaming\\npm\\node\_modules\\cordova\\bin\\cordova
C:\\Users\\brettmn\\AppData\\Roaming\\npm
\`-- cordova@7.0.1
  +-- configstore@2.1.0
  | +-- dot-prop@3.0.0
 
//
// More stuff  
//

    +-- semver-diff@2.1.0
    \`-- string-length@1.0.1

PS D:\\Workspace\\Blog\\salesforce\\ionic>

> At the time of this writing there is  a breaking change in Cordova 7.0.0 we will need Cordova version 6.4.0 that's what the `@6.4.0` is for.

Since we are building android we will need to install the [Android Studio](https://developer.android.com/studio/index.html).  Head over to there to get it and follow the instructions for the install.

With those installed we can create a project.

## Forcedroid Create

There are 2 ways to create a poject with `forcedroid` with the `create` command or with the `createWithTemplate` since I don't have a template in mind I will use the create command.

So lets run `forcedroid create` Iwill be provided parameters so that I can repeat the process easier if I make a mistake.

#### `forcedroid create --apptype=hybrid_local --appname=contacts --packagename=com.wipdeveloper.contacts --organization="WIP Developer.com" --outputdir=contacts`

PS D:\\Workspace\\Blog\\salesforce\\ionic> forcedroid create --apptype=hybrid\_local --appname=contacts --packagename=com.wipdeveloper.contacts --organization="WIP Developer.com" --outputdir=contacts

\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*
\*
\*   Creating android hybrid\_local application using Salesforce Mobile SDK
\*     with app name:        contacts
\*          package name:    com.wipdeveloper.contacts
\*          organization:    WIP Developer.com
\*
\*     in:                   contacts
\*
\*     from template repo:   https://github.com/forcedotcom/SalesforceMobileSDK-Templates#v5.1.0
\*          template path:   HybridLocalTemplate
\*          plugin repo:     https://github.com/forcedotcom/SalesforceMobileSDK-CordovaPlugin#v5.1.0
\*
\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*

Creating a new cordova project.
D:\\Workspace\\Blog\\salesforce\\ionic\\contacts D:\\Workspace\\Blog\\salesforce\\ionic
com.wipdeveloper.contacts@1.0.0 D:\\Workspace\\Blog\\salesforce\\ionic\\contacts
\`-- shelljs@0.7.0
  +-- glob@7.1.2
  | +-- fs.realpath@1.0.0
  | +-- inflight@1.0.6
  | | \`-- wrappy@1.0.2
  | +-- inherits@2.0.3
  | +-- minimatch@3.0.4
 
 // 
 // More stuff 
 //

\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*
\*
\*   Next steps:
\*
\*   Your application project is ready in contacts.
\*   To use your new application in Android Studio, do the following:
\*      - open contacts\\platforms\\android in Android Studio
\*      - build and run
\*   Before you ship, make sure to plug your OAuth Client ID and Callback URI, and OAuth Scopes into contacts\\www\\bootconfig.json
\*
\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*

PS D:\\Workspace\\Blog\\salesforce\\ionic>

Let's look at what those parameters meant.

- `--apptype=hybrid_local`  - This is the type of app we are creating. Availible choices are: native, react\_native, hybrid\_local, and  hybrid\_remote
- `--appname=contacts` - The name of the app.
- `--packagename=com.wipdeveloper.contacts` - The package name. This is a unique name that will be used to identify if in an app store.
- `--organization="WIP Developer.com"` - The name of the company or organization that is creating the app.
- `--outputdir=contacts` - The directory to create the app in.  It can be left blank to create in in the directory you are running the command from.

We have just set up our project after installing the Mobile SDK.  There are a few more steps before we can run this small sample app against our org so let's take a look at that next time.

## Conclusion

Not too difficult yet but if you have hit a snag let me know by leaving a comment below, emailing [brett@wipdeveloper.com](mailto:brett@wipdeveloper.com) or following and yelling at me on [Twitter/BrettMN](https://twitter.com/BrettMN).
