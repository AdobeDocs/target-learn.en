---
title: Use dataProviders to integrate third-party data into Adobe Target
seo-title: Use dataProviders to integrate third-party data into Adobe Target
description: dataProviders is a capability that allows you to easily pass data from third parties to Target.  A third party could be a weather service, a DMP, or even your own web service. You can then use this data to build audiences, target content, and enrich the visitor profile.
seo-description: dataProviders is a capability that allows you to easily pass data from third parties to Target.  A third party could be a weather service, a DMP, or even your own web service. You can then use this data to build audiences, target content, and enrich the visitor profile.
uuid: 48f288a4-8656-4c8a-bac3-3c933d041012
products: SG_TARGET
discoiquuid: 802fe222-48b9-4137-88c0-2a137d161171
index: y
internal: n
snippet: y
---

# Use dataProviders to integrate third-party data into Adobe Target{#use-dataproviders-to-integrate-third-party-data-into-adobe-target}

>[!VIDEO](https://video.tv.adobe.com/v/22349/?quality=12)

## How to use dataProviders {#how-to-use-dataproviders}

1. Implementation expert adds code before at.js (or in the Library Header section of at.js) that makes the API call to the third-party, parses the response and specifies with name/value pairs from the response to send to Target.
1. at.js manages flicker and includes the name/value pairs as custom parameters in the global Target request.
1. Marketer builds audiences in the Target interface based on these custom parameters.
1. Marketer uses these audiences to target experiences, activities, and metrics as well as for reporting audiences.

>[!NOTE]
>
>dataProviders requires at.js 1.3 or above

## Supporting Materials {#supporting-materials}

* [Implement dataProviders in at.js and Adobe Target](../using/dataProviders-atjs-technical-video-implement.md)
* [at.js Functions](https://marketing.adobe.com/resources/help/en_US/target/ov2/cmp_at.js_Functions.html)

