---
layout: "post.11ty.js"
title: "LWC - Loading CSS from a Static Resource"
date: "2020-02-05"
tags: 
  - "Blog"
  - "LWC"
  - "Salesforce"
  - "SalesforceDeveloper"
  - "SalesforceDX"
slug: "lwc-loading-css-from-a-static-resource"
coverImage: "LWC-Loading-CSS-from-a-Static-Resource.png"
---

https://youtu.be/Sgrpghqh7Ec

Hello, I'm Brett with WIPDeveloper.com. We've already taken a look at how to load a static resource so that we could access an image. But what if we want to add some styles from a style library to our lightning Web Component? Conveniently, Salesforce provides us with a `loadStyle` method. So we can load styles from static resources.

## Load Some CSS

So the first thing we would have to do is go to the style library that we want. Or if it's our own custom CSS that we're reusing, we take that and upload it to a static resource. In our project, I've already done that I have a static resource called `stylesToLoad`. And I've already specified the path so I have `nesStylesPath`, and then it's `@salesforce/resourceUrl/stylesToLoad`. And I'm assigning it to `stylePath` online six here. I'm going to want it to load using the `loadStyle`, so I need to import that. We import `loadStyle` from the `lightning/platformResourceLoader`.

In the HTML, I have to find a button that says style me. It has an onClick method that calls the Add style method. I've already assigned classes to the elements that I want styled from the restyle resource that we're going to load. You can see the button is going to be styled as an `nes-btn` and `is-primary`. And then down below the button. There is an icon list that has `nes-mario` and `nes-ash`, `nes-pokeball`, `nes-bulbasaur`, `nes-charmander`, `nes-squirtle` and `nes-kirby`. Right now on our page. We don't see any of those because there's nothing to find. To make use of those. There's nothing defined to make use of those classes.

When we call `addStyle` we want it to call the `loadStyle` method. And the `loadStyle` method takes a reference to the current instance. So `this` and then the path to the style that we want. So our `loadStyle` method is going to use the instance that it's currently in sort of `this` and then it's called passes in the path to the style that we're trying to access. Since style path only references the route of the static resource. Inside the static resource, we have to provide the path to the CSS file that we want.

We can close this and deploy it. I can refresh the page can case you're wondering, yes, I could be doing local development, I just forgot to set that up.

Now let's click our button and see what happens though. There we go. We have our icons with Mario, Ash, a pokey ball, a Bulbasaur, Charmander, Squirtle and Kirby.

But the text on our button looks a little off, let's take a look at how we can get the text to style properly. Since my style library didn't include the fonts, I'm going to load a separate CSS file that's called `fonts.css` to specify the font to use. And since we are loading two styles at the same time, we're going to want to use `Promise.all` so that all the styles load at the same time and are applied once all the styles are completely loaded.

If we were doing Something with a JavaScript library. This end the promise dot all dot then or callback method is when we would take action. So let's save this.

Now let's try it. Now we see that it has the blocky text that I was looking for. One thing to know, the blocky text is everywhere. So this is a good instance on when I would want to scope the styles to a particular element.

## Load CSS When Component is created

Now that we're loading the fonts, even though it's sort of affecting the rest of the page more than we would want it to. Why don't we get it so that we don't actually require a button click to load it.

To make the styles load automatically when the page loads will change from using the `addStyle` method to using a constructor. So the `constructor` from the class will be called when the component is loaded or created.

And to see use a constructor method we have to call `super()`. There we go. You can see that it loads right away when the lightning Web component comes on the page.

And that's how we can load a CSS file from the static resources and apply it to our lightning web components.

## Links

https://wipdeveloper.wpcomstaging.com/lwc-using-a-static-resource/

## That’s it for now.

Remember to sign up for **[The Weekly Stand-Up!](https://wipdeveloper.wpcomstaging.com/newsletter/)**  and you can get updated with any new information we have on WIPDeveloper.com.
