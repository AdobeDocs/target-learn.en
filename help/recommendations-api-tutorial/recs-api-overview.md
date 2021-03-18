---
title: Adobe Recommendations API Overview
keywords: recommendations;adobe recommendations;premium;api;apis
description: Adobe Target Recommendations includes a dedicated set of APIs that allow you to manage your catalog of recommendable products and/or content; manage your recommendations algorithms and campaigns; and deliver recommendations in JSON, HTML, or XML objects to be displayed in web, mobile, email, IOT, and other channels.
kt: 3815
audience: developer
doc-type: tutorial
activity: use
feature: api
topics: recommendations;adobe recommendations;premium;api;apis
solution: Target
author: Judy Kim
---

# Adobe Recommendations API Overview

APIs relevant for [!DNL Recommendations] include [admin APIs](https://docs.adobe.com/content/help/en/target/using/apis/api-overview.html) that allow you to:

* Manage your catalog of recommendable products or content
* Manage your [!DNL Recommendations] algorithms and activities

Using the [!DNL Target] [delivery API](https://docs.adobe.com/content/help/en/target/using/apis/api-overview.html) with Recommendations, you can also:

* Retrieve recommendations in JSON, HTML, or XML objects so they can be displayed in web, mobile, email, Internet of Things (IOT), and other channels.

## Tutorial Description

This tutorial walks developers through hands-on practice using the [!DNL Recommendations] APIs to configure and manage [!DNL Recommendations] catalogs and custom criteria, as well as using the delivery API to retrieve recommendations content. By the end of this tutorial, you will be able to:

* Configure and manage entities using the Recommendations API
* Configure and manage custom criteria using the Recommendations API
* Understand how to use Recommendations with the Delivery API to use recommendations results in non-HTML devices

## Audience

This tutorial is intended for developers new to Target APIs or Recommendations APIs.

## Pre-requisites

Using the Target admin APIs requires [Adobe authentication setup](../apis/configure-io-target-integration.md). Make sure you have this configured prior to beginning this tutorial.

## Resources

Note the following resources, which are necessary to understand this tutorial and follow it successfully:

|Resource|Details|
| --- | --- |
|Postman|Get the [Postman app](https://www.postman.com/downloads/) for your operating system. Postman basic is free with account creation. While not required in order to use Adobe Target APIs in general, Postman makes API workflows easier, and Adobe Target provides several Postman collections to help execute its APIs and learn how they operate. The rest of this tutorial assumes working knowledge of Postman. For assistance, please reference the [Postman documentation](https://learning.getpostman.com/).  |
|References|Familiarity with the following resources is assumed throughout the rest of this tutorial:<UL><li>[Adobe I/O Github](https://github.com/adobeio)</li><li>[Target Adobe I/O documentation](https://developers.adobetarget.com/api/#introduction)</li><li>[Recommendations API documentation](https://developers.adobetarget.com/api/recommendations/)</li></ul>|

[Next "Manage your Recommendations Catalog" >](manage-catalog.md)
