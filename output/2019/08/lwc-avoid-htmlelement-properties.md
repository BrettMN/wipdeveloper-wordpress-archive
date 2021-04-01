---
layout: "post.11ty.js"
title: "LWC - Avoid HTMLElement Properties"
date: "2019-08-22"
tags: 
  - "Blog"
  - "LWC"
  - "Salesforce"
  - "SalesforceDeveloper"
slug: "lwc-avoid-htmlelement-properties"
coverImage: "Screen-Shot-2019-08-22-at-4.42.02-PM.png"
---

* * *

Hello, I'm Brett with WIPDeveloper.com. Last time, we talked about using it as a property in our Lightning web component, and how it was causing an error when the Lightning Debug Mode was enabled. Asking on Twitter did get a response from Kevin V. who works at Salesforce and is one of the architects behind Lightning Web Components. And it seems that all the HTMLElement properties are automatically hooked up to lightning elements, or the LightningElement in LWC.

So if you look at this is on the MDN Docs or Mozilla docs, you can look at all the property names that we probably should be avoiding. So that's this list over here. And I was playing around with it. And I was able, and I'm not saying you should do this, some of these will actually work somewhat. Like you, you use content editable and try to bind to it, it won't throw an error. But it doesn't actually pass the value to the template. Inner text does pass the value to the template. But it's probably best to avoid anything that is declared as a property on the HTMLElement. side now, since it isn't actually listed over here, should be right before `innerText`. It's actually declared on the Element. So not only should you avoid all of these, which probably makes sense, you should avoid all the properties declared in the base Element. And those are listed also on the MDN website. So if you were to list them on your site, or in your JavaScript, it'd be a pretty big list. So almost 115 properties to avoid.

Now, if I uncomment one of these, like, I don't know, `accessKey` and apply it. We will see refreshing the page. But I do get that error. So best to avoid any of the properties to find on HTMLElement and the Element one working with Lightning Web Components. They might be working in a rule for linting to prevent you from being able to save it. So I will include a list below. So if you are having a problem with this, you might stumble upon this and understand why.

## Properties to Avoid

- accessKey
- attributes
- childElementCount
- children
- classList
- className
- clientHeight
- clientLeft
- clientTop
- clientWidth
- currentStyle
- firstElementChild
- id
- innerHTML
- lastElementChild
- localName
- name
- namespaceURI
- nextElementSibling
- onfullscreenchange
- onfullscreenerror
- openOrClosedShadowRoot
- outerHTML
- prefix
- previousElementSibling
- runtimeStyle
- scrollHeight
- scrollLeft
- scrollLeftMax
- scrollTop
- scrollTopMax
- scrollWidth
- shadowRoot
- slot
- tabStop
- tagName
- contentEditable
- contextMenu
- dataset
- dir
- hidden
- innerText
- isContentEditable
- lang
- nonce
- offsetHeight
- offsetLeft
- offsetParent
- offsetTop
- offsetWidth
- onabort
- onanimationcancel
- onanimationend
- onanimationiteration
- onauxclick
- onblur
- oncancel
- oncanplay
- oncanplaythrough
- onchange
- onclick
- onclose
- oncontextmenu
- oncopy
- oncuechange
- oncut
- ondblclick
- ondurationchange
- onended
- onerror
- onfocus
- ongotpointercapture
- oninput
- oninvalid
- onkeydown
- onkeypress
- onkeyup
- onload
- onloadeddata
- onloadedmetadata
- onloadend
- onloadstart
- onlostpointercapture
- onmousedown
- onmouseenter
- onmouseleave
- onmousemove
- onmouseout
- onmouseover
- onmouseup
- onpaste
- onpause
- onplay
- onpointercancel
- onpointerdown
- onpointerenter
- onpointerleave
- onpointermove
- onpointerout
- onpointerover
- onpointerup
- onreset
- onresize
- onscroll
- onselect
- onselectionchange
- onselectstart
- onsubmit
- ontouchcancel
- ontouchstart
- ontransitioncancel
- ontransitionend
- onwheel
- outerText
- style
- tabIndex
- title

## Links

- [Element on MDN](https://developer.mozilla.org/en-US/docs/Web/API/Element)
- [HTMLElement on MDN](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement#Properties)

https://twitter.com/KevinV11n/status/1163683197617467393

## That’s it for now.

Remember to sign up for **[The Weekly Stand-Up!](https://wipdeveloper.wpcomstaging.com/newsletter/)**  and you can get updated with any new information we have on WIPDeveloper.com.
