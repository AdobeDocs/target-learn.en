---
title: Use Data Providers to integrate third-party data into Adobe Target
seo-title: Use Data Providers to integrate third-party data into Adobe Target
description: Data Providers is a capability that allows you to easily pass data from third parties to Target.  A third party could be a weather service, a DMP, or even your own web service. You can then use this data to build audiences, target content, and enrich the visitor profile.
audience: marketer
difficulty: 5
author: Daniel Wright
doc-type: use
activity-type: feature-video
---

# Use Data Providers to integrate third-party data into Adobe Target

Data Providers is a capability that allows you to easily pass data from third parties to Target.  A third party could be a weather service, a DMP, or even your own web service. You can then use this data to build audiences, target content, and enrich the visitor profile.

>[!VIDEO](https://video.tv.adobe.com/v/22349/?quality=12)

## How to use Data Providers

1. Implementation expert adds code before at.js (or in the Library Header section of at.js) that makes the API call to the third-party, parses the response and specifies with name/value pairs from the response to send to Target.
1. at.js manages flicker and includes the name/value pairs as custom parameters in the global Target request.
1. Marketer builds audiences in the Target interface based on these custom parameters.
1. Marketer uses these audiences to target experiences, activities, and metrics as well as for reporting audiences.

>[!NOTE]
>
>Data Providers requires at.js 1.3 or above

## Supporting Materials

* [Implement Data Providers in at.js and Adobe Target](Data Providers-atjs-technical-video-implement.md)
* [Data Providers Documentation](https://docs.adobe.com/content/help/en/target/using/implement-target/client-side/functions-overview/targetgobalsettings.html#data-providers)