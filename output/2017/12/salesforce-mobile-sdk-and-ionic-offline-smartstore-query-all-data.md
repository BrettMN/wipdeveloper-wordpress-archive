---
layout: "post.11ty.js"
title: "Salesforce Mobile SDK and Ionic – Offline – SmartStore Query All Data"
date: "2017-12-18"
tags: 
  - "Blog"
  - "Cordova"
  - "IonicFramework"
  - "Salesforce"
  - "SalesforceDeveloper"
slug: "salesforce-mobile-sdk-and-ionic-offline-smartstore-query-all-data"
coverImage: "Screen-Shot-2017-12-21-at-12.09.51-AM.png"
---

Since we now have a [SmartStore Soup](https://wipdeveloper.wpcomstaging.com/2017/12/11/salesforce-mobile-sdk-and-ionic-offline-smartstore-setup/) that has some of our [Salesforce data in it](https://wipdeveloper.wpcomstaging.com/2017/12/13/salesforce-mobile-sdk-and-ionic-offline-smartstore-saving-data/) we probably want a way to get that data out. Lets starts by by querying everything!

## Query Spec

To query against our soup we will need to create a `querySpec`, at this point you may be wondering what a `querySpec` is, well... Think of a `querySpec` as an object that describes the type of query you want to make.  It will contain such things as the `path` or `indexPath`, `beginKey` and `endKey`, `matchKey`, `orderPath`, `order`, and `pageSize`.

If it sounds like a lot to keep track of, don't worry too much, there's helper functions to create `querySpec`s for the different types of queries.

For now we will try setting up the a query with a `AllQuery` spec.

To do this we will need to tell TypeScript that our `navigator` has an additional property called `smartstore` so lets create an interface that extends `Navigator` with a property of `smartstore` that is type `any`.   Let's add this near the top of the file.

#### `sdkNavigator` Interface

interface sdkNavigator extends Navigator {
  smartstore: any
}

Now lets create a new method called `getAllFromSoup`.  This method will build a `querySpec` by calling the `buildAllQuerySpec` that is a part of the `smartstore` that is added to the navigator.  To get TypeScript to "see" the navigator as the `sdkNavigator` interface we just defined we will need to do a little [type assertion](https://www.typescriptlang.org/docs/handbook/basic-types.html#type-assertions).

Let's take a loot at the type assertion now:

#### Type Assertion

(navigator as sdkNavigator)

What you see here is we have wrapped the `navigator` in parentheses and used the `as` keyword with our interface name to tell TypeScript "trust me I'm a developer and know better".  This will cause TypeScript to use the type you tell it to for all interactions.  Since our `sdkNavigator` extends `Navigator` we can use all the default `Navigator` functions if we wanted.

So we create our `querySpec` with the `indexPath`, the `order` of the results, `pageSize` to return, and the `selectPaths`.

We will need callback functions for `success` and `failure` and for right now I will log the results of both to the developer console.

Finally we call `querySoup` off the `smartstore` with the `this.soupName`, our `querySpec` and our `success` and `failure` callbacks.

#### `getAllFromSoup` Method

getAllFromSoup() {

  var querySpec = (navigator as sdkNavigator).smartstore.buildAllQuerySpec('Name', 'decending', 2, \['Name'\])

  const success = (results) => console.log({ results })

  const failure = (error) => console.log(error)

    ; (navigator as sdkNavigator).smartstore.querySoup(this.soupName, querySpec, success, failure)

}

> The semicolon at the begging of the last line is because we are using a type assertion at the beginning of the line and I haven't been using semicolons at the end of lines.

## Conclusion

Don’t forget to sign up for [**The Weekly Stand-Up!**](https://wipdeveloper.wpcomstaging.com/newsletter/) to receive free the [WIP Developer.com](https://wipdeveloper.wpcomstaging.com/) weekly newsletter every Sunday!
