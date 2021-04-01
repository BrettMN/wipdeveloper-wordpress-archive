---
layout: "post.11ty.js"
title: "LWC  - Experimental Decorators Error"
date: "2019-04-16"
tags: 
  - "Blog"
  - "LWC"
  - "Salesforce"
  - "SalesforceDeveloper"
  - "SalesforceDX"
  - "VSCode"
slug: "lwc-experimental-decorators-error"
coverImage: "Screen-Shot-2019-04-02-at-4.35.56-PM.png"
---

* * *

Hello, I'm Brett with WIPDeveloper.com.

The other day while working on Lightning Web Component, I noticed that in Visual Studio Code, I was getting an error when I was using the wire decorator, and the error says "experimental support for decorators is a feature that is subject to change in future releases set experimental decorator options to remove this warning."

Now, I hadn't changed anything, looking at the sample apps and the Salesforce GitHub repo.

There's no explanation for where this came from or what change occurred. I think it might be because I am using Visual Studio Code Insiders Edition. And one of the updates started using TypeScript because if you look at the end of the message, it says TS and then parentheses 1219. So I think it's using a TypeScript check for whether or not the experimental decorators are used.

And so the work around, because I can, I can still deploy this. So I need to work around so that I can get rid of the red squiggly lines because I don't like red squiggly lines.

So what I did was I created a Ts config file.

And in it it has compiler options and those options are experimental decorators is true and allow JS is true.

#### tsconfig.json

```
{
    "compilerOptions": {
        "experimentalDecorators": true,
        "allowJs": true
    }
}
```

Whether or not you need the allow JS, I don't know. But that was the example I found on the internet and it is working for me and it gets rid of the red squiggly lines.

Now this is mostly a convenience thing since I was able to deploy but if you'd like to see whether or not you have any problems by just looking at the prop problems tab header, this will help clear that up as you see if we don't have the TS config.

We are we are always going to see that we have one problem.

If you have multiple lining web components that have multiple decorators and use, you could easily lose track of whether or not it's a problem or whether or not it's the editor not recognizing the proper recognizing that it's a proper use of a decorator.

## That’s it for now.

Remember to sign up for **[The Weekly Stand-Up!](https://wipdeveloper.wpcomstaging.com/newsletter/)**  and you can get updated with any new information we have on WIPDeveloper.com.
