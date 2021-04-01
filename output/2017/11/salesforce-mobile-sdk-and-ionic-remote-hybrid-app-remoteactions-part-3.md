---
layout: "post.11ty.js"
title: "Salesforce Mobile SDK and Ionic – Remote Hybrid App – RemoteActions Part 3"
date: "2017-11-27"
tags: 
  - "Blog"
  - "Cordova"
  - "IonicFramework"
  - "Salesforce"
  - "SalesforceDeveloper"
slug: "salesforce-mobile-sdk-and-ionic-remote-hybrid-app-remoteactions-part-3"
coverImage: "Screen-Shot-2017-11-28-at-4.52.32-PM.png"
---

Since we have [updated our `contacts-service` to use RemoteActions](https://wipdeveloper.wpcomstaging.com/2017/11/20/salesforce-mobile-sdk-and-ionic-remote-hybrid-app-remoteactions-part-2/) instead of ForceJS we will have to make a couple changes to our app to make use of the results of the RemoteActions since they are not formed the same as when the requests go through ForceJS.

## Find What to Fix

First thing we will need to do is find what needs to be updated.  There are 2 places that we will need to update.  If I hadn't been lazy and I properly defined the types that the methods would return we could run `npm run build` or look at the "Problems" area of our IDE, if it has one, and find those places pretty easily.

To make this that easy lets change the promise results of `any` in our `contacts-service` to return a specific type.  In this case we will define a `Contact` type and use that.

> I am going to define the `Contact` class in the same file as the service since it's going to be pretty small.  If it grows beyond a declaration of some properties I will move it to it's own file.

Near the top of your `contacts-service` add the following:

#### `Contact` Class

class Contact {
  Id: string;
  FirstName: string;
  LastName: string;
  Email: string;
  MobilePhone: string;
  Name: string
}

This is the same type definition we had used to define the `contact` parameter that is passed into `saveContact` so we can update that type to use the `Contact` class as well.

#### `loadContacts` Before

loadContacts() {
  return new Promise<any>((resolve, reject) => {
    this.callRemote('ContactMobileAppController.GetContacts', \[\], resolve, reject)
  })
}

You can see we are return a `Promise` that has a type of `<any>`.  If we replace `<any>` with an array of `Contact` we will get an error with our TypeScript.  And array of `Contact` looks like this btw `<Array<Contact>>`.

#### `loadContacts` After

loadContacts() {
  return new Promise<Array<Contact>>((resolve, reject) => {
    this.callRemote('ContactMobileAppController.GetContacts', \[\], resolve, reject)
  })
}

#### `getContact` Before

getContact(id: string) {
  console.log('getContact called');
  return new Promise<any>((resolve, reject) => {
    this.callRemote('ContactMobileAppController.GetContact', \[id\], resolve, reject);
  })
}

We will do something similar with `getContact` by replacing the `<any>` with `<Contact>` since it returns a promise that's results is one Contact instead of an array.

#### `getContact` After

getContact(id: string) {
  console.log('getContact called');
  return new Promise<Contact>((resolve, reject) => {
    this.callRemote('ContactMobileAppController.GetContact', \[id\], resolve, reject);
  })
}

#### `saveContact` Before

saveContact(
   contact:
     {
       Id: string,
       FirstName: string,
       LastName: string,
       Email: string,
       MobilePhone: string,
       Name: string
     }
  ){

  /// method body

  }

And lets update our `saveContact` method so it looks cleaner and we don't have 2 definitions of `Contact` to maintain.

#### `saveContact` After

saveContact(
  contact: Contact
) { 

   // body stays the same

   }

## Conclusion

Don’t forget to sign up for [**The Weekly Stand-Up!**](https://wipdeveloper.wpcomstaging.com/newsletter/) to receive free the [WIP Developer.com](https://wipdeveloper.wpcomstaging.com/) weekly newsletter every Sunday!
