---
layout: "post.11ty.js"
title: "LWC - getListUi Beta"
date: "2019-09-25"
tags: 
  - "Blog"
  - "LWC"
  - "Salesforce"
  - "SalesforceDeveloper"
slug: "lwc-getlistui-beta"
coverImage: "LWC-getListUi-Beta.png"
---

* * *

Hello, I'm Brett with WIPDeveloper.com. While trying to come up with a way to get a bunch of objects to a lightning web component from Salesforce, I stumbled across this getListUi adapter for the wire adapter.

It's currently in beta. But it looks promising if it becomes ga at some point. So we're going to take a look at it real quick. Let's start with what looks like our list or value list from last time. And I'm going to get rid of everything from the class in the HTML get rid of the buttons. I'm also going to, instead of iterating overvalues, I'm going to iterate over accounts, and each one is going to be called an account. And we're going to track the account ID. So for the template, what I'm changing is, instead of values, it's account, instead of a value isn't a set of values, it's counts instead of value, it's account, instead of the key being that value, it's going to be account that ID. And then I'm going to display the ID from the account. And I want to display something else, but we don't know what that is yet. In the JavaScript down here, you can see I've already imported the wire and the track. So have those available. And I won't be making the mistake of forgetting those again. And I want to track and accounts declaration. And I also we'll be using wire. Well, before we get there, we need to import a couple things. We're going to import the list UY. And that's from lightning ui lyst API, then we need to import the count object from the Salesforce schema.

With those important now we can finish up the wire service that I was starting early. And the method it will call is the get lyst UI. And then we pass in our options. So for our first option we got, we're going to pass on the object API name. And that's going to be our account object that we imported early. And we want we need a list. We're going to need a List API name. So I have a list you created in my Salesforce instance called that API name is all accounts. So we will use that one. And I want to handle this with a method. So and for right now, where we know it's going to return an error or the data. And I just want to log both of those right now. If we did have an error, we would want to do something with it. We're not going to handle it. Besides ignoring it looks like we did not get it to push. Let's save it again.

Forgot the "N" for missed it, your pic. Once that saved, refresh the page, nothing should happen. If we look in the deaf council will see me we have well that's a proxy object. That's not very fun. Let's

Let's an a log function. going to use the rest programs to collect the stuff. And then I'm going to console log in here. Except I'm going to use the JSON API to parse a string of five version of this stuff. Now, I can call this this dot log with the air and the data and it will just be stratified and sent to the council. And I don't have to do that every time I want to lock something. This is the one you can see the second object which would win the data object has an impact. And our records, and we're going to look in the records for the records. So we have at least 50 Records here. And now we can use that. So if there's data, we want to set the accounts. Our object from the data records records can refresh that. You can see we have quite a bit of objects here. But we would like to show the name of the account. So let's go into look at the records and see what it looks like. It has a fields property and the fields property has a name. So we would have to do fields, start name dot value to get the actual value. Here on our template, we'll just do field start named a value, refresh the page once that saves. I don't really have names, but we only have 50 accounts showing what if we wanted to show more than that. Look into the documentation for this, get lyst you I call you can see that it uses the rest parameters table. So we can pass in parameters from this REST request. So we can new page size in here, I'm going to increase it to 2000. And then I want to order by and that was sort by, and I'm going to start by the name. Now when we refresh the page, we shouldn't have quite a few more. Not quite 2000 because I've only created 400 test records, but they're there.

So that's a quick look at using the `getListUi` wire adapter. It's currently in beta. Hopefully, it becomes something we can use in the future. Otherwise we would have to write a custom Apex class to gather the accounts.

## Links

[https://developer.salesforce.com/docs/component-library/documentation/lwc/lwc.reference\_get\_list\_ui](https://developer.salesforce.com/docs/component-library/documentation/lwc/lwc.reference_get_list_ui)

[https://developer.salesforce.com/docs/atlas.en-us.uiapi.meta/uiapi/ui\_api\_resources\_list\_views\_records\_md.htm#request\_parameters](https://developer.salesforce.com/docs/atlas.en-us.uiapi.meta/uiapi/ui_api_resources_list_views_records_md.htm#request_parameters)

## That’s it for now.

Remember to sign up for **[The Weekly Stand-Up!](https://wipdeveloper.wpcomstaging.com/newsletter/)**  and you can get updated with any new information we have on WIPDeveloper.com.
