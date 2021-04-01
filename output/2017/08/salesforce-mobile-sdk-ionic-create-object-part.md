---
layout: "post.11ty.js"
title: "Salesforce Mobile SDK and Ionic - Create Object Part I"
date: "2017-08-09"
tags: 
  - "Blog"
  - "Cordova"
  - "IonicFramework"
  - "Salesforce"
  - "SalesforceDeveloper"
slug: "salesforce-mobile-sdk-ionic-create-object-part"
coverImage: "Screen-Shot-2017-08-13-at-11.42.24-PM.png"
---

Since we worked through our [issue with updating a contact](https://wipdeveloper.wpcomstaging.com/2017/08/07/salesforce-mobile-sdk-ionic-troubleshooting-last-step/) we should try to add a new one.  To do this we are going to repurpose our [`edit-contact` component](https://wipdeveloper.wpcomstaging.com/2017/07/20/saleforce-mobile-sdk-ionic-edit-contact-part/) so that is can also create a contact.

## Update `contact-edit.ts`

One of the first things we should do it rename our `updateContact` method since we will be using it for saving new contacts as well.  I feel that the name `saveContact` would sufficiently conveys that the method serves to save the contact for the purpose of updating or creating.   When we change this name we will need to update the button click as well in the html template.

The other thing we will need is to add an or (`||`) assignment of an empty object (`{}`) to the `this.contact` in the `ionViewDidLoad` fir when the `nav.Params` doesn't have a contact.

#### Or Assigning Empty Object

this.contact = this.navParams.get('contact') || {};

And while we are here let's update line `31`, the call to the `service` to udpate the contact

#### From

this.service.updateContact(this.contact)

#### To

this.service.saveContact(this.contact)

We will be updating the service shortly so it's method name reflects it's new use shortly.

> While we were updating the `edit-contact.ts` I noticed that I had forgot to put labels in the `edit-contact.html` for the different fields.   I have added them at this time.

## Update `contact-service.ts`

Well I think I mention updating the service... let's do that now.   First let's rename the `updateContact` method to `saveContact` as we will be adjusting the service to save a contact if it is new or update an existing one.

The next thing we will do it in our newly renamed `saveContact` method is check if the contact has an `ID` and if it does preform the `update` method like we were.  If it does not have an `Id` we will preform a `create` method.   Otherwise the rest should look pretty similar to what we had before.

#### Update `saveContact` Method

updateContact(
  contact:
    {
      Id: string,
      FirstName: string,
      LastName: string,
      Email: string,
      MobilePhone: string,
      Name: string
    }
) {

  if (contact.Id) {

    delete contact.Name;

    return new Promise(function (resolve, reject) {

      force.login(function () {
        console.log('auth success');
        force.update('contact',
          contact,
          function (result) {
            console.log('update success');
            console.log({ result });
            resolve(result);
          }),
          function (result) {
            console.log('update failed');
            console.log({ result });
            reject(result);
          }
      });

    });
  } else {
    
    return new Promise(function (resolve, reject) {

      force.login(function () {
        console.log('auth success');
        force.create('contact',
          contact,
          function (result) {
            console.log('create success');
            console.log({ result });
            resolve(result);
          }),
          function (result) {
            console.log('create failed');
            console.log({ result });
            reject(result);
          }
      });

    });
  }
}

Now we should make this show up somewhere... maybe the list of contacts would be a good place to start the process to add a new one.

## Conclusion

Don’t forget to sign up for [**The Weekly Stand-Up!**](https://wipdeveloper.wpcomstaging.com/newsletter/) to receive free the [WIP Developer.com](https://wipdeveloper.wpcomstaging.com/) weekly newsletter every Sunday!

Looking for the code and want to follow along?  Find it on [GitHub.com/BrettMN/salesforce-sdk-mobile-with-ionic-starter](https://github.com/BrettMN/salesforce-sdk-mobile-with-ionic-starter)
