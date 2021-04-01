---
layout: "post.11ty.js"
title: "Playing Around with Yarn"
date: "2017-01-26"
tags: 
  - "Blog"
  - "npm"
  - "npm scripts"
  - "yarn"
slug: "playing-around-with-yarn"
---

Back in October Facebook, in collaboration with Exponent, Google, and Tilde, [announced](https://code.facebook.com/posts/1840075619545360) an alternative package manager to npm called [Yarn](https://yarnpkg.com/). Some of the stated goals for this new package manager were:

- to address issues caused by installing the same packages in different orders
- decrease install times by using previously fetched and cached results
- an offline mode
- a way to guarantee that installs determine the same results with lock files

It uses the npm registry so the packages are the same as you have been using the difference is the client you use to access and install the packages.

## Some Commands

A lot of the commands are the same as npm commands:

#### init

npm init => yarn init

#### add a package

npm install <name> => yarn add \[package\]
npm install <name>@<version> => yarn add \[package\]@\[version\]
npm install <name>@<tag> => yarn add \[package\]@\[tag\]

#### run install

npm install => yarn

> In case you havn't caught on the previous examples had aformat of `[npm command] => [yarn command]` where `npm command` is the command for the desired outcome using npm and `[yarn command]` was the command for the desired outcome using Yarn.

More commands can be found in the [documentation](https://yarnpkg.com/en/docs/).

## Install

To install Yarn you go to the [install page](https://yarnpkg.com/en/docs/install). Follow the recomended install procedure for your operating system and pat yourself on the back for a job well done...

## Try it Out

In the project I have I'm going to add a new package. In this case lodash because why not.

#### `yarn add lodash`

\`\`\`
├─ regjsparser@0.1.5

///
/// Stuff was here but removed to require less scrolling
///

└─ yargs@3.32.0
Done in 39.74s.
PS D:\\Workspace\\Blog\\yarn\\npm-scripts-getting-started>

Now since I did this in a project that had packages already it added a `yarn.lock` that is almost 2700 lines long so I wont be posting it here. The `yarn.lock` file should describe to other computers how to install the same packages and what versions so that all people working on the same project have the same experience. What this means is you shouldn't be telling some one "it works on my machine".

## Run a Script

If you read the last few posts yo umay be wondering if switching to Yarn means having to stop using npm scripts. In a word: nope.

You can use the `run` command just like with npm to run a script. Since the project I and trying Yarn out with is the same one that we had at the end of [Getting Started with NPM Scripts - Linting with Standard](https://www.wipdeveloper.com/2017/01/06/getting-started-with-npm-scripts-linting-with-standard/) I can use the following command:

#### `yarn run build:js`

PS D:\\Workspace\\Blog\\yarn\\npm-scripts-getting-started> yarn run build:js
yarn run v0.19.1
$ babel src -d dist --presets es2015
src\\app.js -> dist\\app.js
src\\sub\\sub-app.js -> dist\\sub\\sub-app.js
Done in 1.34s.

> That's right to run scripts with Yarn it's just `yarn run [script name]`

And everything runs just fine and there should be less surprises as the project moves from machine to machine.

## And Also

The logo is a kitten, I mean come on you have to like that.

![Yarn Logo](images/yarn-kitten1.png)

## Conclusion

So far Yarn seems like a good idea. I'm sure there are things that I'm missing but if it holds keeps most of it's ideals in place I might want to add the dist folder to my `.gitignore` since build results should be less questionable with more consistent environment setup for the build. Sound crazy? Leave a comment below or sending an email to me at [brett@wipdeveloper.com](mailto:brett@wipdeveloper.com) and let me know.
