---
layout: "post.11ty.js"
title: "Salesforce Mobile SDK and Ionic – Styling Actions - Part I"
date: "2017-08-16"
tags: 
  - "Blog"
  - "Cordova"
  - "IonicFramework"
  - "Salesforce"
  - "SalesforceDeveloper"
slug: "salesforce-mobile-sdk-ionic-styling-actions-part"
coverImage: "Screen-Shot-2017-08-18-at-12.35.29-AM.png"
---

We now have the ability to edit and delete Contacts from the Contact Details page and this is good!  Thing is we sort of have it looking like it's a web page with those buttons on the page.  Let's make use of Ionic Frameworks Action Sheets so the option to edit or delete looks more native.

## Update `contact-detail.ts`

First thing we should do it update the `contact-detail.ts`.  Changes we make here are going to allow us to open an Action Sheet from a button in the footer of the `Contact Details` page.  It will give the user an option to edit or delete the contact or cancel the action selection.  This will provided a nicer looking experience for the user that feels more like a native app.

We will also update our `deleteContact` method so that it returns users to the `Contacts` page after the delete is performed.

To make all this happen we will need to update our imports from `'ionic-angular'` to include `ActionSheetController` and `Platform`.  We will also need to import the `ContactsPage` component. 

#### Updated Imports

import { Component } from '@angular/core';
import { IonicPage, NavController, NavParams, ModalController, AlertController, ActionSheetController, Platform } from 'ionic-angular';

import { ContactsPage } from '../../pages/contacts/contacts';
import { ContactEditPage } from '../../pages/contact-edit/contact-edit';
import { ContactsServiceProvider } from '../../providers/contacts-service/contacts-service';

To make use of the `ActionSheetController` and `Platform` we will need to include those in the construtor so they are properly injected to the component when it is created.

#### Updated `constructor`

constructor(
  public navCtrl: NavController,
  public navParams: NavParams,
  public modalCtrl: ModalController,
  private service: ContactsServiceProvider,
  public alertCtrl: AlertController,
  public actionSheetCtrl: ActionSheetController,
  public platform: Platform
) { }

For the `updateContact` method I decided to remove the parameter of `contact` since we already have access to it there doesn't seem to be much sense to pass it to the method.  This also makes it easier to call from the action button we will create later on.   To get access to the `contact` we will updated it to use the `this.contact`.

#### Updated `updateContact` Method

updateContact() {
  let editModal = this.modalCtrl.create(ContactEditPage, { contact: this.contact });

  editModal.present();
}

Now we already had a `deleteContact` method that was working but.... the buttons looked in the wrong order.  To fix that we will need change the oder the buttons are listed in the `buttons` array of the options object the alert is created with.

We will also change the `handler` that we use when the `Yes` button is selected.  The update will use the `navCtrl` to set the root to the `ContactsPage` component we imported earlier.

#### Updated `deleteContact` Method

deleteContact() {
  let confirmDelete = this.alertCtrl.create({
    title: \`Delete Contact?\`,
    message: \`Are you sure you want to delete ${this.contact.Name}?\`,
    buttons: \[
      {
        text: 'No',
        handler: () => {

          confirmDelete.dismiss();
        }
      },
      {
        text: 'Yes',
        handler: () => {
          this.service.deleteContact(this.contact.Id)
            .then((result) => {

              this.navCtrl.setRoot(ContactsPage);
            });
        }
      }
    \]
  });

  confirmDelete.present();
}

## Conclusion?

We are not quiet done but we can finish up the rest next time.

Don’t forget to sign up for [**The Weekly Stand-Up!**](https://wipdeveloper.wpcomstaging.com/newsletter/) to receive free the [WIP Developer.com](https://wipdeveloper.wpcomstaging.com/) weekly newsletter every Sunday!

Looking for the code and want to follow along?  Find it on [GitHub.com/BrettMN/salesforce-sdk-mobile-with-ionic-starter](https://github.com/BrettMN/salesforce-sdk-mobile-with-ionic-starter)
