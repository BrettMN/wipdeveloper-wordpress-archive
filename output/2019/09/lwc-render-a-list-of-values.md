---
layout: "post.11ty.js"
title: "LWC - Render a List of Values"
date: "2019-09-23"
tags: 
  - "Blog"
  - "LWC"
  - "Salesforce"
  - "SalesforceDeveloper"
slug: "lwc-render-a-list-of-values"
coverImage: "Screen-Shot-2019-09-22-at-11.41.29-PM.png"
---

* * *

So I've already created a new lightning component called values list. And I've added it to our page. And you can see it already has a lightning card with the title of value says values value less, but it should say values list. And then I have a place for the list to go.

So I'm going to render a list, I have to have some values to render. So I'm just going to add a couple of values in the controller. And we should probably start with zero. So now we have some values to render, and the HTML, the documentation, say to use the template. So we would use it `for:each`, and then we would bind to the values. And then we would have a `for:item`. And that would not be bound to anything, but we would declare a name for it. And I'll just call it value, we can just use the value down here. And if we gave this a key and bound to save it, we should see our list rendered when we refresh the page.

There we go, we now have an unloaded list that has four items in it. Not terribly exciting, but we can also add new. So a couple of things, this is how the documentation will show you how to create the list. But what I'm going to do, cuz it gets a little verbose because we don't, we have template just so that we can have the repeat, or the four syntax on it.

So let's remove that from there and add it directly to our list item. Now we've removed some of the extra. Now we've removed the extra template, because it's not necessary to render it list properly. There we go. It's still working. And you might wonder what happens if you are list where to get a new item? Well, let's give that a shot.

Going to add a new button under the list. Oh, I see what I did. Something I didn't nest is I did not have my list, I did not add that in there. So that that put a button in what call add one. And now when we click this button, it'll call method called add one. So we should probably add that to our controller. So what this is going to do is it's going to add the next number. Oops, combination of control buttons. So when we click our button, it's going to call add one add one is going to push the next number to our list. And now let's click our button.

We are doing something wrong. What is it? Here's what happened. I forgot to add track here. And if we're going to track that we have to import track. And I swear I knew this and I made a note to make sure to do that. But here we are, we've added `track`. Going to close down the debug console. Refresh the page.

Now we can add one, we can add a whole bunch. And every time we add a new one, it renders the list with our new values. Pretty sure we can subtract one. Let's try pop, see what happens. Refresh the page. We have a subtract one. There we go. So you can see our list is changing as we add and push one on to the stack and we pop on off the stack being the array of values.

So that's how we render a list of values using lightning web come on and a little shortcut to make your HTML syntax a little bit less verbose.

## That’s it for now.

Remember to sign up for **[The Weekly Stand-Up!](https://wipdeveloper.wpcomstaging.com/newsletter/)**  and you can get updated with any new information we have on WIPDeveloper.com.
