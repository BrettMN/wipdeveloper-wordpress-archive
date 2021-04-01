---
layout: "post.11ty.js"
title: "Aurelia and ASP.NET 5 - Routing, Views, and Navigation, Oh My"
date: "2015-11-15"
tags: 
  - "Aurelia"
  - "Blog"
slug: "aurelia-and-asp-net-5-routing-views-and-navigation-oh-my"
---

It's been awhile since we looked at using Aurelia with ASP.NET 5 and there have been updates for both. But the wonderful thing with Aurelia has been most breaking changes during the last 11 months have not been with the basic way you build your website. So for this example I will recreate what we had last time we, basically I just copied and pasted all the HTML and JavaScript over to a new ASP.NET 5 project, and proceed from there.

> See [Getting Started with Aurelia and ASP.NET 5](/2015/07/24/getting-started-with-aurelia-and-asp-net-5/) and [Aurelia and ASP.NET 5 - Understanding the Aurelia Parts - The Basics](/2015/07/27/aurelia-and-asp-net-5-understanding-the-aurelia-parts-the-basics/) to see the basics of what we had before. I've also added Bootstrap and Font Awesome to make things look somewhat ok and moved all the logic and views to a separate folder called `app` in the `wwwroot`.

#### Now Where Where We?

This time we will add routing, multiple views and make use of a simple navigation menu that we generate from the router.

Since I added Bootstrap to the project I need to import it in a way it can be used throughout the entire app. To accomplish this add `import 'bootstrap';` to the beginning of your `app.js`.

While we have the `app.js` open we might as well add our second route to the routes collections. So we will our second route to the `config.map` and it will look like this :`{ route:'comments', name:'comments', moduleId: 'comments', nav: true, title: "Comments"}`

##### Updated `app.js`

```javascript
import 'bootstrap';

export class App {  
    configureRouter(config, router){
        config.title = 'ToDo';
        config.map([
            { route:['','main'], name:'main', moduleId:'main', nav:true, title:'Main'},
            { route:'comments', name:'comments', moduleId: 'comments', nav: true, title: "Comments"}
        ]);
        this.router = router;
    }
}
```

#### But We Don't Have a Comments View or Model.... Yet

Now we will have to make the new view and model so we don't get errors when we navigate to `#/comments`. Lets start by adding our `comments.js`. Since we are adding a comments page we will need some very basic features. Our `comments.js` will have three properties: a collection for the comments called, surprise surprise, `comments`; a `name`; and a `message`. The `name` and `message` will hold temporary values till we save the new comment in the `comments`. We will also have a `clearData` method that will clear the `name` and `message`. And an `addComment` method to add a new comment to the `comments` by creating a new comment with the `name` and `message` values. It may sound complicated when reading it like this but it looks pretty simple:

##### `comments.js`

```javascript
import {Comment} from '/app/assets/comment';

export class Comments{  
    comments;
    name;
    message;

    constructor(){
        this.comments = [];
        this.clearData();
    }

    addComment(){
        let newComment = new Comment(this.name, this.message);
        console.log(newComment);
        this.comments.push(newComment);
        this.clearData();
    }

    clearData(){        
        this.name = '';
        this.message = '';
    }
}
```

You may have noticed the first line is an import `import {Comment} from '/app/assets/comment';` so we will be creating a `Comment` class so we can keep our view logic separate from our objects. So let's create a new folder for our assets called something creative, like `assets`. In there lets add our `comment.js` and add our code for our class.

```javascript
export class Comment{

    name;
    message;

    constructor(name, message){
        this.name = name || '';
        this.message = message || '';
    }    
}
```

As you can see it's a pretty simple class with two properties, `name` and `message`, and the constructor that takes two values and assigns them or an empty string to our properties.

With our `comments` viewmodel and out `Comment` class we can add our view next time.
