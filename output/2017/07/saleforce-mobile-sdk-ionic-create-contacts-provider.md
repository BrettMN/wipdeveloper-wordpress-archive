---
layout: "post.11ty.js"
title: "Saleforce Mobile SDK and Ionic – Create Contacts Provider"
date: "2017-07-13"
tags: 
  - "Blog"
  - "Cordova"
  - "IonicFramework"
  - "Salesforce"
  - "SalesforceDeveloper"
slug: "saleforce-mobile-sdk-ionic-create-contacts-provider"
coverImage: "mobile-10-header.png"
---

[Last time](https://wipdeveloper.wpcomstaging.com/2017/07/11/saleforce-mobile-sdk-ionic-create-contacts-page/) we added a Contacts page.  And while it loads it doesn't show anything yet.  We could add all the logic for talking to Salesforce in the controller for the view like we did with the [Home page list of Users](https://wipdeveloper.wpcomstaging.com/2017/07/10/saleforce-mobile-sdk-ionic-adding-ionic-mobile-sdk-part-iv/) but I think we will need to do more than just load the contacts so lets create a separate place to keep that logic.  We will use a "Provider".

## Providers

In Ionic Providers are a way to inject additional functionality into a component.  They allow us to separate our logic that is needed for display and our logic that is needed for communicating with Salesforce.  In other languages they may be called services, or injectables since they provide a "service",  or are "injected".  In our case we will need one to separate out the logic for talking back and forth with Salesforce about Contacts.  So we can create a Provider with the Ionic CLI.

> This provider we are going to create is going to be similar to the service we created back in [Visualforce and Angular – Add a Component and Service](https://wipdeveloper.wpcomstaging.com/2017/04/27/visualforce-and-angular-add-a-component-and-service/)

## Create ContactsService Provider

#### `ionic generate provider contactsService`

PS D:\\Workspace\\Blog\\salesforce\\ionic\\ionicContacts> ionic generate provider contactsService
\[OK\] Generated a provider named contactsService!
PS D:\\Workspace\\Blog\\salesforce\\ionic\\ionicContacts>

This creates a TypeScript file at `src/providers/contacts-service/` with the name of `contacts-service.ts`

#### Default Provider

import { Injectable } from '@angular/core';
import { Http } from '@angular/http';
import 'rxjs/add/operator/map';

/\*
  Generated class for the ContactsServiceProvider provider.

  See https://angular.io/docs/ts/latest/guide/dependency-injection.html
  for more info on providers and Angular DI.
\*/
@Injectable()
export class ContactsServiceProvider {

  constructor(public http: Http) {
    console.log('Hello ContactsServiceProvider Provider');
  }

}

Since we are going to be using ForceJS to make our calls to Salesforce we will need to import it, I will do that at line `5`.   Then lets add a method called `loadContacts` to, guess what, load some contacts.

#### `loadContacts`

loadContacts(){
  let oauth = OAuth.createInstance();

  return oauth.login()
    .then(oauthResult => {
      let service = DataService.createInstance(oauthResult);

      return service.query('SELECT Id, Name FROM Contact LIMIT 50');

    });
}

## Conclusion

That;s all we have for our `contacts-service` right now.  Let's put it to use next time.

Don’t forget to sign up for [**The Weekly Stand-Up!**](https://wipdeveloper.wpcomstaging.com/newsletter/) to receive free the [WIP Developer.com](https://wipdeveloper.wpcomstaging.com/) weekly newsletter every Sunday!
