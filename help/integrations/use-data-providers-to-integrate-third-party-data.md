---
title: How to Use Data Providers to Integrate Third-party Data
description: This tutorial introduces users to Data Providers. Learn how to use the Data Providers capability to easily pass data from third parties to Adobe Target.
role: User, Developer
level: Experienced
topic: Personalization, Integrations
feature: Implementation, Integrations, APIs/SDKs
doc-type: feature video
kt:
author: Daniel Wright
exl-id: 1892136e-14e3-4e52-8b1f-aee806d2f83a
---
# Use Data Providers to integrate third-party data into Adobe Target

[!UICONTROL Data Providers] is a capability that allows you to easily pass data from third parties to Target.  A third party could be a weather service, a DMP, or even your own web service. You can then use this data to build audiences, target content, and enrich the visitor profile.

>[!VIDEO](https://video.tv.adobe.com/v/22349/?quality=12)

## How to use Data Providers

1. Implementation expert adds code before at.js (or in the Library Header section of at.js) that makes the API call to the third-party, parses the response and specifies with name/value pairs from the response to send to [!DNL Target].
1. at.js manages flicker and includes the name/value pairs as custom parameters in the global Target request.
1. Marketer builds audiences in the [!DNL Target] interface based on these custom parameters.
1. Marketer uses these audiences to target experiences, activities, and metrics as well as for reporting audiences.

>[!NOTE]
>
>[!UICONTROL Data Providers] requires at.js 1.3 or above

## Supporting Materials

* [Implement Data Providers in at.js and Adobe Target](implement-data-providers-to-integrate-third-party-data.md)
