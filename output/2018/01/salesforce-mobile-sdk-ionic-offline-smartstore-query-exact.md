---
layout: "post.11ty.js"
title: "Salesforce Mobile SDK and Ionic – Offline – SmartStore Query by Exact"
date: "2018-01-11"
tags: 
  - "Blog"
  - "Cordova"
  - "IonicFramework"
  - "Salesforce"
  - "SalesforceDeveloper"
slug: "salesforce-mobile-sdk-ionic-offline-smartstore-query-exact"
coverImage: "Screen-Shot-2018-01-13-at-9.52.24-AM.png"
---

Sometimes when getting data from the Soup we will need to be able to get one specific record, or a group of records that match a certain criteria.  SmartStore allows us to do this using the Query by Exact feature and the `buildExactQuerySpec` function.  Using `buildExactQuerySpec` we will be able to tailor our query similar to the where clause of a SQL/SOQL statement.

## `buildExactQuerySpec`

Since we already know how to [make a `querySpec`](https://wipdeveloper.wpcomstaging.com/2017/12/20/salesforce-mobile-sdk-and-ionic-offline-smartstore-query-all-data-ii/) so let's look at how `buildExactQuerySpec` is different from `buildAllQuerySpec`.  `buildExactQuerySpec` takes `path`, `matchKey`, `pageSize`, `order`, `orderPath`, `selectPaths` and since `pageSize`, `order`, `selectPaths` are the same as `buildAllQuerySpec` let's focus on the other 3.

#### `path`

What you looking for, similar to `indexPath` with `buildAllQuerySpec`.

#### `matchKey`

The string to match against the `path`.

#### `orderPath`

Used to specify the path to order the search by.

So to query by `Id` we could specify the `'Id'` as the path and pass in an `Id` that we have in our soup.  After building the `querySpec` the rest of calling `querySoup` remains the same.

#### Query by `Id`

exactQuery(): Promise<any> {
  console.log('getContact');

  let id = '003j0000008CVYlAAO';  //id from soup

  let promise = new Promise((resolve, reject) => {

    var querySpec = (navigator as sdkNavigator).smartstore.buildExactQuerySpec('Id', id);

    let success = (results) => {
      console.log(results);
      resolve(results.currentPageOrderedEntries);
    };

    (navigator as sdkNavigator).smartstore.querySoup(this.soupName, querySpec, success, reject);

    promise.then(results => {
      console.log(results);
    });

  });
}

Here you can see we still use a success callback and a failure callback along with using the soup name.

## Conclusion

Don’t forget to sign up for [**The Weekly Stand-Up!**](https://wipdeveloper.wpcomstaging.com/newsletter/) to receive free the [WIP Developer.com](https://wipdeveloper.wpcomstaging.com/) weekly newsletter every Sunday!
