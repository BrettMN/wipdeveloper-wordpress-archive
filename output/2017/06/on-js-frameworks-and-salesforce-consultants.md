---
layout: "post.11ty.js"
title: "On JS Frameworks and Salesforce Consultants"
date: "2017-06-03"
tags: 
  - "Blog"
  - "Craftmanship"
  - "JavaScript"
  - "Salesforce"
  - "SalesforceDeveloper"
slug: "on-js-frameworks-and-salesforce-consultants"
coverImage: "sf-and-fe-frameworks.png"
---

A few days ago a reader by the name oh **Havs** left a comment on [Visualforce with Vue.js – Part 2](/2017/04/04/visualforce-with-vue-js-part-2/) which is great!  They also asked a question, which is also great!

> **Havs** This is awesome! But I wonder about the maintainability here. I would love to be able to use any JS framework in Salesforce... But unless the next developer or consultant know the framework used, the learning curve would be high.. Given that, I could see if it's you're own product, and there is a specific use case, then it would be great.

I left a message at the time but wanted to add to it.

## Maintainability

If you are making decisions based on what you think some developer working on the project later so you stick with plain JavaScript or use just jQuery you are **not** keeping the project maintainable.

Modern front-end frameworks provide ways to write less code, with more (or any) tests and more understandable.

Let's take a look at why.

## Write Less Code

Arguably the only way to get fewer bugs in your program is to have less code and one way to do that is to not create custom frameworks with a jQuery dependency.

I say custom framework because, with or without jQuery,  everything you write to wire up an event handlers, make an http call, or the object you create to manage state is a custom framework.  That means it's up to you to write the tests, handle all edge cases, and there will be no place to turn for help beyond basic JavaScript questions since no one outside of your team is working in this custom framework you have created.

## Maintainable

Most modern frameworks include examples of how to test the application.  Some come with tests setup when you follow the setup guide.  So right out of the gate you are at least 3 steps closer to having your first test written than if you were creating everything custom.

## Understandable

When you use a framework like [Vue.js](/tag/vuejs/) or [Angular](/tag/angular/) you are setting the ground work for a common structure to you application.  It wont require as much time for some one who already knows a specific framework to start contributing to a project since framework specific knowledge eases the barrier to entry.  Can the same be said for a project that is all custom?

## Non-Developer Reasons

So far we have talked about developer reasons for not sticking to the "tried and true" method of plain JavaScript and jQuery but could there be a business case to be made?  If you are worried about the next developer or consultant working on the project, why not put that worry on the business?

Make a case with the project owner or decision maker for using a framework and explain what it means going forward.  In the case of the concern about future developers that means the customer would be agreeing to the responsibility of using developers capable of learning the framework if they don't already know how.

A second non-dev reason to bring the business into the process of choosing a framework is to ensure any legal guidelines are maintained.   As a consultant I have to get clients to agree to the license of a library before it can be used since I wouldn't want to cause my client to violate any legal policy they have.

## Conclusion

Think I am way off? Let me know by leaving a comment below, emailing [brett@wipdeveloper.com](mailto:brett@wipdeveloper.com) or following and yelling at me on [Twitter/BrettMN](https://twitter.com/BrettMN).
