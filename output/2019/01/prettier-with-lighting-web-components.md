---
layout: "post.11ty.js"
title: "Prettier with Lighting Web Components"
date: "2019-01-23"
tags: 
  - "Blog"
  - "LWC"
  - "Prettier"
  - "Salesforce"
  - "SalesforceDeveloper"
  - "SalesforceDX"
slug: "prettier-with-lighting-web-components"
coverImage: "Screen-Shot-2019-01-25-at-3.50.46-PM.png"
---

* * *

Hello I'm Brett with WIPDeveloper.com. If you've been working with Lightning Web Components in Visual Studio Code with the Prettier extension installed, you might have encountered issues where he tried to assign a property to an attribute on your HTML.

## A Prettier Problem

If I try to change the title from the string of web developer calm to the property label it's going to reformat it and cause issues. I'm gonna hit save now I have an issue where it's Prettier has automatically inserted quotes around my property.

The Lightning Web Component linter is saying that you should not have quotes around your property names to prevent Prettier from automatically inserting double quotes around your Properties on your HTML templates in your lightning lab components.

We are going to have to tell Prettier to ignore the HTML files. We can do that in our project so we don't have to uninstalled the extension.

## A Prettier Solution

We create a new file called `.prettierignore`

now we're going to do more than just ignore the HTML files actually got this from René Winkelmeyer and I hope he's okay with me saying his name he works at Salesforce as a dev evangelist. This is a pretty or ignore file from one of the Trailhead example apps.

And I'm going to it's what it's going to do is it tells Prettier to ignore CSS, HTML, SVG files, XML files, and anything in the `.sfdx` folder so Prettier will not check the formatting on those.

All we do is add that to our `.prettierignore` file. Now when we remove the double quotes,

We press save. it did not work. What did I spell wrong?

Where did I create the `.prettierignore` file

You have to create it at the base of your project I was not paying enough attention.

Now we can delete the double quotes.

Press Save it prettier did not re insert the double quotes. The lender does not have problems with our syntax and we can carry on with using

properties from our web component in attributes, I will provide a link for the example `.prettierignore`, I'll also have the entire contents below.

#### `.prettierignore`

```
**/lwc/**/*.css
**/lwc/**/*.html
**/lwc/**/*.svg
**/lwc/**/*.xml
.sfdx
```

## Links

- [.prettierignore Example](https://github.com/trailheadapps/purealoe-lwc/blob/master/.prettierignore)
- [René Winkelmeyer](https://twitter.com/muenzpraeger)

## That’s it for now.

Remember to sign up for **[The Weekly Stand-Up!](https://wipdeveloper.wpcomstaging.com/newsletter/)**  and you can get updated with any new information we have on WIPDeveloper.com.
