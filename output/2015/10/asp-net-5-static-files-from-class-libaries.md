---
layout: "post.11ty.js"
title: "ASP.NET 5 - Static Files From Class Libaries"
date: "2015-10-29"
tags: 
  - "ASP.NET 5"
  - "Blog"
slug: "asp-net-5-static-files-from-class-libaries"
---

Recently I was asked about using files from separate class library projects as static files in an ASP.NET 5 application. And while I can understand wanting to break a project down into smaller portions to allow for easier separation of work between developers, not saying this was the reason for the question just a reason I thought of wanting to do it, it’s not something I had considered before. Now that I thought about it though I can tell you it’s not something I would do.

#### Why? You May Ask

Well, I think of class libraries as a place to build reusable code that is to be shared among multiple projects. Since most static files are generally somewhat specific to a site, unless you are creating a library, I would probably keep the static files in the web project they are going to be used in.

> If you are creating a library for redistribution I would recommend doing it outside of your current solution and having a dedicated solution with client side build pipeline (grunt, gulp, broccolijs, what have you) including tests without all the extra complications of it being a website as well. Then I would recommend importing it into your project using npm, jspm, bower or your client side package management options of choice.

#### But What If…

If you are trying to reproduce virtual directories similar to they way you can configure a sub-directories of a site to be hosted outside of the website file structure in IIS, I wouldn't know how to do that, I also wouldn't recommend it since it would work against making ASP.NET 5 work outside of IIS since your site would become dependent on it to operator properly. This would remove the option of using a Linux server for hosting, yeah you may not care now but you might in a

#### Maybe We Could Just…

Of course if you are trying to copy files from one project to the wwwroot folder when you build you could probably set up a build task that could accomplish that. I wouldn't recommend this either as it would be somewhat fragile. All developers working in the solution would require special knowledge of where the files originate from and how they are copied so they can edit the proper files when necessary. And keep track of what files in the wwwroot folder are not copied from any where. Needless to say this might make on boarding new developers more difficult as they, more than likely, would forget at some point and loose all there changes when they build the project.

#### Best Practice?

Um no, I wouldn’t say this is a best practice, just my practice, at the time of this writing. If you have any reasons why you would want to have static files outside of your web project I would love to hear them in the comments, you might change my opinion on this.
