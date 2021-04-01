---
layout: "post.11ty.js"
title: "LWC Local Development Beta"
date: "2020-01-21"
tags: 
  - "Blog"
  - "LWC"
  - "Salesforce"
  - "SalesforceDeveloper"
  - "SalesforceDX"
slug: "lwc-local-development-beta"
coverImage: "LWC-Local-Development-Beta.png"
---

https://videopress.com/v/HDAoNZeE?preloadContent=metadata

* * *

Hello, I'm Brett with WIPDeveloper.com. In early October, Salesforce released their Lightning Web Components Local Development beta. Let's take a look at setting that up real quick.

First thing we should do is make sure that our SFDX CLI is updated. Looks like I am so now we're going to add the plugin right now the local dev servers and plugin not included with the actual SF dx install so we have to install the plugin. So the command is `sfdx plugins:install @salesforce/lwc-dev-server`.

Now that we have the plugin installed. We can run the local server, `sfdx force:lightning:lwc:start` will start the server. Once it's ready, it'll give us an IP. Once it's ready, it gives us the URL to localhost with a port. We can go there.

With this loaded we can see all the components we have in our current Org. Why don't we load up? Well see which one to do First Component Wire Service.

So with First Component Wire Service, it doesn't work with the way it was originally designed, and that is because there is no user Id. And we have to hard code in a user Id value because there isn't. The local environment doesn't know what an Id to use. So this is the this is my Id in the local environment, I'm maybe doing something that might be bad in the long run. Right now. It was assign the user Id. Unless it's know if it is now it'll assign the string to user Id that gets used for the wire get record. Now if we go back here, we see that it loaded properly. We can go back and take a look at our Apex one. This one should work since We get the user ID in this Apex.

So what is happening is, JavaScript is using a proxy server making calls to Salesforce. So this talks to the app that's running in our console in the app, and our console is talking to Salesforce to get the data. So we can develop locally, and we get faster response time. Let's see. Go to our first component.

Well, that wasn't expected. Let's go back. Let's go to our object list. Now we have a list of we have a list of these, we can make a change.

Here we go. I updated the object list HTML and saved it and the browser automatically refreshed it. So it makes it a much faster modify and validate cycle. So should speed up some UI development using Lightning Web Components.

One thing to note is if you are adding this to an existing project, when you run it the first time it has local dev server as a folder and that contains a whole bunch of stuff. If you look, there's 55 new items that have been added to my get changes. And these were not there before. So to get to reserve, because I don't want to track those. I'm going to go to my `.gitignore`

`.localdevserver` to my `.gitignore` and now we're down to these six changes including the gitignore change.

## Links

[Develop Lightning Web Components Locally (Beta)](https://developer.salesforce.com/docs/component-library/documentation/lwc/lwc.get_started_local_dev) docs

## That’s it for now.

Remember to sign up for **[The Weekly Stand-Up!](https://wipdeveloper.wpcomstaging.com/newsletter/)**  and you can get updated with any new information we have on WIPDeveloper.com.
