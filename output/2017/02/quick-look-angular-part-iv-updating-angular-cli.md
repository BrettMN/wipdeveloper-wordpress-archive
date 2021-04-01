---
layout: "post.11ty.js"
title: "Quick Look @ Angular Part IV - Updating Angular-CLI"
date: "2017-02-27"
tags: 
  - "Angular"
  - "AngularCLI"
  - "Blog"
  - "Quick Look"
slug: "quick-look-angular-part-iv-updating-angular-cli"
---

# Part IV - Update Angular-CLI

Lets see, up to now we have [created a simple app](/2017/02/16/quick-look-angular/), [added a component](/2017/02/20/quick-look-angular-part-ii-add-a-component/) and [added a service](/2017/02/22/quick-look-angular-part-iii-create-a-service/). And I was planning on creating a component to add new tasks but there's a new release of the Angular-CLi, so lets update it.

> Before I could move on to adding the new component I updated my Angular-CLI so I included it here.

## Update Angular-CLI

A new release of the Angular-CLI is out since we started so let uninstall the old one globally and re-install it.

#### Reinstall Globally with NPM

npm uninstall -g angular-cli @angular/cli
npm cache clean
npm install -g @angular/cli@latest

Now lets update the copy in our developer environment:

#### Update Dev Environment

npm install --save-dev @angular/cli@latest

Now if I run `ng serve` I get the following message in my terminal:

#### Update the `angular-cli.json` Warning

Environment configuration does not contain "environmentSource" entry.

A new environmentSource entry replaces the previous source entry inside environments.

To migrate angular-cli.json follow the example below:

Before:

"environments": {
  "source": "environments/environment.ts",
  "dev": "environments/environment.ts",
  "prod": "environments/environment.prod.ts"
}

After:

"environmentSource": "environments/environment.ts",
"environments": {
  "dev": "environments/environment.ts",
  "prod": "environments/environment.prod.ts"
}

So lets update our `angular-cli.json`. What I did us move line 26 to after line 24 making it the new line 25 and change the `source` to `environmentSource`.

Now `ng serve` works fine :)

#### `ng serve` in Action

PS D:\\quick-look\\ng-quick-look> ng serve
\*\* NG Live Development Server is running on http://localhost:4200 \*\*
Hash: b0278f0cc9b3aaad3693
Time: 13872ms
chunk    {0} polyfills.bundle.js, polyfills.bundle.js.map (polyfills) 153 kB {4} \[initial\] \[rendered\]
chunk    {1} main.bundle.js, main.bundle.js.map (main) 13 kB {3} \[initial\] \[rendered\]
chunk    {2} styles.bundle.js, styles.bundle.js.map (styles) 9.77 kB {4} \[initial\] \[rendered\]
chunk    {3} vendor.bundle.js, vendor.bundle.js.map (vendor) 2.99 MB \[initial\] \[rendered\]
chunk    {4} inline.bundle.js, inline.bundle.js.map (inline) 0 bytes \[entry\] \[rendered\]
webpack: Compiled successfully.

Next we can add a new component to make use of the service we created [last time](/2017/02/22/quick-look-angular-part-iii-create-a-service/).

## Code

Code can be found at [Github/BrettMN/quick-look](https://github.com/BrettMN/quick-look/tree/master/ng-quick-look)

## Update Complete

Did you have any issues updating your project? Let me know by leaving a comment below or emailing [brett@wipdeveloper.com](mailto:brett@wipdeveloper.com).
