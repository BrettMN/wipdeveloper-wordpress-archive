---
layout: "post.11ty.js"
title: "LWC - Copy to Clipboard Button"
date: "2019-09-11"
tags: 
  - "Blog"
  - "LWC"
  - "Salesforce"
  - "SalesforceDeveloper"
  - "SalesforceDX"
slug: "lwc-copy-to-clipboard-button"
coverImage: "Screen-Shot-2019-09-10-at-11.56.54-PM.png"
---

* * *

Hi, I'm Brett with WIPDeveloper.com. The other day I saw a question about how to create a copy to clipboard button in lightning web components. So I took a crack at it. And this is what I came up with.

I've created a component that has mark up the `lightning-card` that has a title of Copy to Clipboard, with two text fields, one to copy, and one just paste it in so you can see it and a button that should copy the text.

The markup is pretty straightforward and has an input for the copy input for the pasting and then the button to call copy to clipboard.

In the JavaScript. The one method Copy to Clipboard currently does nothing. So we can click this all we want and then paste it and nothing will happen. I mean, it's pasting spaces right now, but what we want have to do is copy the contents of this input. We're going to do this by first getting input. So we'll have to find the the

`copy-me` text which has the class of `copy-me`.

So query against the `template.querySelector` and that's going to be `.copy-me`.

Now that we have a reference to the input. We're going to select it. So `select` should highlight the text

So let's try it, save this and what should happen when we refresh the page and click the button `Copy Me!` should get selected.

I did see some mentions that this might not work on some browsers. So to account for that, we're also going to use `setSelectionRange`. We want to be the first character all the way to the end. So

we're just making some high number.

Now we don't have to worry necessarily worry if the browser that it gets implemented or used in doesn't follow the select option.

Now we want to use the `Copy` command. And who do we use `document.execCommand` and then the string of the command type that we want in this case `copy`. So

`document.execCommand`.

Copy.

Save this

format it.

Then save it.

Now, when we refresh the page and press the press the copy button, it should highlight and now we should be able to paste copy me into this second text box. And it works.

And it doesn't we can change this to something else. Press copy and then paste it over here. And we can paste it in We can make the text here literally anything and copy the text and paste, paste.

Go. That's it.

If you want to make a copy, using Copy to Clipboard button and the lightning web component that would be one way to do it.

## Links

- [Interact with the clipboard](https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/Interact_with_the_clipboard)
- [HTMLInputElement.select()](https://developer.mozilla.org/en-US/docs/Web/API/HTMLInputElement/select)
- [HTMLInputElement.setSelectionRange()](https://developer.mozilla.org/en-US/docs/Web/API/HTMLInputElement/setSelectionRange)

## That’s it for now.

Remember to sign up for **[The Weekly Stand-Up!](https://wipdeveloper.wpcomstaging.com/newsletter/)**  and you can get updated with any new information we have on WIPDeveloper.com.
