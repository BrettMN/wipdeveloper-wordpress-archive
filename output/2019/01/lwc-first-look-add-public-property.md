---
layout: "post.11ty.js"
title: "LWC – First Look – Add Public Property"
date: "2019-01-22"
tags: 
  - "Blog"
  - "LWC"
  - "Salesforce"
  - "SalesforceDeveloper"
  - "SalesforceDX"
slug: "lwc-first-look-add-public-property"
coverImage: "Screen-Shot-2019-01-23-at-3.47.23-PM-3.png"
---

* * *

Hello, this is Brett with WIPDeveloper.com. So we have our first component. And we've added styles using the Salesforce Lightning design system and Custom CSS.

Right now we can't really reuse our component because the only thing it says is "WIPDeveloper.com is awesome". And while I might think that's a true statement, you might not want it to look that way on your page.

## Creating a Property

So we're going to add a property to our components. So we can assign a value via the community builder in Salesforce.

To do that, we're going to have to go into our component and a property. So we can set a default value as well.

So that in case we don't set it, it'll stick out. Now, in theory, we should be able to use this, as our property.

We shouldn't be able to use our property right now and have display. Let's save it, give it a shot.

Before we do that, we should probably make it a little different. So we know it's coming from the label property. There we go. Now, let's refresh the page. See, if we get an exclamation mark. There we go. We have three exclamation marks. Now, if we go into the Edit page and select our component.

#### Updated `firstComponent.js`

```
import { LightningElement, api } from 'lwc';

export default class FirstComponent extends LightningElement {
  @api label = 'WIPDeveloper.com  !!!';
}
```

## Exposing the Property

We do not have the option to set the label property here. To make it so we can do that we have to go into the first component metadata XML file.

So previously, we set the metadata as exposed true. So we can see it in the app builder. And we gave it the target pages the app page, record page, and homepage. Now what we're going to need to do it is and `targetconfigs` that expose the property that we just created the label property.

So there's `targetconfigs`, this allows us to expose things for the targets that we specified above. So we're going to configure one `targetconfig` for all three types.

Now, this will need a property of targets.

Now I could copy and paste each one of these down there, that's a comma separated list. Or I could just copy and paste it from my other window, which is what I'm going to do. But you can see I have the lightning record page, I have the lightning app page and the lightning homepage on this `targetconfig`.

Now, I want to add a property that will specify that we are exposing the property

`label`.

This has to match the name we specified in our JavaScript component, we have to specify the type and it's a `String`, and then we can provide a default value just so we know that it's always set.

Now side note, I'm a little annoying, but it doesn't auto format. So what I want to get real quick is XML Tools, yes, XML tools want to install that restart just one format and look nice.

There we go, everything is much nicer. I'll provide a link for XML Tools in the blog post below. Now we've exposed the property of label, we should be able to see this in the Lightning App Builder. Once we this to the scratch org.

So it was saying we got an error, the label property does not exist on the component. And that is because I forgot to use the `@api` decorator. So from the inner impart statement, we have to add a we have to have an import for API.

Down here, we would actually use it with an at (`@`) sign.

#### Updated `firstComponent.js-meta.xml`

```
<?xml version="1.0" encoding="UTF-8"?>
<LightningComponentBundle xmlns="http://soap.sforce.com/2006/04/metadata" fqn="firstComponent">
  <apiVersion>45.0</apiVersion>
  <isExposed>true</isExposed>
  <targets>
    <target>lightning__AppPage</target>
    <target>lightning__RecordPage</target>
    <target>lightning__HomePage</target>
  </targets>
  <targetConfigs>
    <targetConfig targets="lightning__RecordPage,lightning__AppPage,lightning__HomePage">
      <property name="label" type="String" default="WIPDeveloper.com"></property>
    </targetConfig>
  </targetConfigs>
</LightningComponentBundle>
```

Now that we've properly decorated with our property with API. Let's push this and we can go back to our Lightning App Builder.

Let's refresh it.

Theres the `label` so we can give it a name

This time lets just give it slightly different label so we can make sure that it's taking the label that we've assigned in the app builder go back.

And there you have it, WIPDeveloper.com exclamation exclamation exclamation, one exclamation. So there we go. We have exposed a property from our custom lightning web component to the lightning app builder so that we can configure it.

## Links

- [XML Tools](https://marketplace.visualstudio.com/items?itemName=DotJoshJohnson.xml)

## That’s it for now.

Remember to sign up for **[The Weekly Stand-Up!](https://wipdeveloper.wpcomstaging.com/newsletter/)**  and you can get updated with any new information we have on WIPDeveloper.com.
