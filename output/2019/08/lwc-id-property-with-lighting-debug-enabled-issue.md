---
layout: "post.11ty.js"
title: "LWC - Id Property with Lighting Debug Enabled Issue"
date: "2019-08-19"
tags: 
  - "Blog"
  - "LWC"
  - "Salesforce"
  - "SalesforceDeveloper"
slug: "lwc-id-property-with-lighting-debug-enabled-issue"
coverImage: "Screen-Shot-2019-08-16-at-11.56.11-PM.png"
---

* * *

Hello, I'm Brett with WIPDeveloper.com. The other day while developing a Lightning web component, I ran into this issue where when importing the Salesforce user ID and assigning it to a property in the component called ID. And this is a very simple component, because that's all it's doing in the JavaScript. And all it's doing in the HTML is displaying the ID. Now, this is pretty straightforward. You think there shouldn't be any issues. And there's not it's loaded on the page.

The issue arises when you enable lightning debug mode. So if I go into the debug mode, and enable it, and refresh the page with component on it, I start seeing this, `render threw an error in 'c:importUserId Trial' [Assert, Violations: Failed to construct '<c-import-user-id-trial>': The results must not have attributes.]` and took a while to figure it out. And saw some responses on Twitter about this. I thought the issue was with the important statement itself. Obviously, it was working before I turn on lightning debug mode. So if I turn it off, and refresh the page, it works again. But if I want the debug modem, that's not a solution. So I'm going to enable it, make sure it's still an issue. And it is. Now, I'm going to change the property name from it to something else. So thanks to you, user, Id save it, push this and refresh the page. Maybe a second time.

Oh, I should update the HTML template.

Refresh the page. We can now see RTD ID. And we can open up the developer console in the browser and see that we are in lightning debug mode, because we get all those wonderful messages from Salesforce. Yay. So if if you are encountering the renderer threw an error, assert violation check to see if you have any properties that are called just ID, ID and adjust accordingly. It's to my understanding, not supposed to be something that's prevented. Based on some of the responses I saw. It's not supposed to be an issue, unless is an API decorated attribute but that is not the case that I encountered.

## That’s it for now.

Remember to sign up for **[The Weekly Stand-Up!](https://wipdeveloper.wpcomstaging.com/newsletter/)**  and you can get updated with any new information we have on WIPDeveloper.com.
