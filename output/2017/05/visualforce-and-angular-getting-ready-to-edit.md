---
layout: "post.11ty.js"
title: "Visualforce and Angular - Getting Ready to Edit"
date: "2017-05-18"
tags: 
  - "Angular"
  - "Blog"
  - "Salesforce"
  - "SalesforceDeveloper"
  - "Typescript"
slug: "visualforce-and-angular-getting-ready-to-edit"
---

One of the advantages of using a framework that encourages creating components that are reusable is you can write less markup and code. We haven't really taken advantage of that yet. Let's get ready to edit a contact.

## Add Editing

Let's add a new method to our `remote-actions.service.ts` called `updateContacts`. It will accept one parameter called `contact` of type `Contact`. It will use `callRemote` to call the `TryAngularController.UpdateContact` method and we will pass it the `contact.Id`, `contact.Email`

#### New `updateContact` Method

updateContact(contact: Contact): Promise<{}> {
  console.log('getContact called');

  return new Promise((resolve, reject) => {
    this.callRemote('TryAngularController.UpdateContact', \[contact.Id, contact.Email\], resolve, reject);
  })
}

On to our `contact-details.component.ts`!

We will be adding a few properties to it but first let's import the `Contact` class like we did [last time](/2017/05/18/visualforce-and-angular-adding-a-contact-type/).

#### Import `Contact`

import { Contact } from '../objects/contact';

Now lets add 2 properties, one called `originalContact` of type `Contact` and one called `editing` of type `boolean`. The `originalContact` will be used to reset the values if we cancel editing and `editing` will be used to manages what state we are in: editing or not editing.

#### New Properties

originalContact: Contact;
editing:boolean;

In `ngOnInit` lets store the `results` in the new `originalContact` property.

#### Updated `ngOnInit`

ngOnInit() {
  console.log('ContactDetailsComponent.ngOnInit')

  const id = this.route.snapshot.paramMap.get('id');
  console.log(id);

  this.service.getContact(id)
    .then(results => {

      this.originalContact = results;

      this.id = results.Id;
      this.name = results.Name;
      this.email = results.Email;
    });
}

We will also need to add some methods for to start editing, cancel editing and to submit our changes when we are done.

First lets add an `edit` method. All it's going to do is change `editing` to `true`.

#### New `edit` Method

edit(){
  this.editing = true;
}

And if we are going to edit we should also have a `cancelEdit` that changes `editing` to false and resets the values.

#### New `cancelEdit` Method

edit(){
  this.editing = true;
}

Of course being able to change a text field is great and all but we want to be able to save those changes with a `onSubmit` method.

#### New `onSubmit` Method

onSubmit(){

  this.editing = false;

  this.originalContact.Email = this.email;

  this.service.updateContact(this.originalContact)
  .then(() => {
    this.ngOnInit()
  });
}

Since the `service.updateContact` promise returns no object we are just going to recall the `ngOnInit` to refresh the data and verify it saved properly.

## Add Some Buttons

All those methods are great but we should try calling one or 2 of them.

On your `contact-details.component.html` let's add a few buttons right before the `Back` button, one to edit, one to cancel editing and one to save changes.

The `Edit` button has a `*ngIf="!editing"` this is an Angular directive to include or exclude a template based on a expression, in this case the expression is `!editing` so the button should appear when we are not editing.

The other odd thing to note is the `(click)="edit()"` this is Angular's way of binding user actions, the `()` indicate the flow of data is from the view to the controller, with the `click` event. So when the user fires the click event by clicking the button the `edit` method will be called.

#### `Edit` Button

<button type="button" \*ngIf="!editing" class="btn btn-primary" (click)="edit()">
  Edit
</button>

#### Similar to the `Edit` button the `Cancel` button has a `*ngIf="editing"` making it appear only when the `editing` is true. The `(click)="cancelEdit()"` calls `cancelEdit` when the user clicks the button.

#### `Cancel` Button

<button type="button" \*ngIf="editing" class="btn btn-danger" (click)="cancelEdit()">
  Cancel
</button>

The `Save` button is slightly different as it's type is submit. This means we will submit the form using the action defined on the form, more on that in a moment. It also has the `*ngIf="editing"` making it appear only when the `editing` is true.

#### `Save` Button

<button type="submit" \*ngIf="editing" class="btn btn-success">
  Save
</button>

Now, where was that submit defined...

## Update the `form`

Since we are actually making this form functional let's update the `form` tag by defining a submit action and giving it a name.

#### Update `form`

<form class="form-horizontal" (ngSubmit)="onSubmit()" #contactForm="ngForm" novalidate>

You see more of that fancy `()` binding from the view to the controller with the parentheses this will call the `onSubmit` method we defined earlier when the form is submitted.

You may also have noticed the `#contactForm="ngForm"` this is storing the `ngForm` that is created by Angular for the form so we can access the values later.

## Conclusion

We are just getting started on being able to edit a `Contact`. Next time we will add a component that will switch between displaying the value and being able to edit the value. What else would you like to see a done in a form? Let me know by leaving a comment below or emailing [brett@wipdeveloper.com](mailto:brett@wipdeveloper.com).
