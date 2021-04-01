---
layout: "post.11ty.js"
title: "LWC - Loading JS from a Static Resource"
date: "2020-02-12"
tags: 
  - "Blog"
  - "LWC"
  - "Salesforce"
  - "SalesforceDeveloper"
  - "SalesforceDX"
slug: "lwc-loading-js-from-a-static-resource"
coverImage: "LWC-Loading-JS-from-a-Static-Resource.png"
---

https://youtu.be/xz6yPHjo530

Hello, I'm Brett with WIPDeveloper.com. Since we've been taking a look at loading from static resources, let's take a look at loading a JavaScript library from a Static Resource.

I've already traded a Lightning Web Component and built out some of the preliminary parts. I have a button that says "Build" that when I click it will call the `build` method. I also have a `<canvas>` because the library I'm going to use is a drawing library. So I have a canvas have a set height and width, it has the the main thing to note here is that I have the `lwc:dom="manual` so that the library will be able to manipulate the DOM of this element. And I gave it a class `build-area`. In our JavaScript file. We have that method called build already created. I also have already imported the `jsToLoad` static resource I've imported the `testFiles` because we're going to make use of one of the images that are in there.

Right now click Build, nothing happens. And that is expected. First thing we're going to do is import the `loadScript` from `lightning/platformResourceLoader`.

So we've importing `loadScript` and `loadScript` starts with a capital S. we're importing `loadScript` from `lightning/platformResourceLoader`. And we're going to make use of that in our `build` method. We already have `jsPath` assigned to `jsPath` and `testFiles` assigned to `testFilePath`. And `loadImage` down here is a helper method we need for the library to access the image will use later on.

When `build` is called, what we're going to do is use `loadScript` to load the library Legra from the static resource `jsToLoad`. So, first thing we need to do is get that so we get that started.

`loadScript` method takes the context that it's supposed to operate in. So `this` and then the path of the file. So and the path in our static resource is going to be `/legra/lib/legra.umd.js` and that should be the correct path. Then, since this is since this is an asynchronous method, we will call `.then()` on it. We will also call have a `.catch` method in case there's an error.

Okay, so for our `catch` method in case something goes wrong, we're just going to log it to the window console. In our in our `then` method we will access Legra from the context of window. So once `loadScript` loads that script it should be added to the window object. So we can use `window.legra` to access it or we can just use `legra` without the window since implied let's just see if this actually loads at first. Okay, now when we look in our local development environment, we see that we are actually logging right here if we put a breakpoint in We see Legra is a class to be used. One of the requirements of Lagra since we are using this is to get that `<canvas>` element we created earlier. So let's start by getting that available.

Here we have our `buildArea` defined and we're using `this.template.querySelector('canvas.build-area').getContext('2d')` to get the 2d context of the `<canvas>` element so now we can use this in our returned promise to access the canvas build area. And with Legra make something happen.

Here we're using Legra calling a new instance of legra, Legra is defined as a class, usually in JavaScript, when it's a class, it should be capitalized. That is not the case right now. So we'll just use a new Legra, pass in the `buildArea` that we got. And that's the 2d context of our canvas element. And the second property here is how large we want the elements we're going to build with.

Next we call the builder and create a rectangle uses the start parameters of 12 and two, and the end parameters of 8 and 8. So let's go look what see what this looks like. And we have a rectangle if we change it, so we can make it a little bigger to see. Close the console, we're not going to need that anymore. So there we have it, a rectangle that uses the Library library to create what appears to be Lego blocks, tops in a rectangle.

We can make more than just rectangles. We can also use it to make the No items. So let's make some of those as well. Yeah, we've got a assortment of objects that we've created once we deploy this into Salesforce for fun, because why not, we can see that our brick design can be present in our Salesforce org, because it seems like a fun thing to do.

The other thing we can do is I mentioned an image earlier so we can get rid of all miss. We're going to use the like Legra library to draw an image. The helper method down here, `loadImages` is `async`, so we have to specify and build as `async` as well. There we go. Things formatted properly. Now we have our image loading up here after we get the `buildArea` with With the path to the static resource that we want to use as our image, the `loadImages` method is just a helper method. So we have the image ready for Legra to use. And then we call `builder.drawImage(img, [0, 0])`.

And looks a little bit hard to see. So let's change the size of the bricks to five. We're going to deploy this right now. There we have it, our Legra Library using an image to draw a little block online and it still works in Salesforce.

## Links

https://legrajs.com/

## That’s it for now.

Remember to sign up for **[The Weekly Stand-Up!](https://wipdeveloper.wpcomstaging.com/newsletter/)**  and you can get updated with any new information we have on WIPDeveloper.com.
