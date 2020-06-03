---
title: Use Recommendations APIs
keywords: recommendations;adobe recommendations;premium;api;apis
description: Adobe Target Recommendations includes a dedicated set of APIs that allow you to manage your catalog of recommendable products and/or content; manage your recommendations algorithms and campaigns; and deliver recommendations in JSON, HTML, or XML objects to be displayed in web, mobile, email, IOT, and other channels.
kt: KT-3815
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
|Admin|Create, modify, and delete activities, audiences, offers, and other objects (including [!DNL Recommendations] entities, criteria, designs, and so on. The [!DNL Recommendations] APIs are a type of admin API.)|<UL><li>[[!DNL Target] Admin API Postman Collection](https://developers.adobetarget.com/api/#admin-postman-collection)</li><li>[[!DNL Recommendations] API Postman Collection](https://developers.adobetarget.com/api/recommendations/#section/Postman)</li></ul>|
|Delivery|Retrieve optimized and personalized content from [!DNL Target] for delivery to an end user.|[[!DNL Target] Delivery API Postman Collection](https://developers.adobetarget.com/api/delivery-api/#section/Getting-Started/Postman-Collection)|
|Reporting|Export activity results and other reporting results.|Reporting APIs are included within the [[!DNL Target] Admin API Postman collection](https://developers.adobetarget.com/api/#admin-postman-collection).|
|Profile|Retrieve and modify user profiles stored in Adobe Target.|[[!DNL Target] Profile API Postman Collection](https://developers.adobetarget.com/api/#profiles)|

Note the distinction between **admin APIs** (including the [!DNL Recommendations] APIs), which let you configure various aspects of Adobe Target, versus **delivery APIs**, which let you retrieve content. Admin APIs require authentication, whereas delivery APIs do not.

## Adobe Recommendations API Overview

APIs relevant for [!DNL Recommendations] include both admin and delivery APIs that allow you to:

* Manage your catalog of recommendable products or content
* Manage your [!DNL Recommendations] algorithms and activities
* Retrieve recommendations in JSON, HTML, or XML objects so they can be displayed in web, mobile, email, Internet of Things (IOT), and other channels.

This tutorial walks you through authentication setup using Adobe I/O, which is required for the admin APIs, followed by hands-on practice using the [!DNL Recommendations] APIs to configure and manage [!DNL Recommendations], and the delivery APIs to get recommendations content.

Note the following resources, which are necessary to understand this tutorial and follow it successfully:

|Resource|Details|
| --- | --- |
|Postman|Get the [Postman app](https://www.postman.com/downloads/) for your operating system. Postman basic is free with account creation. While not required, Postman makes API workflows easier, and Adobe Target provides several Postman collections to help execute its APIs and learn how they operate. The rest of this tutorial assumes usage of Postman.  |
|References|Familiarity with the following resources is assumed throughout the rest of this tutorial:<UL><li>[Adobe I/O Github](https://github.com/adobeio)</li><li>[[!DNL Target] Adobe I/O documentation](https://developers.adobetarget.com/api/#introduction)</li><li>[[!DNL Recommendations] API documentation](https://developers.adobetarget.com/api/recommendations/)</li><li>[Postman documentation](https://learning.getpostman.com/)</li></ul>|

[Next "Configure Adobe.IO Authentication" >](2configure-io-target-integration.md)
