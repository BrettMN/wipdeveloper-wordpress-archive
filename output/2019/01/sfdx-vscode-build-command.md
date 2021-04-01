---
layout: "post.11ty.js"
title: "SFDX VSCode Build Command"
date: "2019-01-07"
tags: 
  - "Blog"
  - "Salesforce"
  - "SalesforceDeveloper"
  - "VSCode"
slug: "sfdx-vscode-build-command"
coverImage: "Screen-Shot-2019-01-07-at-8.40.05-PM.png"
---

https://youtu.be/UdymIsDFinA

Hello, this is Brett with WIPDeveloper.com. With our scratch org ready we can now create a Lighting Web Component and push it to the scratch org to see it in action.

## Command Palette Fatigue

All the commands for SFDX in Visual Studio Code are done through the Command Palette. When pushing to the default org you might get into the habit of making a change, open the Command Palette and pressing enter. This works to push changes to your default org if it was the last command you used but the flow of things will be interrupted if you have recently used a different option with the Command Palette as `SFDX: Push Source to Default Scratch Org` wont be the first option in the recently used list.

We can cut back on these steps and prevent ourselves from accidentally using the wrong command if we bind the `sfdx force:source:push` CLI command to the Visual Studio Code built in "Build" Command.

## Visual Studio Code's Build Command

Visual Studio Code allows us to preform a "Build" Command with the `cmd+shift+b` on Mac or `ctrl+shift+b` on Windows.

![](https://i1.wp.com/wipdeveloper.com/wp-content/uploads/2019/01/Screen-Shot-2019-01-08-at-4.16.09-PM.png?fit=1024%2C375&ssl=1)

Visual Studio Code Build Command in the Keyboard Shortcuts menu.

This Build command has to be configured and when you press it the first time it will ask what task to assign to it.

If you don't have any tasks in your current project it will prompt you to create one from a template.

![](https://i2.wp.com/wipdeveloper.com/wp-content/uploads/2019/01/Screen-Shot-2019-01-08-at-4.24.14-PM.png?fit=1024%2C153&ssl=1)

VS Code asking you to configure a Build Task.  

![](https://i1.wp.com/wipdeveloper.com/wp-content/uploads/2019/01/Screen-Shot-2019-01-08-at-4.24.24-PM.png?fit=1024%2C138&ssl=1)

VS Code offering to create a `task.json` from a template.

![](https://i0.wp.com/wipdeveloper.com/wp-content/uploads/2019/01/Screen-Shot-2019-01-08-at-4.24.34-PM.png?fit=1024%2C243&ssl=1)

VS Code Template Options, we will use **Others**

#### The Others `task.json` Template

```
{
    // See https://go.microsoft.com/fwlink/?LinkId=733558
    // for the documentation about the tasks.json format
    "version": "2.0.0",
    "tasks": [
        {
            "label": "echo",
            "type": "shell",
            "command": "echo Hello"
        }
    ]
}
```

Lets rename the label to `push` and change the command to `sfdx force:source:push`

#### Update `task.json`

```
{
    // See https://go.microsoft.com/fwlink/?LinkId=733558
    // for the documentation about the tasks.json format
    "version": "2.0.0",
    "tasks": [
        {
            "label": "push",
            "type": "shell",
            "command": "sfdx force:source:push"
        }
    ]
}
```

Now if we try the build command we can select to configure `push` as the task to run.

![](https://i1.wp.com/wipdeveloper.com/wp-content/uploads/2019/01/Screen-Shot-2019-01-08-at-4.35.00-PM.png?fit=1024%2C130&ssl=1)

Select `push` to set it as the task that runs when you "Build"

Once it's configured as the build command VS Code sets it as part of the build group and as the default action. The final `task.json` should look somewhat like this.

#### Final `task.json`

```
{
    // See https://go.microsoft.com/fwlink/?LinkId=733558
    // for the documentation about the tasks.json format
    "version": "2.0.0",
    "tasks": [
        {
            "label": "push",
            "type": "shell",
            "command": "sfdx force:source:push",
            "group": {
                "kind": "build",
                "isDefault": true
            }
        }
    ]
}
```

This should allow us to press `cmd+shift+b` on Mac or `ctrl+shift+b` on Windows save our changes to Salesforce and move on the the next task without having to navigate the Command Palette.

## That’s it for now.

Remember to sign up for **[The Weekly Stand-Up!](https://wipdeveloper.wpcomstaging.com/newsletter/)**  and you can get updated with any new information we have on WIPDeveloper.com.
