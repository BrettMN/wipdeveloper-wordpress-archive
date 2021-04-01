---
layout: "post.11ty.js"
title: "Getting Started with NPM Scripts - Watch"
date: "2016-12-05"
tags: 
  - "Blog"
  - "chokidar"
  - "npm"
  - "npm scripts"
slug: "getting-started-with-npm-scripts-watch"
---

[Last time](/2016/12/05/getting-started-with-npm-scripts-babel/) we setup our first npm script to run [Babel](https://babeljs.io/) when we typed `npm run build:js`. This time lets setup a watch script to call our previous script when the javascript changes.

> Yes, I know that Babel has a watch flag `-w` to do this for us but hey, I want setup a watch script and this is what we have so far.

## The Journey Continues

We begin right where we left off, with a very minimal project that has one JavaScript file that we can transpile with our one npm script.

> If you would like to join in at this point you can get the code to begin with at [Getting Started with NPM Scripts - Babel](https://github.com/BrettMN/npm-scripts-getting-started/releases/tag/post01) .

We will implement a watch using the [Chokidar CLI](https://www.npmjs.com/package/chokidar-cli) so lets install is at a dev dependency with `npm install --save-dev chokidar-cli`

> Even though we are installing the "cli" version of Chokidar we will not be able to use in from the command line without it being in an npm script.

And that's all the installing we have for today.

## New Script Time

Now lets setup a script for watching our JavaScript. In the `scripts` section of our `package.json` lets add a comma (`,`) to the line that our `build:js` is on and add the following line after it:

#### `watch:js` script

```
"watch:js": "chokidar src/**/*.js -c "npm run build:js""
```

Lets look at the different parts here real quick:

Script Text

Meaning

"watch:js"

Name of the npm script

chokidar

command that will be exacuted, this is what says to use the chokidar-cli scripts we installed earlier

src/\*\*/\*.js

this is the pattern that Chokidar is looking to match. I have it looking for changes to all files that end with .js in a directory named 'src/'

\-c

The -c is the Chokidar to use a command when a file changes.

"npm run build:js"

This is the command that will be ran when a file matching the pattern changes. Since it contains spaces it requires quotes and I have escaped the quotes so they will work correctly.

This of course means our full `scripts` section now looks like this:

#### Complete `scripts` section

```
  "scripts": {
    "test": "echo "Error: no test specified" && exit 1",
    "build:js": "babel src -d dist --presets es2015",
    "watch:js": "chokidar src/**/*.js -c "npm run build:js""
  },
```

## And Action

Let's run our new `watch:js` script and see what happens by typing `npm run watch:js` in the command line.

#### `npm run watch:js` in Action

```
PS D:WorkspaceBlognpm-scriptsgetting-started> npm run watch:js

> npm-scripts-getting-started@0.0.1 watch:js D:WorkspaceBlognpm-scriptsgetting-started
> chokidar src/**/*.js -c "npm run build:js"

Watching "src/**/*.js" ..  
```

And... nothing...

Ok Now change or add a JavaScript file in the `src/` directory. I will be changing the existing `src/app.js`:

#### Something Changed!

```
Watching "src/**/*.js" ..  
change:srcapp.js

> npm-scripts-getting-started@0.0.1 build:js D:WorkspaceBlognpm-scriptsgetting-started
> babel src -d dist --presets es2015

srcapp.js -> distapp.js  
```

![Action Replay of npm run watch:js](images/npm-scripts-watch.gif)

You can see the line that says what changed `change:srcapp.js` this means the watched files triggered the change action because a file changed. Other trigger events include `add:srcnewapp.js` and `unlink:srcnewapp.js`. The `add` event is probably just a straight forward as the `change` event and the `unlink` event is a delete action. There are also 2 events for directories `addDir` and `unlinkDir` for that are triggered when directories are added and removed.

> An important thing to note is that even though we can detect a file being removed we aren't actually removing the results of the last successful transpile. This means that even though we detected removing `src/newapp.js` there is still a copy of `dist/newapp.js` out there in out `dist` directory. We will look at cleaning that up later though.

If you are keeping score with your own copy of a `package.json` heres what we should have ended up with:

#### Final `package.json`

```
{
  "name": "npm-scripts-getting-started",
  "version": "0.0.1",
  "description": "A simple getting started with npm scripts project",
  "main": "app.js",
  "scripts": {
    "test": "echo "Error: no test specified" && exit 1",
    "build:js": "babel src -d dist --presets es2015",
    "watch:js": "chokidar src/**/*.js -c "npm run build:js""
  },
  "keywords": [
    "npm",
    "scripts",
    "beginner"
  ],
  "author": "BrettMN <brett@wipdeveloper.com> (https://www.wipdeveloper.com)",
  "license": "MIT",
  "devDependencies": {
    "babel-cli": "^6.18.0",
    "babel-preset-es2015": "^6.18.0",
    "chokidar-cli": "^1.2.0"
  },
  "repository": {
    "type": "git",
    "url": "https://github.com/BrettMN/npm-scripts-getting-started.git"
  }
}
```

> All code used in this example can be found at [BrettMN/npm-scripts-getting-started](https://github.com/BrettMN/npm-scripts-getting-started)

## Conclusion

Now that we can set up watches for file changes what else do you think would be worth looking at? I would love to hear about it, leave a comment below or send an email to me at [brett@wipdeveloper.com](mailto:brett@wipdeveloper.com).
