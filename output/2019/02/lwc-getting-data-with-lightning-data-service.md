---
layout: "post.11ty.js"
title: "LWC - Getting Data with Lightning Data Service"
date: "2019-02-18"
tags: 
  - "Blog"
  - "LWC"
  - "Salesforce"
  - "SalesforceDeveloper"
  - "SalesforceDX"
slug: "lwc-getting-data-with-lightning-data-service"
coverImage: "Screen-Shot-2019-02-22-at-4.14.37-PM.png"
---

* * *

Hello, I'm Brett with WIPDeveloper.com. So far with our first lightning web component, we have only gotten markup and some communication between the HTML and the JavaScript file and we haven't done any actual communications with Salesforce. Since we're building to use our components in Salesforce, we're going to need to be able to actually access data that's hosted there.

## Using Lightning Data Service

So we're going to take a look at using the lightning data service. To get information for our component. What I want to do is, instead of hard coding in the label in the JavaScript file, I want to get that as the company name from the user that's logged in and do that we're going to first need to get the User Id

in the JavaScript file. We can import the user id from`@salesforce/user/id`

Now we have that access to that. But we need to expose it in our app. So what I'm going to do is have `id` here and I'm going to just assign the `userId` to it. If I add in reference to the `id` in the markup, I should be able to get the mark `id` for the current user. At the very bottom here, I am going to just add paragraph tag, that tells me that it's the user id.

Now, this is going to be the `id` of the user who's logged in. I'm going to push this real quick.

Go back here, refresh it and I should see…

Going to refresh it and clear out the cache and I should see the ID at the bottom. There we go, user ID.

Now to use the Lightning Data Service we have to we are going now to use the Lightning Data Service we're going to use the `lightning-record-view-form` to get the user information.

Auto complete helps a lot here `lightning-record-view-form` and then we provide it a `record-id`

and we have provided an `object-api-name` that is not ready for a save

and rather than closing it out here I want to put the

wrap the entire thing. Now the entire component we have is now wrapped in as a `lightning-record-view-form` we can use the `ightning-output-field` in place of

yeah `ightning-output-field` and provide it a `field-name` of `CompanyName`.

Now we're also add this so that it is used instead of the label.

Now when we deploy this,

we can come back to our UI press refresh.

And I broke something.

What did I mess up?

Okay, so I see the issue. We're going to read it here

except up here. We're going to actually spell out `record-id`.

I had misspelled `record-id`.

Redeploy, refresh.

Remember, clear the cache and refresh.

What happened is, I had misspelled `record`, so don't do that

Redeploying and refreshing we now have access to our company name. Let's see if we can get rid of where it says company name though, just in case we don't want that. So to make it so that we don't have a company name, what we do is add `variant`.

And we will use the variant of `label-hidden`

And we are going to add that to both of them.

Remove the user ID from the bottom and the name at the bottom to just get all deployed at once.

Refresh the page.

There. Now this is coming from the user who's logged in. Can we prove that it's coming from the user that's logged in? Well, let's go to our settings and update our company name.

What's out a few exclamation marks, because, why not?

Now go back to home

refresh.

Something broke. There it is. took a moment to load up. So there you go. We're now getting our company name using the lightning data service.

## That’s it for now.

Remember to sign up for **[The Weekly Stand-Up!](https://wipdeveloper.wpcomstaging.com/newsletter/)**  and you can get updated with any new information we have on WIPDeveloper.com.
