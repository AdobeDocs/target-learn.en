---
title: How to Use Data Providers to Integrate Third-party Data
description: This tutorial introduces users to Data Providers. Learn how to use the Data Providers capability to easily pass data from third parties to Adobe Target.
role: User, Developer
level: Experienced
topic: Personalization, Integrations
feature: Implementation, Integrations, APIs/SDKs
doc-type: feature video
kt: null
author: Daniel Wright
exl-id: 1892136e-14e3-4e52-8b1f-aee806d2f83a
TQID: https://experienceleague.adobe.com/XiUlJGHSFVxAMqdl6Y7hK9PoXOgiiUI43vrFeAj2Rpo
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
    internal-label: Target
feature_v2:
  - id: adee20bd-51f4-461d-b9db-d215f8756eeb
    internal-label: Audiences
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
    internal-label: Implementation
  - id: f7c7de77-382f-4f48-8b36-61a170f06d3d
    internal-label: Integrations
subfeature_v2:
  - id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
    internal-label: at.js
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
    internal-label: Reporting
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
    internal-label: Personalization
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
