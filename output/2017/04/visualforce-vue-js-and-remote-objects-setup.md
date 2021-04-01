---
layout: "post.11ty.js"
title: "Visualforce, Vue.js and Remote Objects - SetUp"
date: "2017-04-13"
tags: 
  - "Blog"
  - "Salesforce"
  - "SalesforceDeveloper"
  - "VueJS"
slug: "visualforce-vue-js-and-remote-objects-setup"
---

We have seen how to use @RemoteActions to communicate with Salesforce.com but what if you would like to do a little prototyping with out much time invested in Apex development. Or maybe you don't have much/any experience with Apex but would like to start working on the front end. Well, Remote Objects may be for you! Let's take our controller out and re implement our `sf.service.js` to use Remote Objects to do all our [C.R.U.D.](https://en.wikipedia.org/wiki/Create,_read,_update_and_delete) things.

> We probably should have covered this first as it may not meet the needs of your project since it has not transnational support but hey, it's an option. :)

## No Controller

Let's begin by removing the referance to the controller on our `TryVuejs.page`. Just delete the `controller="TryVuejsController"` attribute, pretty easy so far.

> We can leave the Controller in our org as we may want to use it later.

The `apex:page` tag should now look like this:

#### Updated `apex:page` Tag

<apex:page 
  doctype="html-5.0" 
  standardStylesheets="false" 
  showChat="false" 
  applyBodyTag="false" 
  showHeader="false" 
  sidebar="false">

That's it, controller work done.

## Add `apex:RemoteObjects`

On your Visualforce page add the following:

#### Add Remote Objects

<apex:remoteObjects jsNamespace="WIPDeveloperModels">
  <apex:remoteObjectModel 
    name="Contact" 
    fields="Id, Name, MobilePhone, Email, Title, Department, LeadSource, Level\_\_c, Languages\_\_c" />
</apex:remoteObjects>

Here we are adding our Remote Objects. The outer tag, `apex:remoteObjects`, defines a base model and gives it a `jsNamespace` of `WIPDeveloperModels`, if we didn't provide the `jsNamespace` it would default to `RemoteObjectModel` and that would probably be ok but I like `WIPDeveloperModels` more. Since you can provide a `jsNamespace` you could have multiple models on your page.

The `apex:remoteObjectModel` tag has the name of the object you want to use and the the fields from that object your want mapped

With that done we can move on to updating our `sf.service.js` next time.

## To Be Continued...

After we get Remote Objects working what do you think we should try next? Let me know by leaving a comment below or emailing [brett@wipdeveloper.com](mailto:brett@wipdeveloper.com).
