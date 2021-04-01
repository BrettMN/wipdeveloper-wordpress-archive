---
layout: "post.11ty.js"
title: "LWC - Calling a Child's Method"
date: "2019-09-16"
tags: 
  - "Blog"
  - "LWC"
  - "Salesforce"
  - "SalesforceDeveloper"
  - "SalesforceDX"
slug: "lwc-calling-a-childs-method"
coverImage: "LWC-Calling-a-Childs-Method.png"
---

* * *

Hello, I'm Brett with WIPDeveloper.com. Since we've been working with parent and child component, wanted to take a look at how to call a method on a child component from the parent.

First thing we're going to have to do is figure out what method to add to our child component. So there's actually something to call, we're going to add a method to set a piece of text for the let's use in the HTML. We're going to change child here to bind to a property called child text.

And by default, we want it to be set to child we want to expose a method to change that text. So we'll make a new method called set child text.

And it will take a text argument and what is `this.childText` to text.

We also want to be able to reset it. So we will add a second method called `resetChildText`.

And it won't take a parameter, what it will do is

it'll use the `setChildText`, and it'll pass in "Child". We want to call this from the child though. So let's go to our HTML and add a button.

And we will call that `resetText` from here.

So far, nothing should look surprising.

See our reset tech button. It doesn't look like it does anything at the moment because it is just setting this text here back child. And it's never been set from to something that's not child or parent component. We're going to need to add a couple of buttons.

Let's make this in the footer slot and this will be a button.

Set the child one text the second button to set the child to text and it would help if I actually got things set in their proper spaces. Now this doesn't mean need a method named `setChildOneText` and the other one will need a method to call called `setChildTwoText`.

And these won't save because those don't exist.

To us the set child one text, we will have to figure out a way to call the method on this first child.

And we need a way to identify that because what we're going to use is the query selector.

And it's gonna always return the first one. We could use query selector all and grab the second one from the collection that's returned and the first one, but I'd like to be more specific. So I'm going to add a class called one on the first one, so that it can use that in the query selection.

And once again, Quotes at the right spot.

So, this will let us grab and a reference to the first child element, our first child component, then we also need to try and call it will you set out set child text going to make it so it says text from parent for child one.

Now, this will save and we refresh our refresh our page. You should see the buttons and we can set out one text. However, we're getting gonna get an error because `setChildText` isn't actually exposed to make it so we can call it from the parent, we have to decorate it with the API decorator, which we've already.

That shouldn't be.

We've already imported the API decorator. I forgot to mention, we need to add track to the child text, not API. So have to import that as well. But for the set child text, expose it with the API. So other components will be able to utilize it.

Refresh.

Okay, so we saw that the text changed for the first component. So set child one text changes that we set out to text, nothing will happen because we're not actually setting it right now, but we can fix that.

I show you the using the query selector without the class name on the end, child to see.

Okay, that's a refreshing.

And if I set it on to and actually sets it on the first one, because we're not, we don't have anything to identify it as the second one. I like using a class because it's more explicit. We are talking to this one, I'd like to use an ID, but that's not really an option. Since the IDS gets set by and we don't know what they are, the IDS Get set.

As they're rendered on the page, and we're not we don't have a reference to what they are.

So adding a class allows us to target the second child. Now if we do this, it updates the text for a child to

And the first button updates the text for child one. And we can reset the text on both.

And that's it.

We now know how to call method on a child component. And we even know how to specify which child component when there's multiple ones on the page.

## That’s it for now.

Remember to sign up for **[The Weekly Stand-Up!](https://wipdeveloper.wpcomstaging.com/newsletter/)**  and you can get updated with any new information we have on WIPDeveloper.com.
