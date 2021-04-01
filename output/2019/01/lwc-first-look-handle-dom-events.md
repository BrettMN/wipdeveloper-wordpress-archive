---
layout: "post.11ty.js"
title: "LWC - First Look - Handle DOM Events"
date: "2019-01-28"
tags: 
  - "Blog"
  - "LWC"
  - "Salesforce"
  - "SalesforceDeveloper"
  - "SalesforceDX"
slug: "lwc-first-look-handle-dom-events"
coverImage: "Screen-Shot-2019-02-01-at-12.00.41-AM-3.png"
---

* * *

Hello, I'm Brett with WIPDevelopers.com. Now that we've used properties to expose data from our JavaScript to our HTML template, why don't we look at how to handle DOM events and react to it in the JavaScript file. Here we have our HTML template.

## DOM Events

What I want to do is handle when somebody clicks.

It would help if I spelled it correctly. When somebody clicks on this `h1` one I wanted to

I wanted to call a method called `handleClick` on my class

and the JavaScript on the `h1` I've assigned to an `onclick` attribute without quotes the name of the method I want to call on my JavaScript file, and that is surrounded by the curly braces.

So we'll go into our JavaScript file and add that as a method.

Since this is a JavaScript class, we do not have to type function.

First thing I'm going to do is saying that it was clicked in the console

To get rid of the square braces call `window.console.log`.

Now this isn't gonna be terribly exciting. So let's also change the value of our label.

I'm going to split it and I'm going to reverse it. Then we will join it with no spaces or no characters, and I should definitely reassign it to itself.

So what I'm doing here is I take the label or split it on every character into an array and I reverse the array and then I rejoined it into a string and reassign it back to the label. Once deployed out.

Now we can refresh the page now if I click on it, it reverses.

We can keep clicking an arrow key person.

But what if we want to handle another kind of event

instead of handling and `onclick` method, what's handle `onmouseover`?

Now as my when my mouse goes over it, it reverses.

Not terribly useful but we now know how to wire up an event in HTML directly to our JavaScript.

## That’s it for now.

Remember to sign up for **[The Weekly Stand-Up!](https://wipdeveloper.wpcomstaging.com/newsletter/)**  and you can get updated with any new information we have on WIPDeveloper.com.
