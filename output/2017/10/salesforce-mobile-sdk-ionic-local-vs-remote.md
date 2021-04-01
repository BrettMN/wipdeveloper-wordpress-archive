---
layout: "post.11ty.js"
title: "Salesforce Mobile SDK and Ionic - Local vs Remote"
date: "2017-10-10"
tags: 
  - "Blog"
  - "Cordova"
  - "IonicFramework"
  - "Salesforce"
  - "SalesforceDeveloper"
slug: "salesforce-mobile-sdk-ionic-local-vs-remote"
---

If you have been following along you know we created a mobile app that allowed us access to contacts that are  in our Salesforce Org.  That app could be deployed to an app store such as Google Play or the Apple App Store.  And since we used Cordova to build it with HTML, CSS and JavaScript it would be considered a Hybrid App all that was covered [before](https://wipdeveloper.wpcomstaging.com/2017/06/26/saleforce-mobile-sdk-ionic-intro/).

What we didn't talk about was the differences between Hybrid Local and Hybrid Remote.

## Hybrid Local

This is what we have been doing.  Creating a mobile app that deploys all it's recourses (HTML, CSS, and JavaScript) to the device in the app package.  This is great if you want to have you app installed to the device with no worry that is has it's required resources but it is not without drawbacks.

If you deploy this through an app store ever time you want to update a portion of it, no matter how significant, you have to go through the approval process.  This might take a couple days usually but could be an issue if it's a time sensitive change.

## Hybrid Remote

It is also possible to create a mobile app where not everything is packaged and distributed through an app store.  Using the Salesforce Mobile SDK it is possible to use the same technologies we have been using (HTML, CSS, and JavaScript) and have it install like a normal app but some portions of it would like on a server somewhere, in the cloud.  In our case we could create a Visualforce page, use static resources for the JavaScript and CSS and update it without going through the approval process of an app store.

A Hybrid Local app would allow us to deploy updates as soon as we deploy them to our production Org.  As an added benefit, with a Remote Hybrid app using a Visualforce page instead of `html` that is shipped with the app it would be possible to use remote actions inside the app.

## Conclusion

With a better understanding of the differences between a Hybrid Local and Hybrid Remote app let's take a look at creating a Hybrid Remote app.  In the process of doing so we will try to reuse as much of our existing Hybrid Local app in the process.

Don’t forget to sign up for [**The Weekly Stand-Up!**](https://wipdeveloper.wpcomstaging.com/newsletter/) to receive free the [WIP Developer.com](https://wipdeveloper.wpcomstaging.com/) weekly newsletter every Sunday!

Looking for the code and want to follow along?  Find it on [GitHub.com/BrettMN/salesforce-sdk-mobile-with-ionic-starter](https://github.com/BrettMN/salesforce-sdk-mobile-with-ionic-starter)
