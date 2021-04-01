---
layout: "post.11ty.js"
title: "LWC - LoadScript Issue"
date: "2020-02-19"
tags: 
  - "Blog"
  - "LWC"
  - "Salesforce"
  - "SalesforceDeveloper"
  - "SalesforceDX"
slug: "lwc-loadscript-issue"
coverImage: "LWC-LoadScript-Issue.png"
---

https://youtu.be/1ng6p\_317jw

Hello, I'm Brett with WIPDeveloper.com. Since we've taken a look at how to use `loadScript`, I wanted to point out one issue you may encounter when using this library Legra, I originally used the IFFE version of it, which is and immediately invoked function expression. It's a pattern used in JavaScript. The IFFE file is located in `${this.jsPath}/legra/lib/legra.iffe.js`. It's very common, it's been in use for a while.

The issue that it encounters is here it is running in the local environment and you see it works fine. Now when I deploy it, though, now that it's deployed, you see when I click the button, I actually get an error. It says "Legra is not defined". Nothing else has changed. And you might be thinking to yourself, "It was working at the local dev environment. Why is it saying that's not defined now?"

The issue is this library Legra is using Roll Up to build itself. And it needs to apparently have declared itself, output extended equals true. So it doesn't do that. So it's not extending the object that's passed in. So Legra in the locker service it's not being made available because it's not extending the global object.

I got this feedback from and I'm going to do a horrible job pronouncing his name, Pierre-Marie Dartus. And I'm sorry if I got that wrong. I will provide a link below to his Twitter profile and you can thank them. providing that feedback.

I did not see this documented in the lightning Web Components documentation.

If you encounter this error and you're the library using doesn't support extending the object, the window object, try seeing if there's another format to use. For instance, when I change it to the UMD format, which is the universal module definition, it does support or does end up working. so here we can see it is in production, or now we can see that it's working still and local environment. And in Salesforce, you can see it is working again.

If they ever enable way to use a locker service and local environment that would probably be a better approach than grasping at straws for why things aren't working, when you move from one environment to the other. But until then, be on the lookout for your libraries, not being defined in the org If it is working locally.

## Links

[Pierre-Marie Dartus](https://twitter.com/pmdartus)

[https://github.com/BrettMN/lwc-posts](https://github.com/BrettMN/lwc-posts)

## That’s it for now.

Remember to sign up for **[The Weekly Stand-Up!](https://wipdeveloper.wpcomstaging.com/newsletter/)**  and you can get updated with any new information we have on WIPDeveloper.com.
