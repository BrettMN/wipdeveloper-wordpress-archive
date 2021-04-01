---
layout: "post.11ty.js"
title: "LWC - Use Child Components When Rendering A List"
date: "2019-10-25"
tags: 
  - "Blog"
  - "LWC"
  - "Salesforce"
  - "SalesforceDeveloper"
slug: "lwc-use-child-components-when-rendering-a-list"
coverImage: "LWC-Use-Child-Components-When-Rendering-A-List.png"
---

Hello, I'm Brett with web developer.com. Since we're rendering a list of objects, and we want the formatting for each one to be the same, we're going to extract each thing that's being rendered in that list to a separate component. This will make it easier for us to glance at our HTML and see what's going on.

And it makes it more impossible. This be a bigger issue once we have more going on in our HTML. But for right now, since we only have a, we're displaying the name with a dash and the ID. We're going to take that and we're going to add it to a new component that I created. List object list item. Now add that into the template for the object list item somewhere since we took it out of the object list template.

Replace it with the see object list item Then we're going to bind to an account property on there. For each one we were bound bind is the account. Right now, this won't show anything. Since we haven't set up our object list item to accept an item yet. In our object list item JavaScript, we will have to import the API. So now we can set the object on our object list item. This is all similar to using a child component except in this case, we are using child component that gets repeated. We have our child components. Somebody's using child component that's not rendered in the list, we can send data back to the parent using events. This case we have been using a new event called object list items selected And we will pass along the account ID. Now we just have to handle this and the object list. So um, our object list item in the repeat or the for each, we will have an object list items selected, and let's give it a name. Now we just need to make the handler for it. So we're just passing back the ID. So while we don't have anything to do with it right now, what we can do is display it so that we know that it's actually passing back property are selected it will be displayed above our list. And now we just need to capture it. And so once the handler gets called the detail, which is the ID from the account that we have selected will be assigned to With the selected list ID, and that will be displayed on our page. So we can select the first one we see.

Or we can select the second one, or the, whatever number one this one is. And it changes every time we select new. I know for the simple example, this doesn't seem like it'd be very useful. But when you have a repeat that is a complicated, structured HTML layout. Using a component inside the list to render it instead of composing it directly in the list, like say, if you're repeating a bunch of lightning design system cards on the page and I have complex HTML layouts, this would make it a lot easier to reason with, for what is happening for each one.

## Links

https://wipdeveloper.wpcomstaging.com/lwc-using-events-to-pass-data-to-a-parent-component/

https://wipdeveloper.wpcomstaging.com/lwc-using-a-child-component/

https://wipdeveloper.wpcomstaging.com/lwc-passing-data-to-a-child-component/

https://wipdeveloper.wpcomstaging.com/lwc-calling-a-childs-method/

## That’s it for now.

Remember to sign up for **[The Weekly Stand-Up!](https://wipdeveloper.wpcomstaging.com/newsletter/)**  and you can get updated with any new information we have on WIPDeveloper.com.
