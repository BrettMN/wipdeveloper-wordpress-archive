---
layout: "post.11ty.js"
title: "Salesforce Mobile SDK and Ionic – Offline – SmartStore Setup"
date: "2017-12-12"
tags: 
  - "Blog"
  - "Cordova"
  - "IonicFramework"
  - "Salesforce"
  - "SalesforceDeveloper"
slug: "salesforce-mobile-sdk-and-ionic-offline-smartstore-setup"
coverImage: "Screen-Shot-2017-12-14-at-12.42.05-AM.png"
---

Since we are going to be saving some data offline we should start by creating a SmartStore for our data.

## SmartStore Setup

Before we setup SmartStore we should know a couple things.  Each SmartStore database or cache is called a Store.  Stores contain partitions of our data called Soups.  We can create Soups without specifying a Store and these Soups will be kept in the default Store.  It is possible to make Global Stores that persist data even if the Salesforce login expires.

For right now we will be focusing on creating a Soup in the Default Store so we can save some Salesforce records for offline use.

Let's start by creating a new Service Provider with the Ionic CLI generator feature, I will be calling mine `smartstoreService.`

#### Generate Provider

ionic generate provider smartstoreService

Before we get too far we are going to need to let TypeScript know about Cordova... or the Cordova Window object.  To do that let's `declare` Cordova near the top of our service.

#### `declare` Cordova

declare var cordova: any;

Now we will want a name for our Soup we can re-use without re-typing it repeatedly so let's create a `private` property named `soupName` with a value of `contacts`.

#### `soupName`

private soupName = 'contacts'

We will also need a consistent way to access the Cordova plugin for the SmartStore so let's create a private method that returns the results of our `cordova.require`

#### `smartStore` Method

private smartStore(): any {
  return cordova.require("com.salesforce.plugin.smartstore")
}

In the constructor lets register the Soup so that it is ready for action.

To register a Soup we will need to have an Index Spec that will describe what we want to use for indexing our data.  For our little setup I will be using the `Id` and `Name` for the index.  So we will need an array of objects that contain the `path`, or name of the index, and the `type`, as in `string`, `integer`, `floating`, `full_text`, or `json1`.  Both `Id` and `Name` are strings soo... our `indexSpec` should look something like this.

#### `indexSpec`

const indexSpecs = \[
  {
    path: 'Name',
    type: 'string'
  },
  {
    path: 'Id',
    type: 'string'
  }\]

We also pass in success and failure callbacks so let's define those as well.  For now these will be logging to console that we succeeded or failed.

`success` Callback

let success = (soupName) => console.log(\`Soup ${soupName} was successfully created!\`)

`failure` Callback

let failure = (error) => console.error(\`Registering soup fails with error: ${error}\`)

Then to pull it all together we will use the `smartStore` private method and invoke `registerSoup` with our `soupName`, `indexSpec`, `success` and `failure` callbacks.

#### Register Soup

this.smartStore().registerSoup(this.soupName, indexSpecs, success, failure)

Now we have something we can start to work with.

## Conclusion

Don’t forget to sign up for [**The Weekly Stand-Up!**](https://wipdeveloper.wpcomstaging.com/newsletter/) to receive free the [WIP Developer.com](https://wipdeveloper.wpcomstaging.com/) weekly newsletter every Sunday!
