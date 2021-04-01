---
layout: "post.11ty.js"
title: "Quick Look @ Vue.js"
date: "2017-03-06"
tags: 
  - "Blog"
  - "Quick Look"
  - "VueJS"
slug: "quick-look-vue-js"
---

Lets take a quick look at [Vue.js](https://vuejs.org/). It sells it's self as a "progressive framework for building user interfaces". So my take on that is you can enhance your webpage with a sprinkling of Vue.js and not buy the glitter factory it comes with. With a focus on the view layer of a website it is easy to see how you can enhance a page slightly to great effect, something that I feel AngularJS (1.\*) lost in the transition to Angular(2+).

## Getting Started

Getting started is simple, about as simple as the adding two scripts tag to a page (the Vue.js library and your code), identifying an element to have the app reside in, and any binding you plan on using:

#### Whole Vue.js Index page

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Vue.Js Test app</title>
</head>
<body>
  <div id="app">                                                            <= Identify App container
    {{ message }}                                                           <= some binding
  </div>

  <script src="https://unpkg.com/vue"></script>                             <= Vue.js Library
  <script src="app.js"></script>                                            <= Custom Code
</body>
</html>

We should add something to our `app.js` though, so we will create a new Vue app that identifies the element and some data:

#### Starter `app.js`

var app = new Vue({
  el: '#app',
  data: {
    message: 'Hello WIPDeveloper.com!'
  }
})

> I'm using `lite-server` to serve the page up and see it locally, feel free to use any server that you feel comfortable with.

#### Vue.js In Action

It's so complicated I can embed it right here if I wanted to:

{{ message }}

<script src="https://unpkg.com/vue"></script>

<script>var app = new Vue({ el: '#jsa-vue-app', data: { message: 'Hello WIPDeveloper.com!' } })</script>

## More Dynamic?

Well that's interesting but what if we want to display what the user has entered into a text box right next to it.

> While this is very common in examples you probably wont be doing this that often in a "real" app

All we have to do is add an `input` with a `v-model="message"` binding and we will be able to edit the contents of out `message` data property:

#### New `<body>`

<body>
  <div id="app"> 
    <input type="text" v-model="message">                                            <= This is New
    {{ message }}                                                           
  </div>

  <script src="https://unpkg.com/vue"></script>                            
  <script src="app.js"></script>                                           
</body>

#### More Vue.js In Action

It's still so complicated I can embed it right here if I wanted to:

 {{ message }}

<script src="https://unpkg.com/vue"></script>

<script>var app = new Vue({ el: '#jsa-vue-app-2', data: { message: 'Hello WIPDeveloper.com!' } })</script>

## Code

Code can be found at [Github/BrettMN/quick-look](https://github.com/BrettMN/quick-look/tree/master/vue-quick-look)

## Just Getting Started

That's it. You now have a Vue.js app. Let add a little more to to next time, maybe start a todo app? Let me know by leaving a comment below or emailing [brett@wipdeveloper.com](mailto:brett@wipdeveloper.com).
