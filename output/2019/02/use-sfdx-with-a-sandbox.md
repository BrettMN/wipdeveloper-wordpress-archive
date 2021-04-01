---
layout: "post.11ty.js"
title: "Use SFDX with a Sandbox"
date: "2019-02-13"
tags: 
  - "Blog"
  - "Salesforce"
  - "SalesforceDeveloper"
  - "SalesforceDX"
  - "VSCode"
slug: "use-sfdx-with-a-sandbox"
coverImage: "Screen-Shot-2019-02-15-at-4.52.48-PM.png"
---

https://youtu.be/4L\_H2pDNqNI

Hello this Brett with WIPDeveloper.com. Recently I was asked about using the SalesforceDX Visual Studio Code extensions to develop against a sandbox or a non scratch org. And the SalesforceDX Visual Studio Code team has put out a walkthrough on how to do that. But if you follow the directions there might be some questions so I was just going to do an example set up real quick I'll provide a link below for the documentation where this describe.

## Work Against Existing Org

To get started you have Visual Studio Code open the open up the command pallette and you use the command `SFDX: Create Project with manifest` the first time I tried this I was little confused because I didn't have a manifest yet I thought that that meant you had to have the manifest at the time of creation. What it actually is doing is it's creating the project and it also creates the manifest so you don't have to worry about that at this point. Just choose `Create Create Project with manifest`

Give it a Name.

I'm going to call it testOrg and then choose a location. It's going to go in my documents.

Wait a moment, while it generates a project, you can see one of the folders is manifest in there is a product `package.XML`. You don't have to necessarily customize this if you're just going to be if you're going to be doing some basic Apex development.

It has Apex class, Apex component, Apex page, Apex test suite, Apex trigger, Aura and static resource. These are the basic things you're probably going to need if you're going to do some development in Salesforce.

Now we would authorize our art by going to open the command palette and going to `SFDX: Authroize Org` and then choose the type of or you're going to authorize against I'm going to use the production login since I only have a developer work no sandboxes for me.

and I will us VScode. org as the name or alias.

Now what it did is it opened a web browser so it's asking me to log into my Salesforce org and I will do that when I log in.

Now it's going to ask if this is allowed going to say yes, because I want to CLI to access the org.

And I did call it the CLI because it's the CLI that is doing all the work the Visual Studio Code plugins are talking through the CLI to the org

If you look in the output here, you can see that we can make it the org has been authorized and we may now are close the browser if we want

to. The next step would be to retrieve our source code.

Yeah, retrieve the source from the org. So here we were right click on the package and retrieve source in manifest from org.

Now what this is going to do is get anything that is in the org and put it in the `force-app`.

I don't think I have anything in the org so there won't be much to see.

Yeah, it's empty. So no results found

This would have been more dramatic if I had at least one Apex class.

Speaking of an apex class though, we can go and

now create an apex class. I'm going to call it `test`

I want to make a folder for it.

I'm going to make a `classes` folder.

And now everything is in the wrong spot. So I will move the classes folder up to default, I'll take my

test classes and move them into classes.

Now I have some Apex that I can deploy it to my org. And I can do that by right clicking and choosing deploy this source to Ord on the folder or in the file itself, right clicking the folder file over here and choosing deploy this sourced. org right clicking on the folder and deploy this source to org.

And I believe that goes all the way up.

So I can go to here and choose

deploy this source org.

And one thing you got to be careful of is if there's more than one person working in an org, you can overwrite the other person's changes. Because there is no check to see if there are changes on the server,

I get a little paranoid. So the project that I'm using the SalesforceDX with Visual Studio Code extensions

on I'm only deploying one file at a time, because I don't want to

mess up anyone else

To a better workflow.

If you have a better suggestion, feel free to reach out you can find me on Twitter,

@BrettMN, or send an email Brett@WIPDeveloper.com.

For right now what's deploy this to or to be what's deployed this source to org

See the line that acts like a spinner. It says it's was successfully deployed.

Now earlier, we deployed

or we retrieved the source from org, but there wasn't anything to get.

So I'm going to delete the class folder.

Just delete it off the hard drive. Now, if I were to choose the package.xml and retrieve this source, retrieve the source in the manifest from the org.

It's going to pull the class that we just deployed back down. One thing to keep in mind is if we already have a class it will overwrite it. So be a little careful with that.

And now we have a classes folder with our test class

and

Just going to add something misspelled in here.

Now I saved it but I didn't deploy it. So if I re-retrieve this source from the org, it's going to get rid of my something.

So something to be aware of

that my something has now gone

but

You can use this to start working in a sandbox using the SalesforceDX extensions.

## Links

[Org Development Model with VS Code](https://forcedotcom.github.io/salesforcedx-vscode/articles/user-guide/org-development-model)

## That’s all for now.

Remember to sign up for **[The Weekly Stand-Up!](https://wipdeveloper.wpcomstaging.com/newsletter/)**  and you can get updated with any new information we have on WIPDeveloper.com.
