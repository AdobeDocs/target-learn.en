---
title: How to Implement at.js 2.0 in a Single Page Application (SPA)
description: Adobe Target's at.js 2.0 provides rich feature sets that equip your business to execute personalization on next-generation, client-side technologies. Follow these steps to implement at.js 2.0 in a Single Page Application (SPA).
role: Developer
level: Intermediate
topic: SPA, Architecture, Development
feature: Implementation
doc-type: technical video
kt:
author: Daniel Wright
exl-id: 955f0571-5791-4dbb-9931-e6d5c8bb42a7
---
# Implement Adobe Target's at.js 2.0 in a single page application (SPA)

Adobe Target's `at.js` 2.0 provides rich feature sets that equip your business to execute personalization on next-generation, client-side technologies. This version is focused on upgrading `at.js` to have harmonious interactions with single page applications (SPAs).

>[!VIDEO](https://video.tv.adobe.com/v/26248?quality=12)

## How to Implement at.js 2.0 in a SPA

* Implement `at.js` 2.0 in the &lt;head&gt; of your Single Page Application.  
* Implement the `adobe.target.triggerView()` function whenever view changes in your SPA. Various techniques can be employed to do this, such as listening for URL hash changes, listening for custom events fired by your SPA, or embedding the `triggerView()` code directly into your application. You should choose the option that works best for your specific single page application.
* The view name is the first parameter of the `triggerView()` function. Use simple, clear, and unique names to make them easy to select in Target's visual experience composer.
* You can trigger views in small view changes, as well as in non-SPA contexts such as half-way down an infinite scrolling page.
* `at.js` 2.0 and `triggerView()` can be implemented via a tag management solution, such as Adobe Experience Platform Launch.

## at.js 2.0 Limitations

Please be aware of the following limitations of `at.js` 2.0 before upgrading:

* Cross domain tracking is not supported in `at.js` 2.0
* The mboxOverride.browserIp and mboxSession URL parameters are not supported in `at.js` 2.0
* The legacy functions mboxCreate, mboxDefine, mboxUpdate are deprecated in `at.js` 2.0. Default content will be shown and no network requests will be made.

## Library Footer Code Used in the Video

The code below was added to the Library Footer section of the `at.js` library during the video. It fires when the app first loads and then on any hash changes in the app. It uses a cleaned-up version of the hash as the view name, and "home" when the hash is empty. Note that to identify the SPA, the code looks for the text "react/" in the URL, which will most likely need to be updated on your site. Keep in mind, too, that it might be more appropriate for your SPA to fire `triggerView()` off of custom events or by embedding the code directly into your app.

```javascript
function sanitizeViewName(viewName) {
  if (viewName.startsWith('#')) {
    viewName = viewName.substr(1);
  }
  if (viewName.startsWith('/')) {
    viewName = viewName.substr(1);
  }
  return viewName;
}
function triggerView(viewName) {
  viewName = sanitizeViewName(viewName) || 'home';
  // Validate if the Target Libraries are available on your website
  if (typeof adobe != 'undefined' && adobe.target && typeof adobe.target.triggerView === 'function') {
    adobe.target.triggerView(viewName);
    console.log('AT: View triggered on page load: '+viewName)
  }
}
//fire triggerView when the SPA loads and when the hash changes in the SPA
if(window.location.pathname.indexOf('react/') >-1){
    triggerView(location.hash);
}
window.onhashchange = function() {
    if(window.location.pathname.indexOf('react/') >-1){
        triggerView(location.hash);
    }
}
```

## Additional resources

* [Understanding How at.js 2.0 Works (Architecture Diagrams)](understanding-how-atjs-20-works.md)  
* [Use Adobe Target's Visual Experience Composer for Single Page Applications (SPA VEC)](../experiences/use-the-visual-experience-composer-for-single-page-applications.md)
