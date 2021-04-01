---
layout: "post.11ty.js"
title: "Salesforce Mobile SDK and Ionic – Offline – SmartStore Saving Data"
date: "2017-12-14"
tags: 
  - "Blog"
  - "Cordova"
  - "IonicFramework"
  - "Salesforce"
  - "SalesforceDeveloper"
slug: "salesforce-mobile-sdk-and-ionic-offline-smartstore-saving-data"
coverImage: "Screen-Shot-2017-12-14-at-11.52.18-PM.png"
---

Since we have [setup our SmartStore Soup](https://wipdeveloper.wpcomstaging.com/2017/12/11/salesforce-mobile-sdk-and-ionic-offline-smartstore-setup/) we should probably store something in it so it can start providing value... or values.

## Populate SmartStore Soup

To get things started we are going to store the some contact information.  Instead of writing something new to get contacts from Salesforce we can `import` our `contact-service`

#### `import` `ContactsServiceProvider`

import { ContactsServiceProvider } from '../contacts-service/contacts-service'

We will also have to add it to the `constructor` so it is instantiated correctly.

#### Update `constructor`

constructor(private contactsService: ContactsServiceProvider) {

> With the `private` keyword prefacing a parameter of the `constructor` we don't have to save it to an instance property ourselves TypeScript will do that for us.

Now we can create a method that will load contacts into our Soup by using our `contactsService`'s `loadContacts` method to get the contacts.  I will be calling my method  `fillSoup`. and it will call the `contactsService.loadContacts` method.

In the promise resolution, `then`,  we will create 2 callbacks to pass in when we fill our Soup: one for success and and one for failure.  These callbacks will log a message to the console that contains the items or error that they were called with.

We will also use our `private` `smartStore` method to get the SmartStore plugin so we can call `upsertSoupEntries` with our `soupName`, `records` and callbacks.

It will look something like this.

#### `fillSoup` Method

fillSoup() {

  return this.contactsService.loadContacts()
    .then(results => {

      let success = (items) => console.log(\`Items upserted to Soup: ${items}\`)

      let failure = (error) => console.error(\`Soup Upsert Error: ${error}\`)

      this.smartStore().upsertSoupEntries(this.soupName, results.records, success, failure)
    })

}

Now we just need to access the data and we could say our app does "Offline".

## Conclusion

Don’t forget to sign up for [**The Weekly Stand-Up!**](https://wipdeveloper.wpcomstaging.com/newsletter/) to receive free the [WIP Developer.com](https://wipdeveloper.wpcomstaging.com/) weekly newsletter every Sunday!
