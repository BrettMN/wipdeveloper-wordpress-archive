---
layout: "post.11ty.js"
title: "Salesforce Mobile SDK and Ionic – Offline – SmartStore Query All Data II"
date: "2017-12-21"
tags: 
  - "Blog"
  - "Cordova"
  - "IonicFramework"
  - "Salesforce"
  - "SalesforceDeveloper"
slug: "salesforce-mobile-sdk-and-ionic-offline-smartstore-query-all-data-ii"
coverImage: "Screen-Shot-2017-12-22-at-12.12.32-AM.png"
---

Now that we can run a query that returns all the data let's look at the options is has available.

## More QuerySpec

We built our `querySpec` with the following line of code:

var querySpec = (navigator as sdkNavigator).smartstore.buildAllQuerySpec('Name', 'decending', 2, \['Name'\])

And it returns the following object:

#### Results

![Results](images/Screen-Shot-2017-12-21-at-11.22.44-PM.png)

A few of the parameters are some what self explanatory so let's list what they are for an AllQuery real quick in order and a quick description.

#### `indexPath`

What you are looking for.  In the above Query it was `Name`.  This will be the field used for the sort.  This is Case Sensitive.

#### `order`

This one the name says it all.  It can be either “ascending” or “descending.”  By default it's ascending.

#### `pageSize`

How many results to return.  This one defaults to 10.

#### `selectPaths`

The Docs say "Narrows the query scope to only a list of fields that you specify" and well... that wasn't too clear to me what it meant.   I think of it as the fields to return.  If you don't provide an array of fields to return the default is to return all fields. This is Case Sensitive.

You don't have to use any of the parameters expect `indexPath`, the rest are optional.  The catch is the parameters must be passed in in order.  So if you want to use `pageSize` you must provide an `order`.  And if you want to use `selectPaths` you must also provide an `order` and `pageSize`.

If we create a `querySpec` with only an `indexPath` of "Name" and no other parameters the results contain some extra information.

#### More Results

![More Results](images/Screen-Shot-2017-12-22-at-12.02.05-AM.png)

You see each entry returns all the fields and an `attributes` property that contains the `type` and `url` along with some meta information that is used in the SmartStore Soup.

Limiting the returned fields to what is relevant should decrease memory usage a little.

Say we only wanted the "Name" and "Id" fields.  Our `querySpec` would look like this:

var querySpec = (navigator as sdkNavigator).smartstore.buildAllQuerySpec('Name', 'ascending', 2, \['Name'\])

and the results would look like this:

#### More Results

![More Results](images/Screen-Shot-2017-12-22-at-12.11.00-AM-300x252.png)

Nice and clean and just the data we need at this time.

## Conclusion

Don’t forget to sign up for [**The Weekly Stand-Up!**](https://wipdeveloper.wpcomstaging.com/newsletter/) to receive free the [WIP Developer.com](https://wipdeveloper.wpcomstaging.com/) weekly newsletter every Sunday!
