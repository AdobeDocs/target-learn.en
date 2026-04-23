---
title: How to Implement Data Providers to Integrate Third-party Data
description: This tutorial provides implementation details and examples of how to use Adobe Target's Data Providers feature to retrieve data from third-party data providers and pass it in the Target request.
role: Developer
level: Experienced
topic: Personalization, Integrations
feature: Implementation, Integrations, APIs/SDKs
doc-type: technical video
kt: null
author: Daniel Wright
exl-id: fcf6d1a8-e2a7-41ce-9c1c-02985b7afb5a
TQID: https://experienceleague.adobe.com/Oh0ngUGA-ZfpPHnQnN0VRgUG1ta4yqg8Pfm8mhCZTN0
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
    internal-label: Target
feature_v2:
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
    internal-label: Implementation
  - id: f7c7de77-382f-4f48-8b36-61a170f06d3d
    internal-label: Integrations
subfeature_v2:
  - id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
    internal-label: at.js
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
    internal-label: Personalization
---
# Implement [!UICONTROL Data Providers] to integrate third-party data into Adobe Target

Implementation details and examples of how to use Adobe Target's [!UICONTROL Data Providers] feature to retrieve data from third-party data providers and pass it in the Target request.

>[!NOTE]
>
>[!UICONTROL Data Providers] requires `at.js` 1.3 or above

## Implement the Basic Components of Data Providers

>[!VIDEO](https://video.tv.adobe.com/v/22348/?quality=12)

A quick overview of the basic components of a `dataProvider` and how to get your code in the right order.  
A working example with the code used in the video can be found here:
[https://target.enablementadobe.com/data-providers/simple.html](https://target.enablementadobe.com/data-providers/simple.html)

## Integrate with a Third-Party API

>[!VIDEO](https://video.tv.adobe.com/v/22345/)

A more realistic example, integrating a weather API.  
A working example with the code used in the video can be found here:
[https://target.enablementadobe.com/data-providers/3rdparty.html](https://target.enablementadobe.com/data-providers/3rdparty.html)

## Integrate with Multiple Providers

>[!VIDEO](https://video.tv.adobe.com/v/22346/)

How to incorporate data from multiple providers into your global [!DNL Target] request.  
A working example with the code used in the video can be found here:
[https://target.enablementadobe.com/data-providers/combined.html](https://target.enablementadobe.com/data-providers/combined.html)

## Minimize Page Load Impact

>[!VIDEO](https://video.tv.adobe.com/v/22347/)

Minimize the impact on page load time by storing data in a session storage object. Alternatively, you could pass the values as profile parameters using the `profile.` prefix, and just pass them in the first [!DNL Target] request of the session. However, you would be limited to passing fifty profile parameters per request.

A working example with the code used in the video can be found here: [https://target.enablementadobe.com/data-providers/reducedCalls.html](https://target.enablementadobe.com/data-providers/reducedCalls.html)

## Supporting Materials

* [Use Data Providers with Adobe Target](use-data-providers-to-integrate-third-party-data.md)  
