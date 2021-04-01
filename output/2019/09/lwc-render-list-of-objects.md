---
layout: "post.11ty.js"
title: "LWC - Render List of Objects"
date: "2019-09-30"
tags: 
  - "Blog"
  - "LWC"
  - "Salesforce"
  - "SalesforceDeveloper"
slug: "lwc-render-list-of-objects"
coverImage: "LWC-Render-List-of-Objects.png"
---

* * *

Hello, I'm Brett with WIPDeveloper.com, we're going to cover how to render a list of objects that we get back from Salesforce.

To get those objects, we are going to use an apex class. I've called it object list controller, because I'm super creative. Currently, it is returning a list of accounts up to 50. But other than that, it's just the name and the ID of the account. If you'd like to know more about getting data from Salesforce using apex, please see the previous video about getting data from Salesforce with Apex.

The JavaScript makes the call to get the data from the apex and assigns it to an accounts variable, then we're able to use our accounts in the template. So where it says to do list here, we're going to add an unordered list and list item for each. And just like with a variable we assign, we use the for each and then bind to the account. And then the fourth item is the name of the item we want to call it. So we're going to call it an account. And we need to find a key to it.

Since this is an object, and we got it back from Salesforce, we know it has an ID attached to it. Because in our apex, the only two values we are getting for each account is the name and the ID. So for the key, we're going to use the ID.

Now to access each property on each account, when you can use the dot notation. So if we want to access the account name, we've type of account name in the binding syntax, we would need to space it out some so that it doesn't all run together to access the idea as well. And the reason we do that is if we don't we're trying to bond and just to the account, it's going to come back and render it as an object. Here you can see this is where we have bound the account. This is the name and the ID. And the object object is the way account gets rendered. So we'll just get rid of the account Bernie. You can see we have a list of 50 objects. I know test is very original name, try not to copy it.

## Links

https://wipdeveloper.wpcomstaging.com/lwc-getting-data-from-apex/

## That’s it for now.

Remember to sign up for **[The Weekly Stand-Up!](https://wipdeveloper.wpcomstaging.com/newsletter/)**  and you can get updated with any new information we have on WIPDeveloper.com.
