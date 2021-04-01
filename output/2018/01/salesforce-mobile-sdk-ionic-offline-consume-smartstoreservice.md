---
layout: "post.11ty.js"
title: "Salesforce Mobile SDK and Ionic – Offline – Consume SmartStoreService"
date: "2018-01-02"
tags: 
  - "Blog"
  - "Cordova"
  - "IonicFramework"
  - "Salesforce"
  - "SalesforceDeveloper"
slug: "salesforce-mobile-sdk-ionic-offline-consume-smartstoreservice"
coverImage: "Screen-Shot-2018-01-03-at-9.40.26-PM.png"
---

Since we now have a way to [retrieve our contacts](https://wipdeveloper.wpcomstaging.com/2017/07/17/saleforce-mobile-sdk-ionic-query-contacts/), [save them to a Soup](https://wipdeveloper.wpcomstaging.com/2017/12/13/salesforce-mobile-sdk-and-ionic-offline-smartstore-saving-data/), and [Query the Soup](https://wipdeveloper.wpcomstaging.com/2017/12/18/salesforce-mobile-sdk-and-ionic-offline-smartstore-query-all-data/) let's use that stored data to populate our app instead of making calls the the server with each view load.

## Update Contacts

To get the Contacts view to load all the contacts from our Soup we will need to import our `SmartStoreServiceProvider` into our `contacts.ts`.  We will be using the `SmartStoreServiceProvider` in place of the `ContactsServiceProvider` so I will comment our the later and add in the former.

#### Updated Imports

// import { ContactsServiceProvider } from '../../providers/contacts-service/contacts-service';
import { SmartstoreServiceProvider} from '../../providers/smartstore-service/smartstore-service';

This of course means that we will not be able to use the `ContactsServiceProvider` with our constructor, you know since we removed the import for it.  Instead let's use the `SmartStoreServiceProvider` in the constructor and keep it's name as `service`.

#### Updated `constructor`

constructor(public navCtrl: NavController, public navParams: NavParams, private service: SmartstoreServiceProvider, public modalCtrl: ModalController) {
  }

And ideally that will be the last change we have to make it our `contacts.ts` since our goal will be to make the `SmartStoreServiceProvider` a drop in replacement for the same features that the `ContactsServiceProvider` allowed.  Just with offline capabilities.

## Conclusion

Don’t forget to sign up for [**The Weekly Stand-Up!**](https://wipdeveloper.wpcomstaging.com/newsletter/) to receive free the [WIP Developer.com](https://wipdeveloper.wpcomstaging.com/) weekly newsletter every Sunday!
