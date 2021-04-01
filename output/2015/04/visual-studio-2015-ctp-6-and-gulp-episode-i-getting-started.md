---
layout: "post.11ty.js"
title: "Visual Studio 2015 CTP 6 and Gulp - Episode I: Getting Started"
date: "2015-04-26"
tags: 
  - "Blog"
  - "Gulp"
  - "Task Runner Explorer"
  - "Visual Studio"
slug: "visual-studio-2015-ctp-6-and-gulp-episode-i-getting-started"
---

In ASP.NET 5 Bundling and Minification will **[not](https://github.com/aspnet/Home/issues/134)** be handled by Visual Studio. To achieve the same results as was possible with the ASP.NET of yesteryear (or earlier today if that's your thing) a build process like Grunt or Gulp will be necessary. With the Task Runner Explorer that is included with Visual Studio 2015, it is possible to assign predefined tasks to run at certain points during your build process. To make effective use of the new (to .NET) way of doing things; getting an understanding of either [Gulp](http://gulpjs.com/) or [Grunt](http://gruntjs.com/) will be necessary.

I've personally decided to become familiar with Gulp. So far I have not worked with Grunt so I can not give any opinion on it. From my understanding the main differences are that Grunt is set up mostly through configuration and Gulp is setup by programming JavaScript. I could be wrong, but that was my understanding of the main differences. Oh and Grunt has about 3 times as many plugins.

#### What's Gulp again?

Gulp has 4 things that it can do: `task`, `src`, `dest`, and `watch`  
\- `task` is used to define a function that can be called by other functions as a dependency or can be invoked directly. - `src` is used to get files to use in a stream. - `dest` is used as a destination for the stream you are working with and will save files. - `watch` is used to specify a file or group of files to monitor for changes and perform a task or tasks when a change occurs.

> More details about the gulp functions can be found in the [gulp docs](https://github.com/gulpjs/gulp/blob/master/docs/API.md).

#### Do what now?

In this post we will walk through getting Gulp and setting up a gulpfile.js to convert our SCSS to CSS along with concatenate, compress and mangle some JavaScript. I started with a new ASP.NET Web Application and chose the "ASP.NET 5 Preview Empty" template, but you can use any web project you would like.

#### Get Node.js

If you are using Visual Studio 2015 a copy of Node.js should have be installed for use unless you opted out of it. If you need to to get Node.js go to [https://nodejs.org/](https://nodejs.org/) and use the big 'Install' button, follow directions from there.

#### Get Gulp

To get Gulp open a console at your project level and type `npm install -g gulp` like so:

```
C:workspacegulp>npm install -g gulp  
C:UsersBrettAppDataRoamingnpmgulp -> C:UsersBrettAppDataRoamingnpmnode_modulesgulpbingulp.js  
gulp@3.8.11 C:UsersBrettAppDataRoamingnpmnode_modulesgulp  
├── deprecated@0.0.1
├── interpret@0.3.10
├── pretty-hrtime@0.2.2
├── archy@1.0.0
├── v8flags@2.0.5 (user-home@1.1.1)
├── tildify@1.0.0 (user-home@1.1.1)
├── minimist@1.1.1
├── chalk@0.5.1 (ansi-styles@1.1.0, escape-string-regexp@1.0.3, supports-color@0.2.0, has-ansi@0.1.0, strip-ansi@0.3.0)
├── semver@4.3.3
├── orchestrator@0.3.7 (stream-consume@0.1.0, sequencify@0.0.7, end-of-stream@0.1.5)
├── liftoff@2.0.3 (extend@2.0.0, flagged-respawn@0.3.1, resolve@1.1.6, findup-sync@0.2.1)
├── gulp-util@3.0.4 (array-differ@1.0.0, beeper@1.0.0, object-assign@2.0.0, array-uniq@1.0.2, lodash._reescape@3.0.0, lo
dash._reinterpolate@3.0.0, lodash._reevaluate@3.0.0, replace-ext@0.0.1, vinyl@0.4.6, chalk@1.0.0, lodash.template@3.5.0,  
 through2@0.6.5, multipipe@0.1.2, dateformat@1.0.11)
└── vinyl-fs@0.3.13 (graceful-fs@3.0.6, strip-bom@1.0.0, vinyl@0.4.6, defaults@1.0.2, mkdirp@0.5.0, through2@0.6.5, glob
-stream@3.1.18, glob-watcher@0.0.6)
```

> This was the unedited response from the command. I'm going to remove some of the unnecessary feedback from the console output from here on out.

Wait a bit for the install and then install Gulp locally `npm install --save-dev gulp`:

```
C:workspacegulp>npm install --save-dev gulp  
gulp@3.8.11 node_modulesgulp  
...

C:workspacegulp>  
```

With these basic tools you can begin to start getting the specific tools for your task. Lets start with: [gulp-sass](https://www.npmjs.com/package/gulp-sass/) to compile SCSS to CSS, [gulp-concat](https://www.npmjs.com/package/gulp-concat/) to concatenate files, and [gulp-uglify](https://www.npmjs.com/package/gulp-uglify/) to Minify the JavaScript. Use `npm install --save-dev gulp-sass gulp-concat gulp-uglify` to install all three at once, like this:

```
C:workspacegulp>npm install --save-dev gulp-sass gulp-concat gulp-uglify  
/
> node-sass@2.1.1 install C:workspacegulpnode_modulesgulp-sassnode_modulesnode-sass
> node scripts/install.js

> node-sass@2.1.1 postinstall C:workspacegulpnode_modulesgulp-sassnode_modulesnode-sass
> node scripts/build.js

`win32-x64-node-0.12` exists; testing
Binary is fine; exiting  
gulp-concat@2.5.2 node_modulesgulp-concat  
...

gulp-uglify@1.2.0 node_modulesgulp-uglify  
...

gulp-sass@1.3.3 node_modulesgulp-sass  
...

C:workspacegulp>
```

In the output, you can see that the 3 distinct installs occurred.

Fade to back, roll credits....

Ok, just kidding. Continue your adventures with [Visual Studio 2015 CTP 6 and Gulp Episode II: First Task](https://www.wipdeveloper.com/2015/04/29/visual-studio-2015-ctp-6-and-gulp-episode-ii-first-task/).
