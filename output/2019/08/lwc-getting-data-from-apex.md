---
layout: "post.11ty.js"
title: "LWC - Getting Data from Apex"
date: "2019-08-14"
tags: 
  - "Blog"
  - "JavaScript"
  - "LWC"
  - "Salesforce"
  - "SalesforceDeveloper"
  - "SalesforceDX"
slug: "lwc-getting-data-from-apex"
coverImage: "Screen-Shot-2019-08-16-at-3.20.12-PM.png"
---

* * *

Hi, I'm Brett with WIPDeveloper.com. Last time we learned about getting data using the wire service so that we could get information from Salesforce without having to write any server side code or Apex. This time, we're going to take a look at retrieving data from Salesforce by calling an Apex class and having it return the data in a format that we want.

To start with, I have duplicated the component that we had at the end of using the wire service. And it looks the same because it's exactly the same right now. And we will start by changing the only HTML change between the two. We are going to change using wire service to using Apex.

And we'll save that deploy, make sure that we do have two different components on the page.

Looks like it's done.

So there we go, the bottom one is using Apex, or it will be.

So we don't need to make any other changes with the HTML. So we'll close that out. Before we get started with the JavaScript file, let's take a look at the class we're going to use, we're going to use a class called firstComponentController.

It declares one static method called `init`, and it has decorated with the aura enabled and is using cachable equals true.

It's going to return this map that is a string and object and we query for the user ID that's provided. Or we query for the user ID that we get from user info dot get user ID. And if we do find the user, we add that to the return object as the user and then we set the success to true and we return theuser object. So that's all that apex, it's pretty simple. You probably need more than this in your own code.

Now to access that in the lightning web component, we are going to get rid of `getRecord` because we aren't going to use that what we will use is we use,

we will import

`init` actually from Salesforce Apex

first component init.

Just there you saw me using the autocomplete for that is part of the Visual Studio Code plugins. So I don't have to type the whole thing out with did some of the work for me. And we use `init` instead of the he `getrecord` handler.

And we don't need, we're going to actually get rid of all that.

We will pass that into our wire handler. And then we'll have that decorate the method. We're going to call it `handleInit`.

And we'll have it deconstruct the results so that we can get the error

and the data.

Whoops, did not be the type out the data.

And in this function, we will just

Well, what do we want to do? I like to add a little. Since we're playing around with it, I'm going to add a window console log here.

So when we're looking at it in the debug statements, we can know where it was.

And I'm going to pass in the air and the data so that those are logged out.

Now, first thing we should do is actually check to see if there is an error.

So we'll use

if error which, which JavaScript is.

If that object exists, it'll behave. It'll act like a true statement and go into this section of code. And we're going to just log it to the console.

And it would help if I could spell.

And then we will.

We're going to do else/if.

Else if there's data, we're going to set the data on.

We don't have a user yet. We can get rid of the userID, but

this.user

data dot user

and what do we do if that's not right?

Let's just add a little final statement,

just let us know that we got to the wrong part of the code.

Do here, else is spelled wrong.

There we go. So now when the wire service calls `init` in our Apex code, the handler is going to

log the error message and the data object at the start of the method. And then we'll check if there's an error message because most likely, this will end up as a null in the console. But it'll log, something went wrong to the browser console window. If nothing goes wrong, and there is data, we set the data dot user onto the this class. Let's get rid of the user ID right now.

We set the user in this class so that we can access it in the template. And then we, if there's no error and there's no data, start wonder what's going on. Just most likely, that will never happen.

One thing that's different

is we don't actually need all these checks when we want to do because we don't have user data that fields named value to go down. What we want to do is just check

we got so what we're doing here is we're checking to see if

does this user exist? If does we return the user name, otherwise, we return an empty string

And we do that so that

we're just checking this so we don't accidentally try going for the name when the before the users populated because that could throw errors and just be easier if we don't do that. And now let's see if we have it in.

deploy this to Salesforce.

See if we get a name that's not look like we have a name. What did we do wrong?

Oh, let's go to think we need to track this. So a tracking decorator on the user. And that means we have to import it.

So we import it from LWC. And we decorate the user and will deploy this

Let's see if this loads first.

Here we go, are we have our users name, we don't have the rest of the values because right now we are still checking for the user data fields on all the others.

I'm going to copy and paste the return statement from the name so that it's

no, let me just have to just copy and paste that over and over versus typing it out every time.

And right now, that means all of them would be name, but we don't want to

change the email one. If I could spell correctly to email, and the company name to

you guessed that company name. And don't hold on for the suspense. But phone is going to return the user phone.

deploy this, go back to our page and refresh it.

There you go. We have our company name at the top. We have the username, the fake phone number.

WIPdeveloper.com is the company name again, and the email address of the user. So we're returning the same values from our Apex controller as we have seen them on the screen using the same template except for updating the label as we used for the wire service. So that's pretty slick. Of course we aren't using built in functionality for from Salesforce anymore. So we will have to be responsible for maintaining any changes that we with how that logic is handled.

## That’s it for now.

Remember to sign up for **[The Weekly Stand-Up!](https://wipdeveloper.wpcomstaging.com/newsletter/)**  and you can get updated with any new information we have on WIPDeveloper.com.
