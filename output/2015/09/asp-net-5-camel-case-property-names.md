---
layout: "post.11ty.js"
title: "ASP.NET 5 - Camel Case Property Names"
date: "2015-09-21"
tags: 
  - "ASP.NET 5"
  - "Blog"
  - "Json"
slug: "asp-net-5-camel-case-property-names"
---

If you have used ASP.NET MVC in the past you may be used to using Newtonsoft.Json's CamelCasePropertyNamesContractResolver and wondering how to do that with ASP.NET 5. Well the good news is it is possible to still use that handy feature from Newtonsoft.Json and configure it globally.

> For this demo I have set up a simple MVC 6 project with a `ValuesController` similar to how the project was set up in [ASP.NET 5 MVC Controllers: Setup](/2015/05/15/asp-net-5-mvc-controllers-setup/) and [ASP.NET 5 MVC Controllers: Controllers](/2015/05/18/asp-net-5-mvc-controllers-controllers/)

In the `ValuesController` I have modified the `get` to return a custom class.

##### Our new Get()

```csharp
  [HttpGet]
  public IEnumerable<Person> Get()
  {
    return new Person[] {
      new Person { Name = "Bob", Age = 32 },
      new Person { Name = "Mary", Age = 33 },
      new Person { Name = "Pat", Age = 34 }
    };
  }
```

Of course this means we actually need a `Person` class somewhere that looks like this:

##### Look an Overly Simple Person

```csharp
  public class Person
  {
      public string Name { get; set; }
      public int Age { get; set; }
  }
```

Now when we run the project and call the endpoint with a `get` command it will return our three people.

##### Bob, Mary and Pat

```
  [{"Name":"Bob","Age":32},{"Name":"Mary","Age":33},{"Name":"Pat","Age":34}]
```

Of course since we are on the client side now we might want our property names to be camel case like one would expect with 'normal' JavaScript so we have a little adjustment to do.

If you followed along with [ASP.NET 5 MVC Controllers: Setup](/2015/05/15/asp-net-5-mvc-controllers-setup/) your `StartUp.cs` should look like this:

```csharp
  public void ConfigureServices(IServiceCollection services)  
  {
      services.AddMvc();
  }

  public void Configure(IApplicationBuilder app)  
  {
      app.UseMvc(routes =>
      {
          routes.MapRoute(
              name: "default",
              template: "{controller}/{action}/{id?}",
              defaults: new { controller = "Home", action = "Index" });
      });
  }
```

In the `ConfigureServices` method we are going to add some JsonOptions to our MVC and configure the contract resolver and it should end up looking like this:

```csharp
  public void ConfigureServices(IServiceCollection services)  
  {
      services.AddMvc()
                  .AddJsonOptions(options =>
                  {
                      options.SerializerSettings.ContractResolver =
                          new CamelCasePropertyNamesContractResolver();
                  });
  }
```

Now when we run our little program and hit the endpoint with a `get` we should get a slightly different result.

##### Bob, Mary and Pat Take II

```
  [{"name":"Bob","age":32},{"name":"Mary","age":33},{"name":"Pat","age":34}]
```

Now with the property names in camel case we can start accessing the values of our object in our JavaScript without any special considerations for the fact that the object came from the server.

Hope this helps!
