---
layout: "post.11ty.js"
title: "LWC - Passing Data to a Child Component"
date: "2019-08-28"
tags: 
  - "Blog"
  - "LWC"
  - "Salesforce"
  - "SalesforceDeveloper"
  - "SalesforceDX"
slug: "lwc-passing-data-to-a-child-component"
coverImage: "Screen-Shot-2019-08-28-at-3.32.34-PM.png"
---

* * *

Hello, I'm Brett with WIPDeveloper.com. Last time, we added a child component to a custom lightning web component. This time, let's try passing some information to the child component.

This is going to look very similar to using the lightning web components that are provided by Salesforce because the syntax is virtually the same from the parents point of view, the child on the other hand, we have to prepare a little bit.

So I have the child component down here in the lower portion of the screen. And what we're going to do is go to the JavaScript, and we're going to create a property current `ourProperty`. Now we get so we can bind data to it from the parent, we have to use the API decorator. And for the API decorator, we have to import them from the LWC. So we're importing it online five and using it to decorate `ourProperty`. Now we save that there shouldn't be any mission be any differences on our church, because page because we didn't use any change in any market.

So let's add that to our markup, refresh it, there should be just a dash, because we're not actually setting our property.

Now, let's add in our parent component on the upper right hand corner or side of the screen, we're going to duplicate the child component and we're going to add `our-property`, we will assign a value to it.

Save that, and we should get two components over here, one that says child dash out from parent and when it says child dash now.

Since it is decorated with the API decorator, and we aren't trying to expose it through one of the targets. Because even if we were trying to expose it through the targets, I don't know which one would work in this case. So to set a default value we will use will assign a proper assignment value in the JavaScript file. This might cause if you're using lightning debug mode, might see some warnings about setting the property. But this is the way instead of default value that I know of right now.

Now set the default is from child and we can refresh the page. And we should have two components child from parent child from child and that is how we pass data from our parent component to our child component and how to set the property as a default value.

## That’s it for now.

Remember to sign up for **[The Weekly Stand-Up!](https://wipdeveloper.wpcomstaging.com/newsletter/)**  and you can get updated with any new information we have on WIPDeveloper.com.
