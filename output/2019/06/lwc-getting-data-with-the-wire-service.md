---
layout: "post.11ty.js"
title: "LWC – Getting Data with the Wire Service"
date: "2019-06-20"
tags: 
  - "Blog"
  - "LWC"
  - "Salesforce"
  - "SalesforceDeveloper"
  - "SalesforceDX"
slug: "lwc-getting-data-with-the-wire-service"
coverImage: "Screen-Shot-2019-06-21-at-6.38.02-PM.png"
---

* * *

Hello, I'm Brett WIPDeveloper.com. Last time we received data from Salesforce using the Lightning Data Service. This time we're going to take a look at using the wire service to get data out of Salesforce for component.

Before we get too far though, I want to take a moment to thank our sponsor for this episode. [Just Some Apps](https://justsomeapps.com) they are here to help you get more from your technology investments, check them out at [justsomeapps.com](https://justsomeapps.com)

If you would like to be a sponsor, or if you find the content I'm creating at WIPDeveloper.com useful and would like to support the creation of more content, you can do so by going to [patreon.com/BrettMN](https://www.patreon.com/BrettMN) then include a link below. depending upon what level you back at. You can have your name are included in a blog post and immortalized on the internet.

Now let's get to learn about using the wire service. To use the wire service we have to import it from the Lw c collection. So along with lightningElement and api we import for service. The wire service is a decorator similar to the api decorate. So we're going to have to add wire.

And this is actually a method. So we're going to add this on to a property user. But this method

we're going to need to provide a method to and some additional details. So first thing we're going to want to do is import an additional. We want to import a method, get the record so

import getRecord. We're going to import it from lightning/uiRecordApi.

Now this method…

Visual Studiop Code aggressively imported something, we don't need that User.

Now this, we use the getRecord method as the first property in our wire decorator.

This is what will be good doing the work for calling Salesforce with the wire we're it'll work with the wire service to get the record that we want. So to get the record, we're going to have to provide it with the recordId.

So we provide it with $id.

So the wire service knows to get the id property from our instance. We also have to provide it with some fields since we want to get the information from the user

I forgot, thgis has to be on an object. So have to have a recordId is passed the id property.

Close out the object so it doesn't get mad about that.

Now we have to tell you like.

Now there are a couple different ways we can get deals, I'm interested in getting access to the data as easily as possible. So I am going to essentially code in the strings to identify what fields to get off the user object. You can import references to the fields of the objects, but seems beyond the scope of what we're doing right now and I just want to get data for us. So I'm just going to grab the username, email, company name, and phone number.

Now this is all passed in to this array or end of the fields as an array. And that is all we need for our fields.

Now this wire decorator will populate the user record once the page loads and it has a recordId

or userId in this case because the userId is still being imported.

How do we get those values to our user? We could try putting binding at thge bottom just to see what it looks like. I'm going to push this up to Salesforce and let's go and refresh it a few times

It's saying object object because we aren't picking up the properties we want

toString object. It just says object object. So let's go back in here.

I want to change this so it says wire. Yay. But now what I want to do I don't want just the user I want the name.

So on name property.

And get now, I'm going to use a getter in the JavaScript to expose the name. So

return the user.data.fields.name.value.

So once this user object is populated, it's going to have a property called data.

That's, that's going to have a sub property called fields. And that one of those fields will be name because we asked for and we want the value from that field. So if I deploy these to the scratch org.

Refresh the page

That is not what I was expecting.

oh, silly. Have to put get before method.

it is a little odd that it behaved that way, but

let's redeploy this, refresh the page. See how long this takes.

Now there's probably going to be an error. And that's why there's probably delay. It's probably having difficulties evaluating the object.

So let's wait a moment see it pops up.

Doesn't look like it's going to pop up. So what I want to do is, here.

I'm making a lot of assumptions on the user object that all these values exist.

So, one, one thing that I was experiencing before is I was getting fields wasn't valid value.

So we took two fields with null or undefined

we couldn't evaluate the name or the value. So it would just error out. To get around that, this was the fun little thing I did.

So if the user and the user.data and the user.data.fields and the user.data.fields.Name

and one too many. So if there's a user checks to see if there's, and if there's data checks if there's fields if there's fields or checks if there's names if there's a name that checks if there's a value, and only then does it return that value.

Because this is a better we always need to return something.

And I'm just going to return an empty string. I know this doesn't end here to just having one returned back. So rather that why don't I just have a returnValue and then I will return the returnValue. And I will set this only after all those are met.

There, now we have returned, we have one return path. So you can't necessarily get confused by where the phone is going because there's only one way that makes it this method.

The other thing is this is only being changed if all these conditions are met.

So I'm getting tired of saying user.data.fields.Name.value.

So we're just going to deploy this.

Now you see, on first load, you have nothing to report the display the user name.

Back is when the era was before the wire service had a chance to return anything it was trying to evaluate it. And because it was user wasn't populated, there was no data and there was no fields and there was no name. So a couple null checks and we are ready to go. But I got a couple extra fields here. So

I'm going to copy some things three times.

So this first one I'm doing email, and then I will do company name. And then I will do phone. That'll make it a little less errors now for email, I will change the name to email and for company name I don't want a capital C because that's not the JavaScripty way.

Checking your name, company name

And for phone same deal, cahnge teh name to phone.

Save these, but

Now let's deploy this

Refresh over here.

See all our wonderful values here, there's the name, phone number, company email address. But because we are using this, or and it looks like we're just verifying that we got the data.

But what I want to do is actually get rid of the lightning record view for, so I will delete this and I will delete that.

That is going to cause an issue up here we're using lightning output field.

Copy the company name just don't have to type so much

paste it in here and we also use the lightoutput field here.

did not format properly.

save it, redeploy.

Refresh

and it is no longer using the lighting data service.

It does look like the formating changed a little I think it's because the lighting output field had a different format to it and this has a header applied to it.

I'm not too worried because we're just playing around. So that was getting data using the wire data service and exposing it in our lightning web component.

## Links

- [Just Some Apps](https://justsomeapps.com/)
- [Patreon.com/BrettMN](https://www.patreon.com/BrettMN)
- [https://github.com/BrettMN/lwc-posts/tree/master/force-app/main/default/lwc/firstComponentWireService](https://github.com/BrettMN/lwc-posts/tree/master/force-app/main/default/lwc/firstComponentWireService)

## That’s it for now.

Remember to sign up for **[The Weekly Stand-Up!](https://wipdeveloper.wpcomstaging.com/newsletter/)**  and you can get updated with any new information we have on WIPDeveloper.com.
