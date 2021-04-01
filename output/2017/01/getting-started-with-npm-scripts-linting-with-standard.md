---
layout: "post.11ty.js"
title: "Getting Started with NPM Scripts - Linting with Standard"
date: "2017-01-06"
tags: 
  - "Blog"
  - "npm scripts"
  - "standardjs"
slug: "getting-started-with-npm-scripts-linting-with-standard"
---

[When last we left](/2016/12/06/getting-started-with-npm-scripts-watch/) our little npm scrpt starter project we had added a clean function to remove our old JavaScript files. This time we will set up some linting for our JavaScript.

## And the Journey Continues...

Like last we will be starting from where we left off before.

> If you would like to join in at this point you can get the code to begin with at [Getting Started with NPM Scripts - Delete Things!](https://github.com/BrettMN/npm-scripts-getting-started/releases/tag/post03).

Since most of what we are doing is similar to our previous steps I'm going to cut to the chase a bit. Install and save `standard` as a dev dependency:

#### Install `standard`

```
npm install --save-dev standard  
```

Add a new line to the scripts section of your `package.json`:

#### New npm script

```
"lint:js": "standard src/**/*.js"
```

> We pass in the path to our `src/` folder so we only lint the code we are writing.

And Update the `watch:js` to run `lint:js` before `clean:js` and the `build:js`:

#### Updated `watch:js`

```
"watch:js": "chokidar src/**/*.js -c "npm run lint:js && npm run clean:js && npm run build:js"",
```

And we are done.

## But why

If you run `watch:js` now you may notice some new output when you make a change to a file:

```
Watching "src/**/*.js" ..  
change:srcsubsub-app.js

> npm-scripts-getting-started@0.0.3 lint:js D:WorkspaceBlognpm-scriptsgetting-started
> standard src/**/*.js

standard: Use JavaScript Standard Style (http://standardjs.com)  
standard: Run `standard --fix` to automatically fix some problems.  
  D:WorkspaceBlognpm-scriptsgetting-startedsrcapp.js:1:107: Extra semicolon.
  D:WorkspaceBlognpm-scriptsgetting-startedsrcapp.js:3:5: 'myApp' is assigned a value but never used.
  D:WorkspaceBlognpm-scriptsgetting-startedsrcapp.js:3:27: Extra semicolon.
  D:WorkspaceBlognpm-scriptsgetting-startedsrcapp.js:3:28: Newline required at end of file but not found.
  D:WorkspaceBlognpm-scriptsgetting-startedsrcsubsub-app.js:3:5: 'mySubApp' is assigned a value but never used.
```

Did you notice the errors? `Extra semicolon.`, `'myApp' is assigned a value but never used.` and such? These are generated from our new step `lint:js` as we are using the [StandardJS](http://standardjs.com) JavaScript Standard Style linter to raise errors on things that do not conform to [the rules](http://standardjs.com/rules.html).

> a Linter performs [static analysis](https://en.wikipedia.org/wiki/Static_program_analysis), examines the code without running it, and returns errors for things that may cause issue (or bugs)

I can correct these errors in my `src/` folder by removing the semicolons from `app.js` and `sub-app.js`, adding a new line at the end of `app.js`. I could also run `standard --fix` and StandardJS would attempt to fix issues that are pretty straightforward. I imagine most of the errors we started with will be fixed except for the `'mySubApp' is assigned a value but never used.` errors.

To make this easier I will add `--fix` to the script we created previously so it will finally look like this:

#### `lint:js` Final

```
"lint:js": "standard src/**/*.js --fix"
```

## Why StandardJS

I picked StandardJS as the style to use so there was less room for interpretation. If some one joins the project they will have to conform to the style or there will be issues with each change they make. This will help keep a specific coding standard throughout the project and since StandardJS is pretty set there shouldn't be much time used debating each option that could be set in a more configurable linter.

> All code used in this example can be found at [BrettMN/npm-scripts-getting-started](https://github.com/BrettMN/npm-scripts-getting-started)

## Conclusion

Now that we have some coding standards to check things maybe we should add a test or at least the ability at add and run tests. Are there any other steps you would like to see? Let me know by leaving a comment below or sending an email to me at [brett@wipdeveloper.com](mailto:brett@wipdeveloper.com) and let me know.
