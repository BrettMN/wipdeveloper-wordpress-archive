---
layout: "post.11ty.js"
title: "Salesforce Mobile SDK and Ionic – Plugins Part III"
date: "2017-10-02"
tags: 
  - "Blog"
  - "Cordova"
  - "IonicFramework"
  - "Salesforce"
  - "SalesforceDeveloper"
slug: "salesforce-mobile-sdk-ionic-plugins-part-iii"
coverImage: "Screen-Shot-2017-10-02-at-12.06.15-AM.png"
---

Now that we have done all the setup steps to install and provide easier access a plugin using it should be easier.  Let's set up our app to provided a way to email a contact from the action sheet on the Contact Details page.

## Update `Contact-details.ts`

To get access to the plugin we will need to import the Ionic Native Wrapper for the `EmailComposer` so we can use it.

#### Update Imports

import { EmailComposer } from '@ionic-native/email-composer';

We will also need to add it to the constructor so that an instance is availible in our class.

#### Update `constructor`

constructor(
  public navCtrl: NavController,
  public navParams: NavParams,
  public modalCtrl: ModalController,
  private service: ContactsServiceProvider,
  public alertCtrl: AlertController,
  public actionSheetCtrl: ActionSheetController,
  public platform: Platform,
  private emailer: EmailComposer
) { }

After that is done we can add an additional Action after `'Edit'` but before `'Cancel'`  in our `showActions` method.

For our new Action let's give it some `text` that makes people think of sending email... something like `'Email'`.  We can also provide an `icon` similar to what we did with `'Delete'` having a trash can and `'Edit'` using the wrench on iOS  but once again we should try and find something that makes people think of sending email... how about we try the `mail` icon?

For the `handler` we will create an object that has properties for `to`, `subject`, `body`, and `isHtml`.  For `to` we will use the current contacts `email`.  For `subject` let's use a string that says `Hello` and the first name of the contact.  For the `body` we can send a test message now and use the `lastName`, `firstName`, and `email` just to get more practice using the current contact information.  The `isHtml` property is a true/false flag to tell the email plugin weather our message is html or not, I'm going to go with `false` on this one since we are just trying things out and not trying to get toooooo complicated.

#### New `action`

{
  text: 'Email',
  icon: !this.platform.is('ios') ? 'mail' : null,
  handler: () => {

    actionSheet.onDidDismiss(() => {
          let email = {
            to: this.contact.Email,
            subject: \`Hello ${this.contact.FirstName}\`,
            body: \`This is a test email sent to ${this.contact.LastName}, ${this.contact.FirstName} at email address ${this.contact.Email}.\`,
            isHtml: false
          };
          this.emailer.open(email);
    });
  }
}

With our new new action in place we can select to send an email directly to a contact from the details page for that contact.

## Conclusion

Don’t forget to sign up for [**The Weekly Stand-Up!**](https://wipdeveloper.wpcomstaging.com/newsletter/) to receive free the [WIP Developer.com](https://wipdeveloper.wpcomstaging.com/) weekly newsletter every Sunday!

Looking for the code and want to follow along?  Find it on [GitHub.com/BrettMN/salesforce-sdk-mobile-with-ionic-starter](https://github.com/BrettMN/salesforce-sdk-mobile-with-ionic-starter)
