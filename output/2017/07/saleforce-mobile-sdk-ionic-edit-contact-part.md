---
layout: "post.11ty.js"
title: "Saleforce Mobile SDK and Ionic – Edit Contact Part I"
date: "2017-07-21"
tags: 
  - "Blog"
  - "Cordova"
  - "IonicFramework"
  - "Salesforce"
  - "SalesforceDeveloper"
slug: "saleforce-mobile-sdk-ionic-edit-contact-part"
coverImage: "mobile-15-header.png"
---

Now that we can [view a Contacts Details](https://wipdeveloper.wpcomstaging.com/2017/07/19/saleforce-mobile-sdk-ionic-display-contact-details/) we should come up with a way to edit them.  Let's set something up to handle editing now.

## Update `ContactServiceProvider`

To edit a `contact` we will need some way to tell Salesforce of our changes.  Since we are collecting all our calls to Salesforce in the `ContactsServiceProvider` let's add a new method called `updateContact`.   This new method will take one parameters called `contact` and I'm going to give it a type of  `{ Id: string, FirstName: string, LastName: string, Email: string, MobilePhone: string }`.

> What that type means is `contact` will be an object with properties named `Id`, `FirstName`, `LastName`, `Email`, and `MobilePhone` all of type `string`.

Then we will get an instance of the `oAuth` and use it's `login` method, and creating an instance of the `DataService` with the results.  All so we can call `service.update` passing in the name of the object to update and the object that contains the updates.

It should look somewhat like this:

#### `updateContact` Method

updateContact(contact: { Id: string, FirstName: string, LastName: string, Email: string, MobilePhone: string }) {
  let oauth = OAuth.createInstance();

  return oauth.login()
    .then(oauthResult => {
      let service = DataService.createInstance(oauthResult);

      return service.update('Contact', contact);

    });
}

With the call to Salesforce ready we can create the page that will make use of it.

## Create `contactEdit` Page

Lets create a page to handle editing a contact called `contactEdit`.  So let's call `ionic generate page contactEdit`  and get started.

We will use the `contactEdit` page to edit the `FristName`, `LastName`, `Email`, and `MobilePhone`.  We will use the Angular `[(ngModel)]=""` binding, sometimes referred to as a "banana in a box",  to use "2 way data flow" or "2 way binding".  This will allow us to set the original value of the input field and update the view model when we make changes.

We will also only show the form when we have a `contact` to prevent it from having rendering errors similar to what we did on the [`contact-details.html`](https://wipdeveloper.wpcomstaging.com/2017/07/19/saleforce-mobile-sdk-ionic-display-contact-details/).

There are going to be two buttons on the html template, one in the `ion-header` to call a method to dismiss the modal and one in the form to save changes.

Here's the complete html template.

#### Complete `contact-edit.html`

<ion-header>
  <ion-toolbar>
    <ion-title>
      Edit Contact
    </ion-title>
    <ion-buttons start>
      <button ion-button (click)="dismiss()">
        <span ion-text color="primary" showWhen="ios">Cancel</span>
        <ion-icon name="md-close" showWhen="android, windows"></ion-icon>
      </button>
    </ion-buttons>
  </ion-toolbar>
</ion-header>

<ion-content padding>
  <form \*ngIf="contact">
    <label for="FirstName"></label>
    <input type="text" id="FirstName" \[(ngModel)\]="contact.FirstName" name="FirstName">
    <label for="LastName"></label>
    <input type="text" id="LastName" \[(ngModel)\]="contact.LastName" name="LastName">
    <label for="Email"></label>
    <input type="text" id="Email" \[(ngModel)\]="contact.Email" name="Email">
    <label for="MobilePhone"></label>
    <input type="text" id="MobilePhone" \[(ngModel)\]="contact.MobilePhone" name="MobilePhone">
    <button ion-button (click)="updateContact()">Save</button>
  </form>
</ion-content>

## Conclusion

We'll get the rest setup next time.  Think you can figure out what is needed before then?

Don’t forget to sign up for [**The Weekly Stand-Up!**](https://wipdeveloper.wpcomstaging.com/newsletter/) to receive free the [WIP Developer.com](https://wipdeveloper.wpcomstaging.com/) weekly newsletter every Sunday!

Looking for the code and want to follow along?  Find it on [GitHub.com/BrettMN/salesforce-sdk-mobile-with-ionic-starter](https://github.com/BrettMN/salesforce-sdk-mobile-with-ionic-starter)
