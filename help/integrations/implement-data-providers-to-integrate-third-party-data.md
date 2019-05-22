---
title: Implement Data Providers to integrate third-party data into Adobe Target
seo-title: Implement Data Providers to integrate third-party data into Adobe Target
description: Implementation details and examples of how to use Adobe Target's Data Providers feature to retrieve data from third-party data providers and pass it in the Target request.
audience: developer
difficulty: 5
author: Daniel Wright
doc-type: implement
activity-type: technical-video
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

* [Use Data Providers with Adobe Target](use-data-providers-to-integrate-third-party-data.md)  

* [Data Providers Documentation](https://docs.adobe.com/content/help/en/target/using/implement-target/client-side/functions-overview/targetgobalsettings.html#data-providers)