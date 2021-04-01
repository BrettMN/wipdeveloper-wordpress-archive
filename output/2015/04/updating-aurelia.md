---
layout: "post.11ty.js"
title: "Updating Aurelia"
date: "2015-04-09"
tags: 
  - "Aurelia"
  - "Blog"
  - "jspm"
slug: "updating-aurelia"
---

The other day a new version of the 'pre-alpha' client framework Aurelia was released. It was accompanied by a blog post at [Durandal.io](http://blog.durandal.io/2015/04/09/aurelia-update-with-decorators-ie9-and-more/). It contained a section titled "How to Update" that described the steps to update your current Aurelia app to the current version.

The update steps all work great but it might need some clarification. Once you get to updating the "top level" Aurelia libraries it just says to `jspm install` each one found in the `package.json` file.

#### package.json jspm section Before Update

```javascript
"jspm": {
  "dependencies": {
    "aurelia-bootstrapper": "github:aurelia/bootstrapper@^0.9.5",
    "aurelia-dependency-injection": "github:aurelia/dependency-injection@^0.4.5",
    "aurelia-framework": "github:aurelia/framework@^0.8.8",
    "aurelia-http-client": "github:aurelia/http-client@^0.5.5",
    "aurelia-router": "github:aurelia/router@^0.5.8",
    "bootstrap": "github:twbs/bootstrap@^3.3.1",
    "font-awesome": "npm:font-awesome@^4.3.0"
  }
}
```

Now maybe it's just me but I miss-understood what was needed for the `jspm install` command. So to save you some time here's what you need to install with jspm. Use `jspm install` with the beginning of the value string that starts with the source such as 'github:' or 'npm:' but exclude the @version number. So to install 'aurelia-bootstrapper' on the command line you would use:

```
jspm install github:aurelia/bootstrapper  
```

Another thing is you probably want to do is remove references to the older version of each dependency. Either cut them out and past them in a temp file for reference or delete them after you have updated. This way you won't have 2 different versions referenced.

#### package.json jspm section After Update

```javascript
"jspm": {
  "dependencies": {
    "aurelia/bootstrapper": "github:aurelia/bootstrapper@^0.11.0",
    "aurelia/dependency-injection": "github:aurelia/dependency-injection@^0.6.0",
    "aurelia/framework": "github:aurelia/framework@^0.10.0",
    "aurelia/http-client": "github:aurelia/http-client@^0.7.0",
    "aurelia/router": "github:aurelia/router@^0.7.1",
    "bootstrap": "github:twbs/bootstrap@^3.3.1",
    "font-awesome": "npm:font-awesome@^4.3.0"
  },
  "devDependencies": {
    "traceur": "github:jmcriffey/bower-traceur@0.0.87",
    "traceur-runtime": "github:jmcriffey/bower-traceur-runtime@0.0.87"
  }
```

All in all it looks like Aurelia was already off to a decent start and is heading in a nice direction.
