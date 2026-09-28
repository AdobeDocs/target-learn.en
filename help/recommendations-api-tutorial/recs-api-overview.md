---
title: What is the Adobe Recommendations API?
description: This tutorial walks developers through hands-on practice using the Adobe Target Recommendations APIs to configure and manage Recommendations catalogs and custom criteria, as well as using the delivery API to retrieve recommendations content.
role: Developer
level: Intermediate
topic: Personalization, Administration, Integrations, Development
feature: APIs/SDKs, Recommendations, Administration & Configuration, Overview
doc-type: tutorial
kt: 3815
author: Judy Kim
exl-id: 10f80056-fb71-4362-86bc-d161f596cb91
TQID: 'https://experienceleague.adobe.com/NQpsNnhLA0MRP-pJQLS35ymJ2lnulZebvI-Yv4-xSxw'
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
    internal-label: Target
feature_v2:
  - id: f7c7de77-382f-4f48-8b36-61a170f06d3d
    internal-label: Integrations
  - id: a19e8738-9679-599a-b83b-5f2f15f8e4d6
    internal-label: APIs/SDKs
  - id: dfc8a233-f2b5-4811-bf63-b4262aebc5a5
    internal-label: Administration and configuration
  - id: f69bc5f1-ebdb-4306-a281-f2e77daf734c
    internal-label: Activities and tests
subfeature_v2:
  - id: ed58f4a1-16eb-4c8c-b505-be9da766a9ec
    internal-label: Recommendations
  - id: fc9c2184-9102-403f-bd6c-0055021e4bea
    internal-label: Overview
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
topic_v2:
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
    internal-label: Personalization
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
    internal-label: Administration
---
# Adobe Recommendations API Overview

APIs relevant for [!DNL Recommendations] include [admin APIs](https://experienceleague.adobe.com/docs/target/using/apis/api-overview.html?lang=en) that allow you to:

* Manage your catalog of recommendable products or content
* Manage your [!DNL Recommendations] algorithms and activities

Using the [!DNL Target] [delivery API](https://experienceleague.adobe.com/docs/target/using/apis/api-overview.html?lang=en) with Recommendations, you can also:

* Retrieve recommendations in JSON, HTML, or XML objects so they can be displayed in web, mobile, email, Internet of Things (IOT), and other channels.

## Tutorial Description

This tutorial walks developers through hands-on practice using the [!DNL Recommendations] APIs to configure and manage [!DNL Recommendations] catalogs and custom criteria, as well as using the delivery API to retrieve recommendations content. By the end of this tutorial, you will be able to:

* Configure and manage entities using the Recommendations API
* Configure and manage custom criteria using the Recommendations API
* Understand how to use Recommendations with the Delivery API to use recommendations results in non-HTML devices

## Audience

This tutorial is intended for developers new to Target APIs or Recommendations APIs.

## Pre-requisites

Using the Target admin APIs requires [Adobe authentication setup](https://experienceleague.adobe.com/docs/target-dev/developer/api/configure-authentication.html){target="_blank"}. Make sure you have this configured prior to beginning this tutorial.

## Resources

Note the following resources, which are necessary to understand this tutorial and follow it successfully:

|Resource|Details|
| --- | --- |
|Postman|Get the [Postman app](https://www.postman.com/downloads/) for your operating system. Postman basic is free with account creation. While not required in order to use Adobe Target APIs in general, Postman makes API workflows easier, and Adobe Target provides several Postman collections to help execute its APIs and learn how they operate. The rest of this tutorial assumes working knowledge of Postman. For assistance, please reference the [Postman documentation](https://learning.getpostman.com/).  |
|References|Familiarity with the following resources is assumed throughout the rest of this tutorial:<UL><li>[Adobe I/O Github](https://github.com/adobeio)</li><li>[Target Adobe I/O documentation](https://developers.adobetarget.com/api/#introduction)</li><li>[Recommendations API documentation](https://developers.adobetarget.com/api/recommendations/)</li></ul>|

[Next "Manage your Recommendations Catalog" >](https://experienceleague.adobe.com/docs/target-dev/developer/api/recommendations-api/manage-catalog.html){target="_blank"}
