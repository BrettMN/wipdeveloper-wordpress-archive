---
layout: "post.11ty.js"
title: "Salesforce Mobile SDK and Ionic – Remote Hybrid App – RemoteActions"
date: "2017-11-17"
tags: 
  - "Blog"
  - "Cordova"
  - "IonicFramework"
  - "Salesforce"
  - "SalesforceDeveloper"
slug: "salesforce-mobile-sdk-and-ionic-remote-hybrid-app-remoteactions"
coverImage: "Screen-Shot-2017-11-17-at-12.25.53-AM.png"
---

If you've been following along you should have a working app that looks and behaves the same as the Local Hybrid app we had. At this point you may be wondering why we would choose to go with a Remote Hybrid app over the Local Hybrid app.

Well since our Remote Hybrid app uses a Visualforce page we can now add a controller to it and start accessing data with RemoteActions.  Using RemoteActions frees you from worrying about any API limits.

Let's take a look at what that would require.

## Create Custom Controller

First thing we will need to do is create an Apex class for our controller. I will be calling mine `ContactMobileAppController` but feel free to give it any name you like.

The `ContactMobileAppController` class will have 5 methods:

1. `GetContacts` to load contacts
2. `GetContact` to load a single contact
3. `UpdateContact` to update an exisiting contact
4. `NewContact` to create a new contact
5. `DeleteContact` to, _surprise_, delete a contact

#### `ContactMobileAppController`

public with sharing class ContactMobileAppController {

    @RemoteAction
    public static List<Contact> GetContacts(){
        List<Contact> contacts = \[select id, Name from contact LIMIT 50\];

        return contacts;
    }

    @RemoteAction
    public static Contact GetContact(String contactId){
        Contact contact = \[SELECT Id, FirstName, LastName, Name, Email, MobilePhone FROM Contact WHERE Id =: contactId\];

        return contact;
    }

    @RemoteAction
    public static void UpdateContact(String contactId, String firstName, String lastName, String email, String phone){
        Contact contact = \[SELECT Id FROM Contact WHERE Id =: contactId\];

        contact.FirstName = firstName;
        contact.LastName = lastName;
        contact.Email = email;
        contact.MobilePhone = phone;

        update contact;
    }

    @RemoteAction
    public static void NewContact(String firstName, String lastName, String email, String phone){
        Contact newContact = new Contact(FirstName = firstName, LastName = lastName, Email = email, MobilePhone = phone);

        insert newContact;
    }

    @RemoteAction
    public static void DeleteContact(String contactId){
        Contact contact = \[SELECT Id FROM Contact WHERE Id =: contactId\];

        delete contact;
    }
}

Of course to make use of our shiny new controller we will need to add it to the Visualforce page.

## Update Visualforce

To be able to access the remote action we defined in the `ContactMobileAppController` class we will need to add it to the Visualforce page.  To do that we will add an attribute to the `apex:page` tag of `controller` with a value of `ContactMobileAppController`.

#### Updated Visualforce Page

<apex:page
        docType="html-5.0"
        controller="ContactMobileAppController"
        showHeader="false"
        sidebar="false"
        standardStylesheets="false">

## Conclusion

Don’t forget to sign up for [**The Weekly Stand-Up!**](https://wipdeveloper.wpcomstaging.com/newsletter/) to receive free the [WIP Developer.com](https://wipdeveloper.wpcomstaging.com/) weekly newsletter every Sunday!
