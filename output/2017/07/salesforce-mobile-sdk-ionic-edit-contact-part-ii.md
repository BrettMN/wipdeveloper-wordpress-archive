---
layout: "post.11ty.js"
title: "Salesforce Mobile SDK and Ionic – Edit Contact Part II"
date: "2017-07-25"
tags: 
  - "Blog"
  - "Cordova"
  - "IonicFramework"
  - "Salesforce"
  - "SalesforceDeveloper"
slug: "salesforce-mobile-sdk-ionic-edit-contact-part-ii"
coverImage: "mobile-16-header.png"
---

[Previously](https://wipdeveloper.wpcomstaging.com/2017/07/20/saleforce-mobile-sdk-ionic-edit-contact-part/) we updated our `ContactServiceProvider` to  have an `updateContact` method.  Created our `contactEdit` page and worked out the `contact-edit.html`.  Now we need to update the logic for the `contactEdit` component and provide a way to navigate to it.

## Update `contact-edit.ts`

For the `contactsEdit` component's logic we will need to have references to  the `ContactDetailsPage` component and the `ContactsServiceProvider` so we will need to use `import` statements to get those references.  The `ContactsServiceProvider` will be passed into the constructor and we can use the `private` or `public` key word to save a reference to it in the class.  I will call the `ContactsServiceProvider`  reference `service`.

#### Import Statements

import { ContactDetailsPage } from '../contact-details/contact-details';
import { ContactsServiceProvider } from '../../providers/contacts-service/contacts-service';

#### Class `constructor`

constructor(
  public navCtrl: NavController,
  public navParams: NavParams,
  public viewCtrl: ViewController,
  private service: ContactsServiceProvider
) { }

In the class we will need a property to hold a reference to the `contact` we want to edit, so create a property for that purpose,  I will call mine `contact` but feel feel to be creative.

> I'm kidding instead of being creating with the naming of properties, methods and so on try to be descriptive of what the property represents or what the method does.  This will help you, or the next person, when you have to come back to a project after months away.

#### `contact` Property

contact: any;

In the `ionViewDidLoad` method let's get the contact from the `this.navParams` by using the `get` method passing in the name of the parameter we want to access.  You may be thinking that you can only pass simple objects (numbers, strings, or Boolean values) as a parameter but since we are using Angular we can pass an object as a parameter or in this case access an object that was passed as a parameter.

#### Update `ionViewDidLoad` Method

ionViewDidLoad() {
  console.log('ionViewDidLoad ContactEditPage');

  this.contact = this.navParams.get('contact');
}

Now we need a method to save the changes.  How about we call it something like `udpateContact`?  This will call the `updateContact` method on the  `service` we have a reference to.  In the promise we will log the results with a `console.log`  and then we will push  the reference to the `ContactDetailsPage` onto the `navCtrl` with and object that has an `id` that's value is the `this.contact.id`.  We will do this to when the `ContactDetailsPage` loads again it will have a fresh copy of the `contact` with our updates.

#### `updateContact` Method

updateContact() {
  this.service.updateContact(this.contact)
    .then(results => {
      console.log(results);
      this.navCtrl.push(ContactDetailsPage, { "id": this.contact.Id });
    });
}

The last thing we will need is a method to call the `viewCtrl.dismiss` method.  This will be so we can dismiss the `EditContactsPage` when we load it as a modal.

> I may have forgotten to mention that we are making the `EditContactPage` component to we can load it in a modal... Surprise!

#### Complete contact-edit.ts

import { Component } from '@angular/core';
import { IonicPage, NavController, NavParams, ViewController } from 'ionic-angular';

import { ContactDetailsPage } from '../contact-details/contact-details';
import { ContactsServiceProvider } from '../../providers/contacts-service/contacts-service';

@IonicPage()
@Component({
  selector: 'page-contact-edit',
  templateUrl: 'contact-edit.html',
})
export class ContactEditPage {

  contact: any;

  constructor(
    public navCtrl: NavController,
    public navParams: NavParams,
    public viewCtrl: ViewController,
    private service: ContactsServiceProvider
  ) { }

  ionViewDidLoad() {
    console.log('ionViewDidLoad ContactEditPage');

    this.contact = this.navParams.get('contact');
  }

  updateContact() {
    this.service.updateContact(this.contact)
      .then(results => {
        console.log(results);
        this.navCtrl.push(ContactDetailsPage, { "id": this.contact.Id });
      });
  }

  dismiss() {
    this.viewCtrl.dismiss();
  }

}

## Conclusion

Now that we have all the logic ready to edit a contact  let's try calling it next time.

Don’t forget to sign up for [**The Weekly Stand-Up!**](https://wipdeveloper.wpcomstaging.com/newsletter/) to receive free the [WIP Developer.com](https://wipdeveloper.wpcomstaging.com/) weekly newsletter every Sunday!

Looking for the code and want to follow along?  Find it on [GitHub.com/BrettMN/salesforce-sdk-mobile-with-ionic-starter](https://github.com/BrettMN/salesforce-sdk-mobile-with-ionic-starter)
