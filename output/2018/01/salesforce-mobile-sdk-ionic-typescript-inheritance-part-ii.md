---
layout: "post.11ty.js"
title: "Salesforce Mobile SDK and Ionic – TypeScript Inheritance Part II"
date: "2018-01-22"
tags: 
  - "Blog"
  - "Cordova"
  - "IonicFramework"
  - "Salesforce"
  - "SalesforceDeveloper"
  - "Typescript"
slug: "salesforce-mobile-sdk-ionic-typescript-inheritance-part-ii"
coverImage: "Screen-Shot-2018-01-25-at-12.10.20-AM.png"
---

In [Salesforce Mobile SDK and Ionic – TypeScript Inheritance](https://wipdeveloper.wpcomstaging.com/2018/01/15/salesforce-mobile-sdk-ionic-typescript-inheritance/) we used `extend` to inherit from the `ContactsServiceProvider` in our `SmartstoreServiceProvider`.  This allows us to move ahead with adding features to our `SmartstoreServiceProvider` without having to create each necessary method call when we replace the `ContactsServiceProvider`.  Let's look at how.

## What's Inherited

Some of the methods that we were missing: `getContact` and `deleteContact` we not implemented by our `SmartstoreServiceProvider`.  Since we inherited from a `class` that had implementations of those methods we are able to call them on the class.  For right now the implementation of `getContact` and `deleteContact` behave exactly like when we used the `ContactsServiceProvider` as our service since those are the methods we are calling.

We can override existing implementations by by implementing our new version of the method in our `SmartstoreServiceProvider`.  This means eventually we will technically have two different `getContact` and `deleteContact` we will still be able to specify the correct method by using either the `this` keyword to reference the one implemented at the current level of inheritance or by using the `super` keywork to reference the base class.

> In our case the parent or base class is `ContactsServiceProvider`.   `SmartstoreServiceProvider` is a child or subclass.

Speaking of `super`...

## `super`

The `super` keyword is used to reference the base class from the subclass.  This way we can still use the functionality provided by the base class and adjust it to our needs.  We did this in the constructor when we called `super();` before we could access the context of `this`.

In the `constructor` calling `super();` was calling the `constructor` of the base class.  This allows for the base class to be properly instantiated, or created, before we start changing values it might assign.

We can also use the `super` keyword to access methods besides the `constructor`.   We may decide to use the base class version of `getContact` in our subclass after we override `getContact` to perform an action or even to take no parameter and use a hard coded string to get the contact.

#### Example Override

getContact() {
  console.log('SmartstoreServiceProvider.getContact');
  super.getContact('003j0000008CVYlAAO')
    .then(results => {
      // do something cool here
    });
}

> Protip don't use hard coded values.

This is a little contrived example but you can see how it works when you override a method from a base class with a new implementation in the subclass.

## Conclusion

Don’t forget to sign up for [**The Weekly Stand-Up!**](https://wipdeveloper.wpcomstaging.com/newsletter/) to receive free the [WIP Developer.com](https://wipdeveloper.wpcomstaging.com/) weekly newsletter every Sunday!
