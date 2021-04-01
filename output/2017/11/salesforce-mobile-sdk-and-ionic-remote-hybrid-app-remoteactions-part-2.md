---
layout: "post.11ty.js"
title: "Salesforce Mobile SDK and Ionic – Remote Hybrid App – RemoteActions Part 2"
date: "2017-11-20"
tags: 
  - "Blog"
  - "Cordova"
  - "IonicFramework"
  - "Salesforce"
  - "SalesforceDeveloper"
slug: "salesforce-mobile-sdk-and-ionic-remote-hybrid-app-remoteactions-part-2"
coverImage: "Screen-Shot-2017-11-25-at-12.32.55-AM.png"
---

Since we have [setup](https://wipdeveloper.wpcomstaging.com/2017/11/17/salesforce-mobile-sdk-and-ionic-remote-hybrid-app-remoteactions/) our `ContactMobileAppController` we should change our `ContactsServiceProvider` to make use of those RemoteActions.

## Update `ContactsServiceProvider`

Since our app was a working copy of a Local Hybrid app we already have a service provider in place that works.  Because of this we will not create a new one.  Instead let's modify it so that it has the same methods, including parameters and return values, but makes use of RemoteActions instead of ForceJS.

> I'm going to keep a copy of the `ContactsServiceProvider` that uses force.js in a folder called /`contacts-service.forcejs/`.  This way I can switch between the 2 different versions by changing a small portion of the import statement.

We can remove the `import` of the `OAuth` and `DataService` from `forcejs` and the `force` declaration we had.

One thing we will need to do is tell TypeScript about the Visualforce remoting by declaring it.  This will allow us to call the global JavaScript object that is inserted into the page.

#### Declare Visualforce

declare class Visualforce {
  static remoting: { Manager: { invokeAction: any } };
}

To prevent us from re-writting all the setup for calling a remote action I recomend creating a privet method that we can re-use for that purpose.  I like to call mine `callRemote`

#### `callRemote` Method

private callRemote(methodName, params, resolve, reject) {
  console.log(params)
  Visualforce.remoting.Manager.invokeAction(
    methodName,
    ...params,
    function (result, event) {
      console.log({ event })
      console.log({ result })
      if (event.status) {
        resolve(result)
      }
    },
    {
      //Options I am not setting
    }
  );
}

This private method will allow us to make calls to remote actions without having to copy and pastes all the parts that would be the same for each call.

For the rest of the methods we will be replacing the use of the OAuth and DataService with a call to our `callRemote` method.  We do this in a Promise and provide the name of the `RemoteAction` to call, any parameters, along with the `resolve` and `reject` for the promise.

> I will just post the updated methods bellow.  If you have any specific questions feel free to email me brett@wipdeveloper.com or leave a message bellow.

#### Updated `loadContacts`

loadContacts() {
  return new Promise<any>((resolve, reject) => {
    this.callRemote('ContactMobileAppController.GetContacts', \[\], resolve, reject)
  })
}

#### Updated `getContact`

getContact(id: string) {
  console.log('getContact called');
  return new Promise<any>((resolve, reject) => {
    this.callRemote('ContactMobileAppController.GetContact', \[id\], resolve, reject);
  })
}

#### Updated `saveContact`

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
) {

  if (contact.Id) {

    return new Promise((resolve, reject) => {
      this.callRemote('ContactMobileAppController.UpdateContact',
        \[contact.Id, contact.FirstName, contact.LastName, contact.Email, contact.MobilePhone\], resolve, reject);

    });
  } else {

    return new Promise((resolve, reject) => {
      this.callRemote('ContactMobileAppController.NewContact',
        \[contact.FirstName, contact.LastName, contact.Email, contact.MobilePhone\], resolve, reject);

    });
  }
}

#### Updated `deleteContact`

deleteContact(Id: string) {

  return new Promise((resolve, reject) => {
    this.callRemote('ContactMobileAppController.DeleteContact', \[Id\], resolve, reject);
  });
}

With all those changes in place we should be able to make a few small changes in our app and be ready to roll.

## Conclusion

Don’t forget to sign up for [**The Weekly Stand-Up!**](https://wipdeveloper.wpcomstaging.com/newsletter/) to receive free the [WIP Developer.com](https://wipdeveloper.wpcomstaging.com/) weekly newsletter every Sunday!
