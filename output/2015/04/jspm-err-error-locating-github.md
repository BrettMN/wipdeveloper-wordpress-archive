---
layout: "post.11ty.js"
title: "jspm err  Error locating github:..."
date: "2015-04-17"
tags: 
  - "Blog"
  - "jspm"
slug: "jspm-err-error-locating-github"
---

While trying to install some files through jspm the other day I kept receiving an error.

#### Oh noes!

```
E:WorkspaceCurrentProject>jspm install  
     Looking up npm:font-awesome
     Downloading npm:font-awesome@4.3.0

err  Error locating github:aurelia/framework.

warn Installation changes not saved.  
```

Naturally, I tried a few more times to see if it might work. It wouldn't, of course, but the project that caused the error would change. It was cycling through all the projects that were hosted on GitHub that had been installed with jspm. Of course nothing was being saved since `warn Installation changes not saved` after all.

After some frustration I tried `jspm init` just for the fun of it.

```
E:WorkspaceCurrentProject>jspm init  
ok   Verified package.json at package.json  
     Verified config file at config.js
     Looking up loader files...
       es6-module-loader.js
       es6-module-loader.js.map
       system.js
       es6-module-loader.src.js
       system.src.js
       system.js.map

     Using loader versions:
       es6-module-loader@0.16.5
       systemjs@0.16.7

err  Error downloading loader files.

err  Error locating github:jmcriffey/bower-traceur.  
```

#### Ok so it wasn't that fun since it's still broke

After some time trying to resolve this issue that involved steps such as `jspm registry config github`; uninstalling and reinstalling git, node, and jspm; and just generally being frustrated at the lack of answers from the internet, I decided to take a look at the config file for jspm.

#### How to tell if it's any good

I had a computer where jspm was working fine so I compared it's config file to the computer that was not working. On the not working computer, the config file contained values for `registry` and `endpoints` but these values were not on the working computer. While searching I saw that endpoints where changed to registries at version 0.15.0 so there was probably an issue that arose from not properly updating my jspm.

#### And the fix

To resolve this issue I deleted the config file from my `[systempath]/users/[currentuser]/.jspm` folder then things worked correctly again.

```
E:WorkspaceCurrentProject>jspm install  
Looking up npm:font-awesome  
Updating registry cache...  
Looking up github:systemjs/plugin-css  
Looking up github:aurelia/bootstrapper  
... whole
... bunch
... more
... stuff
Looking up github:jmcriffey/bower-traceur  
Looking up github:jmcriffey/bower-traceur-runtime  
ok   Installed traceur-runtime as github:jmcriffey/bower-traceur-runtime@0.0.87 (0.0.87)  
ok   Installed traceur as github:jmcriffey/bower-traceur@0.0.87 (0.0.87)  
ok   Loader files downloaded successfully

ok   Install complete.  
```

#### :)
