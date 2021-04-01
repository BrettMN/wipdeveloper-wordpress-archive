---
layout: "post.11ty.js"
title: "Saleforce Mobile SDK and Ionic - Query Contacts"
date: "2017-07-18"
tags: 
  - "Blog"
  - "Cordova"
  - "IonicFramework"
  - "Salesforce"
  - "SalesforceDeveloper"
slug: "saleforce-mobile-sdk-ionic-query-contacts"
coverImage: "mobile-12-header.png"
---

Now that we have a [provider called `contacts-service.ts`](https://wipdeveloper.wpcomstaging.com/2017/07/12/saleforce-mobile-sdk-ionic-create-contacts-provider/) and our app is [freshly updated](https://wipdeveloper.wpcomstaging.com/2017/07/13/saleforce-mobile-sdk-ionic-update-mobile-sdk/) lets use ForceJS to query for the contacts to display on our [Contacts page](https://wipdeveloper.wpcomstaging.com/2017/07/11/saleforce-mobile-sdk-ionic-create-contacts-page/).

## Create a Query

Like when we added our [user query to the Home page](https://wipdeveloper.wpcomstaging.com/2017/07/06/saleforce-mobile-sdk-ionic-adding-ionic-mobile-sdk-part-iii/) to verify things were set up we will need to import ForceJs into the `ContactsServiceProvider` class.  So let's open up  [`src/providers/contacts-service/contacts-service.ts`](https://wipdeveloper.wpcomstaging.com/2017/07/12/saleforce-mobile-sdk-ionic-create-contacts-provider/) and get started.

#### Original `contacts-service.ts`

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

Above is the complete `contacts-service.ts` just so you know what we start with.  I am going to be removing the `import` of `Http` since we will be using ForceJS and the Salesforce Mobile SDK to handle communication with Salesforce.   So feel fee to delete it at line `2` and where it is injected to the `constructor` at line `15`.

Now let's add an import of `OAuth` and `DataService` from `'forcejs'` , I will do it at line `5` but feel free to add at line `2` or `4` or where ever.

Then let's create a method named `loadContacts`.  In case you are wondering we will use this method to get an instance of the `oAuth` to login with, then create an instance of the `dataService` that we can use the `query` method of to get data from Salesforce.  If will look something like this:

#### `loadContacts` Method

loadContacts(){
  let oauth = OAuth.createInstance();

  return oauth.login()
    .then(oauthResult => {
      let service = DataService.createInstance(oauthResult);

      return service.query('SELECT Id, Name FROM Contact LIMIT 50');

    });
}

## Conclusion

With this method in place lets update our Contacts page component and html template next time.

Don’t forget to sign up for [**The Weekly Stand-Up!**](https://wipdeveloper.wpcomstaging.com/newsletter/) to receive free the [WIP Developer.com](https://wipdeveloper.wpcomstaging.com/) weekly newsletter every Sunday!

Looking for the code and want to follow along?  Find it on [GitHub.com/BrettMN/salesforce-sdk-mobile-with-ionic-starter](https://github.com/BrettMN/salesforce-sdk-mobile-with-ionic-starter)
