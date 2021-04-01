---
layout: "post.11ty.js"
title: "Illuminated Cloud Using External Debug Log for Offline Debugging"
date: "2019-02-06"
tags: 
  - "Blog"
  - "Illuminated Cloud"
  - "Salesforce"
  - "SalesforceDeveloper"
slug: "illuminated-cloud-using-external-debug-log-for-offline-debugging"
coverImage: "Screen-Shot-2019-02-09-at-3.07.58-PM.png"
---

https://youtu.be/dpmWAQA9\_04

Hello, I'm Brett with WIPDeveloper.com. I use Illuminated Cloud for my general day to day development with Salesforce. It has a wonderful offline debugging feature.

## Sharing Log File Blues

But the other day I encountered an issue where I had to debug log that I did not have access to the org of. We were deploying a change that to production and I did not have production access. So I was emailed the log.

## Debugging Emailed Log Files

Now, this might be an issue where you have to sit there and read through the log manually or with Illuminated Cloud, you can set it up so that you can paste the log file into a debug context. So I'm going to show you how to do that so becomes a little bit more obvious.

Go to run, edit configuration. Under Apex offline debugger.

Add a new one with the little plus sign

Apex Offline Debugger.

Now I'm going to say.

I'm gonna give it a name.

I don't believe any of these log levels matter. What we're gonna do is we're gonna take a log file and paste it into the log body.

And at the very top of the log file, the log levels are specified. So you see Apex code debug, Apex profiling info, call out info, and you can't change that here. So I don't believe these settings will change anything.

But we can with this log file and this is just an example log file.

Now I can hit ok. So we choose the debug log from or the we choose the configuration within the drop down External Log press the

little bug to make it start working, stepping through

and now we can do the offline debugging.

I would show you that code here but I did not have time to set up a full sample environment with that, if you get a debug log with the appropriate log levels, like Apex at finest, you can see what values are being assigned where and troubleshoot your issues without being able to, for org you don't have access to.

Or if you are deploying a change set to production. And you since the code never gets deployed, you can't pull up the debug log and step through it in the org environment. Because the code doesn't isn't in the org, but you can pull it back to the environment where you can pull it into your code base for the environment you're deploying from. In this case, I was deploying from a QA environment and we could step through it since it is the same code and see where the issues are. So it works for troubleshooting change, set appointments and for troubleshooting or not actually access.

## Links

[ApexOfflineDebugger demonstration video](https://www.youtube.com/watch?v=7heov_0Yd6E)

## That’s it for now.

Remember to sign up for **[The Weekly Stand-Up!](https://wipdeveloper.wpcomstaging.com/newsletter/)**  and you can get updated with any new information we have on WIPDeveloper.com.
