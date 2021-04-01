---
layout: "post.11ty.js"
title: "Quick Look @ Angular Part III - Create a Service"
date: "2017-02-22"
tags: 
  - "Angular"
  - "AngularCLI"
  - "Blog"
  - "Quick Look"
slug: "quick-look-angular-part-iii-create-a-service"
---

So far we have used the Angular-CLI to [create a simple app](/2017/02/16/quick-look-angular/) and [add a component](/2017/02/20/quick-look-angular-part-ii-add-a-component/) but before we add a second component lets create a service. This will allow us to share information between our current component, `TaskListComponent`, and our future component tentatively named `NewTaskComponent`. This way when we get around to making our new component we can have one point of access to how we manipulate our collection of tasks.

## Add a Service

#### Create `TaskService`

ng g service ./services/task

> You may have noticed that we added `./services/` to the path for our new service. I choose to do this so all services can be located in one folder. If I was making a service dedicated to one component I think I would create the service in the folder of the component.

This will create 2 files in a new folder at `src/app/service/`:

#### `task.service.ts`

import { Injectable } from '@angular/core';

@Injectable()
export class TaskService {

  constructor() { }

}

#### `task.service.spec.ts`

/\* tslint:disable:no-unused-variable \*/

import { TestBed, async, inject } from '@angular/core/testing';
import { TaskService } from './task.service';

describe('TaskService', () => {
  beforeEach(() => {
    TestBed.configureTestingModule({
      providers: \[TaskService\]
    });
  });

  it('should ...', inject(\[TaskService\], (service: TaskService) => {
    expect(service).toBeTruthy();
  }));
});

## Share Data

As riveting as those are lets make the `TaskListComponent` use the `TaskService` to manage the state of the tasks list.

Lets move our `tasks` array and the work we are doing for initializing it from the `TaskListComponent` to the `TaskService`.

Now our `TaskService` should look like this:

#### Updated `task.service.ts`

import { Injectable } from '@angular/core';
import { Task } from '../models/task';                  // <= This is new

@Injectable()
export class TaskService {

  tasks: Task\[\];                                        // <= This is new

  constructor() { }

  // New Method
  init() {
    this.tasks = \[
      {
        "title": "First Item",
        "complete": true,
        "description": "first task to do"
      }
    \];
  }

}

This means we need a reference to the `TaskService` in the `TaskListComponent` now so we will add an `import` for it and pass it in the constructor. We will also call the `TaskService` `init` method from the `ngOnInit` so everything is initialized when we get things started.

#### Updated `task-list.component.ts`

import { Component, OnInit } from '@angular/core';
// import { Task } from '../models/task';               // <= Remove this                 
import { TaskService } from '../services/task.service'; // <= This is new

@Component({
  selector: 'app-task-list',
  templateUrl: './task-list.component.html',
  styleUrls: \['./task-list.component.css'\]
})
export class TaskListComponent implements OnInit {

  // tasks: Task\[\];                                        // <= Remove this

  constructor(private \_taskService: TaskService) { }       // <= This Changed

  ngOnInit() {
    // this.tasks = \[                                      // <= Remove this
    //   {                                                 // <= Remove this
    //     "title": "First Item",                          // <= Remove this
    //     "complete": true,                               // <= Remove this
    //     "description": "first task to do"               // <= Remove this
    //   }                                                 // <= Remove this
    // \];                                                  // <= Remove this

    this.\_taskService.init()                               // <= This is new
      
  }

}

Of course our template should be updated to use `_taskService.tasks` instead of the now nonexistent `tasks` on the controller.

#### Updated `task-list.component.html`

<ul>
  <li \*ngFor="let task of \_taskService.tasks">  <!-- This line changed -->
    <!-- Nothing else changed -->
  </li>
</ul>

Now if you are watching your page reload with `ng serve` you may notice it's not working. Opening the console will reveal a whole lot of error messages. This is because we didn't tell the app to use `TaskService` and it doesn't know where to find it.

## Register Service

To let Angular know we have a service we want to use we will have to register it as a provider at some level.

> I say "at some level" because depending on the size of your app you may not want to register everything to be accesses from everywhere but we can talk about that later perhaps.

For now lets go to our `app/app.module.ts` and add an import for the `TaskService` and then pass it into the providers array.

#### Updated `app.module.ts`

import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';
import { FormsModule } from '@angular/forms';
import { HttpModule } from '@angular/http';
import { AppRoutingModule } from './app-routing.module';

import { AppComponent } from './app.component';
import { TaskListComponent } from './task-list/task-list.component';
import { TaskService } from './services/task.service';              // <= This is new

@NgModule({
  declarations: \[
    AppComponent,
    TaskListComponent
  \],
  imports: \[
    BrowserModule,
    FormsModule,
    HttpModule,
    AppRoutingModule
  \],
  providers: \[
    TaskService                                                        // <= This is new
  \],
  bootstrap: \[AppComponent\]
})
export class AppModule { }

Now your app should load like before so we know things are working with our service.

## Code

Code can be found at [Github/BrettMN/quick-look](https://github.com/BrettMN/quick-look/tree/master/ng-quick-look)

## More Interesting?

Yay! We now have a service! Oddly our app looks exactly the same as it did without the service. Maybe this was a but more work than we will need for a simple TODO app, what do you think? Let me know by leaving a comment below or emailing [brett@wipdeveloper.com](mailto:brett@wipdeveloper.com).
