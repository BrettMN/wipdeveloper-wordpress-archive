---
layout: "post.11ty.js"
title: "TypeScript - Compile with Gulp"
date: "2015-12-12"
tags: 
  - "Blog"
  - "Gulp"
  - "Typescript"
slug: "typescript-compile-with-gulp"
---

![TypeScript](images/typescript_logo_small1.png)

Some times you just want to make a few quick changes to your code and not have to wait for your full IDE to start-up. At those times you have have to use the command line to compile your TypeScript. But typing `tsc app.ts --module amd --target es5` can get tedious, sure you could use the `--watch` option but what if you want to also applying some standards control like tslint? Well, if you configure a gulp workflow to compile your TypeScript you can make this happen. It may also provided an added benefit of taking some work off of your, possibly, overburdened IDE.

#### What You Need

To make it possible to use Gulp to compile your TypeScript you are going to need to install a few things first.

- Nodejs
- npm
- gulp
- gulp-typescript

First Nodejs is required because npm, and gulp are booth dependant on it. Second npm is what we will use to get Gulp and gulp-typescript. Than Gulp is the build pipeline that we will configure to use gulp-typescript to compile our TypeScript to JavaScript.

#### Installation

If this is your first time using node and Gulp I covered installation and basic setup in a earlier post titled [Visual Studio 2015 CTP 6 and Gulp - Episode I: Getting Started](/2015/04/26/Visual-Studio-2015-CTP-6-and-Gulp-Episode-I-Getting-Started). The basics are still the same so I will asume you have successfully installed Nodejs, npm and Gulp.

> Of course if it's been a while since you used Gulp, npm or node you may want to update to the latest versions of each one.

To get `gulp-typescript` we will run the command `npm install gulp-typescript --save-dev` and then we can get on with the show.

#### Configuring

In our `gulpfile.ja` we will do the basic set up of require `gulp` and `gulp-typescript`

##### `gulpfile.js` Begining

```javascript
  var gulp = require('gulp');
  var typescript = require('gulp-typescript');
```

Now that we have access to Gulp and the gulp-typescript plugin we can create a `gulp.task()` with some clever name, I chose 'typescript'.

##### `gulpfile.js` Continued

```javascript
  gulp.task('typescript', function() {
    return gulp.src('app/**/*.ts')
    .pipe(typescript())
    .pipe(gulp.dest('./app/'));
  });
```

We've seen the `gulp.src()` and `gulp.dest()` before, along with the `.pipe()`. Set up this way we will get all the `.ts` files in our `app/` directory and run them through the TypeScript compiler when we call `typescript()`. When we run `gulp typescript` though we may get some errors.

```
PS E:WorkspaceTypeScript> gulp typescript  
[22:31:54] Using gulpfile E:WorkspaceTypeScriptgulpfile.js
[22:31:54] Starting 'typescript'...
appapp.ts(1,15): error TS1148: Cannot compile modules unless the '--module' flag is provided.  
[22:31:55] TypeScript: 1 semantic error
[22:31:55] TypeScript: emit succeeded (with errors)
[22:31:55] Finished 'typescript' after 710 m
```

Here it says I didn't specify a `--module` flag, this is an issue since my file exports a class. To remedy this we will need to specify some options. To set the options for our compilation we pass in a configuration object when we call the our `typescript()`. Something along the lines of `{ module: 'system' }`

##### Final Configuration

```javascript
gulp.task('typescript', function() {  
    return gulp.src('app/**/*.ts')
    .pipe(typescript({
        module: 'system'    
    }))
    .pipe(gulp.dest('./app/'));
});
```

#### Reap the Rewards

Now when we run `gulp typescript` things should work a little different.

```
PS E:WorkspaceTypeScript> gulp typescript  
[23:25:42] Using gulpfile E:WorkspaceTypeScriptgulpfile.js
[23:25:42] Starting 'typescript'...
[23:25:43] Finished 'typescript' after 71
```

Now our can use our compiled JavaScript, yay!

#### Conclusion

Using a build pipeline to compile your TypeScript allows for more flexibility in what happens when it's compiled along with allowing you to choose when it's compiled. Both of these features make it an appealing alternative to relying on your IDE to compile your TypeScript. Of course you may have a different opinion on the topic. If so let us know by leaving a comment bellow or, if you are feeling a little introverted, send an email to me at [brett@wipdeveloper.com](mailto:brett@wipdeveloper.com).
