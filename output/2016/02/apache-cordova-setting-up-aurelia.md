---
layout: "post.11ty.js"
title: "Cordova - Setting  Up to Use Aurelia"
date: "2016-02-05"
tags: 
  - "Aurelia"
  - "Blog"
  - "Cordova"
  - "Gulp"
slug: "apache-cordova-setting-up-aurelia"
---

We have looked at setting up Cordova and building and running on Android in [Cordova - Intro](/2016/01/13/apache-cordova-intro/) and [Cordova - Build Android](/2016/01/19/apache-cordova-build-android/) lets take a look at how to use a single page application framework like Aurelia.

### Setup

First we will need to create a new Cordova project like we did in [Cordova - Intro](/2016/01/13/apache-cordova-intro/). Once you have your new project we will need to initalize npm so we can keep track of our packages, so run `npm init` and proceed through the prompts. Since we are doping our npm stuff now lets also install `jspm`, `gulp` and `gulp-shell`, we will use these in a bit.

### Ruh-Roh Shaggy

While trying to get Aurelia, or more specifically the `system.js` module loader that jspm uses, to load modules properly. One idea I had was to create a new `package.json` that lives in the `www` folder and install jspm there. There are a few reasons I don't want to install jspm in the `www` folder:

- I don't want to deploy the `jspm_packages` folder with the app since the size on disk tends to get rather large.
- When I bundle the app it wont make any sense if the `jspm_packages` is still in the `www` folder.
- I only want one `package.json` to track all my modules.

### Well Shoot Now What?

What if instead of trying to configure `jspm` to install from the root and deploy from the `www` folder and not have issues once deployed to the device we install `jspm` like it was going to run from the root directory and just copy the necessary parts to the `www` folder? If only there was a way to automate this process so it occurrs when I edit a file. Now you may be thinking the answer to this was Gulp... and you'd be right.

### gulpfile

To make this work I created a `gulpfile` that basically has two tasks, to copy the `config.js` file from the root of the directory to the `www` directory and to copy the `jspm_packages` folder to the `www` directory.

#### `gulpfile.js`

```javascript
var gulp = require('gulp');

var dest = 'www/';

gulp.task('copy-config', () => {  
    return gulp.src('config.js')
        .pipe(gulp.dest(dest))
});

gulp.task('copy-jspm', () => {  
    return gulp.src('jspm_packages/**/*', { base: 'jspm_packages/' })
        .pipe(gulp.dest(dest + 'jspm_packages/'))
});

gulp.task('watch', () => {  
    gulp.watch(['config.js'], ['copy-config']);
    gulp.watch(['jspm_packages/**/*'], ['copy-jspm']);

});
```

I also added a watch but once you get your project started you may not need that running since you all the files you will be changing are already in the `www` folder unless you are adding new modules through jspm.

### Build Your App

Now you can build your app as you would normally. You will need to add the `'unsafe-inline'` to your `Content-Security-Policy` meta tag if you plan on using the inline script tags to load Aurelia-Bootstrapper but otherwise you should be ready to build out your Aurelia application.

### Conclusion

It's not fancy but it works. I'm sure there is a way to get the desired results of not copying all of the files from the `jspm_modules` into the `www` folder but hey, you can now start to build out your app and worry about that another time. Have a suggestion? I would like to hear it, leave a comment below or send an email to me at [brett@wipdeveloper.com](mailto:brett@wipdeveloper.com).
