---
layout: "post.11ty.js"
title: "LWC – First Look – Adding Style with CSS"
date: "2019-01-15"
tags: 
  - "Blog"
  - "LWC"
  - "Salesforce"
  - "SalesforceDeveloper"
  - "SalesforceDX"
slug: "lwc-first-look-adding-style-with-css"
coverImage: "Screen-Shot-2019-01-15-at-4.05.32-PM-3.png"
---

* * *

> I'm trying something new. Bellow is a generated transcript from the video with minor editing. If there are any issues, please let me know Brett@WIPDeveloper.com

Hello this Brett with WIPDeveloper.com. Our first component has styles now thanks to the Salesforce Lightning Design System. But sometimes you want to get a little bit more custom and use your own CSS.

## Add a Stylesheet

To do that, we're going to have to go into our component add a CSS file. So in the same directory new file, going to call it `firstComponent.css`.

Since lightning Web Components use the Shadow DOM to style our individual components will use the CSS pseudo class of `:host` to specify in our component only. Let's prevent styles from outsider component from bleeding in and it'll narrow the scope of our styles to change the background color to a light blue. We would have to use the `:host` and apply in our CSS Selector to get the CSS class, which will be a `slds-page-header`.

Assign CSS styles the same as you would with the normal style sheet. Now we can deploy this.

Refresh a few times and now we have a light blue background we might want to also have an effect when we hover on it. So to add a hover effect you can use host again, except this time use parentheses

and passing the hover pseudo class. Here's the CSS selector for the class name again, and this time let's assign the background color white.

Now when we hover over it, we should see the background go from the light blue to white.

Once that it's deployed refresh a few times again.

Now when we hover it goes from the white light blue to white. So if we wanted to target a specific element like is awesome we can use the CSS class.

It's on a paragraph tag.

So we're still need host

change the color to a blue. Deploy this, now we're targeting just a specific element, not the entire element of not our entire customer. So it is possible to do that as well.

Deployed. Refresh

There, now, is awesome is blue we hover over turns white

This is what happens when you come to a website that has developer in the title to get styling advice, blue on blue, maybe not the best plan.

#### Final Styles

```
:host .slds-page-header {
  background-color: lightblue;
}

:host(:hover) .slds-page-header {
  background-color: white;
}

:host p.slds-page-header__name-meta {
  color: blue;
}
```

## Links

- [:host() on MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/:host())
- [Using shadow DOM](https://developer.mozilla.org/en-US/docs/Web/Web_Components/Using_shadow_DOM)

## That’s it for now.

Remember to sign up for **[The Weekly Stand-Up!](https://wipdeveloper.wpcomstaging.com/newsletter/)**  and you can get updated with any new information we have on WIPDeveloper.com.
