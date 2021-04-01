---
layout: "post.11ty.js"
title: "Quick Look @ Vue.js Part III - My First Component"
date: "2017-03-08"
tags: 
  - "Blog"
  - "Quick Look"
  - "VueJS"
slug: "quick-look-vue-js-part-iii-my-first-component"
---

Before we get going remember we have already [started](/2017/03/06/quick-look-vue-js) a Vue.js app and [added some content](/2017/03/07/quick-look-vue-js-part-ii-add-some-content) to that app. Let's clean up some of our markup with a custom component

## Update `app.js`

We are going to create a global component in out `app.js` file. At the top before the line `var app = new Vue({` we are going to add `Vue.component()` to register our component before the app tries to use it.

`Vue.component()` takes an identifier or tag that we will use to place the component and an options object. In our simple case the options object will consist of a `props` property and a `template` property.

The identifier I'm going to use is `task-list` but you can use what you choose, just keep in mind that this is the tag you will use in the markup for the component you create.

For the `props` property it takes an array of names of properties to bind to the component. For now we only need to get access to the `tasks` in our component so I'll just have one name, `tasks`, in my `props` array.

For the template lets copy our everything inside the `<ul>` that we created in the index.html last time, this will be the markup the component uses.

All together now:

#### New and Improveded `app.js`

Vue.component('task-list', {
  props: \['tasks'\],
  template: \`
    <ul>
      <li v-for="task in tasks">
        <div>
          <label for="task-title">
            <input type="checkbox" v-model="task.complete" /> {{ task.title }}
          </label>
          <p>
            {{ task.description }}
          </p>
        </div>
      </div>
    </li>
  </ul>
  \`
})

var app = new Vue({
  el: '#app',
  data: {
    message: 'Hello WIPDeveloper.com!',
    tasks: \[
      {
        title: 'test task one',
        complete: true,
        description: 'this is a task that is complete'
      },

      {
        title: 'test task two',
        complete: false,
        description: 'this is a task that is not complete'
      }
    \]
  }
})

Now we need to make our `index.html` take advantage of our little component.

## Update `index.html`

Delete the `<ul>` and everything inside it. Now add a tag for you new component. I named my `task-list` so I will create a tag `<task-list>` tag. To bind the `tasks` to the component use the `v-bind:task="tasks"` as a property on your components tag to bind the `tasks` from the app to the `tasks` of the component.

#### More Updated `index.html`

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Vue.Js Test app</title>
</head>
<body>
  <div id="app">
    <h1>{{ message }}</h1>
    <task-list v-bind:tasks="tasks"></task-list>

  <script src="https://unpkg.com/vue"></script>
  <script src="app.js"></script>
</body>
</html>

If you look at your app in the browser again it should look the same as before we created the component. If it does congratulations, you are a success!

#### Same App New Component

![Same App New Component](images/quick-look-vue-011.png)

## Code

Code can be found at [Github/BrettMN/quick-look](https://github.com/BrettMN/quick-look/tree/master/vue-quick-look)

## C is for Component or Complete

Now we have cleaned up our markup some but things are starting to get a little cluttered in our `app.js`. We could start splitting things out, what do you think? Let me know by leaving a comment below or emailing [brett@wipdeveloper.com](mailto:brett@wipdeveloper.com).
