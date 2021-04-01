---
layout: "post.11ty.js"
title: "Azure Web App Extensions Hide and Seek"
date: "2015-08-12"
tags: 
  - "Azure"
  - "Blog"
  - "Extensions"
  - "Visual Studio Online"
slug: "azure-web-app-extensions-hide-and-seek"
---

![Azure Loading Screen](images/azure-banner1.png)

The other day while trying to make a change to one of my sites on Azure using the [Preview portal](portal.azure.com) I could not find the extensions under all settings.

Usually after login in and going to my Web App I would go to `All settings ->`

![All settings](images/00-allsettings2.png)

scroll to the bottom and find the extensions there. This time though, Extensions was missing. (dun dun dunnnn)

![Settings missing Extensions](images/01-settings2.png)

Now how was I going to use the `Visual Studio Online "Monaco"` editor to make changes to my site, while it's running in production (Protip: Don't edit your code in production)?

Well I looked around some and tried some buttons out because it's not like I'm going to stop and read the manual (or update email I may have ignored.)

At the top of the menu for the Web App there is a group of buttons and one of them is `Tools`.

![Web App Buttons](images/02-buttons2.png)

It brings up the `Tools` menu (I know it surprised me too.) In the `Tools` menu at the bottom I found the `Extensions` menu button.

![Tools Menu with Extensions](images/03-tools2.png)

Now I could access my long lost extensions and start `live coding` (because live coding means in production, right?)

![Tools Menu with Extensions](images/04-extensions2.png)

#### Something Else

One thing I did notice (besides moving my cheese) the Azure team organized menus into sections.

![Setting Menu with Section Headers](images/05-settings2.png)

So that's neat if you like things grouped together that have some sort of commonality.
