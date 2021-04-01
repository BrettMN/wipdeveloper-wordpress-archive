---
layout: "post.11ty.js"
title: "ASP.NET 5 Static Files - Enabling Default Files"
date: "2016-01-09"
tags: 
  - "ASP.NET 5"
  - "Blog"
slug: "asp-net-5-static-files-enable-default-files"
---

Sometimes you have static resources in your webroot, `wwwroot` by default, that you would like to have served when a request is made to that path. For instance if you go to the root of a site you expect the `index.html` to be served to the browser. This can be done with ASP.NET 5 by adding a method call to `UseDefaultFiles()` off of our app in the `Configure` method of the `Startup.cs`.

> If you followed [ASP.NET 5 and Static Files](/2015/04/02/asp-net-5-and-static-files/) for you set up you'll add the call to `app.UseDefaultFiles()` after the `app.UseStaticFiles()`.

##### Update `Configure` Method

```csharp
public void Configure(IApplicationBuilder app)  
{
    app.UseIISPlatformHandler();
    app.UseDefaultFiles();
    app.UseStaticFiles(); 
}
```

> You need to call `app.UseDefaultFiles()` before you call `app.UseStaticFiles()`

Now when you go to a root directory in your site ASP.NET will try and serve the default file.

Of course sometimes people like to be crazy and setup their own defintion of what a default file is. This is possible by passing in a `DefaultFilesOptions` object when you call `app.UseDefaultFiles()`. Options you can configure include `DefaultFileNames`, `FileProvider`, and the `RequestPath`. I only played around with the `DefaultFileNames`

> I did add a using for `using Microsoft.AspNet.StaticFiles;` to access this without the namespacing to keep things easier to read.

```csharp
app.UseIISPlatformHandler();  
var options = new DefaultFilesOptions {  
        DefaultFileNames = new List<string> { "notIndex.html" } 
    };
app.UseDefaultFiles(options);  
app.UseStaticFiles();  
```

Making this configuration change and adding an html file titled `notIndex.html` to the root of my project now serves the `notIndex.html` when the browsers loads the root of my project. Of course I didn't add a `notIndex.html` to the rest of my directories so this only works for root right now.

#### Conclusion

Hope this helps with configuring your static file options. Have something else you are curious about let us know by leaving a comment bellow or, if you want to keep things on the down-low, send an email to me at [brett@wipdeveloper.com](mailto:brett@wipdeveloper.com).
