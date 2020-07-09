---
title: Adobe Target API Overview
keywords: recommendations;adobe recommendations;premium;api;apis
description: Adobe Target Recommendations includes a dedicated set of APIs that allow you to manage your catalog of recommendable products and/or content; manage your recommendations algorithms and campaigns; and deliver recommendations in JSON, HTML, or XML objects to be displayed in web, mobile, email, IOT, and other channels.
kt: 
audience: developer
doc-type: tutorial
activity: use
feature: recommendations;adobe recommendations;premium;api;apis
topics: recommendations;adobe recommendations;premium;api;apis
solution: Adobe Target
author: Judy Kim
---

# Adobe Target API Overview

Adobe Target APIs may be grouped according to type.

|API Type|What it enables you to do|Download link|
| --- | --- | --- |
|Admin|Create, modify, and delete activities, audiences, offers, and other objects (including [!DNL Recommendations] entities, criteria, designs, and so on. The [!DNL Recommendations] APIs are a type of admin API.)|<UL><li>[Target Admin API Postman Collection](https://developers.adobetarget.com/api/#admin-postman-collection)</li><li>[Recommendations API Postman Collection](https://developers.adobetarget.com/api/recommendations/#section/Postman)</li></ul>|
|Delivery|Retrieve optimized and personalized content from [!DNL Target] for delivery to an end user.|[Target Delivery API Postman Collection](https://developers.adobetarget.com/api/delivery-api/#section/Getting-Started/Postman-Collection)|
|Reporting|Export activity results and other reporting results.|Reporting APIs are included within the [Target Admin API Postman collection](https://developers.adobetarget.com/api/#admin-postman-collection).|
|Profile|Retrieve and modify user profiles stored in Adobe Target.|[Target Profile API Postman Collection](https://developers.adobetarget.com/api/#profiles)|

Note the distinction between **admin APIs** (including the [!DNL Recommendations] APIs), which let you configure various aspects of Adobe Target, versus **delivery APIs**, which let you retrieve content. Admin APIs require authentication, whereas delivery APIs do not.

To use Adobe Target Admin APIs, you first need to configure authentication using Adobe I/O.

[Next "Configure Adobe.IO Authentication" >](configure-io-target-integration.md)
