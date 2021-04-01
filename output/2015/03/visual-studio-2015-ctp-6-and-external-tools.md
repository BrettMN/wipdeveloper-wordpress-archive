---
layout: "post.11ty.js"
title: "Visual Studio 2015 CTP 6 And External Tools"
date: "2015-03-26"
tags: 
  - "Blog"
  - "Visual Studio"
slug: "visual-studio-2015-ctp-6-and-external-tools"
---

The Ladies, Gents and Paperclips at Microsoft are taking the easy road with some aspects of the web development tool chain this go around. Instead of reinventing the wheel that the rest of the web development community is already taking around the block they are just including some of those preexisting tools. What do I mean by this? Well, Visual Studios 2015 installs copies of popular web related applications/tools like Node.js, NPM, Grunt, Bower, and Git.

This is all well and good and helps ease a web forms developer into the strange new world of CSS pre-compiling and bundling or JavaScript Linting and Uglification without the use of System.Web.Optimization. But what if you already have Node.js or use io.js? What happens when you don't want to use Grunt or plan on using something besides Bower?

![What to do now?](https://wipdeveloper.wpcomstaging.com/wp-content/uploads/2017/05/confused-clip3.png?w=300)

### Change the Settings of Course!

The nice people at Microsoft have made it easy to tell Visual Studio where to look for external tools.

Go to Tool -> Options

![Tools Menu](images/00-tools-menu3.png)

Expand Projects and Solutions

![Projects and Solutions](images/01-projects-and-solutions2.png)

And then External Web Tools

![Expanded Projects and Solutions With External Web Tools Selected ](images/02-external-web-tools2.png)

Here you can see the list of Paths that Visual Studios will check for external tools and change the order to how you would like.

![Re-ordered path](images/03-moved-path2.png)

This will check the system path before the External Tools folder that ships with Visual Studios 2015.

With this change you should be using the version that you installed outside of Visual Studios. This will allow you to update and change out External tools as you choose.

### Should you delete the External Tools folder path?

Probably not since there may be tools that it includes that you are not aware of and don't have an alternative installed on your machine. Even if you have all the tools installed outside of Visual Studios currently there is the chance that a future update will add new tools to the folder and your Visual Studio would not be looking for it even as a fall back.
