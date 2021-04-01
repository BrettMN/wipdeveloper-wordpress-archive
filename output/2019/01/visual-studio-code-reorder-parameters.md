---
layout: "post.11ty.js"
title: "Visual Studio Code - Reorder Parameters"
date: "2019-01-16"
tags: 
  - "Blog"
  - "SalesforceDeveloper"
  - "SalesforceDX"
  - "VSCode"
slug: "visual-studio-code-reorder-parameters"
coverImage: "Screen-Shot-2019-01-16-at-9.56.14-PM.png"
---

* * *

> _I’m trying something new. Bellow is a generated transcript from the video with minor editing. If there are any issues, please let me know Brett@WIPDeveloper.com_

Hello, this is Brett with WIPDeveloper.com. Earlier today someone asked how to reorder parameters in Visual Studio code, I found a solution thought it would be easier to find, again, if I shared it with everyone.

## Problem

Sometimes you write your code and put the parameters in the wrong order, like my System.assertEquals, here, I've put actual over the expected value should be and I've put expected where the actual value should be. I can fix this by copying and pasting or deleting one of the values and re-adding it.

I've also messed up the order of my parameters where I want `one` to be first instead of `two`.

## Shifter

I want `two` over here and once again I can do the whole copy paste thing or, and this is an Apex, I can get an extension called Shifter, and I will provide a link below, but Shifter and just install this now I can use `ctrl + alt and left` or `ctrl + alt and right` and reorder my parameters.

It also works in the parameter definition of a method. Didn't have to copy and paste anything. It is pretty simple. So it works in apex. And we can also use it in JavaScript.

So in our JavaScript file here, we can have, if we had a method that had two parameters, we would be able to reorder those parameters the same if we had an array and they were not in the proper order.

We can use it in the array as well. So we can reorder in the definition of a method we can reorder the values of an array and we can also reorder in calling a method.

what, oh.

ESLint wants us to call it on `window` there. Now we have our parameters in the in the wrong way hitting the wrong command we can reorder pretty easy.

That is called Shifter by Gruntfugly, what a lovely name, a Visual Studio Code plugin to help you reorder your parameters or comma other comma separated list.

## Links

- [Shifter](https://marketplace.visualstudio.com/items?itemName=Gruntfuggly.shifter)

## That’s it for now.

Remember to sign up for **[The Weekly Stand-Up!](https://wipdeveloper.wpcomstaging.com/newsletter/)**  and you can get updated with any new information we have on WIPDeveloper.com.
