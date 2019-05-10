---
title: Implement Data Providers to integrate third-party data into Adobe Target
seo-title: Implement Data Providers to integrate third-party data into Adobe Target
description: Implementation details and examples of how to use Adobe Target's Data Providers feature to retrieve data from third-party data providers and pass it in the Target request.
seo-description: Data Providers is a capability that allows you to easily pass data from 3rd parties to Target.  A third party could be a weather API, a DMP, or even your own web service.
uuid: 786070a6-2a72-4168-a0bd-996854c26507
products: SG_TARGET
discoiquuid: 98bbecf3-9ba4-45d0-a8fe-286c34a317fa
doc-type: implement
---

# Implement Data Providers to integrate third-party data into Adobe Target

Implementation details and examples of how to use Adobe Target's Data Providers feature to retrieve data from third-party data providers and pass it in the Target request.

>[!NOTE]
>
>Data Providers requires at.js 1.3 or above

## Implement the Basic Components of Data Providers

>[!VIDEO](https://video.tv.adobe.com/v/22348/?quality=12)

A quick overview of the basic components of a dataProvider and how to get your code in the right order.  
A working example with the code used in the video can be found here:
[https://target.enablementadobe.com/data-providers/simple.html](https://target.enablementadobe.com/data-providers/simple.html)

## Integrate with a Third-Party API

>[!VIDEO](https://video.tv.adobe.com/v/22345/)

A more realistic example, integrating a weather API.  
A working example with the code used in the video can be found here:
[https://target.enablementadobe.com/data-providers/3rdparty.html](https://target.enablementadobe.com/data-providers/3rdparty.html)

## Integrate with Multiple Providers

>[!VIDEO](https://video.tv.adobe.com/v/22346/)

How to incorporate data from multiple providers into your global Target request.  
A working example with the code used in the video can be found here:
[https://target.enablementadobe.com/data-providers/combined.html](https://target.enablementadobe.com/data-providers/combined.html)

## Minimize Page Load Impact

>[!VIDEO](https://video.tv.adobe.com/v/22347/)

Minimize the impact on page load time by storing data in a session storage object. Alternatively, you could pass the values as profile parameters using the "profile." prefix, and just pass them in the first Target request of the session, but you would be limited to passing fifty profile parameters per request.

A working example with the code used in the video can be found here: [https://target.enablementadobe.com/data-providers/reducedCalls.html](https://target.enablementadobe.com/data-providers/reducedCalls.html)

## Supporting Materials

* [Using Data Providers with Adobe Target](Data Providers-atjs-feature-video-use.md)  

* [Data Providers Documentation](https://docs.adobe.com/content/help/en/target/using/implement-target/client-side/functions-overview/targetgobalsettings.html#data-providers)