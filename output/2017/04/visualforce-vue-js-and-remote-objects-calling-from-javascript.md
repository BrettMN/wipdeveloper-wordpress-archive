---
layout: "post.11ty.js"
title: "Visualforce, Vue.js and Remote Objects - Calling From JavaScript"
date: "2017-04-17"
tags: 
  - "Blog"
  - "Salesforce"
  - "SalesforceDeveloper"
  - "VueJS"
slug: "visualforce-vue-js-and-remote-objects-calling-from-javascript"
---

Previously we set up our project to use Remove Objects to retrieve, update, create and delete objects from Salesforce.com. We will finish the process of changing over to Remote Objects by changing our service out.

## Picking Up Where We Left Off

Since we did all the nessisarry work to use our Remote Object lets create a new service for this. I'm going to use the same structure for the service we used with [`@RemoteAction`s](/2017/04/10/visualforce-with-vue-js-part-5-get-data-with-remoteactions/) and just change our the methdo implemenations.

So create a new JavaScript file and give the the basic structure we will build out from:

#### Basic Structure

let sfService = (() => {
  // private variables

  // public variables

  // private functions

  // public functions

  function getContacts() {
  
  }

  function getContact(id) {

  }

  function updateContact(id, languages) {

  }

  function newContact(firstName, lastName, languages) {

  }

  function deleteContact(id) {

  }

  // return object
  return {
    getContacts: getContacts,
    getContact: getContact,
    updateContact: updateContact,
    newContact: newContact,
    deleteContact: deleteContact
  }
})()

You see we have all the same methods and they are currently empty. We also wont be using a "private" helper function this time.

Now let's see how we will impletment each function.

## `getContacts()` Implementation

First thing we will need to do it be able to call `getContacts()`, otherwise our page wont load. For `getContacts()` and the other functions we will have a somewhat similar structure of creating a new `WIPDeveloperModels.Contact`, returning a new `Promise`, and performing an action in the promise.

#### `getContacts()`

function getContacts() {
  let contacts = new WIPDeveloperModels.Contact()

  return new Promise((resolve, reject) => {
    contacts.retrieve({ limit: 50 }, (error, results, event) => {

      if (error) {
        reject(error.message)
      } else {

        resolve(
          results.map(result => {

            return { Id: result.get('Id'), Name: result.get('Name') }
          }))
      }
    })
  })
}

In the promise you see we are calling `contacts.retrieve` and passing in an object that is our search criteria, and a callback function. The search criteria is used to specify what we want to reteave. The callback function accepts an `error`, a `results`, and an `event`.

> More information about the search criteria can be found in the [Visualforce Developer Guide](https://developer.salesforce.com/docs/atlas.en-us.pages.meta/pages/pages_remote_objects_using_retrieve_query_object.htm)

In our callback function we check for an error and handle it if there is one before mapping new objects from the results to get the `Name` and `Id` in plain JavaScript objects and resolving the promise on the results of the mapping.

If the `resolve` around the `results.map` is a little hard to get your head around you can assign the results of the `reults.map` to a variable and `resolve` that. Like this

#### Alternative `resolve`

let mapped =  results.map(result => {

    return { Id: result.get('Id'), Name: result.get('Name') }
  })

resolve(mapped)

## `getContact(id)` Implementation

For `getContact(id)` is similar to `getContacts()` since it uses `contacts.retrieve` and have a search criteria.

#### `getContact(id)`

function getContact(id) {
  let contacts = new WIPDeveloperModels.Contact()

  return new Promise((resolve, reject) => {
    contacts.retrieve({
      where: {
        Id: { eq: id }
      },
      limit: 1
    },
      (error, results, event) => {

        if (error) {
          reject(error.message)
        } else {
          let result = results\[0\]

          resolve({
            Id: result.get('Id'),
            Name: result.get('Name'),
            MobilePhone: result.get('MobilePhone'),
            Email: result.get('Email'),
            Title: result.get('Title'),
            Department: result.get('Department'),
            LeadSource: result.get('LeadSource'),
            Level\_\_c: result.get('Level\_\_c'),
            Languages\_\_c: result.get('Languages\_\_c')
          })
        }

      })
  })
}

You see the search criteria has a `where` property and `limit` of `1`. The `results` is still an array though so I assigned the first, and hopefully, only element to a variable so I don't have to keep typing `[0]` to reference it. In the resolve we are creating a new object with the properties we want to be able to access.

## `updateContact(id, languages)` Implementation

Now we are going to see our first change to creating the new `WIPDeveloperModels.Contact` by passing in an object. The object will set values on the contact that we create. We can than call `update` on that contact to save changes to Salesforce.com.

#### `updateContact(id, languages)`

function updateContact(id, languages) {
  let contact = new WIPDeveloperModels.Contact({ Id: id, Languages\_\_c: languages })

  return new Promise((resolve, reject) => {
    contact.update((error, results) => {

      if (error) {
        reject(error.message)
      } else {
        resolve(results)
      }

    })
  })
}

The callback function takes an `error` and `results`. The `results` is an array of `Id`s that were updated.

## `newContact(firstName, lastName, languages)` Implementation

For `newContact(firstName, lastName, languages)` we pass in an object when creating our new `WIPDeveloperModels.Contact` but we will call `create` on the contact.

#### `newContact(firstName, lastName, languages)`

function newContact(firstName, lastName, languages) {
  let contact = new WIPDeveloperModels.Contact({ FirstName: firstName, LastName: lastName, Languages\_\_c: languages })

  return new Promise((resolve, reject) => {
    contact.create(error => {

      if (error) {
        reject(error.message)
      } else {
        resolve(contact.get('Id'))
      }

    })
  })
}

Since we called `create` the id isn't passed to the callback as a parameter but it is populated on the contact object.

## `deleteContact(id)` Implementation

With `deleteContact(id)` we will call delete on the `contact` we create and pass in the `id` and a callback function.

#### `deleteContact(id)`

function deleteContact(id) {
  let contact = new WIPDeveloperModels.Contact()

  return new Promise((resolve, reject) => {
    contact.del(id, (error, results) => {

      if (error) {
        reject(error.message)
      } else {
        resolve(results)
      }

    })
  })
}

## Run It

We these new functions in place you should be able to run it and things will work like they did with the `@RemoteAction`s. I thought about making a gif or video for it but there wouldn't be any visible difference.

## Conclusion

We now have 2 ways to make the same app on a Visualforce page. Do you have a way you prefer? Let me know by leaving a comment below or emailing [brett@wipdeveloper.com](mailto:brett@wipdeveloper.com).
