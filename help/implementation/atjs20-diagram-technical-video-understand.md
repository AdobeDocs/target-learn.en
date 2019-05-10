---
title: Understanding How Adobe Target's at.js 2.0 Works
seo-title: Understanding How Adobe Target's at.js 2.0 Works
description: at.js 2.0 enhances Adobe Target's support for single page applications (SPA) and integrates with other Experience Cloud solutions. This video and accompanying diagrams explain how everything comes together.
seo-description: at.js 2.0 enhances Adobe Target's support for single page applications (SPA) and integrates with other Experience Cloud solutions. This video and accompanying diagrams explain how everything comes together.
uuid: 4b2adb62-0b03-48e3-8b3f-944690bd8c76
discoiquuid: 8dc1e879-fc82-4286-8491-40836af5c7dc
doc-type: understand
---

# Understanding How Adobe Target's at.js 2.0 Works

at.js 2.0 enhances Adobe Target's support for single page applications (SPA) and integrates with other Experience Cloud solutions. This video and accompanying diagrams explain how everything comes together.

>[!VIDEO](https://video.tv.adobe.com/v/26250?quality=12)

## Architecture Diagrams

![at.js 2.0 behavior on page load](assets/pageload.png)

1. Call returns Experience Cloud ID (ECID). If user is authenticated, another call syncs the customer ID.

1. at.js library loads synchronously and hides the document body (at.js can also be loaded asynchronously with an optional pre-hiding snippet implemented on the page)  

1. Page Load request is made including all configured parameters, ECID, SDID and customer ID

1. Profile scripts execute and feed into the Profile Store. The Store requests qualified audiences from the Audience Library (e.g. audiences shared from Analytics, Audience Manager, etc). Customer Attributes are sent to Profile Store in a batch process.
1. Based on URL, request parameters, and profile data, Target decides which Activities and Experiences to return to the visitor for the current page and future views

1. Targeted content sent back to page, optionally including profile values for additional personalization.

   Targeted content on the current page is revealed as quickly as possible without flicker of default content.

   Targeted content for future views of a single-page application is cached in the browser, so it can be instantly applied without an additional server call when the views are triggered. (See the next diagram for triggerView() behavior).

1. Analytics data sent from the page to the Data Collection Servers
1. Target data is matched to Analytics data via the SDID and is processed into the Analytics reporting storage. Analytics data can then be viewed in both Analytics and Target via A4T reports.

![at.js 2.0 behavior when the triggerView() function is used](assets/triggerview.png)

1. adobe.target.triggerView() is called in the single-page application
1. Targeted content for the view is read from the cache

1. Targeted content is revealed as quickly as possible without flicker of default content

1. Notification request is sent to the Target Profile Store to count the visitor in the activity and increment metrics
1. Analytics data is sent from the SPA to the Data Collection Servers

1. Target data is sent from the Target backend to the Data Collection Servers. Target data is matched to Analytics data via the SDID and is processed into the Analytics reporting storage. Analytics data can then be viewed in both Analytics and Target via A4T reports.

## Additional Resources

* [Implementing at.js 2.0 in a Single Page Application](atjs2-single-page-application-technical-video-implement.md)
* [Using Adobe Target's Visual Experience Composer for Single Page Applications (SPA VEC)](../experiences/visual-experience-composer-for-single-page-applications-feature-video-use.md)
* [How at.js Works Documentation](https://docs.adobe.com/content/help/en/target/using/implement-target/client-side/at-js/how-atjs-works.html)