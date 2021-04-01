---
layout: "post.11ty.js"
title: "LWC - Using a Static Resource"
date: "2020-01-29"
tags: 
  - "Blog"
  - "LWC"
  - "Salesforce"
  - "SalesforceDeveloper"
  - "SalesforceDX"
slug: "lwc-using-a-static-resource"
coverImage: "LWC-Using-a-Static-Resource.png"
---

https://youtu.be/lTWFolZb5LM

Hello, I'm Brett with WIPDeveloper.com. When working with lightning web components, one of the things you might have to access is a static resource. In this case, I would like to display an image inside of one of the Lightning Web Components.

Let's take a look at how to do that.

I've already created a lightning web component to access the static resource. And I've created a static resource two static resources. One has an image and one that a file or folder. I'm going to close those out because we don't need to see them right now, in the template of the component that we're going to access the static resource from, I would like to display the image. So let's create an image element. And our source for the image is actually going to be `imagePath`, which doesn't exist yet.

Over in our JavaScript class, we don't have an `imagePath` yet, but let's make one. What we're going to do is use a important statement to get access to the static resource.

Now we have import `import imageToUse from '@salesforce/resourceUrl/'` and then the name of our static resource, which is `imageToUse`. Now we'll just assign that to image path. Now if we save this both of these are saved.

I don't have this data, I don't have local development running. So I'm going to start that out. Once this is running, I'll go back to my window. That is the wrong one. I'm going to refresh it here. This is the local development. Good see building stuff. And there we go.

We have an image in our custom lightning web component. Now let's deploy it and make sure it's all working. Okay. Looks like it's done. deploying. There we go. That's accessing a static resource that is a single image.

Now if we want to access an image that's inside a folder, static resource is very similar. We're doing is importing the path of the test files route, static resource. And we're assigning it to `folderToUse`. And now we need to assign it in our components so that we have access to it. Now we've assigned `folderToUse` the path default, we've assigned the `folderToUse` path to `folderPath`, and we can go back and look at it. That's right there. You see the path relative path to our static resource folder. But if we look in our folder, We see that test files actually contains an image and some JavaScript. And if we can't just put the `wipdeveloper-banner.png` is we have to create a getter so that we can format the text for it back in the controller, let's create a getter.

So in our getter we are returning to the folder path with `wipdeveloper-banner.png` appended to it. And now we want to access this in our template will assign it to another assignment as the source to another image tag.

I want to get rid of this folder path right now because we don't need it.

Now we can see that we now have two images on our page. And if we deploy this we see our two images. So it seems pretty straightforward. Once you have access to your static resource, you can access the folder or once you have access to your static resource, you can access the files that it contains, since you have the path for and its relative from the root of the static resource.

One thing to note is when using the local development server, you may encounter issues if you add static resources or modified them after the server has been started. We see right now that the static resources are loading properly locally. But if we change the name of our banner image in the folder and update our controller to point to the new the new file name getting deployed right now, and we'll go back to our component and we see that it's not showing both images. If we look at the console, we'll see that it's missing or can't find that banner image. On the server though, it's it shows two images. So what's going on is the static resources are only copied over to the local development server when it started. So we can cancel out of our local development server and restart it And once it's running again, we can go to our local development time.

And everything's working as expected now. So if you're working with static resources, and using local development and you modified or if you've edited your static resource, you might have to restart the local dev environment.

## That’s it for now.

Remember to sign up for **[The Weekly Stand-Up!](https://wipdeveloper.wpcomstaging.com/newsletter/)**  and you can get updated with any new information we have on WIPDeveloper.com.
